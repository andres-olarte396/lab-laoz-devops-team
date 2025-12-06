# .NET Stack - Azure App Service + Container Apps

## 📋 Overview

Stack optimizado para aplicaciones .NET modernas (ASP.NET Core) en Azure, con opciones tanto para App Service como Container Apps.

### Ideal Para
- ✅ Aplicaciones .NET 6/7/8
- ✅ ASP.NET Core Web APIs
- ✅ Blazor WebAssembly/Server
- ✅ Minimal APIs
- ✅ gRPC services
- ✅ Worker Services / Background Jobs
- ✅ Equipos con experiencia Microsoft

### NO Usar Cuando
- ❌ .NET Framework legacy (usar Windows App Service)
- ❌ Requisito de Linux-only stack
- ❌ Necesidad de non-Microsoft stack

### Ventajas
- 🚀 Performance excelente
- 🔧 Tooling de clase mundial (Visual Studio, Rider)
- 📦 NuGet ecosystem robusto
- 🔄 LTS releases (3 años soporte)
- ☁️ Integración nativa con Azure
- 📊 Application Insights built-in

## 🏗️ Architecture Options

### Option 1: App Service (Recommended for most)
```
Internet → Front Door → App Service (3+ instances)
                             ↓
                      Azure SQL Database
                      Redis Cache
                      Blob Storage
```

### Option 2: Container Apps (Cloud-native)
```
Internet → Front Door → Container Apps
                             ↓
                      Azure SQL / Cosmos DB
                      Dapr State Store
                      Service Bus
```

## 🛠️ Technology Stack

### Runtime & Framework
```yaml
.NET Version:
  - .NET 8.0 (LTS, recommended)
  - .NET 7.0 (STS, support until May 2024)
  - .NET 6.0 (LTS, support until Nov 2024)

Frameworks:
  - ASP.NET Core 8.0 (Web API, MVC, Razor Pages)
  - Blazor (Server / WebAssembly / Hybrid)
  - gRPC
  - Minimal APIs
  - SignalR (real-time)

Worker Services:
  - Background Services
  - Hosted Services
  - Queue Processors
```

### Web Hosting
```yaml
Option A - Azure App Service:
  - Tier: Premium P2V3 or higher
  - OS: Linux (cheaper) or Windows
  - Runtime: .NET 8
  - Auto-scale: 3-10 instances
  - Deployment Slots: staging + production

Option B - Azure Container Apps:
  - Consumption-based
  - Scale to zero
  - Dapr integration
  - KEDA scaling
```

### Database
```yaml
Relational (Recommended):
  - Azure SQL Database
    - Tier: General Purpose or Business Critical
    - Always Encrypted for sensitive data
  - Entity Framework Core 8
  - Dapper (micro-ORM alternative)

NoSQL (Optional):
  - Cosmos DB
    - SDK: Microsoft.Azure.Cosmos
  - Redis (caching + distributed locks)
```

### Message Queue
```yaml
Azure Service Bus:
  - Topics & Subscriptions (pub/sub)
  - Queues (point-to-point)
  - Dead Letter Queue
  - SDK: Azure.Messaging.ServiceBus

Azure Storage Queue:
  - Simpler, cheaper alternative
  - Good for basic scenarios
```

### Authentication
```yaml
Microsoft Identity Platform:
  - Azure AD / Entra ID
  - Microsoft.Identity.Web
  - JWT Bearer tokens
  - Role-based access control

Azure AD B2C:
  - External users
  - Social logins
  - Custom policies
```

### Observability
```yaml
Application Insights:
  - SDK: Microsoft.ApplicationInsights.AspNetCore
  - Auto-instrumentation
  - Custom telemetry
  - Distributed tracing (W3C Trace Context)

Structured Logging:
  - Serilog or NLog
  - ILogger<T> interface
  - Log levels: Information, Warning, Error
  
Health Checks:
  - Microsoft.Extensions.Diagnostics.HealthChecks
  - /health endpoint
  - Database, Redis, external API checks
```

### Security
```yaml
Secrets Management:
  - Azure Key Vault
  - SDK: Azure.Security.KeyVault.Secrets
  - Managed Identity for access

API Security:
  - JWT authentication
  - Rate limiting (AspNetCoreRateLimit)
  - CORS configuration
  - API versioning

Data Protection:
  - ASP.NET Core Data Protection
  - Stored in Azure Blob Storage
  - Redis persistence for distributed apps
```

## 📁 Project Structure

### Modern .NET 8 Structure
```
src/
├── MyApp.Api/                      # ASP.NET Core Web API
│   ├── Controllers/
│   │   ├── UsersController.cs
│   │   └── OrdersController.cs
│   ├── Endpoints/                  # Minimal API endpoints (alternative)
│   ├── Program.cs                  # Application entry point
│   ├── appsettings.json
│   └── MyApp.Api.csproj
│
├── MyApp.Application/              # Business logic layer
│   ├── Services/
│   ├── Interfaces/
│   ├── DTOs/
│   ├── Validators/                 # FluentValidation
│   └── MyApp.Application.csproj
│
├── MyApp.Domain/                   # Domain models
│   ├── Entities/
│   ├── Enums/
│   ├── Exceptions/
│   └── MyApp.Domain.csproj
│
├── MyApp.Infrastructure/           # Data access & external services
│   ├── Data/
│   │   ├── ApplicationDbContext.cs
│   │   └── Migrations/
│   ├── Repositories/
│   ├── ExternalServices/
│   └── MyApp.Infrastructure.csproj
│
├── MyApp.Shared/                   # Shared code
│   ├── Constants/
│   ├── Extensions/
│   └── MyApp.Shared.csproj
│
tests/
├── MyApp.Api.Tests/                # Integration tests
├── MyApp.Application.Tests/        # Unit tests
└── MyApp.Infrastructure.Tests/     # Repository tests

infrastructure/
├── main.bicep
├── parameters.dev.json
└── parameters.prod.json

.github/workflows/
└── dotnet-deploy.yml
```

## 🚀 Sample Implementation

### Program.cs (Minimal Hosting Model - .NET 8)
```csharp
using Microsoft.EntityFrameworkCore;
using MyApp.Infrastructure.Data;
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;

var builder = WebApplication.CreateBuilder(args);

// Configuration
if (builder.Environment.IsProduction())
{
    // Load secrets from Key Vault
    var keyVaultUri = new Uri(builder.Configuration["KeyVaultUri"]!);
    builder.Configuration.AddAzureKeyVault(keyVaultUri, new DefaultAzureCredential());
}

// Database
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection"),
        sqlOptions =>
        {
            sqlOptions.EnableRetryOnFailure(
                maxRetryCount: 5,
                maxRetryDelay: TimeSpan.FromSeconds(30),
                errorNumbersToAdd: null);
            sqlOptions.CommandTimeout(30);
        });
});

// Redis Cache
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = builder.Configuration.GetConnectionString("Redis");
    options.InstanceName = "MyApp_";
});

// Authentication
builder.Services.AddAuthentication("Bearer")
    .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AdminOnly", policy => policy.RequireRole("Admin"));
});

// Application Services
builder.Services.AddScoped<IUserService, UserService>();
builder.Services.AddScoped<IOrderService, OrderService>();

// Health Checks
builder.Services.AddHealthChecks()
    .AddDbContextCheck<ApplicationDbContext>()
    .AddRedis(builder.Configuration.GetConnectionString("Redis")!)
    .AddApplicationInsightsPublisher();

// Application Insights
builder.Services.AddApplicationInsightsTelemetry();

// API Documentation
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(options =>
{
    options.SwaggerDoc("v1", new() { Title = "MyApp API", Version = "v1" });
});

// Controllers
builder.Services.AddControllers();

// CORS
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowFrontend", policy =>
    {
        policy.WithOrigins(builder.Configuration["FrontendUrl"]!)
              .AllowAnyMethod()
              .AllowAnyHeader()
              .AllowCredentials();
    });
});

var app = builder.Build();

// Middleware pipeline
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseCors("AllowFrontend");
app.UseAuthentication();
app.UseAuthorization();

// Health check endpoint
app.MapHealthChecks("/health");

// Controllers
app.MapControllers();

// Run migrations on startup (alternative: use deployment script)
using (var scope = app.Services.CreateScope())
{
    var dbContext = scope.ServiceProvider.GetRequiredService<ApplicationDbContext>();
    if (app.Environment.IsDevelopment())
    {
        await dbContext.Database.MigrateAsync();
    }
}

app.Run();
```

### Controller Example
```csharp
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;
using MyApp.Application.DTOs;
using MyApp.Application.Interfaces;

namespace MyApp.Api.Controllers;

[ApiController]
[Route("api/[controller]")]
[Authorize]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;
    private readonly ILogger<UsersController> _logger;

    public UsersController(IUserService userService, ILogger<UsersController> logger)
    {
        _userService = userService;
        _logger = logger;
    }

    [HttpGet]
    [ProducesResponseType(typeof(IEnumerable<UserDto>), StatusCodes.Status200OK)]
    public async Task<ActionResult<IEnumerable<UserDto>>> GetAllUsers(
        [FromQuery] int page = 1,
        [FromQuery] int pageSize = 10)
    {
        _logger.LogInformation("Fetching users - Page: {Page}, PageSize: {PageSize}", page, pageSize);
        
        var users = await _userService.GetUsersAsync(page, pageSize);
        return Ok(users);
    }

    [HttpGet("{id}")]
    [ProducesResponseType(typeof(UserDto), StatusCodes.Status200OK)]
    [ProducesResponseType(StatusCodes.Status404NotFound)]
    public async Task<ActionResult<UserDto>> GetUser(int id)
    {
        var user = await _userService.GetUserByIdAsync(id);
        
        if (user == null)
        {
            _logger.LogWarning("User {UserId} not found", id);
            return NotFound();
        }

        return Ok(user);
    }

    [HttpPost]
    [Authorize(Roles = "Admin")]
    [ProducesResponseType(typeof(UserDto), StatusCodes.Status201Created)]
    [ProducesResponseType(StatusCodes.Status400BadRequest)]
    public async Task<ActionResult<UserDto>> CreateUser([FromBody] CreateUserDto createUserDto)
    {
        if (!ModelState.IsValid)
            return BadRequest(ModelState);

        var user = await _userService.CreateUserAsync(createUserDto);
        
        return CreatedAtAction(
            nameof(GetUser),
            new { id = user.Id },
            user);
    }

    [HttpPut("{id}")]
    [ProducesResponseType(StatusCodes.Status204NoContent)]
    [ProducesResponseType(StatusCodes.Status404NotFound)]
    public async Task<IActionResult> UpdateUser(int id, [FromBody] UpdateUserDto updateUserDto)
    {
        var success = await _userService.UpdateUserAsync(id, updateUserDto);
        
        if (!success)
            return NotFound();

        return NoContent();
    }

    [HttpDelete("{id}")]
    [Authorize(Policy = "AdminOnly")]
    [ProducesResponseType(StatusCodes.Status204NoContent)]
    public async Task<IActionResult> DeleteUser(int id)
    {
        await _userService.DeleteUserAsync(id);
        return NoContent();
    }
}
```

### DbContext Example
```csharp
using Microsoft.EntityFrameworkCore;
using MyApp.Domain.Entities;

namespace MyApp.Infrastructure.Data;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    public DbSet<User> Users => Set<User>();
    public DbSet<Order> Orders => Set<Order>();

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        // Configure entities
        modelBuilder.Entity<User>(entity =>
        {
            entity.HasKey(e => e.Id);
            entity.Property(e => e.Email).IsRequired().HasMaxLength(256);
            entity.HasIndex(e => e.Email).IsUnique();
            entity.Property(e => e.CreatedAt).HasDefaultValueSql("GETUTCDATE()");
        });

        modelBuilder.Entity<Order>(entity =>
        {
            entity.HasKey(e => e.Id);
            entity.Property(e => e.TotalAmount).HasPrecision(18, 2);
            entity.HasOne(e => e.User)
                  .WithMany(u => u.Orders)
                  .HasForeignKey(e => e.UserId)
                  .OnDelete(DeleteBehavior.Cascade);
        });

        // Seed data (optional)
        modelBuilder.Entity<User>().HasData(
            new User { Id = 1, Email = "admin@myapp.com", Name = "Admin User" }
        );
    }
}
```

## 🚀 CI/CD Pipeline

### GitHub Actions
```yaml
name: .NET Deploy to Azure

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

env:
  DOTNET_VERSION: '8.0.x'
  AZURE_WEBAPP_NAME: app-myapp-prod

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Setup .NET
      uses: actions/setup-dotnet@v4
      with:
        dotnet-version: ${{ env.DOTNET_VERSION }}
    
    - name: Restore dependencies
      run: dotnet restore src/MyApp.Api/MyApp.Api.csproj
    
    - name: Build
      run: dotnet build src/MyApp.Api/MyApp.Api.csproj --configuration Release --no-restore
    
    - name: Test
      run: dotnet test --no-build --verbosity normal --collect:"XPlat Code Coverage"
    
    - name: Publish Code Coverage
      uses: codecov/codecov-action@v3
      with:
        files: '**/coverage.cobertura.xml'
    
    - name: Publish
      run: dotnet publish src/MyApp.Api/MyApp.Api.csproj -c Release -o ./publish
    
    - name: Upload artifact
      uses: actions/upload-artifact@v4
      with:
        name: dotnet-app
        path: ./publish

  deploy:
    runs-on: ubuntu-latest
    needs: build
    if: github.ref == 'refs/heads/main'
    environment:
      name: 'Production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}
    
    steps:
    - name: Download artifact
      uses: actions/download-artifact@v4
      with:
        name: dotnet-app
        path: ./publish
    
    - name: Login to Azure
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
    
    - name: Deploy to Azure Web App
      id: deploy-to-webapp
      uses: azure/webapps-deploy@v3
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        slot-name: 'staging'
        package: ./publish
    
    - name: Run EF Migrations
      run: |
        dotnet tool install --global dotnet-ef
        dotnet ef database update --project src/MyApp.Infrastructure --startup-project src/MyApp.Api --connection "${{ secrets.SQL_CONNECTION_STRING }}"
    
    - name: Smoke Test
      run: |
        response=$(curl -s -o /dev/null -w "%{http_code}" https://${{ env.AZURE_WEBAPP_NAME }}-staging.azurewebsites.net/health)
        if [ $response -ne 200 ]; then
          echo "Health check failed with status $response"
          exit 1
        fi
    
    - name: Swap to Production
      uses: azure/CLI@v1
      with:
        inlineScript: |
          az webapp deployment slot swap \
            --name ${{ env.AZURE_WEBAPP_NAME }} \
            --resource-group rg-myapp-prod \
            --slot staging \
            --target-slot production
```

## 📦 Key NuGet Packages

```xml
<!-- MyApp.Api.csproj -->
<ItemGroup>
  <!-- Web Framework -->
  <PackageReference Include="Microsoft.AspNetCore.OpenApi" Version="8.0.0" />
  <PackageReference Include="Swashbuckle.AspNetCore" Version="6.5.0" />
  
  <!-- Authentication -->
  <PackageReference Include="Microsoft.Identity.Web" Version="2.16.0" />
  
  <!-- Health Checks -->
  <PackageReference Include="AspNetCore.HealthChecks.SqlServer" Version="8.0.0" />
  <PackageReference Include="AspNetCore.HealthChecks.Redis" Version="8.0.0" />
  <PackageReference Include="AspNetCore.HealthChecks.ApplicationInsights" Version="8.0.0" />
  
  <!-- Observability -->
  <PackageReference Include="Microsoft.ApplicationInsights.AspNetCore" Version="2.21.0" />
  <PackageReference Include="Serilog.AspNetCore" Version="8.0.0" />
  <PackageReference Include="Serilog.Sinks.ApplicationInsights" Version="4.0.0" />
  
  <!-- Caching -->
  <PackageReference Include="Microsoft.Extensions.Caching.StackExchangeRedis" Version="8.0.0" />
</ItemGroup>

<!-- MyApp.Infrastructure.csproj -->
<ItemGroup>
  <!-- Entity Framework Core -->
  <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="8.0.0" />
  <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="8.0.0" />
  
  <!-- Azure SDKs -->
  <PackageReference Include="Azure.Identity" Version="1.10.4" />
  <PackageReference Include="Azure.Security.KeyVault.Secrets" Version="4.5.0" />
  <PackageReference Include="Azure.Storage.Blobs" Version="12.19.1" />
  <PackageReference Include="Azure.Messaging.ServiceBus" Version="7.17.0" />
  
  <!-- Optional: Dapper (micro-ORM) -->
  <PackageReference Include="Dapper" Version="2.1.24" />
</ItemGroup>

<!-- MyApp.Application.csproj -->
<ItemGroup>
  <!-- Validation -->
  <PackageReference Include="FluentValidation.AspNetCore" Version="11.3.0" />
  
  <!-- Mapping -->
  <PackageReference Include="AutoMapper" Version="12.0.1" />
  <PackageReference Include="AutoMapper.Extensions.Microsoft.DependencyInjection" Version="12.0.1" />
</ItemGroup>
```

## 💰 Cost Estimation

```yaml
Production (.NET App Service):
  - App Service P2V3 (3 instances): ~$570/month
  - Azure SQL (GP 4 vCores): ~$510/month
  - Redis Cache (Standard C1): ~$15/month
  - Application Insights: ~$50/month
  - Storage: ~$10/month
  Total: ~$1,155/month

Production (Container Apps):
  - Container Apps (1M requests): ~$40/month
  - Azure SQL: ~$510/month
  - Redis: ~$15/month
  - App Insights: ~$50/month
  Total: ~$615/month (cheaper if low traffic)
```

## ⚡ Quick Start

```bash
# 1. Create new .NET 8 Web API
dotnet new webapi -n MyApp.Api -f net8.0
cd MyApp.Api

# 2. Add necessary packages
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.ApplicationInsights.AspNetCore
dotnet add package Azure.Identity

# 3. Run locally
dotnet run

# 4. Deploy to Azure
az webapp up --name myapp-dev --runtime "DOTNETCORE:8.0" --sku B1

# 5. Configure connection string
az webapp config appsettings set \
  --name myapp-dev \
  --resource-group <resource-group> \
  --settings DefaultConnection="<sql-connection-string>"
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
