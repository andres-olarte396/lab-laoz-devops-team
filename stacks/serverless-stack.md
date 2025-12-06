# Serverless Stack - Azure Functions

## 📋 Overview

Stack optimizado para arquitecturas serverless usando Azure Functions, ideal para workloads event-driven y cargas de trabajo variables.

### Ideal Para
- ✅ Event-driven applications
- ✅ Cargas de trabajo intermitentes o impredecibles
- ✅ Procesamiento de webhooks y APIs simples
- ✅ Background jobs y scheduled tasks
- ✅ Costos optimizados (pay-per-use)
- ✅ Rápido time-to-market
- ✅ Integración con servicios Azure

### NO Usar Cuando
- ❌ Aplicaciones con estado complejo
- ❌ Long-running processes (>10 min)
- ❌ Tráfico alto y constante (más económico dedicado)
- ❌ Necesidad de control total del runtime
- ❌ Latencia crítica (<10ms)

### Ventajas
- 💰 Costo: Solo pagas por ejecuciones
- 🚀 Auto-scaling automático
- ⚡ Deployment rápido
- 🔧 Mantenimiento mínimo de infraestructura
- 🔌 Integraciones nativas con Azure services
- 📈 Escala a cero (zero cost when idle)

### Desventajas
- ❄️ Cold start latency (1-3 segundos)
- ⏱️ Timeout limits (5-10 min default)
- 🔒 Vendor lock-in
- 🐛 Debugging más complejo
- 💾 Stateless (requiere external storage)
- 📊 Costos impredecibles con alto volumen

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Azure Front Door                          │
│              (CDN + WAF + Routing)                          │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│              Azure API Management                            │
│         (API Gateway + Rate Limiting)                       │
└──────────────────────┬──────────────────────────────────────┘
                       │
         ┌─────────────┼─────────────┐
         │             │             │
┌────────▼───────┐ ┌──▼──────┐ ┌───▼────────┐
│ HTTP Trigger   │ │ Queue   │ │ Timer      │
│ Functions      │ │ Trigger │ │ Trigger    │
│                │ │ Funcs   │ │ Functions  │
└────────┬───────┘ └──┬──────┘ └───┬────────┘
         │             │             │
         └─────────────┼─────────────┘
                       │
         ┌─────────────┼─────────────┐
         │             │             │
┌────────▼───────┐ ┌──▼──────┐ ┌───▼────────┐
│ Cosmos DB      │ │ Blob    │ │ Service    │
│                │ │ Storage │ │ Bus/Queue  │
└────────────────┘ └─────────┘ └────────────┘

┌─────────────────────────────────────────────────────────────┐
│              Monitoring & Logging                            │
│  Application Insights + Log Analytics                       │
└─────────────────────────────────────────────────────────────┘
```

## 🛠️ Technology Stack

### Compute
```yaml
Azure Functions:
  - Hosting Plan: Consumption (serverless) or Premium
  - Runtime: .NET 8, Node.js 20, Python 3.11, Java 17
  - Version: Functions 4.x
  
Scaling:
  - Consumption: Auto (0 to 200 instances)
  - Premium: Pre-warmed + auto-scale (1 to 100 instances)
  - Dedicated: App Service Plan (if needed for VNet integration)
```

### API Gateway
```yaml
Azure API Management:
  - Tier: Consumption (serverless) or Standard
  - Features:
      - Rate limiting
      - Authentication/Authorization
      - Response caching
      - Request transformation
      - API versioning
```

### Storage & Data
```yaml
Database:
  - Cosmos DB (serverless capacity mode)
  - Azure SQL Database (serverless tier)
  - Azure Table Storage (para datos simples)
  
Object Storage:
  - Azure Blob Storage
  - Blob trigger para procesamiento
  
Caching:
  - Azure Cache for Redis (básico tier)
  
Queues:
  - Azure Storage Queue (simple)
  - Azure Service Bus (enterprise)
  - Event Grid (event-driven)
```

### Authentication
```yaml
Identity:
  - Azure AD B2C (usuarios externos)
  - Azure AD (empleados)
  - Managed Identity (service-to-service)
  
Authorization:
  - Function-level keys
  - Azure AD OAuth 2.0
  - API Management policies
```

### CI/CD
```yaml
Source Control:
  - GitHub / Azure Repos
  
Build & Deploy:
  - GitHub Actions
  - Azure DevOps Pipelines
  - Deployment Slots (staging)
  
Deployment:
  - ZIP deploy
  - Container (custom runtime)
  - ARM/Bicep templates
```

### Monitoring
```yaml
Application Insights:
  - Distributed tracing
  - Performance metrics
  - Failure tracking
  - Custom events
  
Log Analytics:
  - Centralized logging
  - Query language (KQL)
  - Alerting
  
Dashboards:
  - Azure Dashboard
  - Grafana (optional)
```

### Security
```yaml
Secrets Management:
  - Azure Key Vault
  - Function App Settings (encrypted)
  
Network Security:
  - Private Endpoints (Premium plan)
  - VNet Integration
  - IP Restrictions
  
API Security:
  - APIM policies
  - OAuth 2.0 / OpenID Connect
  - API keys
  - Rate limiting
```

## 📁 Infrastructure as Code

### Bicep Template
```bicep
// main.bicep
param location string = resourceGroup().location
param appName string
param environment string

// Storage Account (para functions)
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: 'st${appName}${environment}'
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}

// Application Insights
resource appInsights 'Microsoft.Insights/components@2020-02-02' = {
  name: 'appi-${appName}-${environment}'
  location: location
  kind: 'web'
  properties: {
    Application_Type: 'web'
    RetentionInDays: 90
  }
}

// Function App (Consumption Plan)
resource functionApp 'Microsoft.Web/sites@2023-01-01' = {
  name: 'func-${appName}-${environment}'
  location: location
  kind: 'functionapp'
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    serverFarmId: hostingPlan.id
    siteConfig: {
      appSettings: [
        {
          name: 'AzureWebJobsStorage'
          value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccount.name};EndpointSuffix=${az.environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
        }
        {
          name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING'
          value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccount.name};EndpointSuffix=${az.environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
        }
        {
          name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
          value: appInsights.properties.ConnectionString
        }
        {
          name: 'FUNCTIONS_EXTENSION_VERSION'
          value: '~4'
        }
        {
          name: 'FUNCTIONS_WORKER_RUNTIME'
          value: 'dotnet-isolated'
        }
      ]
      netFrameworkVersion: 'v8.0'
    }
  }
}

// Consumption Plan (Serverless)
resource hostingPlan 'Microsoft.Web/serverfarms@2023-01-01' = {
  name: 'plan-${appName}-${environment}'
  location: location
  sku: {
    name: 'Y1'
    tier: 'Dynamic'
  }
}

// Cosmos DB (Serverless)
resource cosmosDb 'Microsoft.DocumentDB/databaseAccounts@2023-04-15' = {
  name: 'cosmos-${appName}-${environment}'
  location: location
  properties: {
    databaseAccountOfferType: 'Standard'
    enableServerless: true
    locations: [
      {
        locationName: location
        failoverPriority: 0
      }
    ]
  }
}

// Service Bus (para queues)
resource serviceBus 'Microsoft.ServiceBus/namespaces@2022-10-01-preview' = {
  name: 'sb-${appName}-${environment}'
  location: location
  sku: {
    name: 'Basic'
  }
}
```

### Project Structure
```
my-serverless-app/
├── src/
│   ├── Functions/
│   │   ├── HttpTriggers/
│   │   │   ├── GetUsers.cs
│   │   │   ├── CreateUser.cs
│   │   │   └── UpdateUser.cs
│   │   ├── QueueTriggers/
│   │   │   ├── ProcessOrder.cs
│   │   │   └── SendEmail.cs
│   │   ├── TimerTriggers/
│   │   │   ├── DailyCleanup.cs
│   │   │   └── SyncData.cs
│   │   └── BlobTriggers/
│   │       └── ProcessImage.cs
│   ├── Models/
│   ├── Services/
│   └── Utilities/
├── infrastructure/
│   ├── main.bicep
│   ├── parameters.dev.json
│   └── parameters.prod.json
├── .github/
│   └── workflows/
│       └── deploy.yml
├── host.json
├── local.settings.json
└── README.md
```

## 🚀 CI/CD Pipeline

### GitHub Actions Workflow
```yaml
name: Deploy Azure Functions

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  AZURE_FUNCTIONAPP_NAME: func-myapp-prod
  AZURE_FUNCTIONAPP_PACKAGE_PATH: './src'
  DOTNET_VERSION: '8.0.x'

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: ${{ env.DOTNET_VERSION }}
    
    - name: Restore dependencies
      run: dotnet restore ${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}
    
    - name: Build
      run: dotnet build ${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }} --configuration Release
    
    - name: Test
      run: dotnet test ${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }} --no-build --verbosity normal
    
    - name: Publish
      run: |
        dotnet publish ${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }} \
          --configuration Release \
          --output ./output
    
    - name: Deploy to Azure Functions
      uses: Azure/functions-action@v1
      with:
        app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
        package: ./output
        publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}
    
    - name: Run Smoke Tests
      run: |
        # Test health endpoint
        curl -f https://${{ env.AZURE_FUNCTIONAPP_NAME }}.azurewebsites.net/api/health
```

### Deployment Slots
```bash
# Create staging slot
az functionapp deployment slot create \
  --name func-myapp-prod \
  --resource-group rg-myapp-prod \
  --slot staging

# Deploy to staging
az functionapp deployment source config-zip \
  --name func-myapp-prod \
  --resource-group rg-myapp-prod \
  --slot staging \
  --src ./output.zip

# Test staging
# Run integration tests against staging slot

# Swap to production
az functionapp deployment slot swap \
  --name func-myapp-prod \
  --resource-group rg-myapp-prod \
  --slot staging \
  --target-slot production
```

## 📊 Monitoring & Observability

### Application Insights Queries (KQL)
```kusto
// Failed Requests
requests
| where success == false
| where timestamp > ago(1h)
| summarize count() by name, resultCode
| order by count_ desc

// Function Execution Duration
requests
| where timestamp > ago(1h)
| summarize 
    p50=percentile(duration, 50),
    p95=percentile(duration, 95),
    p99=percentile(duration, 99)
  by name
| order by p95 desc

// Cold Start Analysis
traces
| where message contains "Cold start"
| where timestamp > ago(24h)
| summarize count() by bin(timestamp, 1h)
| render timechart

// Dependencies (external calls)
dependencies
| where timestamp > ago(1h)
| summarize 
    count(),
    avg(duration),
    max(duration)
  by target, name
| order by avg_duration desc

// Exceptions
exceptions
| where timestamp > ago(1h)
| summarize count() by type, outerMessage
| order by count_ desc
```

### Alerts Configuration
```yaml
Alerts:
  - Name: High Error Rate
    Metric: Failed request percentage
    Threshold: >5% for 5 minutes
    Severity: Critical
    Action: PagerDuty
  
  - Name: High Latency
    Metric: P95 duration
    Threshold: >3 seconds for 10 minutes
    Severity: Warning
    Action: Slack notification
  
  - Name: High Cost
    Metric: Daily execution count
    Threshold: >1 million executions
    Severity: Warning
    Action: Email to DevOps Lead
  
  - Name: Function Failures
    Metric: Exception count
    Threshold: >10 in 5 minutes
    Severity: High
    Action: Slack + create incident
```

### Dashboards
```yaml
Function Overview Dashboard:
  - Request rate (req/min)
  - Success rate %
  - P50, P95, P99 latency
  - Error rate by function
  - Top 5 slowest functions
  
Cost Dashboard:
  - Executions per day
  - Estimated monthly cost
  - Cost by function
  - Execution time consumption
  
Performance Dashboard:
  - Cold starts count
  - Average warm execution time
  - Dependency call duration
  - Queue/blob processing lag
```

## 🔒 Security Best Practices

### Function-Level Security
```csharp
// Example: Secured HTTP Function with Azure AD
[FunctionName("GetSecureData")]
public static async Task<IActionResult> Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "data")] 
    HttpRequest req,
    ILogger log)
{
    // Validate Azure AD token
    var authHeader = req.Headers["Authorization"].FirstOrDefault();
    if (string.IsNullOrEmpty(authHeader))
    {
        return new UnauthorizedResult();
    }
    
    var token = authHeader.Replace("Bearer ", "");
    var claimsPrincipal = await ValidateTokenAsync(token);
    
    if (claimsPrincipal == null)
    {
        return new UnauthorizedResult();
    }
    
    // Check required claim/role
    if (!claimsPrincipal.IsInRole("DataReader"))
    {
        return new ForbidResult();
    }
    
    // Process request
    var data = await GetDataAsync();
    return new OkObjectResult(data);
}
```

### Secrets Management
```json
// local.settings.json (development only, not committed)
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated",
    "CosmosDbConnectionString": "@Microsoft.KeyVault(SecretUri=https://kv-myapp.vault.azure.net/secrets/CosmosDbConnection/)",
    "ApiKey": "@Microsoft.KeyVault(SecretUri=https://kv-myapp.vault.azure.net/secrets/ApiKey/)"
  }
}
```

### Network Security
```bicep
// Private Endpoint for Function App (Premium Plan required)
resource privateEndpoint 'Microsoft.Network/privateEndpoints@2023-04-01' = {
  name: 'pe-${functionApp.name}'
  location: location
  properties: {
    subnet: {
      id: subnet.id
    }
    privateLinkServiceConnections: [
      {
        name: 'functionapp-connection'
        properties: {
          privateLinkServiceId: functionApp.id
          groupIds: [
            'sites'
          ]
        }
      }
    ]
  }
}

// VNet Integration
resource vnetIntegration 'Microsoft.Web/sites/networkConfig@2023-01-01' = {
  parent: functionApp
  name: 'virtualNetwork'
  properties: {
    subnetResourceId: subnet.id
  }
}
```

## 💰 Cost Estimation

### Consumption Plan Pricing
```yaml
Execution Pricing:
  - First 1M executions/month: FREE
  - Additional executions: $0.20 per million
  
Execution Time Pricing:
  - First 400,000 GB-s/month: FREE
  - Additional: $0.000016 per GB-s
  
Example Calculations:
  
  Small App (10K requests/day):
    - Executions: 300K/month → FREE
    - GB-s (avg 500ms, 128MB): 19,200 GB-s → FREE
    - Total: $0/month
  
  Medium App (100K requests/day):
    - Executions: 3M/month → $0.40
    - GB-s (avg 1s, 256MB): 192,000 GB-s → FREE
    - Total: $0.40/month
  
  Large App (1M requests/day):
    - Executions: 30M/month → $5.80
    - GB-s (avg 1s, 512MB): 3,840,000 GB-s → $54.90
    - Total: ~$60.70/month

Additional Costs:
  - Application Insights: ~$50-100/month
  - Cosmos DB (serverless): $0.25/million RU + storage
  - Storage Account: ~$1-10/month
  - Service Bus (basic): ~$0.05/million operations
  
Total Typical Cost: $10-200/month (depending on scale)
```

### Cost Optimization Tips
```yaml
Optimize Execution Time:
  - Minimize cold starts (use Premium plan if critical)
  - Optimize code efficiency
  - Use async/await properly
  - Cache data when possible

Optimize Execution Count:
  - Batch processing where possible
  - Use queue triggers instead of polling
  - Implement idempotency to avoid retries

Optimize Storage:
  - Use Table Storage instead of Cosmos for simple data
  - Implement data lifecycle policies
  - Compress large payloads

Right-Size Memory:
  - Start with 128MB, increase only if needed
  - Monitor memory usage in App Insights
  - Premium plan allows custom memory allocation
```

## 🔄 Migration Strategies

### From Traditional API
```yaml
Phase 1: Wrapper Pattern (2 weeks)
  - Deploy Functions as proxy to existing API
  - Route traffic gradually
  - Test both in parallel
  
Phase 2: Extract Endpoints (4-8 weeks)
  - Migrate one endpoint at a time
  - Start with read-only endpoints
  - Then CRUD operations
  
Phase 3: Data Migration (2-4 weeks)
  - Dual-write pattern during transition
  - Eventual consistency
  - Sync scripts for existing data
  
Phase 4: Decommission (1-2 weeks)
  - Route 100% traffic to Functions
  - Monitor for 1-2 weeks
  - Turn off old API
```

### From Monolith
```yaml
Strangler Pattern:
  1. Identify functions to extract
  2. Implement as Azure Functions
  3. Route traffic via API Management
  4. Gradually increase percentage
  5. Remove from monolith when 100%
```

## ⚡ Quick Start (15 min)

```bash
# 1. Install Azure Functions Core Tools
npm install -g azure-functions-core-tools@4

# 2. Create new Functions project
func init MyFunctionApp --dotnet-isolated

cd MyFunctionApp

# 3. Create HTTP trigger function
func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"

# 4. Run locally
func start

# Test: http://localhost:7071/api/HttpExample?name=World

# 5. Create Azure resources
az group create --name rg-myfunc --location eastus

az storage account create \
  --name stmyfuncapp \
  --resource-group rg-myfunc \
  --location eastus \
  --sku Standard_LRS

az functionapp create \
  --name func-myfuncapp \
  --resource-group rg-myfunc \
  --storage-account stmyfuncapp \
  --consumption-plan-location eastus \
  --runtime dotnet-isolated \
  --functions-version 4

# 6. Deploy
func azure functionapp publish func-myfuncapp

# 7. Test in Azure
curl https://func-myfuncapp.azurewebsites.net/api/HttpExample?name=Azure
```

## 📚 Function Patterns

### HTTP API Pattern
```csharp
[Function("GetUser")]
public async Task<IActionResult> GetUser(
    [HttpTrigger(AuthorizationLevel.Function, "get", Route = "users/{id}")] 
    HttpRequest req,
    string id)
{
    var user = await _userService.GetUserAsync(id);
    return user != null 
        ? new OkObjectResult(user) 
        : new NotFoundResult();
}
```

### Queue Processing Pattern
```csharp
[Function("ProcessOrder")]
public async Task ProcessOrder(
    [QueueTrigger("orders")] string orderMessage,
    [CosmosDB("orders", "processed", Connection = "CosmosDb")] 
    IAsyncCollector<Order> outputOrders)
{
    var order = JsonSerializer.Deserialize<Order>(orderMessage);
    await _orderService.ProcessAsync(order);
    await outputOrders.AddAsync(order);
}
```

### Timer Pattern (Scheduled Jobs)
```csharp
[Function("DailyCleanup")]
public async Task DailyCleanup(
    [TimerTrigger("0 0 2 * * *")] TimerInfo timer) // 2 AM daily
{
    _logger.LogInformation("Running daily cleanup");
    await _cleanupService.CleanOldDataAsync();
}
```

### Blob Processing Pattern
```csharp
[Function("ProcessImage")]
public async Task ProcessImage(
    [BlobTrigger("uploads/{name}")] Stream imageStream,
    string name,
    [Blob("processed/{name}", FileAccess.Write)] Stream outputStream)
{
    await _imageService.ResizeAsync(imageStream, outputStream, 800, 600);
}
```

## 📞 When to Use Each Hosting Plan

```yaml
Consumption Plan:
  Use When:
    - Cost is primary concern
    - Traffic is unpredictable
    - Can tolerate cold starts
    - Simple functions (<5 min execution)
  Cost: $0 for low traffic, scales with usage

Premium Plan:
  Use When:
    - Need to avoid cold starts
    - VNet integration required
    - Longer execution times needed
    - Pre-warmed instances critical
  Cost: ~$150-500/month base

Dedicated (App Service Plan):
  Use When:
    - Already have App Service Plan
    - Predictable, constant traffic
    - Need max control
    - Cost predictability needed
  Cost: Same as App Service Plan
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
