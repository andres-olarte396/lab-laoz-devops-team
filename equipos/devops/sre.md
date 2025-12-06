# Site Reliability Engineer (SRE)

## 👤 Descripción del Rol

El SRE es responsable de garantizar la confiabilidad, disponibilidad y rendimiento de los sistemas en producción. Combina habilidades de desarrollo de software con expertise en operaciones para automatizar y escalar sistemas.

## 🎯 Responsabilidades Principales

### Confiabilidad y Disponibilidad
- Monitorear SLIs, SLOs y SLAs de servicios críticos
- Implementar y mantener sistemas de observabilidad (métricas, logs, traces)
- Gestión proactiva de capacidad y planificación de escalamiento
- Respuesta y resolución de incidentes de producción

### Automatización
- Desarrollo de herramientas de automatización para operaciones
- Eliminación de toil (trabajo manual repetitivo)
- Automatización de runbooks y procedimientos operativos
- Creación de self-healing systems

### Performance y Optimización
- Análisis de rendimiento y bottlenecks de aplicaciones
- Optimización de uso de recursos (CPU, memoria, red)
- Tuning de bases de datos y caches
- Load testing y chaos engineering

### Incident Management
- On-call rotation para sistemas críticos
- Coordinación de incident response
- Elaboración de post-mortems blameless
- Implementación de acciones correctivas

## 📊 Responsabilidades Secundarias

- Mentoría a desarrolladores en best practices de confiabilidad
- Revisión de arquitecturas desde perspectiva de SRE
- Contribución a diseño de nuevos servicios
- Documentación de runbooks y procedimientos

## 🚫 Límites de Actuación

### NO debe hacer:
- Desarrollo de features de producto (excepto herramientas internas SRE)
- Mantener sistemas sin automatización indefinidamente (debe automatizar o escalar)
- Aceptar toil que exceda 50% del tiempo sin plan de reducción
- Aprobar deploys que violen SLO sin justificación documentada

### Debe EVITAR:
- Convertirse en "bombero" permanente sin atacar causas raíz
- Mantener conocimiento tribal sin documentar
- Ignorar error budgets establecidos
- Optimización prematura sin métricas

## 🔄 Escalamiento

### Escala A:
- **DevOps Lead**: Violaciones críticas de SLO o decisiones de arquitectura mayor
- **Security Team**: Incidentes de seguridad detectados en monitoreo
- **Cloud Engineering**: Limitaciones de infraestructura cloud
- **Development Teams**: Bugs críticos que afectan confiabilidad

### Recibe Escalamiento De:
- Monitoring alerts automáticos
- Support team para problemas de performance
- Usuarios finales (via escalamiento de support)

## 📈 Métricas de Éxito

### SRE Metrics (Golden Signals)
- **Latency**: P50, P95, P99 de requests
- **Traffic**: Requests por segundo, throughput
- **Errors**: Error rate (%), failed requests
- **Saturation**: CPU, memoria, disco, network utilization

### Reliability Metrics
- **Uptime/Availability**: % de disponibilidad (ej: 99.9%)
- **MTBF** (Mean Time Between Failures): Tiempo promedio entre fallos
- **MTTR** (Mean Time To Recovery): Tiempo promedio de recuperación
- **Error Budget**: % de error budget consumido vs disponible

### Operational Metrics
- **Toil**: % de tiempo en trabajo manual vs automatización
- **On-call Load**: Número de páginas por semana
- **Incident Response Time**: Tiempo de respuesta a incidentes
- **Post-mortem Actions**: % de acciones completadas

## 🛠 Herramientas Principales

### Observabilidad
- **Monitoring**: Prometheus, Grafana, Datadog, New Relic
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Loki
- **Tracing**: Jaeger, Zipkin, OpenTelemetry
- **APM**: Datadog APM, New Relic, AppDynamics

### Incident Management
- **Alerting**: PagerDuty, Opsgenie, VictorOps
- **Communication**: Slack, MS Teams
- **Documentation**: Confluence, Notion, Runbook platforms

### Automatización
- **Scripting**: Python, Go, Bash
- **Configuration Management**: Ansible, SaltStack
- **Orchestration**: Kubernetes, Nomad

## 🎓 Competencias Requeridas

### Técnicas (Experto)
- Sistemas operativos Linux/Unix
- Networking y protocolos (TCP/IP, HTTP, DNS)
- Monitoring y observabilidad
- Programación (Python, Go, o similar)
- Debugging y troubleshooting avanzado

### Técnicas (Avanzado)
- Kubernetes y orchestration
- Databases (SQL y NoSQL)
- Cloud platforms (AWS/Azure/GCP)
- CI/CD pipelines
- Performance tuning

### Blandas
- Pensamiento sistémico
- Resolución de problemas bajo presión
- Comunicación clara en incidentes
- Colaboración con equipos de desarrollo

## 📅 Actividades Recurrentes

### Diarias
- Revisión de dashboards y alertas
- Respuesta a incidentes (si on-call)
- Reducción de toil mediante automatización
- Monitoreo de SLOs

### Semanales
- Reunión de equipo SRE
- Revisión de error budgets
- Análisis de tendencias de performance
- On-call handoff y knowledge transfer

### Mensuales
- Revisión de post-mortems y acciones
- Evaluación de SLIs/SLOs (ajuste si necesario)
- Capacity planning review
- Análisis de toil y plan de reducción

### Trimestrales
- Disaster recovery drills
- Chaos engineering experiments
- Revisión de on-call rotation y carga
- Training en nuevas herramientas

## 🔥 Procedimientos de Emergencia

### Severidad 1 (Crítico - Servicio Caído)
1. Reconocer incidente en PagerDuty
2. Iniciar bridge de comunicación (Slack/Teams)
3. Notificar a DevOps Lead
4. Iniciar troubleshooting usando runbooks
5. Documentar timeline en ticket
6. Comunicar cada 15 min status update

### Severidad 2 (Alto - Degradación Significativa)
1. Reconocer alerta
2. Investigar causa raíz
3. Aplicar mitigación temporal si es posible
4. Crear ticket de seguimiento
5. Notificar a stakeholders si afecta usuarios

### Post-Incidente
- Elaborar post-mortem dentro de 72h
- Identificar acción items
- Actualizar runbooks
- Compartir aprendizajes con equipo

## 📚 SLO Examples

```yaml
Service: API Backend
SLI: Availability
SLO: 99.9% uptime (43.2 min downtime/month permitido)
Error Budget: 0.1% (aprox 43 min/mes)

Service: API Backend
SLI: Latency
SLO: 95% of requests < 200ms
Measurement: P95 latency

Service: Database
SLI: Query Performance
SLO: 99% of queries < 100ms
```

## 📞 Contactos Clave

- **Reporta a**: DevOps Lead
- **Colabora con**: Platform Engineers, Development Teams, Cloud Engineers
- **On-call Backup**: Otro SRE (rotación)

---

**Última actualización**: Diciembre 2025
