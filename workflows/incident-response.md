# Incident Response Workflow - Respuesta a Incidentes

> **Owner**: DevOps Lead + SRE Team  
> **Última actualización**: 7 de diciembre de 2025  
> **Próxima revisión**: 7 de marzo de 2026

---

## 📋 Resumen Ejecutivo

Este documento define el proceso completo de respuesta a incidentes desde **detección** hasta **post-mortem**, cubriendo SEV-1 (crítico), SEV-2 (mayor), y SEV-3 (menor).

**Objetivo**: Restaurar servicio rápidamente, comunicar efectivamente, y aprender de incidentes para prevenir recurrencia.

**Equipos involucrados**: DevOps/SRE, Desarrollo, Producto, Customer Success, Ejecutivos (según severidad)  
**SLA de respuesta**: SEV-1 <10min, SEV-2 <30min, SEV-3 <4h

---

## 🎯 Objetivos

- **Velocidad**: Detectar y resolver incidentes lo más rápido posible
- **Comunicación**: Mantener stakeholders informados (internal + external)
- **Aprendizaje**: Post-mortem blameless para prevenir recurrencia
- **Preparación**: Runbooks y playbooks para scenarios comunes

---

## 🚨 Clasificación de Severidad

### SEV-1: Critical (Sistema Completamente Caído)

**Definición**:
- Sistema completamente caído o inaccesible
- Pérdida de datos o corrupción
- Brecha de seguridad activa
- Todos los usuarios afectados (100%)

**Ejemplos**:
- Website/app down (500 errors, no loading)
- Database corruption o pérdida de datos
- Payment processing completamente caído
- Data breach activa (credentials expuestas)

**SLA de Respuesta**:
- **Detección → Acknowledged**: <5 minutos
- **Acknowledged → First Response**: <10 minutos
- **First Response → War Room**: <15 minutos
- **Target Resolution**: <2 horas

**Escalación**:
- On-call SRE (inmediato)
- DevOps Lead (T+5min)
- Engineering Manager (T+10min)
- CTO (T+15min)
- CEO (T+30min si no resuelto)

**Comunicación**:
- Internal: #incidents + Slack alert a @channel
- External: Status page update (T+15min)
- Customers: Email notification (T+30min)
- Executives: Direct Slack/call (T+15min)

---

### SEV-2: Major (Degradación Significativa)

**Definición**:
- Funcionalidad crítica degradada pero no completamente caída
- Performance severamente afectada
- 25-75% de usuarios afectados
- Workaround existe pero es doloroso

**Ejemplos**:
- Latency 10x normal (500ms → 5s)
- Feature importante no funciona (ej: checkout slow pero funciona)
- Intermittent errors (50% requests failing)
- Database read replica down (writes OK)

**SLA de Respuesta**:
- **Detección → Acknowledged**: <15 minutos
- **Acknowledged → First Response**: <30 minutos
- **Target Resolution**: <8 horas

**Escalación**:
- On-call SRE (inmediato)
- DevOps Lead (T+30min)
- Engineering Manager (T+2h si no resuelto)

**Comunicación**:
- Internal: #incidents
- External: Status page update (opcional, T+1h)
- Customers: Email si >50% afectados (T+2h)
- Executives: Email update (T+2h)

---

### SEV-3: Minor (Bug No Crítico)

**Definición**:
- Bug evidente pero no bloquea uso
- Feature secundaria no funciona
- <25% usuarios afectados
- Workaround fácil existe

**Ejemplos**:
- UI cosmetic bug (botón desalineado)
- Error message incorrecto (pero funcionalidad OK)
- Feature no crítica rota (ej: export PDF)
- Slow query causando lag ocasional

**SLA de Respuesta**:
- **Detección → Acknowledged**: <4 horas
- **Target Resolution**: <48 horas (puede esperar próximo deploy)

**Escalación**:
- On-call SRE (durante business hours)
- No escalación inmediata

**Comunicación**:
- Internal: #incidents (thread, no @channel)
- External: No status page (a menos que pregunte customer)
- Customers: No comunicación proactiva

---

## 🔄 Workflow de Incident Response

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  DETECTION   │───▶│   TRIAGE     │───▶│   RESPONSE   │───▶│  RESOLUTION  │───▶│ POST-MORTEM  │
│              │    │              │    │              │    │              │    │              │
│ Alert fires  │    │ Classify SEV │    │  War Room    │    │   Deploy     │    │  5 Whys      │
│  <5 min      │    │   <10 min    │    │  Investigate │    │   Validate   │    │ Action Items │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

---

## 1️⃣ Fase 1: Detection (T+0min)

**Objetivo**: Detectar incident lo antes posible, idealmente antes que usuarios reporten.

### Métodos de Detección

**1. Automated Monitoring** (Preferido):
- **Synthetic Monitoring**: Health checks cada 1min (Pingdom, StatusCake)
- **Error Rate Alerts**: Error rate >1% por 5min (DataDog, New Relic)
- **Latency Alerts**: P95 latency >2s por 5min
- **Infrastructure Alerts**: CPU >90%, Memory >90%, Disk >95%
- **Business Metrics**: Conversion drop >20%, orders drop >50%

**2. User Reports**:
- Customer support tickets (#customer-feedback)
- Social media mentions (Twitter, Reddit)
- Direct emails a support@

**3. Internal Discovery**:
- Developer encuentra bug en producción
- QA encuentra regression

### Alert Routing

**PagerDuty/Opsgenie Configuration**:
```yaml
SEV-1 Alerts:
  - Page: On-call SRE (immediate)
  - Escalation: DevOps Lead (5min), EM (10min), CTO (15min)
  - Channels: #incidents (Slack), SMS, Phone call
  
SEV-2 Alerts:
  - Page: On-call SRE (immediate)
  - Escalation: DevOps Lead (30min)
  - Channels: #incidents (Slack), SMS

SEV-3 Alerts:
  - Notification: #incidents (Slack only)
  - No paging (during business hours only)
```

**Checklist - Detection**:
- [ ] Alert fired (automated) OR user reported
- [ ] On-call engineer notified (PagerDuty)
- [ ] Incident ticket created (Jira/ServiceNow)

---

## 2️⃣ Fase 2: Triage (T+0 a T+10min)

**Objetivo**: Clasificar severidad y reunir contexto inicial.

### Paso 2.1: Acknowledge Incident

**Responsable**: On-call SRE  
**Duración**: <5min  
**Entregable**: PagerDuty acknowledged

**Actividades**:
1. Acknowledge alert en PagerDuty (detiene escalación)
2. Crear #incident-YYYY-MM-DD-description channel en Slack
3. Post initial message en #incidents

**Template - Initial Message**:
```markdown
🚨 **INCIDENT DECLARED** 🚨

**Severity**: [SEV-1 / SEV-2 / SEV-3]
**Summary**: [Brief description, ej: "Website down - 500 errors"]
**Impact**: [% users affected, ej: "100% users cannot access site"]
**Incident Channel**: #incident-2025-12-07-website-down
**Incident Commander**: @john-doe (On-call SRE)

**Status**: Investigating...
**Next Update**: [Time, ej: "T+15min"]
```

**Example**:
```markdown
🚨 **INCIDENT DECLARED** 🚨

**Severity**: SEV-1
**Summary**: Payment processing completely down - Stripe API returning 503
**Impact**: 100% users cannot complete checkout (0 orders in last 10min)
**Incident Channel**: #incident-2025-12-07-payments-down
**Incident Commander**: @jane-sre

**Status**: Investigating Stripe API status
**Next Update**: 12:15pm (T+10min)
```

---

### Paso 2.2: Classify Severity

**Responsable**: Incident Commander (On-call SRE)  
**Duración**: <5min  
**Entregable**: Severity level assigned

**Decision Tree**:
```
¿Sistema completamente caído? ───YES──→ SEV-1
         │
         NO
         ↓
¿>50% usuarios afectados? ───YES──→ SEV-2
         │
         NO
         ↓
¿Funcionalidad crítica degradada? ───YES──→ SEV-2
         │
         NO
         ↓
      SEV-3
```

**Re-Classification**:
- Incident puede ser reclasificado durante investigación
- Upgrade severity: Comunicar inmediatamente en #incidents
- Downgrade severity: Comunicar en next update

---

### Paso 2.3: Assemble Response Team

**Responsable**: Incident Commander  
**Duración**: <5min (SEV-1), <15min (SEV-2)  
**Entregable**: Response team notified

**SEV-1 Response Team**:
- **Incident Commander (IC)**: On-call SRE (leads response)
- **Communication Lead (CL)**: Engineering Manager (stakeholder updates)
- **Subject Matter Experts (SMEs)**: 
  - Backend engineer (if API issue)
  - Frontend engineer (if UI issue)
  - Database engineer (if DB issue)
  - Security engineer (if security breach)
- **Scribe**: Non-involved developer (documents timeline)

**How to Assemble**:
1. IC posts in #incident-channel: "@backend-oncall @frontend-oncall join war room"
2. Start Zoom/Google Meet war room
3. Share link in #incident-channel

**SEV-2 Response Team**:
- IC + 1-2 SMEs (no war room necesario)
- Communication via Slack thread

**SEV-3 Response Team**:
- IC only (or assign to developer)

---

## 3️⃣ Fase 3: Response (T+10min a Resolution)

**Objetivo**: Investigar root cause y restaurar servicio.

### Paso 3.1: Initial Investigation

**Responsable**: Incident Commander + SMEs  
**Duración**: 10-30min  
**Entregable**: Hypothesis de root cause

**Investigation Checklist**:

**1. Check Monitoring Dashboards**:
- [ ] Error rate (DataDog/New Relic)
- [ ] Latency (P50, P95, P99)
- [ ] Traffic (requests per second)
- [ ] Infrastructure (CPU, memory, disk)
- [ ] Database (query performance, connections)

**2. Check Recent Changes**:
- [ ] Deployments últimas 24h (Git commits, CI/CD)
- [ ] Infrastructure changes (Terraform, Kubernetes)
- [ ] Configuration changes (feature flags, env vars)
- [ ] Third-party service changes (Stripe, AWS)

**3. Check Logs**:
- [ ] Application logs (CloudWatch, Splunk)
- [ ] Error logs (stack traces)
- [ ] Infrastructure logs (Kubernetes events)
- [ ] Database logs (slow queries)

**4. Check External Dependencies**:
- [ ] Third-party status pages (Stripe, AWS, Cloudflare)
- [ ] DNS resolution (dig, nslookup)
- [ ] SSL certificates (expiry)

**Common Root Causes**:
- **Bad deployment** (40%): Recent code change broke something
- **Infrastructure** (25%): Resource exhaustion (CPU, memory, disk)
- **Database** (20%): Slow query, connection pool exhausted
- **Third-party** (10%): External API down (Stripe, AWS)
- **Configuration** (5%): Feature flag, env var misconfiguration

---

### Paso 3.2: Implement Mitigation

**Responsable**: Incident Commander + SMEs  
**Duración**: Varies (goal: <2h for SEV-1)  
**Entregable**: Service restored

**Mitigation Strategies** (en orden de velocidad):

**1. Rollback** (Fastest: 5-15min):
```bash
# Rollback to previous deployment
kubectl rollout undo deployment/api-server

# Or via CI/CD
git revert <bad-commit>
# Trigger deployment pipeline
```

**When to rollback**:
- ✅ Recent deployment (<24h)
- ✅ Clear cause (code change)
- ✅ Previous version was stable
- ❌ Multiple deployments since last stable
- ❌ Database migration involved (risk)

**2. Feature Flag Disable** (Fastest: <1min):
```bash
# Toggle feature flag OFF
launchdarkly set feature-checkout false

# Or env var
kubectl set env deployment/api FEATURE_NEW_CHECKOUT=false
```

**When to use**:
- ✅ New feature causing issue
- ✅ Feature flag exists
- ✅ Instant rollback needed

**3. Configuration Change** (Fast: 5-10min):
```bash
# Increase resource limits
kubectl set resources deployment/api --limits=cpu=2,memory=4Gi

# Or scale up
kubectl scale deployment/api --replicas=10
```

**When to use**:
- ✅ Resource exhaustion (CPU, memory)
- ✅ Traffic spike (scale horizontally)

**4. Database Fix** (Medium: 15-30min):
```sql
-- Kill long-running queries
SELECT pg_terminate_backend(pid) 
FROM pg_stat_activity 
WHERE state = 'active' AND query_duration > '5 minutes';

-- Add missing index
CREATE INDEX CONCURRENTLY idx_users_email ON users(email);
```

**When to use**:
- ✅ Database slow queries
- ✅ Index missing
- ❌ Avoid schema changes during incident

**5. Code Hotfix** (Slow: 30min-2h):
```bash
# Emergency hotfix branch
git checkout -b hotfix/incident-payments
# Fix bug
git commit -m "hotfix: fix Stripe API timeout"
# Fast-track deployment (skip staging)
```

**When to use**:
- ✅ Rollback not possible
- ✅ Root cause identified and fixable
- ⚠️ Last resort (risky during incident)

---

### Paso 3.3: Validate Mitigation

**Responsable**: Incident Commander + QA  
**Duración**: 5-15min  
**Entregable**: Confirmation service restored

**Validation Checklist**:
- [ ] **Synthetic Checks**: Health checks passing (Pingdom)
- [ ] **Error Rate**: Back to baseline (<0.1%)
- [ ] **Latency**: P95 <500ms (normal)
- [ ] **Traffic**: Requests/sec back to normal
- [ ] **User Testing**: Manual test critical flow (ej: checkout)
- [ ] **Monitoring**: No new alerts firing
- [ ] **Stakeholder Confirmation**: PM/CS confirms users can access

**If Mitigation Failed**:
- Try alternative mitigation strategy
- Escalate to next level (EM → CTO)
- Consider partial mitigation (restore 80% of service)

---

### Paso 3.4: Communication During Incident

**Responsable**: Communication Lead (Engineering Manager)  
**Frequency**: Every 15min (SEV-1), Every 1h (SEV-2)  
**Entregable**: Stakeholder updates

**SEV-1 Communication Timeline**:

**T+0min (Incident Start)**:
- IC posts in #incidents: "INCIDENT DECLARED"

**T+5min**:
- CL posts in #engineering: "@channel Incident ongoing - investigating"

**T+15min**:
- CL updates Status Page: "We are investigating reports of..."
- CL notifies CTO via Slack DM

**T+30min**:
- CL emails executives: "Update on ongoing incident"
- CL alerts Customer Success: "Prepare for support tickets"

**T+60min**:
- CL drafts customer email (if not resolved)
- CL posts update in #incidents: "Still investigating, ETA..."

**T+Resolution**:
- CL posts in #incidents: "INCIDENT RESOLVED"
- CL updates Status Page: "Systems operational"
- CL emails customers: "Incident resolved, apology"

**Status Page Update Templates**:

**Investigating**:
```
We are currently investigating reports of [issue description]. 
We will provide an update within [timeframe].
```

**Identified**:
```
The issue has been identified as [brief explanation]. 
Our team is working on a fix. Estimated resolution: [time].
```

**Monitoring**:
```
A fix has been deployed and we are monitoring the results. 
We expect full recovery within [timeframe].
```

**Resolved**:
```
The incident has been resolved. All systems are now operational. 
We apologize for any inconvenience caused.
```

---

## 4️⃣ Fase 4: Resolution (Service Restored)

**Objetivo**: Confirmar que incident está completamente resuelto y comunicar.

### Paso 4.1: Declare Incident Resolved

**Responsable**: Incident Commander  
**Duración**: <10min  
**Entregable**: Resolution announcement

**Resolution Checklist**:
- [ ] Mitigation deployed and validated
- [ ] Monitoring stable for 30min+ (no new alerts)
- [ ] Error rate back to baseline
- [ ] Latency back to normal
- [ ] User testing confirmed working
- [ ] No new user complaints

**Resolution Announcement Template**:
```markdown
✅ **INCIDENT RESOLVED** ✅

**Incident**: #incident-2025-12-07-payments-down
**Duration**: 1h 23min (12:05pm - 1:28pm)
**Root Cause**: Stripe API timeout due to rate limiting
**Mitigation**: Increased retry logic with exponential backoff

**Timeline**:
- 12:05pm: Alert fired (payments failing)
- 12:10pm: SEV-1 declared, war room started
- 12:25pm: Root cause identified (Stripe rate limit)
- 12:45pm: Hotfix deployed to staging
- 1:15pm: Hotfix deployed to production
- 1:28pm: Validated - 0 payment failures in 15min

**Next Steps**:
- Post-mortem scheduled: Dec 8, 2pm
- Action items will be tracked in Jira

**Impact**:
- 1,234 failed payment attempts
- Estimated revenue loss: $15,000
- 0 data loss

Thanks to @jane-sre, @john-backend, @sarah-em for rapid response! 🙏
```

---

### Paso 4.2: Customer Communication

**Responsable**: Communication Lead + Customer Success  
**Duración**: <1h post-resolution  
**Entregable**: Customer email sent

**Email Template - SEV-1 Resolved**:
```
Subject: Service Restored - [Company Name]

Hi [Customer Name],

We wanted to let you know that the service issue affecting [feature] 
has been resolved as of [time].

What happened:
[Brief, non-technical explanation of issue]

What we did:
[Brief explanation of fix]

Impact to you:
[Specific impact, ej: "You may have experienced payment failures 
between 12pm-1:30pm. All failed payments have been automatically 
retried and processed."]

What we're doing to prevent this:
- [Action item 1]
- [Action item 2]

We sincerely apologize for any inconvenience this may have caused. 
If you have any questions or concerns, please don't hesitate to 
reach out to our support team at support@company.com.

Best regards,
[Engineering Team]
```

**SEV-2**: Email only if >50% users affected  
**SEV-3**: No proactive email (respond if customers ask)

---

## 5️⃣ Fase 5: Post-Mortem (24-48h Post-Incident)

**Objetivo**: Aprender del incident para prevenir recurrencia.

### Paso 5.1: Schedule Post-Mortem Meeting

**Responsable**: Incident Commander  
**Duración**: Meeting: 60min  
**Timing**: 24-48h post-incident (not immediate)  
**Entregable**: Post-mortem document + action items

**Attendees**:
- Incident Commander (facilitator)
- All SMEs who participated
- Engineering Manager
- Product Manager (if customer-facing)
- Customer Success (if high customer impact)

**Agenda (60min)**:
1. **Timeline Review** (15min): What happened, when
2. **Root Cause Analysis** (20min): 5 Whys technique
3. **What Went Well** (10min): Positive reinforcement
4. **What Could Be Improved** (10min): Constructive feedback
5. **Action Items** (5min): Concrete next steps

---

### Paso 5.2: Root Cause Analysis (5 Whys)

**Technique**: Ask "Why?" 5 times para llegar a root cause.

**Example - Payment Incident**:
```
Problem: Payments failing

1. Why? → Stripe API returning 429 (rate limit)
2. Why? → Our API making too many requests to Stripe
3. Why? → Retry logic not implemented, so each failure = immediate retry
4. Why? → Feature was rushed, retry logic was "nice to have" in backlog
5. Why? → No DoD checklist requires error handling/retry logic

→ ROOT CAUSE: Missing Definition of Done for production features
```

**Template - 5 Whys**:
```markdown
## Root Cause Analysis

**Problem**: [What broke]

1. **Why?** [Immediate cause]
2. **Why?** [Underlying cause]
3. **Why?** [Deeper cause]
4. **Why?** [Process failure]
5. **Why?** [Organizational failure]

**Root Cause**: [Fundamental issue to fix]

**Contributing Factors**:
- [Factor 1]
- [Factor 2]
```

---

### Paso 5.3: Action Items

**Responsable**: Engineering Manager (ensures follow-through)  
**Duración**: Varies  
**Entregable**: Jira tickets with owners and deadlines

**Action Item Template**:
```markdown
## Action Items

### Immediate (This Week)
- [ ] **[JIRA-123]** Add retry logic to Stripe API calls
  - Owner: @john-backend
  - Deadline: Dec 10
  - Priority: P0

### Short-Term (This Month)
- [ ] **[JIRA-124]** Create runbook for Stripe rate limit scenarios
  - Owner: @jane-sre
  - Deadline: Dec 20
  - Priority: P1

- [ ] **[JIRA-125]** Update DoD checklist to require error handling
  - Owner: @sarah-em
  - Deadline: Dec 31
  - Priority: P1

### Long-Term (This Quarter)
- [ ] **[JIRA-126]** Implement circuit breaker pattern for all external APIs
  - Owner: @tech-lead
  - Deadline: Q1 2026
  - Priority: P2

- [ ] **[JIRA-127]** Load testing for all critical flows
  - Owner: @qa-lead
  - Deadline: Q1 2026
  - Priority: P2
```

**Follow-Up**:
- Engineering Manager tracks action items weekly
- Post-mortem review in next Retrospective
- Metrics: % action items completed within deadline

---

### Post-Mortem Document Template

**Full template**: See [Proceso: Post-Mortem](../procesos/post-mortem.md)

**Key Sections**:
1. **Summary** (3-5 lines)
2. **Timeline** (minute-by-minute for SEV-1)
3. **Root Cause** (5 Whys)
4. **Impact** (users affected, revenue loss, duration)
5. **What Went Well** (positive reinforcement)
6. **What Could Be Improved** (blameless)
7. **Action Items** (with owners and deadlines)

---

## 🎭 RACI Matrix - Incident Response

| Actividad | On-Call SRE | DevOps Lead | EM | CTO | PM | CS |
|-----------|-------------|-------------|----|----|----|----|
| **Detection** | | | | | | |
| Alert acknowledgment | **R/A** | I | I | I | I | I |
| Severity classification | **R/A** | C | C | I | I | I |
| **Triage** | | | | | | |
| Incident Commander role | **R/A** | I | I | I | I | I |
| Assemble response team | **R** | **A** | C | I | I | I |
| **Response** | | | | | | |
| Technical investigation | **R/A** | C | I | I | I | I |
| Mitigation implementation | **R/A** | C | I | I | I | I |
| **Communication** | | | | | | |
| Internal updates (#incidents) | **R** | C | **A** | I | I | I |
| Status page updates | C | C | **R** | **A** | C | I |
| Customer email (SEV-1) | I | C | **R** | **A** | C | **C** |
| Executive notification | I | C | **R** | **A** | I | I |
| **Post-Incident** | | | | | | |
| Schedule post-mortem | **R/A** | C | C | I | I | I |
| Facilitate post-mortem | **R** | C | **A** | I | C | I |
| Action item tracking | C | C | **R/A** | I | I | I |

---

## 📊 Métricas de Incident Response

### Incident Metrics (Track in DataDog/Jira)

**Volume**:
- Incidents per week (SEV-1/2/3 breakdown)
- Incidents by component (API, DB, Frontend, Infrastructure)

**Response Time**:
- **Time to Acknowledge**: Alert → Acknowledged (Target: <5min)
- **Time to First Response**: Alert → First mitigation attempt (Target: <10min SEV-1)
- **Mean Time to Resolution (MTTR)**: Alert → Resolved
  - SEV-1: Target <2h
  - SEV-2: Target <8h
  - SEV-3: Target <48h

**Communication**:
- **Time to Status Page**: Alert → Status page update (Target: <15min SEV-1)
- **Time to Customer Email**: Alert → Email sent (Target: <60min SEV-1)
- **Update Frequency**: Avg time between updates (Target: <15min SEV-1)

**Post-Mortem**:
- % incidents with post-mortem (Target: 100% SEV-1/2, 50% SEV-3)
- % action items completed within deadline (Target: >80%)
- Incident recurrence rate (Target: <10%)

**DORA Metric**:
- **Change Failure Rate**: % deployments causing incidents (Target: <15%)

---

## 🚨 Runbooks por Scenario

Para scenarios comunes, ver runbooks específicos:

### Infrastructure
- [Database Failover Runbook](../runbooks/database-failover.md)
- [High CPU Troubleshooting](../runbooks/high-cpu-troubleshooting.md)
- [Disk Space Full](../runbooks/disk-space-full.md)
- [Memory Leak Investigation](../runbooks/memory-leak-investigation.md)

### Security
- [DDoS Mitigation](../runbooks/ddos-mitigation.md)
- [Security Breach Response](../procesos/security-response.md)

### Application
- [API Rate Limiting](../runbooks/api-rate-limiting.md) (TBD)
- [Third-Party API Outage](../runbooks/third-party-outage.md) (TBD)

---

## 🔗 Links Relacionados

### Procesos
- [Post-Mortem Process](../procesos/post-mortem.md) - Blameless post-mortem template
- [Security Response](../procesos/security-response.md) - Security-specific incidents
- [Incident Management](../procesos/incident-management.md) - Incident management overview

### Comunicación
- [Incident Communication](../comunicacion/incident-communication.md) - Communication protocols
- [External Stakeholders](../comunicacion/external-stakeholders.md) - Customer communication

### Workflows
- [Feature Development](feature-development.md) - Para entender deployment process
- [Release Management](release-management.md) - Release train y rollback procedures

### Runbooks
- [Runbooks Directory](../runbooks/README.md) - All operational runbooks

---

**Mantenido por**: DevOps Lead + SRE Team  
**Última actualización**: 7 de diciembre de 2025  
**Próxima revisión**: 7 de marzo de 2026  
**Versión**: 1.0
