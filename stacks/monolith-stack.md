# Monolith Stack - Azure App Service

## 📋 Overview

Stack tradicional optimizado para aplicaciones monolíticas en Azure App Service, ideal para migración lift-and-shift y aplicaciones existentes.

### Ideal Para
- ✅ Migración rápida desde on-premise
- ✅ Aplicaciones legacy existentes
- ✅ Equipos pequeños/medianos
- ✅ Time-to-market rápido
- ✅ Arquitectura tradicional probada
- ✅ Menor complejidad operacional
- ✅ Bases de código consolidadas

### NO Usar Cuando
- ❌ Necesidad de escalar componentes independientemente
- ❌ Equipos grandes con entregas independientes
- ❌ Requisitos de tecnologías mixtas
- ❌ Escalado masivo global
- ❌ Desacoplamiento crítico

### Ventajas
- 🚀 Deployment simple (single unit)
- 🔧 Debugging más fácil
- 💰 Costos predecibles
- 📦 Gestión simplificada
- 🔄 Transacciones ACID directas
- 📊 Menor latencia interna

### Desventajas
- ⚖️ Escalado todo-o-nada
- 🐌 Deployments más lentos
- 🔧 Tech stack único
- 📈 Límites de escalabilidad
- 🔥 Blast radius mayor
- 👥 Coordinación de equipos necesaria

## 🏗️ Architecture

```
                   Internet
                      │
┌─────────────────────▼─────────────────────┐
│         Azure Front Door                   │
│    (Global LB + CDN + WAF)                │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│    Azure Application Gateway               │
│         (Regional LB + WAF)               │
└─────────────────────┬─────────────────────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
┌───────▼──────┐ ┌───▼──────┐ ┌───▼──────┐
│ App Service  │ │ App      │ │ App      │
│ (Primary)    │ │ Service  │ │ Service  │
│ East US      │ │ Instance │ │ Instance │
│              │ │ 2        │ │ 3        │
└───────┬──────┘ └───┬──────┘ └───┬──────┘
        │             │             │
        └─────────────┼─────────────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
┌───────▼──────┐ ┌───▼──────┐ ┌───▼──────┐
│ Azure SQL    │ │ Redis    │ │ Blob     │
│ Database     │ │ Cache    │ │ Storage  │
│ (Primary)    │ │          │ │          │
└───────┬──────┘ └──────────┘ └──────────┘
        │
┌───────▼──────┐
│ SQL Replica  │
│ (Read-only)  │
│ West US      │
└──────────────┘

┌─────────────────────────────────────────┐
│      Application Insights               │
│      + Log Analytics                    │
└─────────────────────────────────────────┘
```

## 🛠️ Technology Stack

### Compute
```yaml
Azure App Service:
  - Tier: Standard S1 (dev), Premium P2V3 (prod)
  - OS: Windows or Linux
  - Runtime: .NET 8, Node.js 20, Python 3.11, Java 17, PHP 8.2
  - Instances: 3 (production), auto-scale 3-10
  - Deployment Slots: Production + Staging
  
Features:
  - Auto-scaling: CPU, Memory, HTTP Queue
  - Deployment Slots: Blue-Green deployments
  - Custom Domains: HTTPS with free SSL
  - Always On: Keep app warm
  - Health Check: /health endpoint
```

### Load Balancing
```yaml
Azure Front Door:
  - Global load balancing
  - CDN for static assets
  - WAF protection
  - SSL termination
  
Application Gateway:
  - Regional load balancing
  - Path-based routing
  - Session affinity
  - WAF v2
```

### Database
```yaml
Azure SQL Database:
  - Tier: General Purpose (dev), Business Critical (prod)
  - Size: 4 vCores, 32GB RAM
  - Storage: 250GB
  - Backup: Automated (7-35 days retention)
  - Geo-replication: Secondary read-only replica
  
Features:
  - Automatic tuning
  - Query Performance Insights
  - Long-term retention (10 years)
  - Point-in-time restore
  - Always Encrypted (sensitive data)
```

### Caching
```yaml
Azure Cache for Redis:
  - Tier: Standard C1 (dev), Premium P1 (prod)
  - Size: 1GB (dev), 6GB (prod)
  - Persistence: RDB snapshots
  - Clustering: Premium tier
  
Use Cases:
  - Session state
  - Output caching
  - Database query caching
  - Distributed locking
```

### Storage
```yaml
Azure Blob Storage:
  - Tier: Hot (frequent access), Cool (backups)
  - Replication: LRS (dev), GRS (prod)
  
Use Cases:
  - File uploads
  - Static assets
  - Backups
  - Logs archive
```

### Authentication
```yaml
Azure AD / Entra ID:
  - Easy Auth (App Service built-in)
  - OAuth 2.0 / OpenID Connect
  - Multi-factor authentication
  - Conditional access policies
  
Azure AD B2C (external users):
  - Social logins (Google, Facebook)
  - Custom user flows
  - Branded login pages
```

### CI/CD
```yaml
Azure DevOps Pipelines:
  - Build pipeline (CI)
  - Release pipeline (CD)
  - Deployment gates
  - Approval workflows
  
GitHub Actions:
  - Alternative to Azure DevOps
  - GitHub-native integration
```

### Monitoring
```yaml
Application Insights:
  - Application Performance Monitoring
  - Distributed tracing
  - Custom metrics
  - Availability tests
  
Azure Monitor:
  - Metrics & logs
  - Alerts
  - Action groups
  - Dashboards
  
Log Analytics:
  - Centralized logging
  - KQL queries
  - Workbooks
```

## 📁 Infrastructure as Code

### Bicep Template
```bicep
// main.bicep
param location string = resourceGroup().location
param appName string
param environment string
param sqlAdminUsername string
@secure()
param sqlAdminPassword string

// App Service Plan
resource appServicePlan 'Microsoft.Web/serverfarms@2023-01-01' = {
  name: 'plan-${appName}-${environment}'
  location: location
  sku: {
    name: environment == 'prod' ? 'P2V3' : 'S1'
    tier: environment == 'prod' ? 'PremiumV3' : 'Standard'
    capacity: environment == 'prod' ? 3 : 1
  }
  properties: {
    reserved: true // Linux
  }
}

// App Service
resource appService 'Microsoft.Web/sites@2023-01-01' = {
  name: 'app-${appName}-${environment}'
  location: location
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    serverFarmId: appServicePlan.id
    httpsOnly: true
    siteConfig: {
      alwaysOn: true
      http20Enabled: true
      minTlsVersion: '1.2'
      ftpsState: 'Disabled'
      healthCheckPath: '/health'
      linuxFxVersion: 'DOTNETCORE|8.0'
      appSettings: [
        {
          name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
          value: appInsights.properties.ConnectionString
        }
        {
          name: 'ASPNETCORE_ENVIRONMENT'
          value: environment == 'prod' ? 'Production' : 'Development'
        }
      ]
      connectionStrings: [
        {
          name: 'DefaultConnection'
          connectionString: 'Server=tcp:${sqlServer.properties.fullyQualifiedDomainName},1433;Initial Catalog=${sqlDatabase.name};Authentication=Active Directory Managed Identity;'
          type: 'SQLAzure'
        }
        {
          name: 'RedisConnection'
          connectionString: '${redisCache.properties.hostName}:${redisCache.properties.sslPort},password=${redisCache.listKeys().primaryKey},ssl=True,abortConnect=False'
          type: 'Custom'
        }
      ]
    }
  }
}

// Staging Slot
resource stagingSlot 'Microsoft.Web/sites/slots@2023-01-01' = if (environment == 'prod') {
  parent: appService
  name: 'staging'
  location: location
  properties: {
    serverFarmId: appServicePlan.id
    siteConfig: {
      alwaysOn: true
    }
  }
}

// Auto-scale Settings
resource autoScaleSettings 'Microsoft.Insights/autoscalesettings@2022-10-01' = if (environment == 'prod') {
  name: 'autoscale-${appService.name}'
  location: location
  properties: {
    enabled: true
    targetResourceUri: appServicePlan.id
    profiles: [
      {
        name: 'Auto scale condition'
        capacity: {
          minimum: '3'
          maximum: '10'
          default: '3'
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
              value: '1'
              cooldown: 'PT5M'
            }
          }
          {
            metricTrigger: {
              metricName: 'CpuPercentage'
              metricResourceUri: appServicePlan.id
              timeGrain: 'PT1M'
              statistic: 'Average'
              timeWindow: 'PT5M'
              timeAggregation: 'Average'
              operator: 'LessThan'
              threshold: 30
            }
            scaleAction: {
              direction: 'Decrease'
              type: 'ChangeCount'
              value: '1'
              cooldown: 'PT5M'
            }
          }
        ]
      }
    ]
  }
}

// SQL Server
resource sqlServer 'Microsoft.Sql/servers@2023-05-01-preview' = {
  name: 'sql-${appName}-${environment}'
  location: location
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    administratorLogin: sqlAdminUsername
    administratorLoginPassword: sqlAdminPassword
    minimalTlsVersion: '1.2'
    publicNetworkAccess: 'Enabled' // Change to 'Disabled' for private endpoint
  }
}

// SQL Database
resource sqlDatabase 'Microsoft.Sql/servers/databases@2023-05-01-preview' = {
  parent: sqlServer
  name: 'sqldb-${appName}-${environment}'
  location: location
  sku: {
    name: environment == 'prod' ? 'BC_Gen5_4' : 'GP_Gen5_2'
    tier: environment == 'prod' ? 'BusinessCritical' : 'GeneralPurpose'
  }
  properties: {
    collation: 'SQL_Latin1_General_CP1_CI_AS'
    maxSizeBytes: 268435456000 // 250GB
    catalogCollation: 'SQL_Latin1_General_CP1_CI_AS'
    zoneRedundant: environment == 'prod'
    readScale: environment == 'prod' ? 'Enabled' : 'Disabled'
    requestedBackupStorageRedundancy: environment == 'prod' ? 'Geo' : 'Local'
  }
}

// Allow Azure services to access SQL
resource sqlFirewallRule 'Microsoft.Sql/servers/firewallRules@2023-05-01-preview' = {
  parent: sqlServer
  name: 'AllowAzureServices'
  properties: {
    startIpAddress: '0.0.0.0'
    endIpAddress: '0.0.0.0'
  }
}

// Redis Cache
resource redisCache 'Microsoft.Cache/redis@2023-08-01' = {
  name: 'redis-${appName}-${environment}'
  location: location
  properties: {
    sku: {
      name: environment == 'prod' ? 'Premium' : 'Standard'
      family: environment == 'prod' ? 'P' : 'C'
      capacity: environment == 'prod' ? 1 : 1
    }
    enableNonSslPort: false
    minimumTlsVersion: '1.2'
    redisConfiguration: {
      'maxmemory-policy': 'allkeys-lru'
    }
  }
}

// Storage Account
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: 'st${replace(appName, '-', '')}${environment}'
  location: location
  sku: {
    name: environment == 'prod' ? 'Standard_GRS' : 'Standard_LRS'
  }
  kind: 'StorageV2'
  properties: {
    minimumTlsVersion: 'TLS1_2'
    supportsHttpsTrafficOnly: true
    accessTier: 'Hot'
  }
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

// Outputs
output appServiceUrl string = 'https://${appService.properties.defaultHostName}'
output sqlServerFqdn string = sqlServer.properties.fullyQualifiedDomainName
output appInsightsKey string = appInsights.properties.InstrumentationKey
```

## 🚀 CI/CD Pipeline

### Azure DevOps Pipeline (YAML)
```yaml
trigger:
  branches:
    include:
    - main
    - develop

variables:
  buildConfiguration: 'Release'
  dotnetVersion: '8.0.x'

stages:
- stage: Build
  displayName: 'Build & Test'
  jobs:
  - job: Build
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: UseDotNet@2
      displayName: 'Install .NET SDK'
      inputs:
        packageType: 'sdk'
        version: $(dotnetVersion)
    
    - task: DotNetCoreCLI@2
      displayName: 'Restore NuGet Packages'
      inputs:
        command: 'restore'
        projects: '**/*.csproj'
    
    - task: DotNetCoreCLI@2
      displayName: 'Build Solution'
      inputs:
        command: 'build'
        projects: '**/*.csproj'
        arguments: '--configuration $(buildConfiguration)'
    
    - task: DotNetCoreCLI@2
      displayName: 'Run Unit Tests'
      inputs:
        command: 'test'
        projects: '**/*Tests.csproj'
        arguments: '--configuration $(buildConfiguration) --collect:"XPlat Code Coverage"'
    
    - task: PublishCodeCoverageResults@1
      displayName: 'Publish Code Coverage'
      inputs:
        codeCoverageTool: 'Cobertura'
        summaryFileLocation: '$(Agent.TempDirectory)/**/*coverage.cobertura.xml'
    
    - task: DotNetCoreCLI@2
      displayName: 'Publish Application'
      inputs:
        command: 'publish'
        publishWebProjects: true
        arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
        zipAfterPublish: true
    
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifacts'
      inputs:
        pathToPublish: '$(Build.ArtifactStagingDirectory)'
        artifactName: 'drop'

- stage: DeployDev
  displayName: 'Deploy to Development'
  dependsOn: Build
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/develop'))
  jobs:
  - deployment: DeployDev
    pool:
      vmImage: 'ubuntu-latest'
    environment: 'Development'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            displayName: 'Deploy to App Service'
            inputs:
              azureSubscription: 'Azure-Connection'
              appName: 'app-myapp-dev'
              package: '$(Pipeline.Workspace)/drop/*.zip'

- stage: DeployProd
  displayName: 'Deploy to Production'
  dependsOn: Build
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
  jobs:
  - deployment: DeployStaging
    pool:
      vmImage: 'ubuntu-latest'
    environment: 'Production-Staging'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            displayName: 'Deploy to Staging Slot'
            inputs:
              azureSubscription: 'Azure-Connection'
              appName: 'app-myapp-prod'
              deployToSlotOrASE: true
              resourceGroupName: 'rg-myapp-prod'
              slotName: 'staging'
              package: '$(Pipeline.Workspace)/drop/*.zip'
          
          - task: AzureAppServiceManage@0
            displayName: 'Start Staging Slot'
            inputs:
              azureSubscription: 'Azure-Connection'
              Action: 'Start Azure App Service'
              WebAppName: 'app-myapp-prod'
              SpecifySlotOrASE: true
              ResourceGroupName: 'rg-myapp-prod'
              Slot: 'staging'
          
          - task: PowerShell@2
            displayName: 'Smoke Tests on Staging'
            inputs:
              targetType: 'inline'
              script: |
                $response = Invoke-WebRequest -Uri "https://app-myapp-prod-staging.azurewebsites.net/health" -UseBasicParsing
                if ($response.StatusCode -ne 200) {
                  Write-Error "Health check failed"
                  exit 1
                }
  
  - deployment: SwapToProduction
    dependsOn: DeployStaging
    pool:
      vmImage: 'ubuntu-latest'
    environment: 'Production'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureAppServiceManage@0
            displayName: 'Swap Staging to Production'
            inputs:
              azureSubscription: 'Azure-Connection'
              Action: 'Swap Slots'
              WebAppName: 'app-myapp-prod'
              ResourceGroupName: 'rg-myapp-prod'
              SourceSlot: 'staging'
              SwapWithProduction: true
          
          - task: PowerShell@2
            displayName: 'Smoke Tests on Production'
            inputs:
              targetType: 'inline'
              script: |
                Start-Sleep -Seconds 30
                $response = Invoke-WebRequest -Uri "https://app-myapp-prod.azurewebsites.net/health" -UseBasicParsing
                if ($response.StatusCode -ne 200) {
                  Write-Error "Production health check failed - consider rollback"
                  exit 1
                }
```

## 📊 Monitoring & Observability

### Application Insights Queries
```kusto
// Request Performance
requests
| where timestamp > ago(1h)
| summarize 
    count(),
    p50=percentile(duration, 50),
    p95=percentile(duration, 95),
    p99=percentile(duration, 99)
  by name
| order by p95 desc

// Failed Requests
requests
| where success == false
| where timestamp > ago(1h)
| summarize count() by resultCode, name
| order by count_ desc

// Dependencies (SQL, Redis, HTTP calls)
dependencies
| where timestamp > ago(1h)
| summarize 
    count(),
    avgDuration=avg(duration),
    maxDuration=max(duration)
  by type, target
| order by avgDuration desc

// Exceptions
exceptions
| where timestamp > ago(24h)
| summarize count() by type, outerMessage
| order by count_ desc
| take 20

// Slow SQL Queries
dependencies
| where type == "SQL"
| where duration > 1000 // > 1 second
| project timestamp, name, duration, data, resultCode
| order by duration desc

// User Sessions
pageViews
| where timestamp > ago(1h)
| summarize sessions=dcount(session_Id) by bin(timestamp, 5m)
| render timechart
```

### Alerts
```yaml
Performance Alerts:
  - High CPU Usage (>80% for 5 min)
  - High Memory Usage (>85% for 5 min)
  - Slow Response Time (p95 >3s for 10 min)
  - HTTP 5xx Errors (>10 in 5 min)

Availability Alerts:
  - Health Check Failed (2 consecutive failures)
  - App Service Down
  - SQL Database Unavailable

Cost Alerts:
  - Daily cost exceeds budget
  - DTU usage >90%
  - Storage approaching limit
```

## 🔒 Security Best Practices

### Configuration
```json
// appsettings.json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=tcp:sql-myapp-prod.database.windows.net,1433;Initial Catalog=sqldb-myapp-prod;Authentication=Active Directory Managed Identity;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "ApplicationInsights": {
    "ConnectionString": "InstrumentationKey=xxxxx"
  },
  "Redis": {
    "InstanceName": "myapp",
    "Configuration": "redis-myapp-prod.redis.cache.windows.net:6380,password=<from-keyvault>,ssl=True"
  }
}
```

### Managed Identity Setup (C#)
```csharp
// Program.cs
var builder = WebApplication.CreateBuilder(args);

// SQL Connection with Managed Identity
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
    options.UseSqlServer(connectionString, sqlOptions =>
    {
        sqlOptions.EnableRetryOnFailure(
            maxRetryCount: 5,
            maxRetryDelay: TimeSpan.FromSeconds(30),
            errorNumbersToAdd: null);
    });
});

// Redis with Managed Identity
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = builder.Configuration["Redis:Configuration"];
    options.InstanceName = builder.Configuration["Redis:InstanceName"];
});

// Application Insights
builder.Services.AddApplicationInsightsTelemetry();

var app = builder.Build();

// Health check endpoint
app.MapHealthChecks("/health");

app.Run();
```

## 💰 Cost Estimation

```yaml
Production Environment (Monthly):
  
  App Service (P2V3, 3 instances):
    - Price: $0.264/hour x 3 = $0.792/hour
    - Monthly: ~$570
  
  Azure SQL (Business Critical, 4 vCores):
    - Price: ~$1,200/month
    - Storage (250GB): ~$125/month
    - Backup (GRS): ~$30/month
  
  Redis (Premium P1, 6GB):
    - Price: ~$270/month
  
  Storage Account:
    - Storage: ~$20/month
    - Transactions: ~$5/month
  
  Application Insights:
    - Ingestion (50GB/month): ~$50/month
  
  Front Door (optional):
    - Base: ~$35/month
    - Data transfer: ~$30/month
  
  Total: ~$2,335/month

Development Environment:
  - App Service (S1, 1 instance): ~$70/month
  - Azure SQL (GP, 2 vCores): ~$380/month
  - Redis (Standard C1): ~$15/month
  - Storage: ~$10/month
  - App Insights: ~$20/month
  Total: ~$495/month

Cost Optimization:
  - Use Reserved Instances (30-40% savings)
  - Azure Hybrid Benefit (SQL license)
  - Auto-shutdown for dev environments
  - Right-size based on actual usage
```

## 🔄 Migration Path

### From On-Premise
```yaml
Phase 1: Assessment (1-2 weeks)
  - Inventory applications
  - Check compatibility
  - Database migration assessment
  
Phase 2: Environment Setup (1 week)
  - Deploy infrastructure (Bicep)
  - Configure networking
  - Setup CI/CD pipelines
  
Phase 3: Data Migration (2-4 weeks)
  - Database Migration Service
  - Initial data sync
  - Validation
  
Phase 4: Application Migration (2-4 weeks)
  - Deploy to staging
  - Integration testing
  - Performance testing
  
Phase 5: Cutover (1 week)
  - DNS switchover
  - Monitor closely
  - Rollback plan ready
```

## ⚡ Quick Start

```bash
# 1. Clone template
git clone https://github.com/myorg/monolith-template
cd monolith-template

# 2. Create Azure resources
az group create --name rg-myapp-dev --location eastus

az deployment group create \
  --resource-group rg-myapp-dev \
  --template-file infrastructure/main.bicep \
  --parameters appName=myapp environment=dev sqlAdminPassword=<strong-password>

# 3. Configure connection strings
az webapp config connection-string set \
  --name app-myapp-dev \
  --resource-group rg-myapp-dev \
  --connection-string-type SQLAzure \
  --settings DefaultConnection="<sql-connection-string>"

# 4. Deploy application
az webapp deployment source config-zip \
  --name app-myapp-dev \
  --resource-group rg-myapp-dev \
  --src ./publish.zip

# 5. Verify
curl https://app-myapp-dev.azurewebsites.net/health
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
