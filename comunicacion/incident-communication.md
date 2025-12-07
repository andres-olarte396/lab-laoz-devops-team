# Incident Communication - Comunicación Durante Incidentes Críticos

## 📋 Resumen Ejecutivo

**Problema**: Incident SEV-1 → Caos total. Nadie sabe qué está pasando, clientes se enteran por Twitter, C-suite pregunta "¿Por qué no nos avisaron?", equipo debugging sin tiempo para comunicar.

**Solución**: **Incident communication process** con roles claros (Incident Commander, Communication Lead), templates, timeline definido, y notificaciones automáticas.

**Beneficio**:
- Comunicación clara durante crisis (todos saben qué está pasando)
- Stakeholders informados (C-suite, clientes, sales, support)
- Menos interrupciones al equipo técnico (Communication Lead maneja updates)
- Transparencia con clientes (status page, emails)
- Post-mortem completo (toda la comunicación documentada)

---

## 🎯 Roles en Incident Communication

### Incident Commander (IC)

**Quién**: On-call SRE/DevOps Lead (rotación semanal)

**Responsibilities**:
- Declarar incident y severidad (SEV-1, SEV-2, SEV-3)
- Crear incident channel (#incident-YYYY-MM-DD-description)
- Coordinar respuesta técnica (assign tasks, triage)
- Tomar decisiones (rollback, failover, escalation)
- Declarar "incident resolved"
- Schedule post-mortem (dentro de 48 horas)

**NOT responsible for**:
- ❌ Comunicar a stakeholders (Communication Lead hace esto)
- ❌ Fix técnico (delegue a developers/DevOps)
- ❌ Escribir post-mortem (IC lidera, pero equipo colabora)

---

### Communication Lead (CL)

**Quién**: Engineering Manager o designado (backup: Product Manager)

**Responsibilities**:
- Postear updates en canales internos (#engineering, #incidents)
- Notificar a stakeholders (CTO, executives)
- Coordinar con Customer Success (para comunicación a clientes)
- Postear en status page (si clientes afectados)
- Enviar emails a clientes (con CS)
- Documentar timeline de comunicación
- Preparar FAQ para support team

**NOT responsible for**:
- ❌ Debugging técnico (IC maneja esto)
- ❌ Tomar decisiones técnicas (IC decide)

---

### Scribe

**Quién**: Developer o QA (no involucrado en el fix)

**Responsibilities**:
- Documentar timeline del incident (quién hizo qué, cuándo)
- Anotar decisiones y rationale
- Capturar logs, screenshots, comandos ejecutados
- Preparar material para post-mortem

**Tools**:
- Google Doc compartido (collaborative)
- Slack threads (auto-documentation)
- Screenshot tool (Snagit, Greenshot)

---

## 🚨 Incident Communication Process (by Severity)

### SEV-1 (Critical - Outage Total)

**Definition**: 
- Production completamente down
- Revenue-impacting (no se pueden procesar pagos)
- Data breach (acceso no autorizado a customer data)
- Security incident crítico

**Example**: Login system down, checkout broken, database corrupted

---

#### Timeline SEV-1

**T+0 (Detection)**

IC Actions:
1. Declare SEV-1 en #incidents
2. Create dedicated channel: `#incident-2025-12-07-login-outage`
3. Invite core team:
   - DevOps/SREs (on-call + backup)
   - Tech Leads (affected services)
   - Engineering Manager (Communication Lead)
   - Product Manager (business context)
   - QA (for testing fixes)

**Template** (IC en #incidents):
```markdown
🚨 **SEV-1 INCIDENT DECLARED**

**Incident**: Login system completely down
**Started**: 2025-12-07 14:30 UTC
**Impact**: 100% of users cannot log in
**Incident Channel**: #incident-2025-12-07-login-outage
**Incident Commander**: @bob-sre

All hands on deck. Join #incident-2025-12-07-login-outage for coordination.
```

---

**T+5 min**

CL Actions:
1. Post in #engineering (all engineering team)
2. Notify CTO via Slack DM + Phone call
3. Create Google Doc for timeline (share with IC)

**Template** (CL en #engineering):
```markdown
🚨 **P0 INCIDENT IN PROGRESS**

**What**: Login system is down
**Impact**: All users cannot log in (100% outage)
**Started**: 14:30 UTC
**Status**: Investigating root cause
**IC**: @bob-sre
**War Room**: #incident-2025-12-07-login-outage

**Next Update**: In 15 minutes (14:50 UTC)

Do NOT reach out to IC directly. Updates will be posted here every 15 min.
```

---

**T+15 min**

IC Actions (in incident channel):
- Post investigation update (what we know so far)

CL Actions:
1. Post update in #engineering
2. Email to exec team (CTO, CEO, COO)
3. Alert Customer Success Lead (prepare for customer emails)

**Email Template** (to Exec Team):
```
Subject: P0 Incident Update - Login System Down

Hi Team,

We are currently experiencing a P0 incident affecting our login system.

STATUS: Investigating
IMPACT: 100% of users cannot log in
STARTED: 14:30 UTC (15 minutes ago)
ETA: TBD (will update in 15 minutes)

ACTIONS TAKEN:
- Incident Commander assigned (@bob-sre)
- War room created (#incident-2025-12-07-login-outage)
- DevOps team investigating root cause

NEXT UPDATE: 14:50 UTC

War room: [Link to Slack channel]

- Communication Lead
```

---

**T+30 min**

IC Actions:
- Continue investigation
- Post update (findings so far)

CL Actions:
1. Post update in #engineering
2. Update exec team (email or Slack)
3. **Coordinate with Customer Success**: Prepare status page update

**Status Page Update** (via CS):
```
INVESTIGATING

We are currently investigating an issue affecting login functionality. 
Users may be unable to log in at this time. 

We are working to resolve this as quickly as possible and will provide 
updates every 15 minutes.

Last update: 15:00 UTC
Next update: 15:15 UTC
```

4. **Prepare customer email** (draft, don't send yet - wait for IC approval)

**Customer Email Template** (Draft):
```
Subject: [Action Required] Login Issue - We're Working on It

Dear Customer,

We are currently experiencing a technical issue affecting our login system. 
You may be unable to log in at this time.

WHAT'S HAPPENING:
We detected an issue with our login service at 14:30 UTC today. Our 
engineering team is actively working to resolve this.

IMPACT:
Login functionality is currently unavailable. If you are already logged in, 
you can continue using the application normally.

WHAT WE'RE DOING:
- Our team identified the root cause
- We are deploying a fix
- We expect to restore service within the next 30 minutes

WHAT YOU SHOULD DO:
- If you need to log in, please wait 30 minutes and try again
- If you are already logged in, you can continue working normally
- No action is required from you

We sincerely apologize for the inconvenience. We will send another update 
in 15 minutes.

For real-time updates, visit our status page: https://status.company.com

Thank you for your patience.

Best regards,
[Company Name] Team
```

---

**T+45 min (Mitigation in Progress)**

IC Actions:
- Deploy fix or rollback
- Monitor stability

CL Actions:
1. Update #engineering ("Fix deployed, monitoring")
2. Update exec team
3. **IF fix is working**: Approve customer email (send via CS)
4. Update status page

---

**T+60 min (Resolved)**

IC Actions:
- Declare "incident resolved" in incident channel
- Continue monitoring for 30 min (ensure no regression)

CL Actions:
1. Post all-clear in #engineering
2. Email exec team (incident resolved)
3. Update status page ("Resolved")
4. Send customer email (all-clear)
5. Prepare post-mortem schedule

**All-Clear Post** (#engineering):
```markdown
✅ **INCIDENT RESOLVED**

**Incident**: Login system down
**Duration**: 1 hour 15 minutes (14:30 - 15:45 UTC)
**Impact**: 100% of users unable to log in
**Resolution**: Deployed fix + rollback to stable version

**What happened**:
[Brief summary - full post-mortem coming in 48 hours]

**Monitoring**:
We are continuing to monitor the system for the next 30 minutes.

**Post-Mortem**:
Scheduled for Friday 10am. Link: [Calendar invite]

Thanks to everyone who responded quickly. Great teamwork! 🙌

IC: @bob-sre
```

**Customer Email (All-Clear)**:
```
Subject: [Resolved] Login Issue Fixed

Dear Customer,

Good news! We have resolved the login issue that affected our service 
from 14:30 to 15:45 UTC today.

RESOLUTION:
Our team identified and fixed the root cause. Login functionality is 
now fully restored.

WHAT HAPPENED:
[Brief, non-technical explanation]
We deployed a code change that inadvertently broke login functionality. 
We rolled back the change and deployed a fix.

IMPACT:
The issue lasted 1 hour and 15 minutes. Users were unable to log in 
during this time. If you were already logged in, you were not affected.

WHAT WE'RE DOING TO PREVENT THIS:
- We are conducting a full post-mortem analysis
- We are improving our testing process to catch similar issues
- We are implementing additional monitoring

We sincerely apologize for the disruption. We take reliability seriously 
and are committed to learning from this incident.

If you have any questions, please contact support@company.com

Thank you for your patience and understanding.

Best regards,
[Company Name] Team
```

---

**Post-Incident (Within 48 hours)**

IC + Team Actions:
1. Complete post-mortem doc (timeline, root cause, action items)
2. Post-mortem meeting (entire engineering team)
3. Share post-mortem externally (blog post if major incident)

CL Actions:
1. Compile all communication (emails, Slack posts, status page updates)
2. Document lessons learned (what worked, what didn't)
3. Update communication templates if needed

---

### SEV-2 (High - Degradation Parcial)

**Definition**:
- Partial functionality broken (not complete outage)
- Significant user impact (>20% users affected)
- Workaround available
- DDoS attack (mitigated but ongoing)

**Example**: Search is slow, mobile app crashing for iOS users, payment processing delayed

---

#### Timeline SEV-2

**Key Differences from SEV-1**:
- Updates every **1 hour** (not 15 min)
- No dedicated incident channel (use #devops or #incidents)
- Status page update **recommended** (not mandatory)
- Customer email **optional** (only if >50% users affected)
- CTO notification **optional** (Engineering Manager decides)

**T+0**: IC declares SEV-2 in #incidents (thread)
**T+15 min**: CL posts in #engineering
**T+30 min**: CL notifies Engineering Manager
**T+1 hour**: CL posts update in #engineering
**T+Resolution**: CL posts all-clear

**Template** (IC en #incidents):
```markdown
⚠️ **SEV-2 INCIDENT**

**Issue**: Search functionality is slow
**Started**: 15:30 UTC
**Impact**: ~30% of users experiencing slow search (>5 sec)
**IC**: @alice-devops
**Thread**: Use this thread for updates

Investigating. Update in 1 hour.
```

---

### SEV-3 (Medium - Minor Impact)

**Definition**:
- Minor functionality broken
- <10% users affected
- Workaround exists
- No revenue impact

**Example**: Dark mode toggle not working, export to CSV failing for some users

---

#### Timeline SEV-3

**Key Differences from SEV-2**:
- Updates every **4 hours** (or when status changes)
- Use #devops (no #incidents post needed)
- No status page update
- No customer email
- No executive notification

**T+0**: IC posts in #devops (thread)
**T+Resolution**: IC posts fix deployed

---

## 📊 Communication Channels by Incident Type

| Stakeholder | SEV-1 | SEV-2 | SEV-3 |
|-------------|-------|-------|-------|
| **#incidents** | ✅ Immediate | ✅ Immediate | ❌ |
| **#engineering** | ✅ Every 15 min | ✅ Every 1 hour | ❌ |
| **#devops** | ✅ (dedicated channel) | ✅ (thread) | ✅ (thread) |
| **CTO** | ✅ Phone + Slack (5 min) | ⚠️ Optional (30 min) | ❌ |
| **Exec Team** | ✅ Email (15 min) | ⚠️ Optional (1 hour) | ❌ |
| **Customer Success** | ✅ Immediate (prepare emails) | ⚠️ Optional | ❌ |
| **Status Page** | ✅ Required (30 min) | ⚠️ Recommended | ❌ |
| **Customer Email** | ✅ Required (30-60 min) | ⚠️ If >50% affected | ❌ |
| **Public Blog** | ⚠️ If major (post-incident) | ❌ | ❌ |

---

## 📝 Communication Templates

### Incident Declaration

**SEV-1** (in #incidents):
```markdown
🚨 **SEV-1 INCIDENT DECLARED**

**Incident**: [Brief description]
**Started**: YYYY-MM-DD HH:MM UTC
**Impact**: [% users affected, what's broken]
**Incident Channel**: #incident-YYYY-MM-DD-description
**IC**: @username

All hands on deck. Join incident channel for coordination.
```

**SEV-2** (in #incidents):
```markdown
⚠️ **SEV-2 INCIDENT**

**Issue**: [Brief description]
**Started**: YYYY-MM-DD HH:MM UTC
**Impact**: [% users affected]
**IC**: @username
**Thread**: Use this thread for updates

Investigating. Update in 1 hour.
```

---

### Internal Updates

**#engineering Update** (every 15 min for SEV-1):
```markdown
🚨 **P0 UPDATE** - T+[X] minutes

**Status**: Investigating | Mitigating | Resolved
**What we know**: [Brief update]
**What we're doing**: [Actions being taken]
**ETA**: [If known] or TBD

**Next update**: In 15 minutes

War room: #incident-YYYY-MM-DD-description
```

---

### Executive Communication

**Email to CTO/Exec Team**:
```
Subject: P0 Incident Update - [Brief Description]

Hi Team,

STATUS: [Investigating | Mitigating | Resolved]
IMPACT: [% users, what's broken]
STARTED: [Time] ([Duration] ago)
ETA: [If known]

WHAT HAPPENED:
[Brief explanation]

ACTIONS TAKEN:
- [Action 1]
- [Action 2]

NEXT UPDATE: [Time]

War room: [Slack link]

- Communication Lead
```

---

### Customer Communication

**Status Page Post**:
```
INVESTIGATING

We are currently investigating an issue affecting [feature/service]. 

[Brief description of impact]

We are working to resolve this as quickly as possible and will provide 
updates every [15/30/60] minutes.

Last update: [Time] UTC
Next update: [Time] UTC
```

**Customer Email** (during incident):
```
Subject: [Action Required] Service Issue - We're Working on It

Dear Customer,

We are currently experiencing a technical issue affecting [feature].

WHAT'S HAPPENING:
[Brief, non-technical explanation]

IMPACT:
[What customers can and cannot do]

WHAT WE'RE DOING:
[Actions being taken]

WHAT YOU SHOULD DO:
[Recommended workaround or actions]

We will send another update in [X] minutes.

For real-time updates: https://status.company.com

Thank you for your patience.

Best regards,
[Company Name] Team
```

---

### Post-Mortem Communication

**Internal** (post-mortem meeting invite):
```
Subject: Post-Mortem: [Incident Name]

Hi Team,

We are scheduling a post-mortem for the incident that occurred on 
[Date].

WHEN: [Date/Time]
WHERE: [Zoom link or meeting room]
DURATION: 1 hour

AGENDA:
1. Timeline review (10 min)
2. Root cause analysis (20 min)
3. What went well (10 min)
4. What went wrong (10 min)
5. Action items (10 min)

POST-MORTEM DOC: [Google Doc link]

Please review the doc before the meeting.

This is a blameless post-mortem. Our goal is to learn and improve.

See you there!
```

**External** (blog post - if major incident):
```
Title: Incident Report: [Brief Description] on [Date]

On [Date], from [Start Time] to [End Time] UTC ([Duration]), our users 
were unable to [functionality] due to [brief cause].

We sincerely apologize for the disruption.

WHAT HAPPENED
[Timeline of events]

ROOT CAUSE
[Technical but understandable explanation]

WHAT WE'RE DOING TO PREVENT THIS
- [Action item 1]
- [Action item 2]
- [Action item 3]

CONCLUSION
We take reliability seriously and are committed to learning from this 
incident. Thank you for your patience and understanding.

For questions: support@company.com

— The Engineering Team
```

---

## 🎭 RACI: Incident Communication

| Actividad | IC | CL | Scribe | CTO | CS | DevOps |
|-----------|----|----|--------|-----|----|----|
| **Declare incident** | A/R | I | I | I | I | C |
| **Create incident channel** | A/R | I | I | I | I | C |
| **Post in #engineering** | I | A/R | I | I | I | I |
| **Notify CTO (SEV-1)** | I | A/R | I | C | I | I |
| **Email exec team** | I | A/R | I | C | I | I |
| **Status page update** | I | A | I | I | R | I |
| **Customer email** | I | A | I | I | R | I |
| **Document timeline** | C | C | A/R | I | I | C |
| **Declare resolved** | A/R | I | I | I | I | C |
| **Schedule post-mortem** | A/R | C | C | I | I | C |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 📊 Incident Communication Metrics

### Metrics to Track

| Metric | SEV-1 Target | SEV-2 Target |
|--------|--------------|--------------|
| **Time to first internal update** | <5 min | <15 min |
| **Time to CTO notification** | <5 min | <30 min |
| **Time to status page update** | <30 min | <1 hour |
| **Time to customer email** | <60 min | N/A |
| **Update frequency** | Every 15 min | Every 1 hour |
| **Post-mortem completion** | <48 hours | <1 week |

---

## ✅ Success Criteria

### Mes 1
- ✅ IC + CL roles assigned (on-call rotation)
- ✅ Templates created y comunicados al equipo
- ✅ First incident manejado con nuevo process

### Mes 2-3
- ✅ Time to first update <10 min (avg SEV-1)
- ✅ CTO satisfecho con incident communication
- ✅ Customer satisfaction post-incident >3.5/5

### Mes 4+
- ✅ All SEV-1 incidents con communication completa (status page, emails)
- ✅ Post-mortem completion 100% (<48 hours)
- ✅ Zero "Why wasn't I notified?" complaints

---

## 🔗 Links Relacionados

- [Channel Ownership](./channel-ownership.md) - Canales #incidents, #devops
- [Escalation Matrix](./escalation-matrix.md) - Cuándo escalar incidents
- [Post-Mortem Process](../procesos/post-mortem.md) - Análisis post-incidente
- [Incident Management](../procesos/incident-management.md) - Proceso técnico de incident response

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager (Communication Lead)  
**Review Cycle**: Post cada SEV-1 incident (lessons learned)
