# Change Management - Gestión de Cambios

## 📋 Resumen Ejecutivo

**Problema**: Cambios no controlados en producción causan outages, conflictos entre equipos, y sorpresas desagradables ("¿quién cambió el firewall?").

**Solución**: **Change Management Process formal** con risk assessment, approval workflows, change windows, y rollback plans.

**Beneficio**:

- Cambios coordinados (no conflictos entre equipos)
- Risk assessment antes de cambios (prevenir outages)
- Auditabilidad (sabemos qué cambió, cuándo, quién aprobó)
- Compliance (regulaciones requieren change control)

---

## 🎯 Change Management Process

### Full Change Lifecycle

```
Request → Risk Assessment → CAB Review →
Approval → Schedule → Implementation →
Verification → Documentation → Closure
```

**Duration**:

- Standard Change: 3-5 días (request → implementation)
- Emergency Change: <4 horas
- Pre-approved Change: <1 día

---

## 📝 Change Types

### 1. Standard Change

**Definition**: Normal, planned changes to production

**Examples**:

- Application deployment (new features)
- Infrastructure changes (scaling, new servers)
- Configuration changes (firewall rules, DNS)
- Database schema changes

**Approval Required**: Change Advisory Board (CAB)

**Lead Time**: Mínimo 3 días business antes de implementation

**Change Window**: Horario laboral o maintenance window

---

### 2. Emergency Change

**Definition**: Urgent changes para resolver SEV-1/2 incidents

**Examples**:

- Hotfix para production outage
- Security patch crítico (0-day vulnerability)
- Rollback de deployment fallido

**Approval Required**: DevOps Lead (post-facto si es SEV-1)

**Lead Time**: Inmediato

**Change Window**: Cualquier momento (24/7)

**Post-Implementation**: Retrospective CAB review dentro de 48h

---

### 3. Pre-Approved Change (Standard/Normal Change)

**Definition**: Cambios repetitivos, bajo riesgo, pre-aprobados por CAB

**Examples**:

- Regular application deployments (siguiendo CI/CD pipeline establecido)
- Certificate renewals (automated)
- Log rotation
- Scheduled backups

**Approval Required**: None (ya pre-aprobado)

**Lead Time**: Seguir calendario/proceso establecido

**Criteria for Pre-Approval**:

- Documented procedure (runbook)
- Tested multiple times sin issues
- Automated rollback disponible
- Low risk (no afecta >10% usuarios si falla)

---

### 4. Major Change

**Definition**: Cambios significativos, alto impacto, alto riesgo

**Examples**:

- Data center migration
- Major version upgrade (OS, database)
- Architecture change (monolith → microservices)
- Merger/acquisition integration

**Approval Required**: CAB + CTO + CEO (si aplica)

**Lead Time**: Mínimo 2 semanas

**Change Window**: Dedicated maintenance window (notificar usuarios con anticipación)

**Testing Required**: Full UAT (User Acceptance Testing) en Staging

---

## 🛡️ Risk Assessment

### Risk Matrix

**Impact** (X-axis) × **Likelihood** (Y-axis)

|            | **Low Impact** | **Medium Impact** | **High Impact**  |
| ---------- | -------------- | ----------------- | ---------------- |
| **High**   | 🟡 Medium Risk | 🟠 High Risk      | 🔴 Critical Risk |
| **Medium** | 🟢 Low Risk    | 🟡 Medium Risk    | 🟠 High Risk     |
| **Low**    | 🟢 Low Risk    | 🟢 Low Risk       | 🟡 Medium Risk   |

---

### Impact Assessment

**Low Impact** (🟢):

- <5% usuarios afectados si falla
- No revenue impact
- Fácil rollback (<10 min)

**Medium Impact** (🟡):

- 5-20% usuarios afectados
- <$10k revenue at risk
- Rollback posible pero toma tiempo (<1 hora)

**High Impact** (🟠):

- 20-50% usuarios afectados
- $10k-$100k revenue at risk
- Rollback complejo (>1 hora) o risky

**Critical Impact** (🔴):

- > 50% usuarios afectados
- > $100k revenue at risk
- No rollback disponible (irreversible)
- Compliance/legal implications

---

### Likelihood Assessment

**Low Likelihood** (<10%):

- Change tested extensively en Staging
- Similar changes succeeded before (>10x)
- Automated deployment with health checks
- Rollback plan tested

**Medium Likelihood** (10-30%):

- Change tested en Staging (limited)
- Similar changes succeeded before (2-10x)
- Manual deployment steps
- Rollback plan documented pero no tested

**High Likelihood** (>30%):

- Change NOT tested en Staging
- First time doing this type of change
- Complex manual steps
- No rollback plan

---

### Risk Score Calculation

**Risk Score** = Impact × Likelihood

**Actions Based on Risk**:

| Risk Level       | Action                                                      |
| ---------------- | ----------------------------------------------------------- |
| 🟢 Low Risk      | Standard approval, can proceed                              |
| 🟡 Medium Risk   | CAB review required, detailed rollback plan                 |
| 🟠 High Risk     | CAB + DevOps Lead approval, dry-run in Staging, war room    |
| 🔴 Critical Risk | CAB + CTO approval, dedicated maintenance window, all hands |

---

## 👥 Change Advisory Board (CAB)

### CAB Composition

**Core Members** (always present):

- DevOps Lead (Chair)
- Tech Lead (Backend)
- Tech Lead (Frontend)
- QA Lead
- Security Engineer

**Optional Members** (as needed):

- Product Manager (for product-impacting changes)
- Customer Support Lead (for user-facing changes)
- DBA (for database changes)
- Network Engineer (for infra changes)

---

### CAB Meeting Schedule

**Frequency**: Weekly (every Tuesday 10am)

**Duration**: 30-60 min

**Agenda**:

1. Review new change requests (5 min each)
2. Risk assessment
3. Approve/Reject/Request more info
4. Review previous week's changes (lessons learned)

---

### CAB Review Criteria

**Questions CAB Asks**:

1. **What is changing?** (specific components, scope)
2. **Why is this change needed?** (business justification)
3. **What's the risk if we DON'T make this change?** (cost of inaction)
4. **What's the risk if we DO make this change?** (failure scenarios)
5. **Has this been tested?** (Staging, UAT, load testing)
6. **What's the rollback plan?** (how to undo if fails)
7. **Who is responsible?** (change owner, approver, implementer)
8. **When will this happen?** (date, time, duration)
9. **What dependencies exist?** (other teams, external services)
10. **How will we know if it succeeded?** (success criteria, monitoring)

---

### CAB Decision Options

**1. Approved** ✅

- Change can proceed as planned
- Implementation scheduled

**2. Approved with Conditions** ⚠️

- Change approved BUT must meet conditions first
- Examples: "Approved IF tested in Staging first", "Approved IF rollback plan documented"

**3. Rejected** ❌

- Change not approved
- Reasons: Too risky, not enough info, timing bad
- Requestor can resubmit with more details

**4. Deferred** 🕐

- Not enough time to review
- Reschedule for next CAB meeting
- Requestor provides more details

---

## 📋 Change Request Template

### RFC (Request for Change) Form

````markdown
# Change Request: [Title]

**Change ID**: CHG-20250115-001
**Requestor**: @alice-developer
**Submitted**: 2025-01-15
**Target Date**: 2025-01-20 (Tuesday, 22:00 UTC)

---

## 1. Change Summary

**What is changing?**
[Brief 1-2 sentence description]

**Why is this change needed?**
[Business justification, problem being solved]

---

## 2. Change Details

**Type**: [Standard / Emergency / Major / Pre-Approved]

**Affected Systems**:

- [ ] Frontend (Web App)
- [ ] Backend API
- [ ] Database
- [ ] Infrastructure
- [ ] Third-party integrations

**Specific Components**:

- Component 1: [describe]
- Component 2: [describe]

---

## 3. Risk Assessment

**Impact**: [Low / Medium / High / Critical]
**Likelihood**: [Low / Medium / High]
**Risk Score**: [Low 🟢 / Medium 🟡 / High 🟠 / Critical 🔴]

**Impact Analysis**:

- Users affected: [X% or "None"]
- Revenue at risk: [$ amount or "None"]
- Downtime expected: [X minutes or "Zero downtime"]

**Failure Scenarios**:

1. [What could go wrong #1]
   - Likelihood: [%]
   - Mitigation: [How to prevent]
2. [What could go wrong #2]
   - Likelihood: [%]
   - Mitigation: [How to prevent]

---

## 4. Testing

**Testing Completed**:

- [ ] Unit tests passed
- [ ] Integration tests passed
- [ ] Staging deployment successful
- [ ] Load testing (if applicable)
- [ ] Security scan (if applicable)

**Test Results**: [Link to test report or summary]

---

## 5. Rollback Plan

**Rollback Available**: [Yes / No / Partial]

**Rollback Procedure**:

```bash
# Step 1: [command]
# Step 2: [command]
# Estimated rollback time: <X minutes>
```
````

**Rollback Tested**: [Yes / No]

---

## 6. Implementation Plan

**Implementation Steps**:

1. [Step 1] (Duration: X min, Owner: @person)
2. [Step 2] (Duration: X min, Owner: @person)
3. [Step 3] (Duration: X min, Owner: @person)

**Total Estimated Duration**: [X minutes]

**Implementation Window**:

- Start: 2025-01-20 22:00 UTC
- End: 2025-01-20 23:00 UTC (max)

**Communication Plan**:

- [ ] Notify #engineering (L-2 days)
- [ ] Update status page (L-1 hour)
- [ ] Notify Customer Support (L-1 hour)
- [ ] Post-implementation update (#engineering)

---

## 7. Success Criteria

**How will we know this succeeded?**

- [ ] Health checks passing
- [ ] Error rate <0.5%
- [ ] Latency P95 <300ms
- [ ] No user complaints (first 2 hours)

**Monitoring**:

- Dashboard: [Link]
- Alerts: [Which alerts to watch]

---

## 8. Dependencies

**Depends On**:

- [ ] [Other change CHG-XXX must complete first]
- [ ] [External vendor notification]

**Blocks**:

- [ ] [This change blocks CHG-YYY]

---

## 9. Approvals

**Required Approvals**:

- [ ] DevOps Lead: ******\_\_\_\_******
- [ ] Tech Lead: ******\_\_\_\_******
- [ ] Security (if applicable): ******\_\_\_\_******
- [ ] CAB Review: ******\_\_\_\_******

**CAB Decision**: [Approved / Approved with Conditions / Rejected / Deferred]
**CAB Notes**: [Feedback from CAB]

---

## 10. Post-Implementation

**Implementation Status**: [Successful / Failed / Rolled Back]
**Actual Duration**: [X minutes]
**Issues Encountered**: [List any issues]
**Lessons Learned**: [What went well, what didn't]

**Post-Mortem Required**: [Yes / No]

```

---

## 📅 Change Windows

### Preferred Change Windows

**Option 1: Maintenance Window** (Recommended for High Risk)
- **When**: Sunday 02:00-06:00 UTC (lowest traffic)
- **Notification**: Users notified 7 days in advance
- **Use for**: Major changes, database migrations, infrastructure

**Option 2: Business Hours Deployment** (Low Risk only)
- **When**: Tuesday-Thursday 10:00-16:00 local time
- **Notification**: Internal teams only
- **Use for**: Standard application deployments (with rollback)

**Option 3: Late Evening** (Medium Risk)
- **When**: Weekdays 20:00-23:00 UTC
- **Notification**: Internal + status page
- **Use for**: Backend changes, API updates

---

### Deployment Freeze Periods

**No deployments during** (except emergency):

1. **Fridays after 16:00** (no support over weekend)
2. **Public Holidays** (December 24-26, December 31-January 1, etc.)
3. **High Traffic Events** (Black Friday, Cyber Monday for retail)
4. **Major Company Events** (product launches, board meetings)

---

## 🚀 Implementation Phase

### Pre-Implementation Checklist

**L-7 days**:
- [ ] Change request submitted
- [ ] CAB review scheduled

**L-3 days**:
- [ ] CAB approval received
- [ ] Implementation plan finalized
- [ ] Rollback plan tested in Staging
- [ ] Notify stakeholders (#engineering, Customer Support)

**L-1 day**:
- [ ] Confirm change window availability
- [ ] Review implementation steps with team
- [ ] Pre-position rollback commands
- [ ] Update status page (if user-facing)

**L-1 hour**:
- [ ] Final go/no-go decision
- [ ] War room channel created (for High Risk changes)
- [ ] Monitoring dashboards open
- [ ] On-call engineer on standby

---

### During Implementation

**Communication**:
- Post start time en #engineering
- Update every 15-30 min for High Risk changes
- Post completion en #engineering

**Monitoring**:
- Watch error rates, latency, health checks
- Compare metrics pre-change vs post-change

**Decision Points**:
- If error rate >5% → Pause, investigate
- If error rate >10% → Rollback immediately
- If unexpected issues → Rollback, don't debug in production

---

### Post-Implementation Checklist

**Immediate** (T+0):
- [ ] Verify success criteria met
- [ ] Post completion update (#engineering, status page)
- [ ] Monitor for 2 hours (stay on call)

**T+24 hours**:
- [ ] Review metrics (error rates, latency, user complaints)
- [ ] Close change ticket
- [ ] Update change log

**T+48 hours** (if High/Critical Risk):
- [ ] Post-implementation review meeting
- [ ] Document lessons learned
- [ ] Update runbooks if needed

---

## 📊 Change Metrics

### Metric #1: Change Success Rate

**Definition**: % of changes que NO requieren rollback

**Target**: >90%

**How to Improve**:
- Better testing en Staging
- More thorough risk assessment
- Rollback drills

---

### Metric #2: Change Lead Time

**Definition**: Time from change request → implementation

**Target**:
- Standard Change: <5 días
- Emergency Change: <4 horas

---

### Metric #3: CAB Approval Rate

**Definition**: % of changes approved on first submission

**Target**: >70%

**If low**: Change requests need more details/better preparation

---

### Metric #4: Emergency Change Frequency

**Definition**: Number of emergency changes per month

**Target**: <3/month

**If high**: Indicates poor planning or quality issues

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | Requestor | DevOps | Tech Lead | CAB | Manager |
| --------------------------------- | --------- | ------ | --------- | --- | ------- |
| Submit change request             | R/A       | C      | C         | I   | I       |
| Risk assessment                   | R         | C      | C         | A   | I       |
| CAB review                        | C         | R      | R         | A   | I       |
| Approve/Reject                    | I         | C      | C         | R/A | C       |
| Schedule change                   | R         | C/A    | C         | I   | I       |
| Implement change                  | R/A       | C      | C         | I   | I       |
| Monitor post-implementation       | R         | C/A    | C         | I   | I       |
| Rollback (if needed)              | R         | C/A    | C         | I   | I       |
| Document lessons learned          | R/A       | C      | C         | I   | I       |

---

## 🚀 Implementation Roadmap

### Sprint 0: Define Process

- [ ] Document change types (Standard, Emergency, Pre-Approved, Major)
- [ ] Define risk matrix
- [ ] Create RFC template
- [ ] Identify CAB members

---

### Sprint 1-2: CAB Setup

- [ ] Schedule weekly CAB meetings
- [ ] Train team on change process
- [ ] Create change request form (Jira Service Desk)
- [ ] Pilot with 5 changes

---

### Sprint 3-4: Refinement

- [ ] Review first month of changes
- [ ] Optimize RFC template (reduce bureaucracy)
- [ ] Identify pre-approved changes
- [ ] Document emergency change process

---

### Sprint 5+: Automation

- [ ] Automate change notifications (Slack bots)
- [ ] Dashboard for change calendar
- [ ] Metrics tracking (success rate, lead time)

---

## ✅ Success Criteria

### Mes 1
- ✅ CAB meetings weekly
- ✅ All Standard changes go through CAB
- ✅ RFC template in use

### Mes 2-3
- ✅ Change success rate >85%
- ✅ Change lead time <7 días
- ✅ 10+ pre-approved changes identified

### Mes 4+
- ✅ Change success rate >90%
- ✅ Emergency changes <3/month
- ✅ CAB approval rate >70%

---

## 🔗 Links Relacionados

- [Incident Management](./incident-management.md) - Emergency change process
- [Deployment Procedures](./deployment-procedures.md) - Implementation details
- [CI/CD Pipeline](./cicd-pipeline.md) - Automated deployment

---

## 📚 Antipatterns (Evitar)

### ❌ Antipattern #1: Change Process Too Heavy

**Problema**: Requiere 20-page RFC para cambiar 1 línea de config

**Por qué es malo**: Teams bypass process, change management becomes irrelevant

**Solución**: Right-size process to risk. Pre-approve low-risk changes.

---

### ❌ Antipattern #2: Rubber-Stamp CAB

**Problema**: CAB approves todo sin review real ("Just approve it, we're busy")

**Por qué es malo**: Process becomes theater, no risk mitigation

**Solución**: CAB debe challenge requests, ask hard questions, reject si no hay info

---

### ❌ Antipattern #3: No Rollback Plan

**Problema**: "We'll figure out rollback if something goes wrong"

**Por qué es malo**: Panic during incident, long MTTR

**Solución**: Mandatory rollback plan for all changes, tested en Staging

---

### ❌ Antipattern #4: Everything is Emergency

**Problema**: "This is urgent! Emergency change needed!" (para feature no crítico)

**Por qué es malo**: Erodes trust, real emergencies ignored

**Solución**: DevOps Lead must approve emergency changes, challenge urgency

---

**Versión**: 1.0
**Última Actualización**: 2025-12-06
**Owner**: DevOps Lead
**Review Cycle**: Trimestral
```
