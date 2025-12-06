# Scale-Up Stack - Growth Phase

## 📋 Overview

Stack optimizado para empresas en fase de crecimiento acelerado que han validado product-market fit y necesitan escalar operaciones, usuarios y equipo.

### Ideal Para
- ✅ Startups Series A/B con tracción
- ✅ 10K-500K usuarios activos
- ✅ Equipos de 10-50 personas
- ✅ Crecimiento 10-50% mensual
- ✅ Múltiples features/productos
- ✅ Expansión internacional
- ✅ B2B SaaS en crecimiento

### NO Usar Cuando
- ❌ Aún en fase MVP (usar Startup MVP Stack)
- ❌ Enterprise desde día 1 (usar Enterprise Stack)
- ❌ Tráfico estable sin crecimiento
- ❌ Menos de 5K usuarios

### Ventajas
- 📈 **Auto-scaling**: Maneja picos de tráfico
- 🌍 **Multi-región**: Baja latencia global
- 🔒 **Security mejorada**: Compliance ready
- 👥 **Team scalability**: Múltiples equipos
- 💪 **High availability**: 99.95% SLA
- 🔄 **Zero-downtime deployments**: Blue-green, canary

### Retos de Scale-Up
```yaml
Technical Challenges:
  - Performance bajo carga
  - Database bottlenecks
  - Monolith breaking point
  - Technical debt acumulado
  - Monitoring complexity

Organizational:
  - Múltiples equipos
  - Code ownership
  - Release coordination
  - On-call rotations
  - Knowledge silos

Business:
  - Feature velocity vs stability
  - Cost optimization
  - Compliance requirements
  - SLA commitments
```

## 🏗️ Architecture

```
                    Internet
                       │
                       ▼
        ┌──────────────────────────┐
        │   Azure Front Door       │ ← Global CDN + WAF
        │   (Premium tier)         │   Multi-region routing
        └──────────┬───────────────┘
                   │
        ┌──────────┴────────────┐
        │                       │
        ▼                       ▼
   ┌─────────┐            ┌─────────┐
   │ Region  │            │ Region  │
   │ Primary │            │ Secondary│
   │ (East)  │            │ (West)   │
   └────┬────┘            └────┬─────┘
        │                      │
        ▼                      ▼
   ┌──────────────────────────────────┐
   │   Azure App Service              │
   │   (Premium V3, Auto-scale 2-20)  │
   └──────────┬───────────────────────┘
              │
   ┌──────────┼────────────┬──────────┐
   │          │            │          │
   ▼          ▼            ▼          ▼
┌─────┐  ┌────────┐  ┌────────┐  ┌────────┐
│Azure│  │ Redis  │  │ Service│  │ Cosmos │
│ SQL │  │Premium │  │  Bus   │  │   DB   │
│ GP  │  │ (P1)   │  │Standard│  │(optional)
└─────┘  └────────┘  └────────┘  └────────┘
   │
   ▼
┌──────────────────┐
│ Read Replicas    │
│ (Geo-distributed)│
└──────────────────┘
```

## 🛠️ Technology Stack

### Application Architecture

#### Modular Monolith (Recommended first step)
```yaml
Structure:
  - Bounded contexts dentro del monolito
  - Clear module boundaries
  - Shared kernel mínimo
  - Database per module (schemas)
  
Benefits:
  - Más simple que microservices
  - Fácil refactoring
  - Single deployment
  - Preparado para split futuro
  
When to split:
  - >50 developers
  - Clear service boundaries
  - Independent scaling needs
```

#### Hybrid Architecture (Transitioning)
```yaml
Core Monolith:
  - Main business logic
  - User management
  - Core features
  
Extracted Services:
  - Payment processing (PCI compliance)
  - Email/notifications (high volume)
  - Analytics/reporting (CPU intensive)
  - File processing (async workloads)
  - Search (Elasticsearch/Cognitive Search)
```

### Backend Stack

#### .NET (Recommended for scale)
```yaml
Runtime: .NET 8 LTS
Framework: ASP.NET Core
Architecture: Clean Architecture / Vertical Slices
ORM: Entity Framework Core + Dapper (reads)
Patterns:
  - CQRS (Command Query Responsibility Segregation)
  - Mediator (MediatR)
  - Repository + Unit of Work
  - Outbox pattern (reliable messaging)
```

#### Node.js (Alternative)
```yaml
Runtime: Node.js 20 LTS
Framework: NestJS (enterprise structure)
ORM: Prisma + raw SQL for complex queries
Patterns:
  - Modules + Dependency Injection
  - Guards & Interceptors
  - Event-driven architecture
```

### Database Strategy

#### Primary Database
```yaml
Azure SQL Database:
  - General Purpose tier (4-8 vCores)
  - Active geo-replication
  - Read replicas (secondary regions)
  - Point-in-time restore (35 days)
  - Automatic tuning enabled
  
PostgreSQL Alternative:
  - General Purpose (4-8 vCores)
  - Read replicas
  - pgBouncer for connection pooling
```

#### Caching Layer
```yaml
Azure Cache for Redis Premium:
  - P1 (6GB) - P3 (26GB)
  - Cluster mode for horizontal scaling
  - Zone redundancy
  - Persistence (RDB + AOF)
  - Geo-replication
  
Use Cases:
  - Session storage
  - API response caching
  - Rate limiting
  - Leaderboards/counters
  - Pub/Sub messaging
```

#### Search
```yaml
Azure Cognitive Search:
  - Full-text search
  - Faceted navigation
  - Auto-complete
  - Semantic search
  
Elasticsearch (Self-hosted on AKS):
  - Complex queries
  - Log aggregation
  - Analytics
```

#### Message Queue
```yaml
Azure Service Bus:
  - Premium tier (messaging units)
  - Topics + Subscriptions
  - Dead-letter queues
  - Duplicate detection
  - Scheduled messages
  
Use Cases:
  - Async processing
  - Event distribution
  - Decoupling services
  - Reliable delivery
```

### Hosting & Compute

```yaml
Azure App Service Premium V3:
  - P1V3: 2 vCPU, 8GB RAM (~$250/month)
  - P2V3: 4 vCPU, 16GB RAM (~$500/month)
  - P3V3: 8 vCPU, 32GB RAM (~$1000/month)
  
Auto-scaling:
  - Min instances: 2 (HA)
  - Max instances: 10-20 (growth)
  - Scale metrics: CPU, Memory, HTTP Queue
  - Scale schedule: Business hours boost
  
Deployment Slots:
  - Production
  - Staging
  - Preview (feature branches)
```

### Frontend

```yaml
React/Next.js:
  - Server Components (Next.js 14+)
  - App Router
  - Incremental Static Regeneration
  - Edge middleware
  
State Management:
  - React Query (server state)
  - Zustand (client state)
  - Context API (theme, auth)
  
Performance:
  - Code splitting per route
  - Dynamic imports
  - Image optimization (next/image)
  - Web Vitals monitoring
```

### CDN & Traffic Management

```yaml
Azure Front Door Premium:
  - Global load balancing
  - WAF with OWASP rules
  - Bot protection
  - DDoS protection (L7)
  - URL rewrite/redirect
  - Geo-filtering
  - Custom domains (unlimited)
  - SSL/TLS termination
  
Cost: ~$35/month + data transfer
```

### Monitoring & Observability

```yaml
Application Insights:
  - Distributed tracing
  - Dependency tracking
  - Custom metrics
  - Live metrics stream
  - Smart detection (anomalies)
  
Log Analytics:
  - Centralized logging
  - KQL queries
  - Retention 30-90 days
  - Integration with alerts
  
Grafana + Prometheus (Optional):
  - Custom dashboards
  - Business metrics
  - SLA tracking
```

### CI/CD

```yaml
GitHub Actions:
  - Matrix builds (multi-env)
  - Automated testing (unit, integration, E2E)
  - Security scanning (Snyk, SAST)
  - Performance testing (K6, Artillery)
  - Deployment strategies:
    * Blue-Green (zero downtime)
    * Canary (gradual rollout)
    * Feature flags (LaunchDarkly/Unleash)
  
Azure DevOps (Alternative):
  - Pipeline as code
  - Approval gates
  - Release dashboards
```

### Security & Compliance

```yaml
Azure Key Vault:
  - Secrets management
  - Certificate rotation
  - Managed identities
  
Azure AD B2C:
  - User authentication
  - MFA
  - Social logins
  - Custom policies
  
Security Tools:
  - OWASP ZAP (penetration testing)
  - SonarQube (code quality)
  - Snyk (dependency scanning)
  - Azure Defender
  
Compliance:
  - GDPR ready
  - SOC 2 Type II preparation
  - ISO 27001 alignment
```

## 📁 Project Structure

```
scale-up-app/
├── src/
│   ├── modules/                    # Bounded contexts
│   │   ├── users/
│   │   │   ├── domain/
│   │   │   │   ├── User.cs
│   │   │   │   └── IUserRepository.cs
│   │   │   ├── application/
│   │   │   │   ├── commands/
│   │   │   │   │   ├── CreateUser.cs
│   │   │   │   │   └── UpdateUser.cs
│   │   │   │   ├── queries/
│   │   │   │   │   └── GetUser.cs
│   │   │   │   └── validators/
│   │   │   ├── infrastructure/
│   │   │   │   ├── UserRepository.cs
│   │   │   │   └── UserDbContext.cs
│   │   │   └── api/
│   │   │       └── UsersController.cs
│   │   ├── orders/
│   │   ├── payments/
│   │   ├── notifications/
│   │   └── analytics/
│   ├── shared/
│   │   ├── kernel/
│   │   │   ├── Result.cs
│   │   │   ├── Error.cs
│   │   │   └── DomainEvent.cs
│   │   ├── infrastructure/
│   │   │   ├── Database/
│   │   │   ├── Caching/
│   │   │   ├── Messaging/
│   │   │   └── Logging/
│   │   └── api/
│   │       ├── Middleware/
│   │       └── Filters/
│   └── Program.cs
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── e2e/
│   └── performance/
├── infrastructure/
│   ├── bicep/
│   │   ├── main.bicep
│   │   ├── app-service.bicep
│   │   ├── database.bicep
│   │   ├── networking.bicep
│   │   └── monitoring.bicep
│   └── terraform/ (alternative)
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── deploy-staging.yml
│       ├── deploy-production.yml
│       └── performance-test.yml
├── docs/
│   ├── architecture/
│   ├── runbooks/
│   └── API.md
└── README.md
```

## 🚀 Sample Implementation

### Clean Architecture - User Module

```csharp
// src/modules/users/domain/User.cs
public class User : Entity
{
    public UserId Id { get; private set; }
    public Email Email { get; private set; }
    public string Name { get; private set; }
    public UserStatus Status { get; private set; }
    public DateTime CreatedAt { get; private set; }
    
    private User() { } // EF Core
    
    public static Result<User> Create(Email email, string name)
    {
        if (string.IsNullOrWhiteSpace(name))
            return Result.Failure<User>(UserErrors.InvalidName);
            
        var user = new User
        {
            Id = UserId.New(),
            Email = email,
            Name = name,
            Status = UserStatus.Active,
            CreatedAt = DateTime.UtcNow
        };
        
        user.RaiseDomainEvent(new UserCreatedEvent(user.Id));
        return Result.Success(user);
    }
    
    public Result Deactivate()
    {
        if (Status == UserStatus.Deactivated)
            return Result.Failure(UserErrors.AlreadyDeactivated);
            
        Status = UserStatus.Deactivated;
        RaiseDomainEvent(new UserDeactivatedEvent(Id));
        return Result.Success();
    }
}
```

```csharp
// src/modules/users/application/commands/CreateUser.cs
public record CreateUserCommand(string Email, string Name) : IRequest<Result<Guid>>;

public class CreateUserCommandHandler : IRequestHandler<CreateUserCommand, Result<Guid>>
{
    private readonly IUserRepository _userRepository;
    private readonly IUnitOfWork _unitOfWork;
    private readonly ILogger<CreateUserCommandHandler> _logger;
    
    public CreateUserCommandHandler(
        IUserRepository userRepository,
        IUnitOfWork unitOfWork,
        ILogger<CreateUserCommandHandler> logger)
    {
        _userRepository = userRepository;
        _unitOfWork = unitOfWork;
        _logger = logger;
    }
    
    public async Task<Result<Guid>> Handle(
        CreateUserCommand request,
        CancellationToken cancellationToken)
    {
        // Check if user exists
        var emailResult = Email.Create(request.Email);
        if (emailResult.IsFailure)
            return Result.Failure<Guid>(emailResult.Error);
            
        var existingUser = await _userRepository.GetByEmailAsync(
            emailResult.Value,
            cancellationToken);
            
        if (existingUser is not null)
            return Result.Failure<Guid>(UserErrors.EmailAlreadyExists);
        
        // Create user
        var userResult = User.Create(emailResult.Value, request.Name);
        if (userResult.IsFailure)
            return Result.Failure<Guid>(userResult.Error);
        
        // Save to database
        await _userRepository.AddAsync(userResult.Value, cancellationToken);
        await _unitOfWork.SaveChangesAsync(cancellationToken);
        
        _logger.LogInformation(
            "User created successfully. UserId: {UserId}",
            userResult.Value.Id.Value);
        
        return Result.Success(userResult.Value.Id.Value);
    }
}
```

```csharp
// src/modules/users/api/UsersController.cs
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly ISender _sender;
    
    public UsersController(ISender sender) => _sender = sender;
    
    [HttpPost]
    [ProducesResponseType(StatusCodes.Status201Created)]
    [ProducesResponseType(StatusCodes.Status400BadRequest)]
    public async Task<IActionResult> Create(
        [FromBody] CreateUserRequest request,
        CancellationToken cancellationToken)
    {
        var command = new CreateUserCommand(request.Email, request.Name);
        var result = await _sender.Send(command, cancellationToken);
        
        if (result.IsFailure)
            return BadRequest(result.Error);
        
        return CreatedAtAction(
            nameof(GetById),
            new { id = result.Value },
            result.Value);
    }
    
    [HttpGet("{id:guid}")]
    [ResponseCache(Duration = 60, VaryByQueryKeys = new[] { "id" })]
    public async Task<IActionResult> GetById(
        Guid id,
        CancellationToken cancellationToken)
    {
        var query = new GetUserByIdQuery(id);
        var result = await _sender.Send(query, cancellationToken);
        
        if (result.IsFailure)
            return NotFound();
        
        return Ok(result.Value);
    }
}
```

### Caching Strategy

```csharp
// src/shared/infrastructure/Caching/RedisCacheService.cs
public class RedisCacheService : ICacheService
{
    private readonly IConnectionMultiplexer _redis;
    private readonly ILogger<RedisCacheService> _logger;
    
    public async Task<T?> GetAsync<T>(
        string key,
        CancellationToken cancellationToken = default)
    {
        var db = _redis.GetDatabase();
        var value = await db.StringGetAsync(key);
        
        if (value.IsNullOrEmpty)
            return default;
        
        return JsonSerializer.Deserialize<T>(value!);
    }
    
    public async Task SetAsync<T>(
        string key,
        T value,
        TimeSpan? expiration = null,
        CancellationToken cancellationToken = default)
    {
        var db = _redis.GetDatabase();
        var serialized = JsonSerializer.Serialize(value);
        
        await db.StringSetAsync(
            key,
            serialized,
            expiration ?? TimeSpan.FromMinutes(10));
    }
    
    public async Task<T> GetOrCreateAsync<T>(
        string key,
        Func<Task<T>> factory,
        TimeSpan? expiration = null,
        CancellationToken cancellationToken = default)
    {
        var cached = await GetAsync<T>(key, cancellationToken);
        if (cached is not null)
            return cached;
        
        var value = await factory();
        await SetAsync(key, value, expiration, cancellationToken);
        
        return value;
    }
}
```

### Database Configuration with Read Replicas

```csharp
// src/shared/infrastructure/Database/DbContextFactory.cs
public class ApplicationDbContextFactory
{
    private readonly string _primaryConnectionString;
    private readonly string _readReplicaConnectionString;
    
    public ApplicationDbContext CreatePrimaryContext()
    {
        var optionsBuilder = new DbContextOptionsBuilder<ApplicationDbContext>();
        optionsBuilder.UseSqlServer(_primaryConnectionString);
        return new ApplicationDbContext(optionsBuilder.Options);
    }
    
    public ApplicationDbContext CreateReadOnlyContext()
    {
        var optionsBuilder = new DbContextOptionsBuilder<ApplicationDbContext>();
        optionsBuilder
            .UseSqlServer(_readReplicaConnectionString)
            .UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking);
        return new ApplicationDbContext(optionsBuilder.Options);
    }
}

// Usage in queries
public class GetUserByIdQueryHandler
{
    private readonly ApplicationDbContextFactory _contextFactory;
    
    public async Task<Result<UserDto>> Handle(GetUserByIdQuery query)
    {
        // Use read replica for queries
        await using var context = _contextFactory.CreateReadOnlyContext();
        
        var user = await context.Users
            .AsNoTracking()
            .Where(u => u.Id == query.UserId)
            .ProjectTo<UserDto>()
            .FirstOrDefaultAsync();
        
        return user is not null
            ? Result.Success(user)
            : Result.Failure<UserDto>(UserErrors.NotFound);
    }
}
```

### Auto-scaling Configuration

```bicep
// infrastructure/bicep/app-service.bicep
resource autoScaleSettings 'Microsoft.Insights/autoscalesettings@2022-10-01' = {
  name: '${appServicePlan.name}-autoscale'
  location: location
  properties: {
    enabled: true
    targetResourceUri: appServicePlan.id
    profiles: [
      {
        name: 'Default autoscale'
        capacity: {
          minimum: '2'
          maximum: '20'
          default: '2'
        }
        rules: [
          {
            metricTrigger: {
              metricName: 'CpuPercentage'
              metricResourceUri: appServicePlan.id
              timeGrain: 'PT1M'
              statistic: 'Average'
              timeWindow: 'PT5M'
              timeAggregation: 'Average'
              operator: 'GreaterThan'
              threshold: 70
            }
            scaleAction: {
              direction: 'Increase'
              type: 'ChangeCount'
              value: '2'
              cooldown: 'PT5M'
            }
          }
          {
            metricTrigger: {
              metricName: 'CpuPercentage'
              metricResourceUri: appServicePlan.id
              timeGrain: 'PT1M'
              statistic: 'Average'
              timeWindow: 'PT10M'
              timeAggregation: 'Average'
              operator: 'LessThan'
              threshold: 30
            }
            scaleAction: {
              direction: 'Decrease'
              type: 'ChangeCount'
              value: '1'
              cooldown: 'PT10M'
            }
          }
        ]
      }
      {
        name: 'Business hours boost'
        capacity: {
          minimum: '4'
          maximum: '20'
          default: '4'
        }
        recurrence: {
          frequency: 'Week'
          schedule: {
            timeZone: 'Eastern Standard Time'
            days: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
            hours: [8]
            minutes: [0]
          }
        }
      }
    ]
  }
}
```

## 💰 Cost Estimation

### Small Scale-Up (10K-50K users)
```yaml
App Service P1V3 (2 instances): $500/month
Azure SQL GP (4 vCores): $800/month
Redis Premium P1: $252/month
Service Bus Standard: $10/month
Front Door Premium: $35/month + bandwidth
Storage: $20/month
Application Insights: $50/month
Key Vault: $5/month

Total: ~$1,670/month + bandwidth (~$2,000/month total)
```

### Medium Scale-Up (50K-200K users)
```yaml
App Service P2V3 (4 instances): $2,000/month
Azure SQL GP (8 vCores): $1,600/month
Redis Premium P2: $504/month
Service Bus Premium (1 MU): $677/month
Front Door Premium: $100/month + bandwidth
Storage: $50/month
Application Insights: $150/month
Azure Cognitive Search: $250/month

Total: ~$5,330/month + bandwidth (~$6,500/month total)
```

### Large Scale-Up (200K-500K users)
```yaml
App Service P3V3 (6-8 instances): $6,000/month
Azure SQL BC (8 vCores) + replicas: $4,000/month
Redis Premium P3 (cluster): $1,008/month
Service Bus Premium (2 MU): $1,354/month
Front Door Premium: $300/month + bandwidth
Storage: $100/month
Application Insights: $300/month
Cognitive Search: $500/month

Total: ~$13,560/month + bandwidth (~$16,000/month total)
```

## ⚡ Quick Start

```bash
# 1. Clone scale-up template
git clone https://github.com/yourorg/scaleup-template.git
cd scaleup-template

# 2. Setup infrastructure
az group create --name rg-scaleup-prod --location eastus
az deployment group create \
  --resource-group rg-scaleup-prod \
  --template-file infrastructure/bicep/main.bicep \
  --parameters @infrastructure/bicep/parameters.prod.json

# 3. Configure CI/CD
# Add secrets to GitHub:
# - AZURE_CREDENTIALS
# - DATABASE_CONNECTION_STRING
# - REDIS_CONNECTION_STRING

# 4. Deploy
git push origin main  # Triggers GitHub Actions
```

## 📊 Key Metrics

```yaml
Performance SLAs:
  - API Response Time: p95 < 200ms, p99 < 500ms
  - Database Query Time: p95 < 100ms
  - Cache Hit Rate: > 90%
  - Uptime: 99.95% (4.38h downtime/year)

Scale Metrics:
  - Requests per Second: Track trends
  - Active Users: Real-time monitoring
  - Database Connections: Monitor pool utilization
  - Memory/CPU: Per instance tracking

Business Metrics:
  - Monthly Active Users (MAU)
  - Customer Acquisition Cost (CAC)
  - Lifetime Value (LTV)
  - Churn Rate
  - Feature Adoption
```

---

**Owner**: Engineering Manager / Platform Team  
**Última actualización**: Diciembre 2025
