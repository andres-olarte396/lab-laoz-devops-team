# Incident Management - Detección y Respuesta

## 📋 Resumen Ejecutivo

**Problema**: Cuando producción falla, el caos reina: nadie sabe quién responde, cómo escalar, qué comunicar, resultando en downtime prolongado y clientes furiosos.

**Solución**: **Incident Management Process estructurado** con severidades claras, escalation paths definidos, war room procedures, y blameless postmortem.

**Beneficio**:

- MTTR (Mean Time to Recovery): De 4 horas → <1 hora
- Comunicación clara a stakeholders durante incidents
- Learning from incidents (no repetir errores)
- Confianza del equipo en crisis management

---

## 🎯 Incident Lifecycle

```
Detection → Acknowledgment → Assessment → Response →
Resolution → Communication → Post-Mortem → Improvement
```

**Duration**:

- SEV-1: Detection → Resolution <2 horas
- SEV-2: Detection → Resolution <8 horas
- SEV-3: Detection → Resolution <2 días

---

## 🚨 Severity Levels

### SEV-1 (Critical) - 🔴 P0

**Definition**: Sistema crítico completamente caído, data loss, >50% usuarios afectados

**Examples**:

- Sitio web principal inaccesible (500 errors, DNS down)
- Database corrupted o inaccesible
- Payment processing completamente caído
- Data breach o security incident activo
- Pérdida de datos de usuarios

**Response Time**: <15 minutos

**Escalation**: Inmediata

- Page on-call SRE (PagerDuty/phone)
- Notify Tech Lead + Engineering Manager
- Create #incident-YYYYMMDD-NNN war room channel
- Notify CTO (si no resolved en 1 hora)
- Notify Customer Support + PM

**Communication**:

- Updates cada 15-30 min
- Status page update inmediata
- Twitter/social media si público

**On-call Requirements**:

- Engineer disponible 24/7
- Responde en <10 min
- Laptop/internet siempre accesible

---

### SEV-2 (High) - 🟠 P1

**Definition**: Funcionalidad crítica degradada, 20-50% usuarios afectados, workaround disponible

**Examples**:

- Proceso de pago lento (timeout ocasional pero funciona)
- API crítica con 10% error rate (no 100%)
- Search feature no funciona (users pueden navegar manualmente)
- Email notifications con delay >1 hora

**Response Time**: <1 hora

**Escalation**:

- Page on-call SRE
- Notify Tech Lead
- Create incident thread en #incidents
- Notify Engineering Manager (si no resolved en 2 horas)

**Communication**:

- Updates cada 1-2 horas
- Status page update
- Internal Slack #incidents

---

### SEV-3 (Medium) - 🟡 P2

**Definition**: Funcionalidad no-core afectada, <20% usuarios, workaround fácil disponible

**Examples**:

- Feature secundaria no funciona (ej: comments, ratings)
- Admin panel lento
- Reporting dashboards desactualizados
- Non-critical integration down (analytics, marketing tools)

**Response Time**: <4 horas

**Escalation**:

- Notify on-call SRE (Slack/email, no page)
- Notify Tech Lead
- Create Jira ticket

**Communication**:

- Update 1x al día
- Internal Slack solo

---

### SEV-4 (Low) - 🟢 P3

**Definition**: Bug menor, cosmético, <5% usuarios

**Examples**:

- Typo en UI
- Logo desalineado
- Console warning (no error)
- Feature flag incorrectly configured (no user impact)

**Response Time**: <1 día laboral

**Escalation**: None (regular workflow)

**Communication**: Jira ticket, fix en próximo sprint

---

## 📞 Escalation Paths

### Path 1: Technical Escalation

```
[Incident Detected]
    ↓
[On-call SRE] (acknowledge <10 min)
    ↓
¿SEV-1 o SEV-2?
    ├─ YES → [Page Secondary On-call (backup)]
    │         ↓
    │         [Notify Tech Lead]
    │         ↓
    │         [Create War Room #incident-YYYYMMDD-NNN]
    │         ↓
    │         ¿Still unresolved after 1h?
    │              ├─ YES → [Escalate to Engineering Manager]
    │              │          ↓
    │              │          ¿Still unresolved after 2h?
    │              │               ├─ YES → [Escalate to CTO]
    │              │               └─ NO → [Continue mitigation]
    │              └─ NO → [Continue mitigation]
    └─ NO (SEV-3/4) → [SRE handles solo]
```

---

### Path 2: Business Escalation

```
[Incident Detected (SEV-1 or SEV-2)]
    ↓
[Engineering Manager notified]
    ↓
¿Customer-facing impact?
    ├─ YES → [Notify Product Manager]
    │         ↓
    │         [Notify Customer Support Lead]
    │         ↓
    │         [Update Status Page]
    │         ↓
    │         ¿Media/PR risk? (viral on Twitter, etc.)
    │              ├─ YES → [Notify VP/CEO + PR team]
    │              └─ NO → [Continue]
    └─ NO → [Internal incident only]
```

---

## 🏥 Incident Response Procedures

### Step 1: Detection

**How incidents are detected**:

1. **Automated Alerts** (80% of incidents)

   - Monitoring tools: Datadog, Grafana, Azure Monitor
   - PagerDuty/Opsgenie triggers
   - Error rate spike >5%
   - Latency P95 >1000ms
   - Health check failures

2. **User Reports** (15% of incidents)

   - Support tickets
   - Twitter mentions
   - Customer complaints

3. **Manual Discovery** (5% of incidents)
   - Engineer notices issue during regular work
   - Smoke tests after deployment

---

### Step 2: Acknowledgment

**Who**: On-call SRE

**SLA**: <10 min for SEV-1/2, <1 hour for SEV-3

**Actions**:

1. **Acknowledge alert** en PagerDuty (stops paging)
2. **Initial assessment**:
   - ¿Qué está roto?
   - ¿Cuántos usuarios afectados?
   - ¿Qué severidad?
3. **Create incident** en incident management tool (PagerDuty, Jira)
4. **Post initial update** en #incidents Slack channel

**Template**:

```markdown
🚨 **INCIDENT DECLARED**

**Severity**: SEV-1 🔴
**Title**: Production API returning 500 errors
**Impact**: All users unable to login
**Detected**: 2025-01-15 14:32 UTC
**Owner**: @oncall-sre-alice
**Status**: Investigating

Will update in 15 min.
```

---

### Step 3: Assessment

**Who**: On-call SRE + backup (if SEV-1/2)

**Duration**: 5-15 min

**Questions to Answer**:

1. **What's broken?** (specific service, API, database, etc.)
2. **How many users affected?** (%, absolute number)
3. **What's the business impact?** (revenue loss, reputation, compliance)
4. **What changed recently?** (deployment, config change, infra change)
5. **Is this a new issue or recurring?** (check past incidents)

**Tools**:

- Monitoring dashboards (Grafana)
- Log aggregation (Elasticsearch, Splunk)
- APM (Application Performance Monitoring: Datadog, New Relic)
- Recent deploy history (CI/CD logs)

**Output**: Severity classification (SEV-1/2/3/4)

---

### Step 4: War Room (SEV-1/2 only)

**When**: SEV-1 immediately, SEV-2 if not resolved in 30 min

**How**: Create Slack channel `#incident-YYYYMMDD-NNN`

**Naming**: `#incident-20250115-001` (date + incident number)

---

**War Room Roles**:

| Role                      | Responsibilities                                       | Who                         |
| ------------------------- | ------------------------------------------------------ | --------------------------- |
| **Incident Commander**    | Coordinates response, makes decisions, delegates tasks | On-call SRE (or Tech Lead)  |
| **Responders**            | Investigate, mitigate, fix the issue                   | SRE, Backend Dev, DevOps    |
| **Communicator**          | Updates stakeholders, status page, Slack               | Engineering Manager or PM   |
| **Scribe**                | Documents timeline, actions taken (for post-mortem)    | Junior SRE or available dev |
| **Subject Matter Expert** | Domain knowledge (DB, networking, specific service)    | Called in as needed         |

---

**War Room Rules**:

1. **Single thread of communication**: Todo en #incident-YYYYMMDD-NNN, no DMs
2. **Incident Commander has final say**: No debates, IC decides
3. **Action items explicit**: "Alice, check database logs" (not "someone should check logs")
4. **No blame**: Focus en fixing, not "who caused this"
5. **Status updates regular**: Every 15-30 min for SEV-1, every 1-2h for SEV-2

---

**War Room Communication Template**:

```markdown
📊 **STATUS UPDATE** (14:45 UTC)

**Current Status**: Investigating
**Root Cause**: Unknown (suspecting database connection pool exhaustion)
**Actions Taken**:

- ✅ Increased connection pool from 100 → 200
- ✅ Restarted application pods
- 🔄 Monitoring error rates (currently 8%, was 15%)

**Next Steps**:

- [ ] Analyze slow query logs (Alice, ETA 10 min)
- [ ] Check for long-running transactions (Bob, ETA 5 min)

**ETA to Resolution**: 30 min

Next update in 15 min.
```

---

### Step 5: Mitigation & Resolution

**Goal**: Stop the bleeding FIRST, find root cause LATER

**Mitigation Options** (fast):

1. **Rollback** (fastest: <5 min)

   ```bash
   kubectl rollout undo deployment/myapp --namespace=production
   ```

   - Use if: Recent deployment caused issue
   - Downside: Lose new features

2. **Restart Services** (fast: <10 min)

   ```bash
   kubectl rollout restart deployment/myapp
   ```

   - Use if: Memory leak, stuck connections
   - Downside: Temporary downtime during restart

3. **Scale Up** (fast: <10 min)

   ```bash
   kubectl scale deployment/myapp --replicas=10
   ```

   - Use if: Traffic spike, capacity issue
   - Downside: Higher cost

4. **Kill Switch / Feature Flag** (fast: <5 min)

   ```bash
   # Disable problematic feature
   kubectl set env deployment/myapp FEATURE_X_ENABLED=false
   ```

   - Use if: Specific feature causing issues
   - Downside: Users lose feature

5. **Traffic Rerouting** (medium: <20 min)
   - Redirect traffic to backup region
   - Failover to DR site
   - Use if: Regional outage, datacenter issue

---

**Resolution** (slower, permanent fix):

Once mitigated (service is up, users unblocked), work on permanent fix:

- Identify root cause
- Develop proper fix (code patch, config change)
- Test in Staging
- Deploy to Production
- Monitor

---

### Step 6: Communication

**Internal Communication** (Slack #incidents):

- SEV-1: Every 15-30 min
- SEV-2: Every 1-2 hours
- SEV-3: Once daily

**External Communication** (Status Page):

- SEV-1: Update immediately + every 30 min
- SEV-2: Update within 1 hour + every 2 hours
- SEV-3: Update within 4 hours

**Status Page Template**:

```markdown
🔴 **Investigating** - We are investigating reports of login failures.
Users may be unable to access the application.
Posted: 14:32 UTC

🟡 **Identified** - We have identified the issue as a database connection
pool exhaustion. We are working on a fix.
Updated: 14:50 UTC

🟢 **Resolved** - The issue has been resolved. All services are operational.
Updated: 15:15 UTC
```

---

**Customer Support Communication**:

When SEV-1/2 incident occurs:

1. Notify Support Lead immediately
2. Provide template response for users:

```markdown
**Template for Support Team**:

Hi [Customer],

We are aware of an issue affecting login functionality. Our engineering
team is actively working on a resolution. We expect to have this resolved
within the next hour.

We apologize for the inconvenience. You can check real-time status at
https://status.mycompany.com

Thank you for your patience.
```

---

### Step 7: Post-Mortem

**When**: Within 48 hours of SEV-1/2 resolution

**Who**: Incident Commander writes, team reviews

**Format**: See [Post-Mortem Process](./post-mortem.md)

**Key Sections**:

1. What happened (timeline)
2. Root cause (5 Whys)
3. Impact (users, revenue, duration)
4. What went well
5. What went wrong
6. Action items (prevent recurrence)

---

## 📋 Incident Templates

### Incident Declaration Template

```markdown
🚨 **INCIDENT DECLARED**

**Incident ID**: INC-20250115-001
**Severity**: SEV-[1/2/3/4] [🔴/🟠/🟡/🟢]
**Title**: [Short description]
**Impact**: [Who is affected and how]
**Detected**: [YYYY-MM-DD HH:MM UTC]
**Detection Method**: [Alert/User Report/Manual]
**Owner**: [@oncall-engineer]
**Status**: [Investigating/Identified/Mitigating/Resolved]

**Details**:
[More context]

**Timeline**:

- 14:32 - Incident detected
- 14:35 - On-call acknowledged
- 14:40 - Severity assessed as SEV-1

**Next Update**: [Time]
```

---

### Status Update Template

```markdown
📊 **STATUS UPDATE** ([HH:MM UTC])

**Status**: [Investigating/Identified/Mitigating/Monitoring/Resolved]
**Root Cause**: [Known/Suspected/Unknown]

**Actions Taken**:

- ✅ [Completed action 1]
- ✅ [Completed action 2]
- 🔄 [In-progress action 3]

**Current Metrics**:

- Error rate: X% (was Y%)
- Latency P95: Xms (was Yms)
- Affected users: X% (was Y%)

**Next Steps**:

- [ ] [Action item] (Owner: @person, ETA: XX min)

**ETA to Resolution**: [Time estimate or "Unknown"]

**Next Update**: [Time]
```

---

### Resolution Template

```markdown
✅ **INCIDENT RESOLVED**

**Incident ID**: INC-20250115-001
**Severity**: SEV-1 🔴
**Title**: Production API 500 errors
**Duration**: 43 minutes (14:32 - 15:15 UTC)
**Impact**: 100% of users unable to login

**Root Cause**: Database connection pool exhaustion due to increased traffic
from marketing campaign (not communicated to engineering).

**Resolution**:

- Increased connection pool from 100 → 200
- Restarted application pods
- Traffic returned to normal

**Follow-up Actions**:

1. Post-mortem scheduled for Jan 16, 10am
2. Add monitoring alert for connection pool usage >80%
3. Establish process for engineering to be notified of marketing campaigns

**Post-Mortem**: [Link to be added]

Thank you to @alice, @bob, @charlie for rapid response.
```

---

## 📊 Incident Metrics

### Metric #1: Mean Time to Detect (MTTD)

**Definition**: Time from incident occurrence → Detection

**Target**:

- SEV-1: <5 min (via automated alerts)
- SEV-2: <15 min

**How to Improve**:

- Better monitoring coverage
- Synthetic checks (probe endpoints every 1 min)
- User error reporting (auto-report JS errors)

---

### Metric #2: Mean Time to Acknowledge (MTTA)

**Definition**: Time from detection → On-call acknowledges

**Target**:

- SEV-1: <10 min
- SEV-2: <30 min

**How to Improve**:

- PagerDuty escalation (if no ack in 10 min, page backup)
- On-call compensation (pay engineers for being on-call)

---

### Metric #3: Mean Time to Mitigate (MTTM)

**Definition**: Time from acknowledgment → Service restored (users unblocked)

**Target**:

- SEV-1: <1 hour
- SEV-2: <4 hours

**How to Improve**:

- Faster rollback (1-click rollback button)
- Runbooks (step-by-step guides for common incidents)
- Chaos engineering (practice failures)

---

### Metric #4: Mean Time to Recovery (MTTR)

**Definition**: Time from detection → Permanent fix deployed

**Target**:

- SEV-1: <2 hours
- SEV-2: <8 hours

**How to Improve**:

- Root cause analysis training
- Post-mortem action items actually implemented

---

### Metric #5: Incident Frequency

**Definition**: Number of SEV-1/2 incidents per month

**Target**: <2 SEV-1/month, <5 SEV-2/month

**How to Improve**:

- Post-mortem action items
- Proactive monitoring
- Chaos engineering

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                       | On-call SRE | Tech Lead | Eng Manager | CTO | PM  |
| ------------------------------- | ----------- | --------- | ----------- | --- | --- |
| Detect incident (alerts)        | R/A         | I         | I           | I   | I   |
| Acknowledge incident            | R/A         | C         | I           | I   | I   |
| Assess severity                 | R/A         | C         | C           | I   | I   |
| Create war room (SEV-1/2)       | R/A         | C         | C           | I   | I   |
| Coordinate response (IC role)   | R/A         | C         | C           | I   | I   |
| Investigate root cause          | R           | C/A       | C           | I   | I   |
| Mitigate/Resolve                | R/A         | C         | C           | I   | I   |
| Communicate internally          | R           | C         | A           | I   | C   |
| Communicate externally (status) | C           | C         | R           | C   | A   |
| Write post-mortem               | R/A         | C         | C           | I   | C   |
| Implement action items          | R           | A         | C           | I   | C   |

**Legend**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup On-call Rotation

- [ ] Define on-call rotation (weekly? bi-weekly?)
- [ ] Setup PagerDuty/Opsgenie
- [ ] Configure alert routing
- [ ] Document on-call responsibilities
- [ ] Compensate on-call engineers (pay, comp time)

---

### Sprint 1-2: Incident Response Process

- [ ] Document severity levels (SEV-1/2/3/4)
- [ ] Define escalation paths
- [ ] Create Slack channel templates
- [ ] Train team on incident response

---

### Sprint 3-4: War Room Procedures

- [ ] Define war room roles (IC, Responders, Communicator, Scribe)
- [ ] Create communication templates
- [ ] Practice war room with mock incident (tabletop exercise)

---

### Sprint 5-6: Status Page & External Comms

- [ ] Setup status page (Statuspage.io, Atlassian Statuspage)
- [ ] Integrate with monitoring alerts
- [ ] Train Customer Support on incident comms

---

### Sprint 7+: Post-Mortem Culture

- [ ] Establish blameless post-mortem culture
- [ ] Track action items from post-mortems
- [ ] Share learnings company-wide (monthly incident review)

---

## ✅ Success Criteria

### Mes 1

- ✅ On-call rotation established
- ✅ PagerDuty configured
- ✅ All engineers trained on severity levels

### Mes 2-3

- ✅ War room procedures practiced (1 tabletop exercise)
- ✅ MTTA <30 min for SEV-1
- ✅ Status page updates within 1h for SEV-1/2

### Mes 4+

- ✅ MTTR <1 hour for SEV-1
- ✅ Post-mortem written for 100% of SEV-1/2 incidents
- ✅ Action items from post-mortems completed >70%

---

## 🔗 Links Relacionados

- [Post-Mortem Process](./post-mortem.md) - Blameless post-mortem template
- [Monitoring & Alerting](./monitoring-alerting.md) - Alert configuration
- [CI/CD Pipeline](./cicd-pipeline.md) - Rollback procedures

---

## 📚 Antipatterns (Evitar)

### ❌ Antipattern #1: Blame Culture

**Problema**: "Who broke production?" "It's Alice's fault!"

**Por qué es malo**: Engineers scared to take risks, hide mistakes, no learning

**Solución**: Blameless post-mortems, focus on SYSTEMS not people

---

### ❌ Antipattern #2: No Post-Mortem

**Problema**: Incident resolved, everyone moves on, no documentation

**Por qué es malo**: Same incident repeats next month

**Solución**: Mandatory post-mortem for SEV-1/2 within 48h, track action items

---

### ❌ Antipattern #3: Hero Culture

**Problema**: "Alice saved the day again! She's amazing!" (Alice worked 14h straight)

**Por qué es malo**: Burnout, single point of failure, not sustainable

**Solución**: Rotate on-call, document runbooks (so anyone can respond), celebrate TEAMS not individuals

---

### ❌ Antipattern #4: Too Many Incidents Normalized

**Problema**: "Oh, another SEV-2, no big deal, happens every week"

**Por qué es malo**: Complacency, incidents become BAU (business as usual)

**Solución**: If >2 SEV-1/month or >5 SEV-2/month → RED FLAG, executive escalation needed

---

### ❌ Antipattern #5: Ignored Action Items

**Problema**: Post-mortem lists 10 action items, 0 completed

**Por qué es malo**: Same incident repeats, team loses trust in process

**Solución**: Track action items in Jira, assign owners, review in next retro

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-06  
**Owner**: DevOps Lead / SRE Lead  
**Review Cycle**: Trimestral
