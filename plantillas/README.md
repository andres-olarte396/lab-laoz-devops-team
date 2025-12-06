# Plantillas y Formatos Estándar

Esta sección contiene templates reutilizables para documentación recurrente del equipo DevOps.

## 📋 Índice de Plantillas

1. [Post-Mortem](#post-mortem-template)
2. [Runbook](#runbook-template)
3. [Change Request](#change-request-template)
4. [Architecture Decision Record (ADR)](#adr-template)
5. [Onboarding Checklist](#onboarding-checklist)
6. [Incident Report](#incident-report-template)
7. [Release Notes](#release-notes-template)
8. [Project Proposal](#project-proposal-template)

---

## Post-Mortem Template

**Archivo**: `post-mortem-template.md`

```markdown
# Post-Mortem: [Título del Incidente]

**Fecha del Incidente**: YYYY-MM-DD  
**Severidad**: SEV-1 / SEV-2 / SEV-3  
**Facilitador**: [Nombre]  
**Participantes**: [Lista de nombres]  
**Estado**: Draft / Final

---

## Resumen Ejecutivo
[1-2 párrafos explicando qué pasó, impacto, y resolución en términos simples]

**Duración Total**: [X horas, Y minutos]  
**Usuarios Afectados**: [Número o %]  
**Impacto en Negocio**: [Descripción breve]

---

## Timeline

| Tiempo | Evento | Persona/Sistema |
|--------|--------|-----------------|
| HH:MM | Incidente iniciado (causa raíz) | [Quién/Qué] |
| HH:MM | Primera detección | [Sistema/Persona] |
| HH:MM | Alerta enviada | [Sistema] |
| HH:MM | Incidente reconocido | [Persona] |
| HH:MM | Investigación iniciada | [Persona] |
| HH:MM | Causa raíz identificada | [Persona] |
| HH:MM | Mitigación aplicada | [Persona] |
| HH:MM | Servicio restaurado | [Sistema] |
| HH:MM | Incidente resuelto | [Persona] |

**Tiempo Total de Detección**: [X minutos]  
**Tiempo Total de Resolución**: [X horas, Y minutos]

---

## Causa Raíz

### ¿Qué sucedió?
[Explicación técnica detallada de la causa raíz]

### ¿Por qué sucedió?
[5 Whys análisis]
1. Why? [Respuesta]
2. Why? [Respuesta]
3. Why? [Respuesta]
4. Why? [Respuesta]
5. Why? [Respuesta - Causa raíz fundamental]

### Factores Contribuyentes
- [Factor 1]
- [Factor 2]
- [Factor 3]

---

## Impacto

### Usuarios
- [Descripción del impacto a usuarios]
- [Métricas: error rate, latency, etc.]

### Negocio
- [Impacto financiero estimado]
- [Impacto en SLAs]
- [Impacto en reputación]

### Sistemas
- [Servicios afectados]
- [Dependencias impactadas]

---

## Resolución

### ¿Qué se hizo para resolver?
[Pasos tomados para restaurar el servicio]

### ¿Por qué funcionó?
[Explicación de la solución]

---

## Qué Funcionó Bien

- ✅ [Aspecto positivo 1]
- ✅ [Aspecto positivo 2]
- ✅ [Aspecto positivo 3]

---

## Qué Puede Mejorar

- ⚠️ [Área de mejora 1]
- ⚠️ [Área de mejora 2]
- ⚠️ [Área de mejora 3]

---

## Action Items

| # | Acción | Owner | Deadline | Prioridad | Status |
|---|--------|-------|----------|-----------|--------|
| 1 | [Acción correctiva] | [Nombre] | YYYY-MM-DD | High/Med/Low | Open/In Progress/Done |
| 2 | [Acción preventiva] | [Nombre] | YYYY-MM-DD | High/Med/Low | Open/In Progress/Done |
| 3 | [Mejora de proceso] | [Nombre] | YYYY-MM-DD | High/Med/Low | Open/In Progress/Done |

---

## Aprendizajes

### Técnicos
- [Aprendizaje 1]
- [Aprendizaje 2]

### Proceso
- [Aprendizaje 1]
- [Aprendizaje 2]

---

## Anexos

### Logs Relevantes
```
[Logs importantes]
```

### Gráficas/Screenshots
[Adjuntar imágenes]

### Links Relacionados
- Incident ticket: [Link]
- Slack thread: [Link]
- Monitoring dashboard: [Link]

---

**Notas Adicionales**: [Cualquier información adicional relevante]

**Aprobado por**: [DevOps Lead]  
**Fecha de Aprobación**: YYYY-MM-DD
```

---

## Runbook Template

**Archivo**: `runbook-template.md`

```markdown
# Runbook: [Nombre del Servicio/Procedimiento]

**Servicio**: [Nombre]  
**Owner**: [Nombre del team/persona]  
**Última Actualización**: YYYY-MM-DD  
**Versión**: X.Y

---

## Descripción

### ¿Qué es este servicio?
[Descripción breve del servicio o procedimiento]

### ¿Cuándo usar este runbook?
[Escenarios donde este runbook es aplicable]

---

## Información de Contacto

| Rol | Contacto | Horario |
|-----|----------|---------|
| Primary On-Call | [Nombre/PagerDuty] | 24/7 |
| Backup On-Call | [Nombre/PagerDuty] | 24/7 |
| Service Owner | [Nombre] | Business hours |
| Escalation | [Nombre] | As needed |

---

## Arquitectura

### Diagrama
[Insertar diagrama de arquitectura]

### Componentes
- **Component 1**: [Descripción]
- **Component 2**: [Descripción]
- **Component 3**: [Descripción]

### Dependencias
- **Upstream**: [Servicios de los que depende]
- **Downstream**: [Servicios que dependen de este]

---

## Monitoreo y Alertas

### Dashboards
- [Link a dashboard principal]
- [Link a dashboard de performance]

### Alertas Comunes

#### Alert: [Nombre del Alert]
- **Severidad**: Critical/Warning/Info
- **Descripción**: [Qué significa esta alerta]
- **Threshold**: [Valor de threshold]
- **Acción**: Ver sección [X] de este runbook

---

## Procedimientos Operativos

### Inicio del Servicio

```bash
# Comandos para iniciar el servicio
kubectl apply -f deployment.yaml
kubectl rollout status deployment/[name]
```

**Verificación**:
- [ ] Health check endpoint responde 200: `curl http://[url]/health`
- [ ] Logs no muestran errores: `kubectl logs -f [pod]`
- [ ] Métricas aparecem en Grafana

### Detener el Servicio

```bash
# Comandos para detener
kubectl scale deployment/[name] --replicas=0
```

**Verificación**:
- [ ] Pods terminados: `kubectl get pods`
- [ ] No hay tráfico activo

### Reinicio del Servicio

```bash
# Comando de rolling restart
kubectl rollout restart deployment/[name]
```

---

## Troubleshooting

### Problema: Servicio No Responde

**Síntomas**:
- Health checks failing
- 5xx errors
- No response

**Diagnóstico**:
```bash
# Check pod status
kubectl get pods -l app=[name]

# Check logs
kubectl logs -f [pod-name]

# Check events
kubectl describe pod [pod-name]
```

**Resolución**:
1. Verificar si pods están running
2. Si pods no están healthy, revisar logs
3. Si error de resources, verificar CPU/memory limits
4. Si error de config, verificar ConfigMap/Secrets
5. Si todo lo anterior OK, restart pods

**Escalamiento**: Si no se resuelve en 15 min, escalar a [Persona/Team]

---

### Problema: Alta Latencia

**Síntomas**:
- P95 latency > [threshold]
- Slow response times

**Diagnóstico**:
```bash
# Check resource utilization
kubectl top pods

# Check database performance
[comando específico]
```

**Resolución**:
1. Verificar CPU/Memory utilization
2. Check database slow queries
3. Verificar cache hit rate
4. Considerar scale up/out

---

### Problema: [Otro Problema Común]

[Repetir estructura de arriba]

---

## Procedimientos de Emergencia

### Rollback

**Cuándo hacer rollback**:
- Nueva versión causando errores críticos
- Change failure rate > 50%
- No se puede identificar fix rápido

**Procedimiento**:
```bash
# Rollback to previous version
kubectl rollout undo deployment/[name]

# Verificar
kubectl rollout status deployment/[name]
```

### Scale Up (Emergencia)

```bash
# Scale to more replicas
kubectl scale deployment/[name] --replicas=[number]
```

### Failover a DR

[Procedimiento específico si aplica]

---

## Mantenimiento

### Backup

**Frecuencia**: [Diario/Semanal]  
**Ubicación**: [Dónde se guardan backups]  
**Retención**: [Cuánto tiempo]

**Procedimiento**:
```bash
# Comando de backup
[comando]
```

### Restore

```bash
# Comando de restore
[comando]
```

### Rotación de Secretos

**Frecuencia**: [90 días, etc.]  
**Procedimiento**: [Pasos]

---

## Configuración

### Variables de Entorno

| Variable | Descripción | Valor Default |
|----------|-------------|---------------|
| `VAR_1` | [Descripción] | [Valor] |
| `VAR_2` | [Descripción] | [Valor] |

### ConfigMaps

```yaml
# Ejemplo de ConfigMap
apiVersion: v1
kind: ConfigMap
metadata:
  name: [name]
data:
  key: value
```

---

## Referencias

- Architecture Doc: [Link]
- API Documentation: [Link]
- Monitoring Dashboard: [Link]
- Source Code: [Link]
- Deployment Pipeline: [Link]

---

## Changelog

| Fecha | Versión | Cambios | Autor |
|-------|---------|---------|-------|
| YYYY-MM-DD | 1.0 | Initial version | [Nombre] |

```

---

## Change Request Template

**Archivo**: `change-request-template.md`

```markdown
# Change Request: [Título]

**CR ID**: CR-YYYY-NNNN  
**Requestor**: [Nombre]  
**Date Submitted**: YYYY-MM-DD  
**Type**: Standard / Expedited / Emergency  
**Status**: Draft / Submitted / Approved / Implemented / Closed

---

## Descripción del Cambio

### ¿Qué se va a cambiar?
[Descripción detallada del cambio]

### ¿Por qué es necesario este cambio?
[Justificación de negocio o técnica]

### Sistemas Afectados
- [Sistema 1]
- [Sistema 2]
- [Sistema 3]

---

## Detalles Técnicos

### Implementación
[Pasos técnicos para implementar el cambio]

```bash
# Comandos o código relevante
```

### Rollback Plan
[Cómo revertir si algo sale mal]

```bash
# Comandos de rollback
```

---

## Risk Assessment

### Nivel de Riesgo
- [ ] Low - Mínimo impacto, fácilmente reversible
- [ ] Medium - Impacto moderado, rollback disponible
- [ ] High - Impacto significativo, rollback complejo
- [ ] Critical - Impacto severo a negocio

### Riesgos Identificados

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|---------|------------|
| [Riesgo 1] | Low/Med/High | Low/Med/High | [Plan de mitigación] |
| [Riesgo 2] | Low/Med/High | Low/Med/High | [Plan de mitigación] |

---

## Testing

### Tested In
- [ ] Development
- [ ] Staging
- [ ] Production (limited rollout)

### Test Results
[Resumen de resultados de testing]

---

## Implementation Plan

### Scheduled Time
- **Date**: YYYY-MM-DD
- **Start Time**: HH:MM [Timezone]
- **Expected Duration**: [X hours]
- **Maintenance Window**: Yes / No

### Prerequisites
- [ ] [Prerequisito 1]
- [ ] [Prerequisito 2]

### Implementation Steps

1. [Paso 1]
   - Tiempo estimado: [X min]
   - Owner: [Nombre]
   
2. [Paso 2]
   - Tiempo estimado: [X min]
   - Owner: [Nombre]

### Verification Steps
- [ ] [Verificación 1]
- [ ] [Verificación 2]

---

## Communication Plan

### Notification
- [ ] Stakeholders notificados
- [ ] Development teams notificados
- [ ] Customer-facing teams notificados (si aplica)
- [ ] Status page updated (si downtime esperado)

### Communication Template
```
Subject: [Scheduled Maintenance / Change Notice]

Dear Team,

We will be performing [descripción del cambio] on [fecha] from [hora inicio] to [hora fin].

Expected Impact: [Descripción]

Please contact [persona] if you have questions.

Thank you,
DevOps Team
```

---

## Approvals

| Approver | Role | Status | Date |
|----------|------|--------|------|
| [Nombre] | DevOps Lead | Pending/Approved/Rejected | YYYY-MM-DD |
| [Nombre] | Service Owner | Pending/Approved/Rejected | YYYY-MM-DD |
| [Nombre] | Security (if needed) | Pending/Approved/Rejected | YYYY-MM-DD |

---

## Post-Implementation

### Actual vs Planned

| Aspect | Planned | Actual |
|--------|---------|--------|
| Start Time | HH:MM | HH:MM |
| End Time | HH:MM | HH:MM |
| Duration | [X hours] | [X hours] |
| Issues | None expected | [Descripción] |

### Success Criteria
- [ ] [Criterio 1 cumplido]
- [ ] [Criterio 2 cumplido]
- [ ] No errors en logs
- [ ] Performance metrics normal

### Lessons Learned
[Qué se aprendió durante la implementación]

---

**Sign-off**: [Nombre]  
**Date**: YYYY-MM-DD
```

---

## ADR Template

**Archivo**: `adr-template.md`

```markdown
# ADR-NNNN: [Título de la Decisión]

**Status**: Proposed / Accepted / Deprecated / Superseded  
**Date**: YYYY-MM-DD  
**Deciders**: [Lista de personas involucradas]  
**Technical Story**: [Link a ticket/issue]

---

## Context

[Describe el contexto y el problema que estamos tratando de resolver. Sé específico sobre las restricciones técnicas, de negocio, políticas, etc.]

---

## Decision

[Describe la decisión que se tomó]

Decidimos [acción] porque [razón].

---

## Options Considered

### Option 1: [Nombre]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]

### Option 2: [Nombre]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]

### Option 3: [Nombre] ⭐ **SELECTED**

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]

**Why Selected**: [Razón por la cual se seleccionó esta opción]

---

## Consequences

### Positive
- [Consecuencia positiva 1]
- [Consecuencia positiva 2]

### Negative
- [Consecuencia negativa 1 y plan de mitigación]
- [Consecuencia negativa 2 y plan de mitigación]

### Neutral
- [Cambios que son neutros]

---

## Implementation

### Tasks
- [ ] [Tarea 1]
- [ ] [Tarea 2]
- [ ] [Tarea 3]

### Timeline
[Cuándo se implementará]

### Success Metrics
[Cómo mediremos si fue exitosa]

---

## References

- [Link a documentación relevante]
- [Link a spike técnico]
- [Link a proof of concept]

---

## Updates

| Date | Update | Author |
|------|--------|--------|
| YYYY-MM-DD | Initial version | [Nombre] |
| YYYY-MM-DD | [Descripción de update] | [Nombre] |
```

---

## Onboarding Checklist

Ver archivo: [`onboarding-checklist.md`](./onboarding-checklist.md)

---

## Incident Report Template

Ver archivo: [`incident-report-template.md`](./incident-report-template.md)

---

## Release Notes Template

Ver archivo: [`release-notes-template.md`](./release-notes-template.md)

---

## Project Proposal Template

Ver archivo: [`project-proposal-template.md`](./project-proposal-template.md)

---

**Última actualización**: Diciembre 2025
