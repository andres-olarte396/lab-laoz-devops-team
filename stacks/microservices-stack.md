# Microservices Stack - Azure Kubernetes

## 📋 Overview

Stack optimizado para arquitecturas de microservicios ejecutándose en Azure Kubernetes Service (AKS).

### Ideal Para
- ✅ Sistemas complejos con múltiples dominios de negocio
- ✅ Equipos grandes y autónomos
- ✅ Necesidades de escalamiento independiente
- ✅ Alta disponibilidad y resiliencia
- ✅ Deployment frecuente de servicios individuales

### NO Usar Cuando
- ❌ Equipo pequeño (<5 developers)
- ❌ MVP o prototipo rápido
- ❌ Presupuesto limitado (<$500/mes)
- ❌ Dominio de negocio simple
- ❌ Baja experiencia en Kubernetes

### Ventajas
- 🚀 Escalamiento independiente por servicio
- 🔄 Deployments independientes
- 🛡️ Fault isolation
- 🎯 Technology diversity (diferentes lenguajes por servicio)
- 👥 Team autonomy

### Desventajas
- 💰 Costo base alto ($800-1500/mes)
- 🔧 Complejidad operativa alta
- 📚 Steep learning curve
- 🐛 Debugging distribuido complejo
- 🔗 Network overhead

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Azure Front Door                          │
│                    (CDN + WAF)                              │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│              Azure Application Gateway                       │
│              (Ingress Controller)                           │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                                                              │
│            Azure Kubernetes Service (AKS)                    │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ Service A    │  │ Service B    │  │ Service C    │      │
│  │ (Pods)       │  │ (Pods)       │  │ (Pods)       │      │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘      │
│         │                  │                  │              │
│  ┌──────▼──────────────────▼──────────────────▼───────┐    │
│  │         Service Mesh (Istio/Linkerd)              │    │
│  └───────────────────────────────────────────────────┘    │
│                                                              │
└──────────────────────┬──────────────────────────────────────┘
                       │
         ┌─────────────┼─────────────┐
         │             │             │
┌────────▼───────┐ ┌──▼──────┐ ┌───▼────────┐
│ Azure SQL DB   │ │ Cosmos  │ │ Redis      │
│                │ │ DB      │ │ Cache      │
└────────────────┘ └─────────┘ └────────────┘

         │
┌────────▼───────────────────────────┐
│    Azure Service Bus / Event Hub   │
│    (Async Communication)           │
└────────────────────────────────────┘
```

## 🛠️ Technology Stack

### Compute
```yaml
Primary:
  - Azure Kubernetes Service (AKS)
  - Node Pools: 
      - System: 2-3 nodes (Standard_D4s_v3)
      - User: 3-10 nodes (Standard_D8s_v3 + autoscaling)
  - Availability Zones: Enabled (3 zones)
  
Container Runtime:
  - containerd
  - Azure Container Registry (ACR) for images
```

### Orchestration
```yaml
Kubernetes:
  - Version: 1.28+ (latest stable)
  - Cluster Autoscaler: Enabled
  - Pod Autoscaler: HPA + KEDA
  
Service Mesh:
  - Istio 1.20+ or Linkerd 2.14+
  - mTLS between services
  - Traffic management
  - Observability
  
Ingress:
  - NGINX Ingress Controller or
  - Azure Application Gateway Ingress Controller (AGIC)
  - Cert-manager for TLS
```

### Storage & Data
```yaml
Databases:
  - Azure SQL Database (relational data)
  - Cosmos DB (document/NoSQL)
  - Azure Database for PostgreSQL (si preferido a SQL)
  
Caching:
  - Azure Cache for Redis
  
Object Storage:
  - Azure Blob Storage
  
Messaging:
  - Azure Service Bus (transactional)
  - Azure Event Hub (streaming)
  - RabbitMQ (si on-cluster preferido)
```

### CI/CD
```yaml
Source Control:
  - GitHub / Azure Repos
  
CI/CD Platform:
  - GitHub Actions (preferred) or
  - Azure DevOps Pipelines
  
GitOps:
  - ArgoCD or Flux CD
  - Helm for packaging
  
Artifact Registry:
  - Azure Container Registry (ACR)
  - Helm chart repository
```

### Monitoring & Observability
```yaml
Metrics:
  - Prometheus (in-cluster)
  - Azure Monitor for containers
  
Visualization:
  - Grafana
  
Logging:
  - Fluent Bit → Azure Log Analytics
  - Alternative: ELK Stack
  
Tracing:
  - Jaeger or Azure Application Insights
  - OpenTelemetry for instrumentation
  
Alerting:
  - Prometheus Alertmanager
  - Azure Monitor Alerts
  - PagerDuty integration
```

### Security
```yaml
Identity:
  - Azure AD Workload Identity
  - Managed Identities
  
Secrets:
  - Azure Key Vault
  - External Secrets Operator
  
Network Security:
  - Network Policies (Calico/Azure NPM)
  - Azure Firewall
  - Private Endpoints
  
Security Scanning:
  - Trivy (container scanning)
  - OPA/Gatekeeper (policy enforcement)
  - Aqua/Twistlock (runtime security)
  
API Security:
  - Azure API Management (optional)
  - OAuth2/OpenID Connect
  - Rate limiting
```

## 📁 Infrastructure as Code

### Terraform Structure
```hcl
# Directory structure
terraform/
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
├── modules/
│   ├── aks-cluster/
│   ├── acr/
│   ├── databases/
│   ├── networking/
│   └── monitoring/
└── global/

# Example: AKS Cluster Module
module "aks" {
  source = "./modules/aks-cluster"
  
  cluster_name        = "microservices-${var.environment}"
  resource_group_name = azurerm_resource_group.main.name
  location            = var.location
  
  kubernetes_version = "1.28"
  
  default_node_pool = {
    name       = "system"
    vm_size    = "Standard_D4s_v3"
    node_count = 3
    min_count  = 2
    max_count  = 5
  }
  
  additional_node_pools = [
    {
      name       = "apps"
      vm_size    = "Standard_D8s_v3"
      node_count = 3
      min_count  = 3
      max_count  = 10
    }
  ]
  
  network_profile = {
    network_plugin    = "azure"
    service_cidr      = "10.0.0.0/16"
    dns_service_ip    = "10.0.0.10"
  }
  
  enable_auto_scaling = true
  enable_pod_security_policy = true
  
  tags = var.common_tags
}
```

### Kubernetes Manifests Structure
```yaml
# k8s/
k8s/
├── base/                    # Kustomize base
│   ├── namespace.yaml
│   ├── service-mesh/
│   ├── ingress/
│   └── monitoring/
├── services/
│   ├── service-a/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   ├── hpa.yaml
│   │   └── configmap.yaml
│   ├── service-b/
│   └── service-c/
└── overlays/
    ├── dev/
    ├── staging/
    └── prod/
```

## 🚀 CI/CD Pipeline

### Multi-Service Pipeline Strategy
```yaml
# .github/workflows/microservice-deploy.yml
name: Microservice Deploy

on:
  push:
    paths:
      - 'services/service-a/**'
    branches: [main]

jobs:
  detect-changes:
    runs-on: ubuntu-latest
    outputs:
      services: ${{ steps.filter.outputs.changes }}
    steps:
      - uses: dorny/paths-filter@v2
        id: filter
        with:
          filters: |
            service-a:
              - 'services/service-a/**'
            service-b:
              - 'services/service-b/**'

  build-and-test:
    needs: detect-changes
    runs-on: ubuntu-latest
    strategy:
      matrix:
        service: ${{ fromJSON(needs.detect-changes.outputs.services) }}
    steps:
      - uses: actions/checkout@v3
      
      - name: Build Docker Image
        run: |
          docker build -t ${{ env.ACR_NAME }}.azurecr.io/${{ matrix.service }}:${{ github.sha }} \
            -f services/${{ matrix.service }}/Dockerfile \
            services/${{ matrix.service }}
      
      - name: Run Tests
        run: |
          docker run --rm ${{ env.ACR_NAME }}.azurecr.io/${{ matrix.service }}:${{ github.sha }} \
            npm test
      
      - name: Security Scan
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: ${{ env.ACR_NAME }}.azurecr.io/${{ matrix.service }}:${{ github.sha }}
          severity: 'CRITICAL,HIGH'
      
      - name: Push to ACR
        run: |
          az acr login --name ${{ env.ACR_NAME }}
          docker push ${{ env.ACR_NAME }}.azurecr.io/${{ matrix.service }}:${{ github.sha }}

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    steps:
      - name: Update ArgoCD Application
        run: |
          # Update image tag in GitOps repo
          # ArgoCD auto-syncs and deploys
```

### Deployment Strategy
```yaml
# Progressive Delivery con Argo Rollouts
apiVersion: argoproj.io/v1alpha1
kind: Rollout
metadata:
  name: service-a
spec:
  replicas: 5
  strategy:
    canary:
      steps:
      - setWeight: 20
      - pause: {duration: 5m}
      - setWeight: 40
      - pause: {duration: 5m}
      - setWeight: 60
      - pause: {duration: 5m}
      - setWeight: 80
      - pause: {duration: 5m}
      
      analysis:
        templates:
        - templateName: success-rate
        startingStep: 2
        
      trafficRouting:
        istio:
          virtualService:
            name: service-a-vsvc
```

## 📊 Monitoring & Observability

### Key Metrics
```yaml
# Golden Signals per Service
Latency:
  - P50, P95, P99 response time
  - Measure: Histogram
  - Alert: P95 > 200ms

Traffic:
  - Requests per second
  - Measure: Counter
  - Alert: Sudden drop >50%

Errors:
  - Error rate %
  - Measure: Counter
  - Alert: >1% for 5min

Saturation:
  - CPU, Memory utilization
  - Pod count vs limits
  - Alert: >80% sustained

# Infrastructure Metrics
Cluster:
  - Node CPU/Memory
  - Pod count
  - PVC usage
  
Network:
  - Ingress traffic
  - Service mesh latency
  - Connection pool status
```

### Dashboards
```yaml
Required Dashboards:
  1. Cluster Overview
     - Node health
     - Resource utilization
     - Pod status
  
  2. Service Overview (per service)
     - Request rate, latency, errors
     - Dependencies map
     - Resource usage
  
  3. Service Mesh
     - Traffic flow
     - Success rate per route
     - mTLS status
  
  4. Business Metrics
     - Transactions/sec
     - Conversion rate
     - Custom KPIs
```

### Alerting Rules
```yaml
# Prometheus alerts
groups:
- name: microservices
  rules:
  - alert: HighErrorRate
    expr: |
      rate(http_requests_total{status=~"5.."}[5m]) 
      / rate(http_requests_total[5m]) > 0.01
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "High error rate on {{ $labels.service }}"
  
  - alert: HighLatency
    expr: |
      histogram_quantile(0.95, 
        rate(http_request_duration_seconds_bucket[5m])
      ) > 0.2
    for: 5m
    labels:
      severity: warning
    annotations:
      summary: "High P95 latency on {{ $labels.service }}"
  
  - alert: PodCrashLooping
    expr: |
      rate(kube_pod_container_status_restarts_total[15m]) > 0
    for: 5m
    labels:
      severity: warning
```

## 🔒 Security Baseline

### Network Security
```yaml
# Network Policy Example
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: service-a-netpol
spec:
  podSelector:
    matchLabels:
      app: service-a
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: api-gateway
    ports:
    - protocol: TCP
      port: 8080
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: service-b
    ports:
    - protocol: TCP
      port: 8080
  - to:
    - namespaceSelector:
        matchLabels:
          name: data
    ports:
    - protocol: TCP
      port: 5432
```

### Pod Security
```yaml
# Pod Security Standards
apiVersion: v1
kind: Pod
metadata:
  name: service-a
spec:
  securityContext:
    runAsNonRoot: true
    runAsUser: 1000
    fsGroup: 2000
    seccompProfile:
      type: RuntimeDefault
  
  containers:
  - name: app
    image: myapp:latest
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop:
        - ALL
    resources:
      requests:
        memory: "256Mi"
        cpu: "250m"
      limits:
        memory: "512Mi"
        cpu: "500m"
```

### Secrets Management
```yaml
# Using External Secrets Operator
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: service-a-secrets
spec:
  refreshInterval: 1h
  secretStoreRef:
    name: azure-keyvault
    kind: SecretStore
  target:
    name: service-a-secrets
  data:
  - secretKey: db-password
    remoteRef:
      key: service-a-db-password
```

## 💰 Cost Estimation

### Base Monthly Cost (Production)
```yaml
Compute (AKS):
  - System node pool (3x D4s_v3): ~$430
  - User node pool (5x D8s_v3): ~$1,430
  - Subtotal: ~$1,860/month

Storage:
  - Managed Disks (500GB): ~$50
  - Blob Storage (1TB): ~$20
  - Subtotal: ~$70/month

Database:
  - Azure SQL (S3): ~$200
  - Cosmos DB (400 RU/s): ~$100
  - Redis Cache (C1): ~$75
  - Subtotal: ~$375/month

Networking:
  - Load Balancer: ~$20
  - Application Gateway: ~$140
  - Bandwidth: ~$50
  - Subtotal: ~$210/month

Monitoring:
  - Log Analytics: ~$100
  - Application Insights: ~$50
  - Subtotal: ~$150/month

Total Base Cost: ~$2,665/month
```

### Cost Optimization
- Reserved instances: Save 30-40% en compute
- Autoscaling: Escalar durante horas no-pico
- Spot instances: Para workloads tolerantes
- Storage tiering: Mover datos antiguos a cool/archive

### Cost by Scale
- **Small** (dev): ~$600/month
- **Medium** (staging): ~$1,200/month
- **Large** (production): ~$2,665/month
- **X-Large** (high traffic): ~$5,000+/month

## 🔄 Migration Path

### From Monolith
```yaml
Strategy: Strangler Fig Pattern

Phases:
  1. Extract Edge Services (2-4 weeks)
     - Auth service
     - API Gateway
     - Static content
  
  2. Extract Business Capabilities (2-3 months)
     - Identify bounded contexts
     - One service at a time
     - Keep monolith running
  
  3. Data Migration (ongoing)
     - Dual-write pattern
     - Eventual consistency
     - Saga pattern for distributed transactions
  
  4. Decommission Monolith (final phase)
     - When <10% traffic remains
```

### From VMs
```yaml
Strategy: Lift and Shift + Refactor

Phases:
  1. Containerize (1-2 months)
     - Create Dockerfiles
     - Test locally
     - Push to ACR
  
  2. Deploy to AKS (2-4 weeks)
     - Create K8s manifests
     - Deploy to dev environment
     - Load testing
  
  3. Migrate Services (3-6 months)
     - One service at a time
     - Blue-green deployment
     - Rollback plan ready
  
  4. Optimize (ongoing)
     - Right-size resources
     - Implement autoscaling
     - Add service mesh
```

## ⚡ Quick Start (15 min)

```bash
# 1. Prerequisites
az login
az account set --subscription <subscription-id>

# 2. Clone template
git clone https://github.com/[org]/microservices-template.git my-project
cd my-project

# 3. Initialize Terraform
cd terraform/environments/dev
terraform init

# 4. Create infrastructure
terraform plan -out=tfplan
terraform apply tfplan
# Wait ~15-20 minutes for AKS cluster

# 5. Connect to cluster
az aks get-credentials --resource-group rg-my-project-dev --name aks-my-project-dev

# 6. Deploy baseline (Istio, monitoring, etc.)
kubectl apply -f k8s/base/

# 7. Deploy sample service
kubectl apply -f k8s/services/sample-api/

# 8. Verify
kubectl get pods -A
kubectl get svc -A

# 9. Access application
kubectl port-forward svc/sample-api 8080:80
# Visit http://localhost:8080

# 10. Setup ArgoCD for GitOps
kubectl apply -f k8s/base/argocd/
```

## 📚 Additional Resources

- [Microservices Patterns](https://microservices.io/patterns)
- [AKS Best Practices](https://docs.microsoft.com/azure/aks/best-practices)
- [Istio Documentation](https://istio.io/docs)
- [12-Factor App](https://12factor.net/)

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
