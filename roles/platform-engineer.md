# Platform Engineer

## 👤 Descripción del Rol

El Platform Engineer diseña, construye y mantiene plataformas internas y herramientas que permiten a los desarrolladores trabajar de manera más eficiente. Crea abstracciones sobre infraestructura compleja para facilitar self-service y autonomía de equipos.

## 🎯 Responsabilidades Principales

### Diseño de Plataformas
- Diseñar y construir plataformas de desarrollo internas
- Crear abstracciones y APIs para servicios de infraestructura
- Implementar self-service portals y herramientas para desarrolladores
- Definir estándares y patterns para deployment

### Developer Experience (DevEx)
- Mejorar la experiencia de desarrolladores con herramientas internas
- Reducir tiempo desde código hasta producción
- Crear documentación y guías de uso de plataforma
- Recopilar feedback de desarrolladores y actuar sobre él

### Infrastructure as Code (IaC)
- Desarrollar y mantener módulos de Terraform/Bicep reutilizables
- Crear templates de infraestructura para diferentes tipos de apps
- Gestión de estado de infraestructura (Terraform state)
- Implementar políticas de compliance y governance

### Kubernetes y Orchestration
- Gestión de clusters Kubernetes multi-tenant
- Configuración de namespaces, RBAC, network policies
- Implementación de operators y custom resources
- Service mesh management (Istio, Linkerd)

## 📊 Responsabilidades Secundarias

- Mentoría a equipos de desarrollo en uso de plataforma
- Contribución a decisiones de arquitectura
- Soporte a SRE en troubleshooting de plataforma
- Evaluación de nuevas tecnologías de plataforma

## 🚫 Límites de Actuación

### NO debe hacer:
- Gestionar aplicaciones individuales de equipos (excepto ejemplos/templates)
- Tomar decisiones de arquitectura de producto
- Implementar features de aplicaciones de negocio
- Mantener configuraciones ad-hoc por equipo sin estandarizar

### Debe EVITAR:
- Crear plataformas sin validar con usuarios (developers)
- Construir soluciones over-engineered para problemas simples
- Ignorar feedback de desarrolladores sobre usabilidad
- Crear abstracciones que oculten información crítica

## 🔄 Escalamiento

### Escala A:
- **DevOps Lead**: Decisiones de arquitectura de plataforma mayor
- **Security Team**: Validación de configuraciones de seguridad
- **SRE**: Problemas de performance o reliability de plataforma
- **Cloud Engineering**: Limitaciones o features de infraestructura cloud

### Recibe Escalamiento De:
- Equipos de desarrollo para soporte de plataforma
- CI/CD Engineers para integración de herramientas
- Security Engineers para implementación de controles

## 📈 Métricas de Éxito

### Platform Adoption
- **Adoption Rate**: % de equipos usando la plataforma
- **Self-Service Rate**: % de deploys sin intervención manual
- **Time to First Deploy**: Tiempo desde onboarding hasta primer deploy
- **Platform Availability**: Uptime de servicios de plataforma

### Developer Productivity
- **Lead Time**: Tiempo desde commit hasta producción
- **Build Time**: Duración promedio de builds
- **Developer Satisfaction**: NPS o CSAT score de desarrolladores
- **Support Tickets**: Número y tipo de tickets de soporte

### Platform Efficiency
- **Resource Utilization**: % uso de recursos provisionados
- **Cost per Deploy**: Costo promedio por deployment
- **Automation Coverage**: % de tareas automatizadas
- **Standardization**: % de workloads usando templates estándar

## 🛠 Herramientas Principales

### Infrastructure as Code
- **Terraform**: Gestión de infraestructura multi-cloud
- **Pulumi**: IaC con lenguajes de programación
- **Crossplane**: Kubernetes-native IaC
- **Bicep/ARM**: Azure Resource Manager

### Kubernetes Ecosystem
- **Kubernetes**: Orquestación de contenedores
- **Helm**: Package manager para Kubernetes
- **ArgoCD / FluxCD**: GitOps continuous delivery
- **Kustomize**: Template-free Kubernetes configuration

### Developer Portals
- **Backstage**: Developer portal open-source
- **Port**: Internal developer portal
- **Custom solutions**: APIs, dashboards internos

### Policy & Governance
- **OPA (Open Policy Agent)**: Policy enforcement
- **Kyverno**: Kubernetes-native policy management
- **Checkov**: IaC security scanning

## 🎓 Competencias Requeridas

### Técnicas (Experto)
- Kubernetes architecture y operations
- Infrastructure as Code (Terraform, Pulumi)
- API design y development
- Containerización (Docker, containerd)

### Técnicas (Avanzado)
- Cloud platforms (AWS/Azure/GCP)
- CI/CD pipelines
- Scripting (Python, Go, Bash)
- Networking (DNS, Load Balancers, Ingress)
- Service mesh (Istio, Linkerd)

### Blandas
- Product thinking (plataforma como producto)
- Empatía con desarrolladores
- Comunicación técnica clara
- Recopilación de feedback y priorización

## 📅 Actividades Recurrentes

### Diarias
- Revisión de health de plataforma (dashboards)
- Respuesta a tickets de soporte de desarrolladores
- Code review de IaC y configuraciones
- Trabajo en mejoras de plataforma

### Semanales
- Reunión de equipo de plataforma
- Office hours con equipos de desarrollo
- Revisión de métricas de adopción y uso
- Planning de mejoras y nuevas features

### Mensuales
- Encuesta de satisfacción a desarrolladores
- Revisión de roadmap de plataforma
- Capacity planning de clusters
- Auditoría de cumplimiento de estándares

### Trimestrales
- Evaluación de nuevas tecnologías
- Deprecation planning de componentes legacy
- Disaster recovery drills
- Training sessions para desarrolladores

## 🏗️ Ejemplos de Entregables

### Templates de Infraestructura
```
terraform-modules/
├── app-service/
├── aks-cluster/
├── database/
├── storage/
└── networking/
```

### Platform Features
- **Golden Paths**: Templates pre-aprobados para tipos de apps comunes
- **Service Catalog**: Catálogo de servicios disponibles para provisionar
- **Developer CLI**: Herramienta de línea de comandos para interactuar con plataforma
- **Documentation Hub**: Portal de documentación y guías

### Kubernetes Standards
- Pod Security Standards enforcement
- Resource quotas y limits por namespace
- Network policies por defecto
- Ingress configurations estándar

## 📚 Golden Paths Example

```yaml
# Golden Path: Microservicio Stateless
Components:
  - Container Registry
  - Kubernetes Deployment (HPA enabled)
  - Service + Ingress
  - Secrets management (Azure Key Vault)
  - Monitoring (Prometheus + Grafana)
  - Logging (ELK Stack)
  
Template: microservice-stateless
Self-service: Yes
Approval Required: No
Time to provision: ~5 minutes
```

## 🎯 North Star Metric

**Developer Velocity**: Reducir el tiempo y esfuerzo que toma a un desarrollador llevar código a producción de manera segura y confiable.

## 📞 Contactos Clave

- **Reporta a**: DevOps Lead
- **Colabora con**: Development Teams, SRE, CI/CD Engineers, Security
- **Usuarios**: Todos los equipos de desarrollo

---

**Última actualización**: Diciembre 2025
