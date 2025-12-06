# Equipo DevOps

## 📋 Visión General

El equipo de DevOps actúa como **Platform Team** en el modelo Team Topologies, proporcionando servicios de infraestructura, CI/CD, y herramientas que habilitan a los equipos de desarrollo para entregar software de manera rápida y confiable.

## 🎯 Misión del Equipo

> "Construir y mantener plataformas internas que permitan a los equipos de desarrollo desplegar software de manera autónoma, segura y eficiente."

### Principios Clave

- **Self-Service**: Los equipos de desarrollo pueden desplegar sin depender de tickets a DevOps
- **Automation First**: Todo lo que se hace más de una vez se automatiza
- **Infrastructure as Code**: Toda infraestructura es versionada y reproducible
- **Security by Default**: Seguridad integrada desde el diseño
- **Observability**: Visibilidad completa de sistemas en producción

## 👥 Roles del Equipo

### 1. [Platform Engineer](platform-engineer.md)

**Focus**: Construir plataformas internas y herramientas para developers

```yaml
Responsabilidades:
  - Kubernetes platform management
  - Internal Developer Platform (IDP)
  - CI/CD pipelines como producto
  - Developer tooling

Tech Stack:
  - Kubernetes / Azure Kubernetes Service
  - Terraform / Bicep
  - Azure DevOps / GitHub Actions
  - ArgoCD / Flux

Seniority: Típicamente Senior (5+ años)
```

### 2. [Cloud Engineer](cloud-engineer.md)

**Focus**: Diseño y gestión de infraestructura cloud

```yaml
Responsabilidades:
  - Azure infrastructure design
  - Resource optimization (cost + performance)
  - Networking & security
  - Disaster recovery

Tech Stack:
  - Azure (Compute, Storage, Networking)
  - Terraform / Bicep
  - Azure CLI / PowerShell
  - ARM Templates

Seniority: Mid to Senior (3-8 años)
```

### 3. [Site Reliability Engineer (SRE)](sre.md)

**Focus**: Reliability, performance, y incident response

```yaml
Responsabilidades:
  - Service reliability (SLIs, SLOs, SLAs)
  - Incident response & postmortems
  - Performance optimization
  - Capacity planning

Tech Stack:
  - Application Insights / Grafana
  - Azure Monitor
  - Prometheus
  - On-call tooling (PagerDuty)

Seniority: Senior (5+ años)
```

### 4. [CI/CD Engineer](cicd-engineer.md)

**Focus**: Build, test, y deployment automation

```yaml
Responsabilidades:
  - CI/CD pipeline design
  - Build optimization
  - Deployment strategies (blue/green, canary)
  - Release automation

Tech Stack:
  - GitHub Actions
  - Azure Pipelines
  - Jenkins
  - ArgoCD

Seniority: Mid to Senior (3-8 años)
```

### 5. [Security Engineer (DevSecOps)](security-engineer.md)

**Focus**: Seguridad integrada en CI/CD y runtime

```yaml
Responsabilidades:
  - Security scanning (SAST, DAST)
  - Vulnerability management
  - Compliance automation
  - Security policies as code

Tech Stack:
  - SonarQube / Snyk
  - Azure Security Center
  - Trivy / Grype (container scanning)
  - Open Policy Agent

Seniority: Senior (5+ años)
```

### 6. [DevOps Lead](devops-lead.md)

**Focus**: Liderazgo técnico y estrategia del equipo

```yaml
Responsabilidades:
  - DevOps strategy & roadmap
  - Platform architecture
  - Team mentorship
  - Cross-team collaboration

Tech Stack:
  - Amplio conocimiento de todas las áreas
  - Strategic thinking
  - Technical leadership

Seniority: Staff / Lead (8+ años)
```

## 🏗️ Estructura del Equipo

### Team Size por Company Stage

```yaml
Startup (10-20 people total):
  DevOps Team: 1 person
  Profile: Generalist DevOps Engineer
  Focus: MVP infrastructure, basic CI/CD

Scale-up (20-50 people):
  DevOps Team: 2-3 people
  Roles:
    - 1 Senior DevOps/Platform Engineer (lead)
    - 1-2 Mid DevOps/Cloud Engineers
  Focus: Platform stabilization, automation

Medium Company (50-100 people):
  DevOps Team: 4-6 people
  Roles:
    - 1 DevOps Lead
    - 2 Platform Engineers
    - 1 SRE
    - 1 Cloud Engineer
    - 1 Security Engineer (or shared)
  Focus: Self-service platform, reliability

Enterprise (100+ people):
  DevOps Team: 8-15 people
  Roles:
    - 1 DevOps Lead
    - 3-4 Platform Engineers
    - 2-3 SREs
    - 2 Cloud Engineers
    - 1-2 Security Engineers
    - 1-2 CI/CD Engineers
  Focus: Multi-tenant platform, advanced tooling
```

### Reporting Structure

```
Director of Engineering
    │
    ├── Engineering Manager (Development Teams)
    │   ├── Tech Lead (Frontend)
    │   ├── Tech Lead (Backend)
    │   └── Tech Lead (Mobile)
    │
    └── DevOps Lead / Platform Lead
        ├── Platform Engineers (2-4)
        ├── SREs (1-3)
        ├── Cloud Engineers (1-2)
        └── Security Engineer (1-2)
```

## 🎯 Ownership Model

### What DevOps Owns

```yaml
Infrastructure: ✓ Kubernetes clusters
  ✓ Azure subscriptions & resources
  ✓ Networking (VNets, subnets, NSGs)
  ✓ Identity & Access Management
  ✓ Cost optimization

CI/CD: ✓ Pipeline templates & frameworks
  ✓ Build agents & runners
  ✓ Artifact repositories
  ✓ Deployment tooling

Observability: ✓ Monitoring platform (Application Insights, Grafana)
  ✓ Logging aggregation
  ✓ Alerting rules & routing
  ✓ Dashboards (platform-level)

Security: ✓ Security scanning tools
  ✓ Secrets management (Azure Key Vault)
  ✓ Network security
  ✓ Compliance automation
```

### What Development Teams Own (with DevOps support)

```yaml
Applications:
  ✓ Application code
  ✓ Application-specific pipelines (using DevOps templates)
  ✓ Application monitoring & alerts
  ✓ Deployment manifests (Helm charts, K8s manifests)
  ✓ Database migrations

Responsibility:
  - DevOps provides: Platform, tools, templates
  - Development uses: Self-service capabilities
  - Partnership: "You build it, you run it" (with platform support)
```

## 🔄 Interaction Modes (Team Topologies)

### X-as-a-Service (Primary - 70%)

```yaml
Modelo:
  - DevOps provides platform & tools as a service
  - Development teams consume self-service
  - Minimal hand-offs, maximum autonomy

Examples:
  - CI/CD pipeline templates
  - Kubernetes namespace provisioning (automated)
  - Monitoring dashboards (automated)
  - Secret rotation (automated)

Communication:
  - Documentation & runbooks
  - Internal portal (developer portal)
  - Async (tickets only for exceptions)
```

### Collaboration (20%)

```yaml
Contexto:
  - New infrastructure patterns
  - Complex integrations
  - Performance troubleshooting
  - Security incidents

Examples:
  - Architecture design sessions
  - Production incident response
  - Performance optimization
  - Security reviews

Communication:
  - Scheduled sessions
  - War rooms (incidents)
  - Design reviews
```

### Facilitating (10%)

```yaml
Contexto:
  - Knowledge transfer
  - Upskilling development teams
  - New technology adoption

Examples:
  - Kubernetes training
  - CI/CD best practices
  - Infrastructure as Code workshops
  - Security awareness

Communication:
  - Workshops & training
  - Documentation
  - Office hours
  - Pair programming
```

## 📊 Tech Stack del Equipo

### Infrastructure as Code

```yaml
Primary:
  - Terraform (multi-cloud, mature)
  - Bicep (Azure-native)

Supporting:
  - ARM Templates (legacy)
  - Pulumi (exploring)

Strategy:
  - Terraform for core infrastructure
  - Bicep for Azure-specific resources
  - Modular, reusable components
```

### Container Orchestration

```yaml
Platform:
  - Kubernetes (Azure Kubernetes Service)
  - Docker

Tools:
  - Helm (package management)
  - Kustomize (configuration management)
  - ArgoCD / Flux (GitOps)

Add-ons:
  - Istio / Linkerd (service mesh)
  - KEDA (autoscaling)
  - Cert-manager (certificates)
```

### CI/CD

```yaml
Primary:
  - GitHub Actions (preferred for new projects)
  - Azure Pipelines (legacy, migration in progress)

Supporting:
  - Jenkins (legacy workloads)
  - ArgoCD (deployments)

Strategy:
  - Standardized pipeline templates
  - Reusable workflows
  - Self-service pipeline generation
```

### Observability

```yaml
Monitoring:
  - Azure Monitor / Application Insights (APM)
  - Grafana (visualization)
  - Prometheus (metrics)

Logging:
  - Azure Log Analytics
  - ELK Stack (Elasticsearch, Logstash, Kibana)

Tracing:
  - Application Insights (distributed tracing)
  - Jaeger (exploring)

Alerting:
  - Azure Monitor Alerts
  - PagerDuty (on-call management)
```

### Security

```yaml
Scanning:
  - SonarQube (SAST)
  - Snyk / Trivy (dependency scanning)
  - Aqua / Trivy (container scanning)

Secrets:
  - Azure Key Vault
  - HashiCorp Vault (exploring)

Policies:
  - Open Policy Agent (OPA)
  - Azure Policy

Compliance:
  - Terraform Compliance
  - Checkov
```

## 📈 Métricas del Equipo

### DORA Metrics (Team enables)

```yaml
Deployment Frequency:
  Elite: Multiple deploys per day
  High: Once per day to once per week
  Medium: Once per week to once per month
  Low: Less than once per month

  Target: Elite (platform enables this)

Lead Time for Changes:
  Elite: Less than 1 hour
  High: 1 day to 1 week
  Medium: 1 week to 1 month
  Low: More than 1 month

  Target: High to Elite

Mean Time to Recovery (MTTR):
  Elite: Less than 1 hour
  High: Less than 1 day
  Medium: 1 day to 1 week
  Low: More than 1 week

  Target: Elite (quick rollback capabilities)

Change Failure Rate:
  Elite: 0-15%
  High: 16-30%
  Medium: 31-45%
  Low: 46-60%

  Target: Elite
```

### Platform Metrics

```yaml
Reliability:
  - Platform uptime: > 99.9%
  - Kubernetes cluster availability: > 99.95%
  - Pipeline success rate: > 95%
  - Automated rollback success: > 99%

Performance:
  - Pipeline execution time: < 10 min (CI)
  - Deployment time: < 5 min
  - Infrastructure provisioning: < 15 min
  - Incident detection time: < 5 min

Developer Experience:
  - Time to first deployment (new service): < 2 hours
  - Self-service adoption: > 80%
  - Developer satisfaction: > 4/5
  - Support tickets trend: Decreasing

Cost:
  - Cloud cost optimization: 10-20% reduction annually
  - Resource utilization: > 70%
  - Waste elimination: Continuous
```

### Security Metrics

```yaml
Vulnerabilities:
  - Critical vulnerabilities: 0
  - High severity: < 5
  - Time to patch critical: < 24 hours
  - Security scanning coverage: 100%

Compliance:
  - Policy compliance: > 95%
  - Security audit findings: Decreasing
  - Secrets in code: 0
  - Encryption at rest/transit: 100%
```

## 🎯 OKRs Ejemplo (Q1 2025)

### Objective 1: Improve Developer Productivity

```yaml
Key Results:
  - KR1: Reduce pipeline execution time from 15min to 8min (47% improvement)
  - KR2: Achieve 90% self-service adoption for deployments (from 60%)
  - KR3: Time to provision new environment < 10 min (from 45 min)
```

### Objective 2: Enhance Platform Reliability

```yaml
Key Results:
  - KR1: Achieve 99.95% platform uptime (from 99.8%)
  - KR2: Reduce MTTR to < 30 min (from 2 hours)
  - KR3: Zero critical incidents caused by platform (from 2/quarter)
```

### Objective 3: Optimize Cloud Costs

```yaml
Key Results:
  - KR1: Reduce cloud spend by 15% through optimization
  - KR2: Implement autoscaling for 100% of services
  - KR3: Achieve 75% average resource utilization (from 45%)
```

## 🗓️ Ceremonias del Equipo

### Daily Standup (15 min)

```yaml
When: 9:00 AM
Format:
  - What did you do yesterday?
  - What will you do today?
  - Any blockers?
  - Incidents or critical issues

Focus: Quick sync, identify blockers
```

### Weekly Platform Review (1 hora)

```yaml
When: Monday 10:00 AM
Attendees: DevOps team + Tech Leads
Topics:
  - Platform metrics review
  - Upcoming infrastructure changes
  - Developer feedback
  - Roadmap updates
```

### Incident Postmortem (1 hora, ad-hoc)

```yaml
When: Within 48h of incident resolution
Format:
  - Timeline of events
  - Root cause analysis
  - What went well / What didn't
  - Action items (no blame)

Output: Postmortem document
```

### Sprint Planning (2 horas, bi-weekly)

```yaml
When: Every 2 weeks
Format:
  - Review backlog
  - Prioritize work
  - Technical feasibility
  - Capacity planning
  - Commitment
```

### Sprint Retrospective (1 hora, bi-weekly)

```yaml
When: End of sprint
Format:
  - What went well
  - What to improve
  - Action items
  - Process improvements
```

### On-Call Handoff (30 min, weekly)

```yaml
When: Monday morning
Format:
  - Previous week incidents
  - Known issues
  - Upcoming changes
  - Handoff to new on-call
```

## 🤝 Interacción con Otros Equipos

### Con Desarrollo (Daily)

```yaml
Mode: X-as-a-Service (primary) + Collaboration
Touchpoints:
  - Self-service platform usage (daily)
  - Pipeline support (as needed)
  - Architecture reviews (weekly)
  - Incident response (when needed)

Communication:
  - Slack channel: #devops-support
  - Documentation: Internal portal
  - Office hours: Wednesdays 2-4 PM
```

### Con Product (Weekly)

```yaml
Mode: Facilitating
Touchpoints:
  - Infrastructure roadmap alignment
  - Capacity planning
  - Feature feasibility (infrastructure)

Communication:
  - Weekly sync meeting
  - Roadmap reviews (quarterly)
```

### Con Arquitectura (Weekly)

```yaml
Mode: Collaboration
Touchpoints:
  - Architecture decision reviews
  - Technology evaluation
  - Platform design
  - Security architecture

Communication:
  - Design review sessions
  - Architecture forums
```

### Con Security (Daily)

```yaml
Mode: Collaboration
Touchpoints:
  - Security scanning integration
  - Vulnerability remediation
  - Compliance automation
  - Incident response

Communication:
  - Security reviews
  - Threat modeling sessions
```

## 📚 Recursos y Herramientas

### Internal Developer Portal

```yaml
URL: https://developer.company.com
Content:
  - Service catalog
  - Pipeline templates
  - Infrastructure docs
  - Runbooks
  - Getting started guides
  - API documentation
```

### Documentation

```yaml
Location: Confluence / GitHub Wiki
Sections:
  - Architecture diagrams
  - Infrastructure as Code repos
  - Runbooks & procedures
  - Incident response playbooks
  - Training materials
```

### Communication Channels

```yaml
Slack:
  -  #devops-team (internal)
  -  #devops-support (company-wide)
  -  #incidents (alerts & coordination)
  -  #deployments (deployment notifications)
```

## 🚀 Career Paths en DevOps

### Individual Contributor Track

```yaml
Junior DevOps → Mid DevOps → Senior DevOps → Staff DevOps → Principal DevOps

Focus: Technical depth, specialization
Timeline: 8-12 años to Staff
```

### Specialization Paths

```yaml
Platform Engineering:
  - Internal Developer Platforms
  - Kubernetes expertise
  - Developer experience

Site Reliability:
  - Production systems
  - Incident management
  - Reliability engineering

Security (DevSecOps):
  - Security automation
  - Compliance
  - Threat modeling

Cloud Architecture:
  - Multi-cloud
  - Cost optimization
  - Scalability
```

### Management Track

```yaml
Senior DevOps → DevOps Lead → Director of DevOps/Platform → VP Engineering

Transition: Typically 5-8 years experience
Focus: Team building, strategy, stakeholder management
```

## 📖 Learning Resources

### Books

```yaml
Essential:
  - "The Phoenix Project" - Gene Kim
  - "The DevOps Handbook" - Gene Kim et al.
  - "Site Reliability Engineering" - Google
  - "Infrastructure as Code" - Kief Morris

Advanced:
  - "Accelerate" - Nicole Forsgren
  - "Team Topologies" - Matthew Skelton
  - "Building Secure & Reliable Systems" - Google
```

### Certifications

```yaml
Azure:
  - AZ-104: Azure Administrator
  - AZ-400: DevOps Engineer Expert
  - AZ-305: Azure Solutions Architect

Kubernetes:
  - CKA: Certified Kubernetes Administrator
  - CKAD: Certified Kubernetes Application Developer
  - CKS: Certified Kubernetes Security Specialist

Other:
  - Terraform Associate
  - AWS Solutions Architect (multi-cloud)
  - Certified Ethical Hacker (security focus)
```

---

**Team Lead**: DevOps Lead  
**Reporta a**: Director of Engineering / CTO  
**Team Type**: Platform Team (Team Topologies)  
**Última actualización**: Diciembre 2025
