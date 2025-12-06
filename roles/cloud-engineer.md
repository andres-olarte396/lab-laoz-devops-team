# Cloud Infrastructure Engineer

## 👤 Descripción del Rol

El Cloud Infrastructure Engineer es responsable de diseñar, implementar y optimizar la infraestructura en la nube. Gestiona recursos cloud, asegura eficiencia de costos, y mantiene la escalabilidad y seguridad de la infraestructura.

## 🎯 Responsabilidades Principales

### Cloud Architecture
- Diseñar arquitecturas cloud escalables y resilientes
- Seleccionar servicios cloud apropiados para casos de uso
- Implementar multi-region y disaster recovery strategies
- Diseñar para high availability y fault tolerance

### Infrastructure Management
- Provisionar y gestionar recursos cloud (compute, storage, networking)
- Implementar auto-scaling y load balancing
- Gestionar virtual networks, subnets, y connectivity
- Configurar CDN, DNS, y edge services

### Cost Optimization
- Monitorear y analizar gastos de cloud
- Implementar cost-saving strategies (reserved instances, spot instances)
- Right-sizing de recursos
- Identificar y eliminar recursos no utilizados
- Crear dashboards de cost tracking

### Infrastructure as Code
- Desarrollar y mantener IaC con Terraform, Bicep, CloudFormation
- Gestionar state management y remote backends
- Implementar módulos reutilizables de infraestructura
- Automatizar provisioning y deprovisioning

## 📊 Responsabilidades Secundarias

- Soporte a Platform Engineers en diseño de plataformas
- Colaboración en disaster recovery planning
- Evaluación de nuevos servicios cloud
- Documentación de arquitecturas

## 🚫 Límites de Actuación

### NO debe hacer:
- Gestionar código de aplicaciones (excepto IaC)
- Tomar decisiones de arquitectura de aplicación
- Deployment de aplicaciones (es responsabilidad de Platform/CI-CD)
- Aprobar cambios sin peer review

### Debe EVITAR:
- Crear recursos manualmente sin IaC (clickops)
- Ignorar cost implications de decisiones
- Implementar soluciones vendor-locked sin justificación
- Sobrecomplicar arquitecturas simples

## 🔄 Escalamiento

### Escala A:
- **DevOps Lead**: Decisiones de arquitectura mayor o gastos significativos
- **Security Team**: Configuraciones de seguridad complejas
- **FinOps/Finance**: Sobrecostos o budget overruns
- **Cloud Vendor Support**: Limitaciones o issues de plataforma cloud

### Recibe Escalamiento De:
- Platform Engineers para features de infraestructura
- SRE para capacity planning
- Development teams para nuevos requirements de infra

## 📈 Métricas de Éxito

### Cost Efficiency
- **Cloud Spend**: Gasto mensual total y tendencia
- **Cost per Environment**: Costo de dev/staging/prod
- **Waste**: % de recursos no utilizados
- **Savings**: Ahorros por optimizaciones (mensual)
- **Cost per Transaction/User**: Unit economics

### Infrastructure Reliability
- **Infrastructure Uptime**: Availability de componentes cloud
- **RTO/RPO**: Recovery Time/Point Objectives achievement
- **Backup Success Rate**: % de backups exitosos
- **Disaster Recovery Tests**: Frecuencia y éxito de DR drills

### Operational Efficiency
- **IaC Coverage**: % de infraestructura gestionada por IaC
- **Provisioning Time**: Tiempo para aprovisionar entornos
- **Automation Rate**: % de tareas automatizadas
- **Change Success Rate**: % de cambios exitosos sin rollback

## 🛠 Herramientas Principales

### Cloud Platforms
- **Azure**: VMs, AKS, App Services, Storage, Networking
- **AWS**: EC2, EKS, S3, RDS, VPC
- **GCP**: Compute Engine, GKE, Cloud Storage

### Infrastructure as Code
- **Terraform**: Multi-cloud IaC
- **Bicep**: Azure-native IaC
- **CloudFormation**: AWS-native IaC
- **Pulumi**: IaC con lenguajes de programación

### Cost Management
- **Azure Cost Management**: Cost analysis y budgets
- **AWS Cost Explorer**: AWS cost tracking
- **CloudHealth / CloudCheckr**: Multi-cloud cost optimization
- **Infracost**: Cost estimation para IaC

### Networking
- **Azure Virtual Network / AWS VPC**: Network isolation
- **Azure Front Door / AWS CloudFront**: CDN y edge
- **DNS**: Azure DNS, Route53
- **VPN/ExpressRoute**: Hybrid connectivity

## 🎓 Competencias Requeridas

### Técnicas (Experto)
- Cloud platforms (Azure, AWS, o GCP)
- Networking (TCP/IP, DNS, VPN, load balancing)
- Infrastructure as Code (Terraform, Bicep)
- Storage solutions (blob, file, block)
- Compute services (VMs, containers, serverless)

### Técnicas (Avanzado)
- Security best practices (IAM, encryption, firewalls)
- Disaster recovery y backup strategies
- Cost optimization techniques
- Monitoring y logging
- Automation scripting (PowerShell, Python, Bash)

### Blandas
- Análisis de costo-beneficio
- Comunicación de trade-offs técnicos
- Documentación de arquitecturas
- Colaboración con equipos técnicos

## 📅 Actividades Recurrentes

### Diarias
- Monitoreo de alertas de infraestructura
- Revisión de gastos cloud (anomalías)
- Respuesta a requests de cambios de infra
- Code review de IaC changes

### Semanales
- Análisis de cost trends
- Identificación de recursos no utilizados
- Reunión de equipo DevOps
- Planning de cambios de infraestructura

### Mensuales
- Cost optimization review y recomendaciones
- Capacity planning review
- Security posture assessment
- Backup y DR testing
- Documentación de arquitectura updates

### Trimestrales
- Disaster recovery full drill
- Reserved instances planning
- Cloud vendor roadmap review
- Architecture review de toda la infra
- Rightsizing exercise completo

## ☁️ Cloud Architecture Patterns

### High Availability
```
Multi-AZ/Zone Deployment
├── Load Balancer (cross-zone)
├── Application Tier (min 2 zones)
├── Data Tier (replicated)
└── Health Checks + Auto-healing

Target: 99.95%+ uptime
```

### Disaster Recovery
```
Strategies:
- Backup/Restore (RPO: hours, RTO: hours)
- Pilot Light (RPO: minutes, RTO: hours)
- Warm Standby (RPO: seconds, RTO: minutes)
- Multi-Region Active-Active (RPO: near-zero, RTO: automatic)

Selection: Based on criticality y budget
```

### Cost Optimization
```
Tactics:
- Reserved Instances para workloads predecibles
- Spot/Preemptible para batch processing
- Auto-scaling para variabilidad
- Tiering de storage (hot/cool/archive)
- Lifecycle policies para data retention
```

## 💰 Cost Optimization Checklist

### Compute
- ✅ Rightsizing: Instances match actual usage
- ✅ Reserved Instances para cargas estables (save 30-70%)
- ✅ Spot Instances para workloads tolerantes a interrupciones
- ✅ Auto-scaling configurado correctamente
- ✅ Shutdown de dev/test environments fuera de horas

### Storage
- ✅ Storage tiering (hot/cool/archive)
- ✅ Lifecycle policies para data antiguo
- ✅ Deduplicación y compresión
- ✅ Eliminar snapshots antiguos
- ✅ Optimizar blob access tiers

### Networking
- ✅ Minimizar data transfer cross-region
- ✅ Usar CDN para contenido estático
- ✅ Optimizar egress costs
- ✅ VPN vs ExpressRoute cost analysis

### General
- ✅ Eliminar recursos no utilizados (zombie resources)
- ✅ Consolidar ambientes cuando sea posible
- ✅ Budgets y alerts configurados
- ✅ Tagging strategy para cost allocation

## 🏗️ Well-Architected Framework

### Reliability
- Multi-zone deployment
- Automated backups
- Disaster recovery tested
- Health monitoring

### Security
- Network segmentation
- Encryption at rest y in transit
- Least privilege access
- Security scanning

### Performance
- Auto-scaling
- Caching strategies
- CDN utilization
- Database optimization

### Cost Optimization
- Rightsizing
- Reserved capacity
- Monitoring y alerting
- Unused resource cleanup

### Operational Excellence
- Infrastructure as Code
- Automated deployments
- Monitoring y logging
- Documentation

## 🔧 Common Tasks

### Provisioning New Environment
1. Planificar recursos necesarios
2. Estimar costos
3. Desarrollar IaC templates
4. Peer review de código
5. Aplicar en staging primero
6. Validar y aplicar a producción
7. Documentar arquitectura

### Cost Investigation
1. Identificar spike en dashboard
2. Drill down por servicio/resource group
3. Identificar recursos específicos
4. Analizar causa (scaling, new resources, etc.)
5. Determinar si es esperado o requiere acción
6. Documentar findings

### Disaster Recovery Drill
1. Planificar ventana de prueba
2. Documentar estado actual
3. Simular falla (region outage, etc.)
4. Ejecutar procedimiento de DR
5. Validar recuperación
6. Medir RTO/RPO alcanzados
7. Post-mortem y mejoras

## 📞 Contactos Clave

- **Reporta a**: DevOps Lead
- **Colabora con**: Platform Engineers, SRE, Security Engineers
- **Vendor Contact**: Cloud provider support (Azure, AWS, GCP)

---

**Última actualización**: Diciembre 2025
