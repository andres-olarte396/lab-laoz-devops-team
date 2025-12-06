# Herramientas y Stack Tecnológico

Este documento cataloga todas las herramientas utilizadas por el equipo DevOps, organizadas por categoría con sus casos de uso específicos.

## 📊 Índice por Categoría

1. [Cloud Platforms](#-cloud-platforms)
2. [Infrastructure as Code](#-infrastructure-as-code)
3. [CI/CD](#-cicd)
4. [Containerización](#-containerización)
5. [Orchestration](#-orchestration)
6. [Monitoring & Observability](#-monitoring--observability)
7. [Security](#-security)
8. [Configuration Management](#-configuration-management)
9. [Collaboration](#-collaboration)
10. [Cost Management](#-cost-management)

---

## ☁️ Cloud Platforms

### Microsoft Azure
**Propósito**: Plataforma cloud principal  
**Usado Por**: Todo el equipo  
**Casos de Uso**:
- Hosting de aplicaciones (App Services, AKS)
- Storage (Blob, Files, Queues)
- Databases (SQL Database, Cosmos DB)
- Networking (VNet, Load Balancer)

**Servicios Clave**:
```
Compute:
├── Azure App Service (Web apps, APIs)
├── Azure Kubernetes Service (AKS)
├── Azure Functions (Serverless)
└── Virtual Machines

Storage:
├── Blob Storage
├── Azure Files
├── Queue Storage
└── Disk Storage

Data:
├── Azure SQL Database
├── Cosmos DB
├── Azure Database for PostgreSQL/MySQL
└── Azure Cache for Redis

Networking:
├── Virtual Network (VNet)
├── Load Balancer
├── Application Gateway
├── Azure Front Door
└── Azure DNS
```

### AWS (Amazon Web Services)
**Propósito**: Plataforma cloud secundaria / multi-cloud  
**Usado Por**: Cloud Engineer, Platform Engineer  
**Servicios Equivalentes a Azure**:
- EC2 ↔ Virtual Machines
- EKS ↔ AKS
- Lambda ↔ Azure Functions
- S3 ↔ Blob Storage
- RDS ↔ Azure SQL Database

---

## 🏗️ Infrastructure as Code

### Terraform
**Propósito**: IaC multi-cloud  
**Usado Por**: Cloud Engineer, Platform Engineer  
**Casos de Uso**:
- Provisionar infraestructura en Azure/AWS
- Gestionar recursos cloud declarativamente
- Módulos reutilizables para estándares

**Stack**:
```hcl
Tool: Terraform v1.6+
State Backend: Azure Storage / Terraform Cloud
Modules: Internal module registry
Providers: azurerm, aws, kubernetes
```

### Bicep
**Propósito**: IaC nativo de Azure  
**Usado Por**: Cloud Engineer  
**Casos de Uso**:
- Recursos Azure-specific
- Templates ARM simplificados
- Integración nativa con Azure

### Pulumi
**Propósito**: IaC con lenguajes de programación  
**Usado Por**: Platform Engineer  
**Casos de Uso**:
- IaC complejo con lógica
- Reutilización de código
- Type-safety

---

## 🚀 CI/CD

### GitHub Actions
**Propósito**: CI/CD nativo de GitHub  
**Usado Por**: CI/CD Engineer, Development Teams  
**Casos de Uso**:
- Build y test automation
- Deployment pipelines
- Scheduled jobs

**Workflow Example**:
```yaml
Stages:
├── Checkout code
├── Setup environment
├── Install dependencies
├── Run linters
├── Run tests
├── Build artifacts
├── Security scanning
└── Deploy
```

### Azure DevOps
**Propósito**: CI/CD enterprise  
**Usado Por**: CI/CD Engineer  
**Casos de Uso**:
- Pipelines complejos multi-stage
- Artifact management
- Release orchestration

**Components**:
- Azure Pipelines (CI/CD)
- Azure Repos (Git)
- Azure Artifacts (package registry)
- Azure Boards (work tracking)

### ArgoCD
**Propósito**: GitOps continuous delivery para Kubernetes  
**Usado Por**: Platform Engineer, CI/CD Engineer  
**Casos de Uso**:
- Declarative Kubernetes deployments
- Automated sync from Git
- Multi-cluster management

### Jenkins
**Propósito**: Automation server (legacy systems)  
**Usado Por**: CI/CD Engineer  
**Casos de Uso**:
- Legacy pipelines (migration to GitHub Actions in progress)
- Custom automation jobs

---

## 📦 Containerización

### Docker
**Propósito**: Containerización de aplicaciones  
**Usado Por**: Todo el equipo  
**Casos de Uso**:
- Build de container images
- Local development environments
- Multi-stage builds

### Azure Container Registry (ACR)
**Propósito**: Container image registry  
**Usado Por**: CI/CD Engineer, Platform Engineer  
**Casos de Uso**:
- Almacenar container images
- Vulnerability scanning
- Geo-replication

### Docker Compose
**Propósito**: Multi-container local development  
**Usado Por**: Development Teams  
**Casos de Uso**:
- Local development stacks
- Integration testing

---

## ⚙️ Orchestration

### Kubernetes
**Propósito**: Container orchestration  
**Usado Por**: Platform Engineer, SRE  
**Casos de Uso**:
- Production workload orchestration
- Auto-scaling
- Service discovery

**Ecosystem**:
```
Core:
├── AKS (Azure Kubernetes Service)
├── kubectl (CLI)
└── kubeconfig management

Extensions:
├── Helm (package manager)
├── Kustomize (configuration management)
├── Cert-manager (certificate automation)
└── External-dns (DNS automation)
```

### Helm
**Propósito**: Package manager para Kubernetes  
**Usado Por**: Platform Engineer  
**Casos de Uso**:
- Deploy aplicaciones pre-packaged
- Templating de manifests
- Release management

---

## 📊 Monitoring & Observability

### Prometheus
**Propósito**: Metrics collection y alerting  
**Usado Por**: SRE  
**Casos de Uso**:
- Time-series metrics
- Alerting rules
- Service monitoring

### Grafana
**Propósito**: Visualization y dashboards  
**Usado Por**: SRE, DevOps Lead  
**Casos de Uso**:
- Metrics visualization
- Custom dashboards
- Alerting

**Dashboard Types**:
- Infrastructure overview
- Application metrics
- SLO tracking
- Cost dashboards

### ELK Stack (Elasticsearch, Logstash, Kibana)
**Propósito**: Log aggregation y analysis  
**Usado Por**: SRE  
**Casos de Uso**:
- Centralized logging
- Log search y analysis
- Log visualization

**Alternative**: Azure Monitor Logs / Log Analytics

### Datadog
**Propósito**: Full-stack observability  
**Usado Por**: SRE, Platform Engineer  
**Casos de Uso**:
- APM (Application Performance Monitoring)
- Infrastructure monitoring
- Log management
- Synthetic monitoring

### Jaeger / Zipkin
**Propósito**: Distributed tracing  
**Usado Por**: SRE  
**Casos de Uso**:
- Trace requests across microservices
- Performance bottleneck identification
- Dependency analysis

### PagerDuty
**Propósito**: Incident management y on-call  
**Usado Por**: SRE, DevOps Lead  
**Casos de Uso**:
- On-call scheduling
- Alert routing
- Escalation policies
- Incident tracking

---

## 🔒 Security

### Snyk
**Propósito**: Dependency vulnerability scanning  
**Usado Por**: Security Engineer  
**Casos de Uso**:
- Open source dependency scanning
- Container image scanning
- IaC scanning

### SonarQube
**Propósito**: Code quality y SAST  
**Usado Por**: Security Engineer, CI/CD Engineer  
**Casos de Uso**:
- Static code analysis
- Security vulnerability detection
- Code smell detection
- Technical debt tracking

### OWASP ZAP
**Propósito**: DAST (Dynamic Application Security Testing)  
**Usado Por**: Security Engineer  
**Casos de Uso**:
- Web application security testing
- API security testing
- Penetration testing

### Azure Key Vault
**Propósito**: Secrets management  
**Usado Por**: Security Engineer, Platform Engineer  
**Casos de Uso**:
- Store secrets, keys, certificates
- Managed identities integration
- Secret rotation

### Trivy
**Propósito**: Container y IaC security scanning  
**Usado Por**: Security Engineer  
**Casos de Uso**:
- Container image vulnerability scanning
- IaC misconfiguration detection
- Filesystem scanning

### OPA (Open Policy Agent)
**Propósito**: Policy as Code  
**Usado Por**: Security Engineer, Platform Engineer  
**Casos de Uso**:
- Kubernetes admission control
- Terraform policy enforcement
- API authorization

---

## ⚙️ Configuration Management

### Ansible
**Propósito**: Configuration management y automation  
**Usado Por**: SRE, Platform Engineer  
**Casos de Uso**:
- Server configuration
- Application deployment (legacy)
- Orchestration tasks

### Git
**Propósito**: Version control  
**Usado Por**: Todo el equipo  
**Plataformas**:
- GitHub (primary)
- Azure Repos (enterprise projects)

**Branching Strategy**: GitFlow / Trunk-based development

---

## 💬 Collaboration

### Slack
**Propósito**: Team communication  
**Usado Por**: Todo el equipo  
**Canales Clave**:
- `#incidents` - Incident coordination
- `#devops-support` - Support requests
- `#deployments` - Deployment notifications
- `#alerts` - Automated alerts

### Microsoft Teams
**Propósito**: Enterprise communication  
**Usado Por**: Todo el equipo  
**Casos de Uso**:
- Video meetings
- Cross-team collaboration
- Document sharing

### Confluence
**Propósito**: Documentation y knowledge base  
**Usado Por**: Todo el equipo  
**Casos de Uso**:
- Runbooks
- Architecture documentation
- Post-mortems
- Team wiki

### Jira
**Propósito**: Work tracking  
**Usado Por**: DevOps Lead, todo el equipo  
**Casos de Uso**:
- Sprint planning
- Incident tracking
- Change requests
- Service desk

---

## 💰 Cost Management

### Azure Cost Management
**Propósito**: Azure cost analysis  
**Usado Por**: Cloud Engineer, DevOps Lead  
**Casos de Uso**:
- Cost analysis y reporting
- Budget alerts
- Cost allocation by tags

### Infracost
**Propósito**: IaC cost estimation  
**Usado Por**: Cloud Engineer  
**Casos de Uso**:
- Terraform cost estimation
- PR cost comments
- Cost policy enforcement

### CloudHealth / CloudCheckr
**Propósito**: Multi-cloud cost optimization  
**Usado Por**: Cloud Engineer, DevOps Lead  
**Casos de Uso**:
- Cost optimization recommendations
- Reserved instance planning
- Multi-cloud cost visibility

---

## 🔧 Development Tools

### Visual Studio Code
**Propósito**: Primary IDE  
**Usado Por**: Todo el equipo  
**Extensiones Clave**:
- Terraform
- Kubernetes
- Docker
- YAML
- GitLens

### kubectl
**Propósito**: Kubernetes CLI  
**Usado Por**: Platform Engineer, SRE  
**Plugins**:
- kubectx/kubens
- stern (log viewing)
- k9s (terminal UI)

### Azure CLI (az)
**Propósito**: Azure management CLI  
**Usado Por**: Cloud Engineer, Platform Engineer  

### Terraform CLI
**Propósito**: Infrastructure management  
**Usado Por**: Cloud Engineer, Platform Engineer  

---

## 📚 Tool Selection Criteria

Al evaluar nuevas herramientas, consideramos:

### Technical Criteria
- ✅ Compatibility con stack existente
- ✅ Scalability para nuestro uso
- ✅ API availability para automatización
- ✅ Multi-cloud support (preferido)
- ✅ Active development y community

### Operational Criteria
- ✅ Ease of maintenance
- ✅ Documentation quality
- ✅ Learning curve
- ✅ Support options

### Business Criteria
- ✅ Total cost of ownership
- ✅ Vendor lock-in risk
- ✅ Security y compliance
- ✅ SLA guarantees

---

## 🔄 Tool Lifecycle

### Evaluation (2-4 semanas)
- Proof of concept
- Technical validation
- Cost analysis
- Security review

### Pilot (1-3 meses)
- Limited deployment
- Feedback collection
- Performance validation
- Training materials

### Adoption (3-6 meses)
- Full rollout
- Documentation
- Team training
- Process integration

### Deprecation
- Migration plan
- Timeline communication
- Data export
- License termination

---

## 📞 Tool Owners

| Categoría | Primary Owner | Backup |
|-----------|---------------|--------|
| Cloud Platforms | Cloud Engineer | DevOps Lead |
| IaC | Cloud Engineer | Platform Engineer |
| CI/CD | CI/CD Engineer | DevOps Lead |
| Kubernetes | Platform Engineer | SRE |
| Monitoring | SRE | Platform Engineer |
| Security Tools | Security Engineer | DevOps Lead |
| Cost Management | Cloud Engineer | DevOps Lead |

---

**Última actualización**: Diciembre 2025
