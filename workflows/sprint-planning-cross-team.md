# Sprint Planning Cross-Team - Planificación Multi-Equipo

> **Owner**: Engineering Manager + Product Manager  
> **Última actualización**: 7 de diciembre de 2025  
> **Próxima revisión**: 7 de marzo de 2026

---

## 📋 Resumen Ejecutivo

Este documento define el proceso de **Sprint Planning cuando múltiples equipos deben coordinarse** para entregar features que cruzan boundaries (ej: Frontend + Backend + Data Engineering + DevOps).

**Objetivo**: Alinear capacidad, identificar dependencias críticas, y crear un plan de sprint sincronizado que evite bloqueos.

**Frecuencia**: Cada 2 semanas (inicio de sprint)  
**Duración**: 3 horas total (2h Planning + 1h Cross-Team Sync)

---

## 🎯 Objetivos

- **Visibilidad**: Todos los equipos conocen qué están construyendo otros equipos
- **Dependencias**: Identificar y mitigar dependencias críticas antes que se conviertan en bloqueos
- **Capacidad**: Calcular capacity realista considerando vacaciones, on-call, tech debt
- **Priorización**: Alinear prioridades cross-team (evitar equipos trabajando en features incompatibles)
- **Commitment**: Cada equipo hace commitment realista basado en velocity histórica

---

## 🔄 Workflow Completo

```
┌────────────────┐    ┌────────────────┐    ┌────────────────┐    ┌────────────────┐
│  PRE-PLANNING  │───▶│  TEAM PLANNING │───▶│  CROSS-TEAM    │───▶│   REFINEMENT   │
│                │    │                │    │     SYNC       │    │                │
│  Capacity calc │    │  Story points  │    │  Dependencies  │    │  Adjust plans  │
│  (día antes)   │    │  (90min)       │    │  (60min)       │    │  (30min)       │
└────────────────┘    └────────────────┘    └────────────────┘    └────────────────┘
```

---

## 🗓️ Timeline del Sprint Planning Day

**Sprint Planning ocurre el Lunes Week 1** (asumiendo sprints de 2 semanas)

### Viernes Previo (Día -3): Pre-Planning

**09:00 - 10:00**: Engineering Managers calculan **capacity** por equipo  
**10:00 - 11:00**: Product Managers refinan **top priorities** para próximo sprint  
**11:00 - 12:00**: Tech Leads identifican **technical dependencies** preliminares

### Lunes (Sprint Planning Day)

**09:00 - 10:30**: **Team Planning (Individual)** - Cada equipo planea en paralelo  
**10:30 - 10:45**: ☕ Break  
**10:45 - 11:45**: **Cross-Team Sync** - Todos los equipos juntos  
**11:45 - 12:15**: **Refinement & Adjustments** - Equipos ajustan sus planes  
**12:15 - 12:30**: **Sprint Goal Announcement** - EM/PM comunican sprint goal final

---

## 1️⃣ Fase 1: Pre-Planning (Viernes Previo)

**Objetivo**: Preparar inputs necesarios para Planning Day.

### Paso 1.1: Capacity Calculation

**Responsable**: Engineering Manager (cada equipo)  
**Duración**: 1h  
**Entregable**: Capacity spreadsheet por equipo

**Fórmula de Capacity**:
```
Capacity (story points) = 
  (Team Size × Days Available × Velocity per Person) - Overhead

Donde:
- Team Size = Developers en el equipo
- Days Available = 10 días (2 semanas) - Vacaciones - Feriados
- Velocity per Person = Historical velocity / team size (ej: 40 SP / 5 devs = 8 SP/dev)
- Overhead = On-call (20%), Meetings (15%), Tech Debt (10%)
```

**Template - Capacity Calculation**:

| Equipo | Team Size | Days Available | Velocity/Person | Overhead | **Total Capacity** |
|--------|-----------|----------------|-----------------|----------|--------------------|
| **Frontend** | 5 devs | 50 person-days | 8 SP/dev | -15 SP | **25 SP** |
| **Backend** | 6 devs | 55 person-days | 7 SP/dev | -18 SP | **24 SP** |
| **Data Eng** | 3 devs | 30 person-days | 6 SP/dev | -8 SP | **10 SP** |
| **DevOps** | 2 devs | 20 person-days | 5 SP/dev | -5 SP | **5 SP** |
| **QA** | 4 devs | 40 person-days | 6 SP/dev | -10 SP | **14 SP** |

**Ajustes de Overhead**:
- **On-call rotation**: -20% capacity (1 dev dedicado a incidents)
- **Meetings**: -15% capacity (daily standups, 1-on-1s, retro, planning)
- **Tech Debt**: -10% capacity (bug fixes, refactoring)
- **Vacaciones/Feriados**: Restar días completos

**Example - Backend Team**:
```
Team Size: 6 developers
Sprint: Dec 9 - Dec 20 (2 weeks = 10 working days)

Days Available:
- Total: 6 devs × 10 days = 60 person-days
- Vacations: 1 dev on PTO (Dec 16-20) = -5 days
- Adjusted: 55 person-days

Velocity per Person:
- Last 3 sprints: 42 SP, 38 SP, 40 SP → Avg 40 SP
- Per person: 40 SP / 6 devs = 6.67 SP/dev/sprint

Overhead:
- On-call: 1 dev @ 50% capacity = -3 SP
- Meetings: 15% × 40 SP = -6 SP
- Tech Debt: 10% × 40 SP = -4 SP
- Bug fixes: -5 SP (backlog de production bugs)
- Total overhead: -18 SP

Final Capacity: 40 SP - 18 SP = 22 SP
```

**Output**: Shared spreadsheet con capacity de todos los equipos

---

### Paso 1.2: Priority Refinement

**Responsable**: Product Manager (cada producto)  
**Duración**: 1h  
**Entregable**: Priorized backlog top 10 items

**Actividades**:
1. **Review Roadmap**: Confirmar que features planeadas siguen siendo priorities
2. **Stakeholder Input**: Confirmar con executives/customers si hay cambios
3. **Dependencies Check**: Verificar que features priorizadas no están bloqueadas
4. **Estimation Review**: Confirmar que top items tienen story points estimados

**Template - Priority List**:

| Rank | Feature | Business Value | Team(s) | Estimate | Dependencies |
|------|---------|----------------|---------|----------|--------------|
| **1** | Payment Gateway v2 | $500K ARR | Backend, Frontend | 21 SP | None |
| **2** | Analytics Dashboard | Customer retention | Frontend, Data Eng | 13 SP | Data pipeline (ready) |
| **3** | API Rate Limiting | Prevent abuse | Backend, DevOps | 8 SP | None |
| **4** | Mobile Onboarding | 30% conversion | Frontend (mobile) | 13 SP | Design (in progress) |
| **5** | Database Sharding | Scale to 10M users | Backend, DevOps, Data | 34 SP | Architecture spike (done) |

**RICE Scoring** (para priorización):
```
RICE Score = (Reach × Impact × Confidence) / Effort

Ejemplo:
- Reach: 10,000 users affected
- Impact: 3 (massive impact on scale 0-3)
- Confidence: 80%
- Effort: 21 SP

RICE = (10,000 × 3 × 0.8) / 21 = 1,142
```

Ordenar features por RICE score descendente.

---

### Paso 1.3: Technical Dependencies Mapping

**Responsable**: Tech Lead (cada equipo)  
**Duración**: 1h  
**Entregable**: Dependency matrix

**Actividades**:
1. Review top 10 features del PM
2. Identificar dependencies técnicas entre equipos
3. Clasificar dependencies: **Critical** (blocker), **Important** (nice-to-have), **Optional**

**Template - Dependency Matrix**:

| Feature | Team A (Needs) | Team B (Provides) | Type | Due Date | Status |
|---------|----------------|-------------------|------|----------|--------|
| **Payment Gateway v2** | Frontend | Backend: POST /api/payments v2 | 🔴 Critical | Sprint Week 1 | Not Started |
| **Payment Gateway v2** | Backend | DevOps: Stripe webhook config | 🔴 Critical | Sprint Week 1 | In Progress |
| **Analytics Dashboard** | Frontend | Data Eng: Analytics API | 🔴 Critical | Sprint Week 1 | ✅ Done |
| **Database Sharding** | Backend | DevOps: New DB cluster | 🔴 Critical | Sprint Week 1 | Not Started |
| **Database Sharding** | Backend | Data Eng: Migration scripts | 🟡 Important | Sprint Week 2 | Not Started |

**Dependency Types**:
- 🔴 **Critical**: Blocker - Work cannot start without this
- 🟡 **Important**: Needed for completion, but work can start
- 🟢 **Optional**: Nice-to-have, not blocking

**Red Flags** (escalar a EM/PM):
- ❌ Critical dependency "Not Started" y due date Week 1
- ❌ Circular dependency (Team A espera Team B, Team B espera Team A)
- ❌ External dependency fuera de nuestro control (third-party API)

---

## 2️⃣ Fase 2: Team Planning (Individual)

**Timing**: Lunes 09:00 - 10:30 (90min)  
**Formato**: Cada equipo planea **en paralelo** en salas separadas

### Paso 2.1: Team Sprint Planning

**Responsable**: Engineering Manager + Product Manager (del equipo)  
**Duración**: 90min  
**Entregable**: Sprint backlog con commitment

**Agenda (90min)**:
1. **Sprint Goal** (10min): PM explica objetivo del sprint
2. **Capacity Review** (5min): EM presenta capacity calculation
3. **Story Selection** (45min): Equipo selecciona stories del backlog
4. **Story Breakdown** (20min): Break down large stories en tasks
5. **Commitment** (10min): Equipo hace commitment final

**Story Selection Process**:
```
Backlog Priorizado (por PM):
┌─────────────────────────────────┐
│ 1. Payment Gateway v2 (21 SP)   │ ← High priority
│ 2. Analytics Dashboard (13 SP)  │
│ 3. API Rate Limiting (8 SP)     │
│ 4. Mobile Onboarding (13 SP)    │
│ 5. Database Sharding (34 SP)    │ ← Too big for 1 sprint
└─────────────────────────────────┘

Team Capacity: 25 SP

Selected Stories:
✅ Payment Gateway v2 (21 SP)
✅ API Rate Limiting (8 SP)
❌ Analytics Dashboard (13 SP) - No capacity
❌ Database Sharding (34 SP) - Too big, needs breakdown

Total Commitment: 21 + 8 = 29 SP
→ OVERCOMMITTED by 4 SP ⚠️

Action: Negotiate con PM - ¿podemos bajar scope de Payment Gateway?
```

**Commitment Guidelines**:
- ✅ Commit at **80-90% capacity** (buffer para unknowns)
- ❌ No commit >100% capacity (recipe for burnout)
- ✅ Include tech debt (~10% capacity)
- ✅ Include bug fixes de production

**Template - Team Sprint Backlog**:

| Story | Story Points | Assignee | Dependencies | Status |
|-------|--------------|----------|--------------|--------|
| **Payment Gateway v2** | | | | |
| - Backend: Stripe integration | 8 SP | @john | None | Not Started |
| - Frontend: New checkout flow | 8 SP | @sarah | Backend API (Week 1) | Not Started |
| - QA: E2E tests | 5 SP | @mike | Frontend (Week 2) | Not Started |
| **API Rate Limiting** | | | | |
| - Backend: Rate limiter middleware | 5 SP | @jane | None | Not Started |
| - DevOps: Redis cache setup | 3 SP | @david | None | Not Started |

**Output**: Cada equipo tiene su sprint backlog con commitment

---

## 3️⃣ Fase 3: Cross-Team Sync (Todos Juntos)

**Timing**: Lunes 10:45 - 11:45 (60min)  
**Formato**: Todos los equipos en 1 sala (o Zoom)

### Paso 3.1: Sprint Showcase (30min)

**Responsable**: Engineering Manager (cada equipo presenta 5min)  
**Duración**: 30min (6 equipos × 5min)  
**Entregable**: Shared understanding de todos los commitments

**Template - Team Showcase (5min)**:
```markdown
**Team**: Backend
**Sprint Goal**: Ship Payment Gateway v2 + API Rate Limiting
**Commitment**: 29 SP (capacity: 25 SP) ⚠️ Overcommitted

**Key Features**:
1. Payment Gateway v2 (21 SP)
   - Stripe integration (Week 1)
   - Webhook handling (Week 1)
   - Refund API (Week 2)

2. API Rate Limiting (8 SP)
   - Rate limiter middleware (Week 1)
   - Redis cache (Week 1)

**Dependencies Needed**:
- DevOps: Stripe webhook config (Week 1) 🔴 Critical
- DevOps: Redis setup (Week 1) 🔴 Critical

**Dependencies We Provide**:
- Frontend: POST /api/payments/v2 endpoint (Week 1 Wed)
- Frontend: GET /api/payments/:id/refund (Week 2 Mon)

**Risks**:
- Overcommitted by 4 SP - may need to cut Refund API
- Stripe API docs incomplete (working with their support)
```

**Attendees Toman Notas**:
- ✅ Qué features están construyendo otros equipos
- ✅ Qué dependencies necesitan de mi equipo
- ⚠️ Risks que podrían afectar mi equipo

---

### Paso 3.2: Dependency Resolution (20min)

**Responsable**: Engineering Managers (todos)  
**Duración**: 20min  
**Entregable**: Dependency agreements + mitigation plans

**Proceso**:
1. **Review Dependency Matrix**: Proyectar matriz en pantalla
2. **Identify Conflicts**: Buscar dependencies "Critical" + "Not Started"
3. **Negotiate**: Equipos negocian timelines
4. **Document Agreements**: Escribir acuerdos en matriz

**Example - Dependency Negotiation**:
```
❌ CONFLICT IDENTIFIED:

Feature: Payment Gateway v2
- Frontend necesita: Backend API by Week 1 Wed (Dec 11)
- Backend commitment: Week 1 Fri (Dec 13) ← 2 días tarde

NEGOTIATION:
- Option 1: Frontend espera hasta Fri (delay su work)
- Option 2: Backend prioriza API (mover otro work a Week 2)
- Option 3: Backend entrega mock API Wed, real API Fri

DECISION: Option 3 (Mock API)
- Backend entrega mock API Wed Dec 11 (2h work)
- Frontend puede empezar development Wed
- Backend entrega real API Fri Dec 13
- QA testing usa mock hasta Fri

✅ AGREEMENT DOCUMENTED
```

**Dependency Mitigation Strategies**:
- **Mock APIs**: Backend entrega mock endpoint, Frontend puede empezar
- **Feature Flags**: Ship partially complete, hide behind flag
- **Parallel Work**: Teams trabajan en paralelo, integrate al final
- **Buffer Time**: Add 2-3 días buffer a critical dependencies

**Red Flags que Requieren Escalación**:
- ❌ Circular dependency (A espera B, B espera A) → Necesita re-architecture
- ❌ External dependency bloqueada (third-party) → PM debe buscar alternativa
- ❌ Team no puede proveer dependency → Re-prioritize sprint

**Output**: Dependency matrix actualizada con agreements

---

### Paso 3.3: Capacity Balancing (10min)

**Responsable**: Engineering Manager (todos)  
**Duración**: 10min  
**Entregable**: Balanced commitments across teams

**Check for Imbalances**:

| Team | Capacity | Commitment | Utilization | Status |
|------|----------|------------|-------------|--------|
| Frontend | 25 SP | 18 SP | 72% | ⚠️ Underutilized |
| Backend | 24 SP | 29 SP | 121% | 🔴 Overcommitted |
| Data Eng | 10 SP | 10 SP | 100% | ✅ Balanced |
| DevOps | 5 SP | 8 SP | 160% | 🔴 Overcommitted |
| QA | 14 SP | 12 SP | 86% | ✅ Balanced |

**Issues**:
- Backend overcommitted 121% (29 SP vs 24 SP capacity)
- DevOps overcommitted 160% (8 SP vs 5 SP capacity)
- Frontend underutilized 72% (could take more work)

**Resolution**:
```
Option 1: Move Work Frontend → Backend
- Frontend toma parte del Backend work (ej: API validation logic)
- Backend reduce scope

Option 2: Cut Scope
- Backend corta Refund API feature (8 SP) → Move to next sprint
- New commitment: 21 SP (88% utilization) ✅

Option 3: Borrow Resources
- 1 Backend dev ayuda DevOps con Redis setup (pair programming)
- Reduces DevOps load

DECISION: Option 2 (Cut Scope)
- Backend cuts Refund API (move to Sprint N+1)
- DevOps gets help from Backend for Redis (2 days pairing)
```

**Capacity Balancing Guidelines**:
- Target: **80-90% utilization** across all teams
- ✅ 70-90% = Healthy
- ⚠️ 90-100% = Risky (no buffer)
- 🔴 >100% = Overcommitted (must cut scope)
- ⚠️ <70% = Underutilized (add more work)

---

## 4️⃣ Fase 4: Refinement & Adjustments (30min)

**Timing**: Lunes 11:45 - 12:15  
**Formato**: Equipos vuelven a salas separadas

### Paso 4.1: Adjust Sprint Plans

**Responsable**: Engineering Manager + Team  
**Duración**: 30min  
**Entregable**: Final sprint backlog

**Actividades**:
1. **Update Backlog**: Reflejar agreements de Cross-Team Sync
2. **Re-assign Work**: Basado en dependency timelines
3. **Add Buffer**: Para dependencies críticas (ej: +1 día slack)
4. **Final Review**: Team confirma que commitment es achievable

**Example - Backend Team Adjustments**:
```markdown
BEFORE Cross-Team Sync:
- Payment Gateway v2 (21 SP)
- API Rate Limiting (8 SP)
- Total: 29 SP (overcommitted)

CHANGES FROM SYNC:
- ❌ Cut: Refund API (8 SP) → Moved to Sprint N+1
- ✅ Added: Help DevOps with Redis (3 SP pairing)
- ✅ Added: Mock API for Frontend (2 SP)

AFTER Adjustments:
- Payment Gateway v2 - Base (13 SP)
- API Rate Limiting (8 SP)
- Mock API delivery (2 SP)
- Help DevOps (3 SP)
- Total: 26 SP (108% capacity) ← Still slightly over

FINAL CUT:
- Move "API versioning" task (3 SP) to tech debt backlog
- Final: 23 SP (96% capacity) ✅ GOOD
```

**Checklist - Final Sprint Plan**:
- [ ] Capacity 80-90% utilized
- [ ] Critical dependencies have agreements (with dates)
- [ ] Team agrees commitment is achievable
- [ ] High-risk items have mitigation plans
- [ ] Tech debt included (~10% capacity)

---

### Paso 4.2: Sprint Goal Finalization

**Responsable**: Engineering Manager + Product Manager  
**Duración**: 15min (en paralelo con 4.1)  
**Entregable**: Sprint goal statement

**Template - Sprint Goal**:
```markdown
**Sprint N Goal**: [One sentence describing sprint objective]

**Success Criteria**:
1. [Measurable outcome 1]
2. [Measurable outcome 2]
3. [Measurable outcome 3]

**Teams Involved**: [List teams]
**Key Features**: [2-3 main features]
**Critical Dependencies**: [Top 2-3 dependencies]
```

**Example**:
```markdown
**Sprint 47 Goal**: Launch Payment Gateway v2 to 10% users (beta)

**Success Criteria**:
1. POST /api/payments/v2 endpoint live in production
2. 100 beta customers successfully process payments via v2
3. 0 critical bugs in payment flow

**Teams Involved**: Backend, Frontend, DevOps, QA
**Key Features**: Stripe integration, New checkout UI, Rate limiting
**Critical Dependencies**: 
- DevOps: Stripe webhook config (Week 1)
- Data Eng: Analytics API (Week 1)
```

**Sprint Goal Guidelines**:
- ✅ One sentence, clear and concise
- ✅ Measurable (not "improve performance", but "reduce latency to <500ms")
- ✅ Achievable (based on capacity)
- ❌ Too broad ("build new features")
- ❌ Too specific ("merge PR #1234")

---

## 📢 Sprint Kickoff Announcement

**Timing**: Lunes 12:15 - 12:30 (15min)  
**Formato**: All-hands Slack message + Meeting

### Sprint Kickoff Message

**Responsable**: Engineering Manager (senior)  
**Duración**: 15min  
**Entregable**: Slack announcement en #engineering

**Template**:
```markdown
🚀 **SPRINT 47 KICKOFF** 🚀

**Dates**: Dec 9 - Dec 20 (2 weeks)
**Sprint Goal**: Launch Payment Gateway v2 to 10% users (beta)

**Team Commitments**:
- **Backend** (23 SP): Payment Gateway v2, API Rate Limiting
- **Frontend** (22 SP): New Checkout UI, Analytics Dashboard
- **DevOps** (5 SP): Stripe webhooks, Redis cache
- **Data Eng** (10 SP): Analytics API, Data pipeline
- **QA** (12 SP): E2E tests, Load testing

**Critical Dependencies** (⚠️ Watch These):
1. DevOps → Backend: Stripe webhook config (Due: Wed Dec 11)
2. Backend → Frontend: Mock API (Due: Wed Dec 11)
3. Data Eng → Frontend: Analytics API (Due: Fri Dec 13)

**Risks**:
- Backend slightly overcommitted (96% capacity) - may need to descope
- External: Stripe API docs incomplete (tracking with their support)

**Daily Standup**: 9:30am in #standup-engineering
**Mid-Sprint Check**: Fri Dec 13, 2pm (review progress on dependencies)

Let's ship it! 💪

Questions? → #sprint-planning-questions
```

---

## 🔄 Durante el Sprint: Dependency Tracking

### Mid-Sprint Dependency Check (Viernes Week 1)

**Responsable**: Engineering Manager  
**Duración**: 30min  
**Formato**: Sync meeting con teams que tienen dependencies

**Agenda**:
1. **Review Dependency Matrix** (10min): Status update
2. **Identify Blockers** (10min): Cualquier dependency atrasada
3. **Mitigation** (10min): Plan para unblock

**Example - Dependency Status**:

| Dependency | Provider | Consumer | Due Date | Status | Action |
|------------|----------|----------|----------|--------|--------|
| Stripe webhook | DevOps | Backend | Wed Dec 11 | ✅ Done | None |
| Mock API | Backend | Frontend | Wed Dec 11 | ✅ Done | None |
| Analytics API | Data Eng | Frontend | Fri Dec 13 | ⚠️ At Risk | Data Eng needs +2 days |
| Redis cache | DevOps | Backend | Fri Dec 13 | 🔴 Blocked | Redis cluster issue |

**Mitigation Actions**:
- **Analytics API**: Frontend uses dummy data until Mon Dec 16 (Feature Flag)
- **Redis cache**: Backend uses in-memory cache temporarily, migrate to Redis Week 2

---

## 🎭 RACI Matrix - Sprint Planning Cross-Team

| Actividad | EM | PM | Tech Lead | Developers | QA | DevOps |
|-----------|----|----|-----------|------------|----|----|
| **Pre-Planning** | | | | | | |
| Capacity calculation | **R/A** | I | C | I | I | I |
| Priority refinement | C | **R/A** | I | I | I | I |
| Dependency mapping | C | I | **R/A** | C | I | C |
| **Team Planning** | | | | | | |
| Sprint goal definition | **A** | **R** | C | I | I | I |
| Story selection | **A** | **R** | C | C | C | C |
| Story breakdown | C | C | **R** | **A** | C | C |
| Commitment | **A** | C | C | **R** | C | C |
| **Cross-Team Sync** | | | | | | |
| Sprint showcase | **R/A** | C | C | I | I | I |
| Dependency resolution | **R/A** | C | **C** | I | I | I |
| Capacity balancing | **R/A** | C | C | I | I | I |
| **Refinement** | | | | | | |
| Adjust sprint plans | **A** | C | **R** | C | I | I |
| Sprint kickoff announcement | **R/A** | C | I | I | I | I |

---

## 📊 Métricas de Cross-Team Planning

### Planning Effectiveness

**Commitment Accuracy**:
```
Commitment Accuracy = Stories Completed / Stories Committed

Target: >80%
- >90% = Excellent (good estimation)
- 80-90% = Good
- 70-80% = Needs improvement
- <70% = Poor (over-committing)
```

**Dependency Success Rate**:
```
Dependency Success = Dependencies Delivered On-Time / Total Dependencies

Target: >85%
- >90% = Excellent
- 80-90% = Good
- <80% = Poor (causing blockers)
```

**Velocity Stability**:
```
Velocity Variance = StdDev(Last 6 Sprints Velocity)

Target: <15%
- <10% = Very stable
- 10-15% = Stable
- 15-25% = Unstable
- >25% = Chaotic (fix process)
```

**Sprint Goal Achievement**:
```
% Sprints where Sprint Goal achieved

Target: >75%
- >85% = Excellent
- 75-85% = Good
- <75% = Goals too ambitious or poor execution
```

### Cross-Team Collaboration

**Cross-Team Stories**:
```
% Stories que requieren >1 team

Track over time:
- Increasing = More cross-team work (good for innovation, bad for speed)
- Decreasing = Teams more autonomous (Team Topologies goal)
```

**Blocked Days**:
```
Avg days per sprint que team está blocked por dependency

Target: <1 day/sprint
- 0 days = Excellent
- <1 day = Good
- 1-2 days = Needs improvement
- >2 days = Poor dependency management
```

---

## 🚨 Antipatterns - Qué Evitar

### ❌ Antipattern 1: "Commit First, Check Dependencies Later"

**Problema**: Equipos commiten sin verificar si dependencies están disponibles.

**Consecuencia**: Sprint bloqueado, teams idle.

**Solución**: Dependency mapping ANTES de commitment (Pre-Planning phase).

---

### ❌ Antipattern 2: "100% Capacity Commitment"

**Problema**: Equipos commiten exactamente su capacity (sin buffer).

**Consecuencia**: Cualquier unknown (bug, sick day) causa sprint failure.

**Solución**: Commit 80-90% capacity, deja 10-20% buffer.

---

### ❌ Antipattern 3: "Siloed Planning"

**Problema**: Cada equipo planea independientemente, sin comunicación.

**Consecuencia**: Duplicate work, misaligned priorities, integration hell.

**Solución**: Cross-Team Sync meeting (obligatorio).

---

### ❌ Antipattern 4: "Dependency Date Slippage Sin Comunicación"

**Problema**: Team se da cuenta que no puede entregar dependency on-time, pero no comunica.

**Consecuencia**: Dependent team descubre blocker tarde, no puede mitigar.

**Solución**: Mid-Sprint Dependency Check + proactive communication.

---

### ❌ Antipattern 5: "Feature Creep Durante Sprint"

**Problema**: PM agrega features mid-sprint porque "hay capacity".

**Consecuencia**: Original commitment no se cumple, team burnout.

**Solución**: Scope freeze después de Planning Day (excepto critical bugs).

---

## 🔗 Links Relacionados

### Ceremonias
- [Sprint Planning](../ceremonias/sprint-planning.md) - Single-team planning
- [Daily Standup](../ceremonias/daily-standup.md) - Daily sync
- [Sprint Review](../ceremonias/sprint-review.md) - Demo de features
- [Retrospective](../ceremonias/retrospective.md) - Process improvement

### Workflows
- [Feature Development](feature-development.md) - Feature delivery process
- [Release Management](release-management.md) - Release coordination
- [Incident Response](incident-response.md) - Production issues

### Procesos
- [Capacity Planning](../procesos/capacity-planning.md) - Cálculo de capacity
- [Dependency Management](../procesos/dependency-management.md) - Managing cross-team deps
- [Estimation](../procesos/estimation.md) - Story point estimation

### Comunicación
- [Team Communication](../comunicacion/team-communication.md) - Communication channels
- [Cross-Team Collaboration](../comunicacion/cross-team-collaboration.md) - Collaboration patterns

### Métricas
- [Sprint Metrics](../metricas/sprint-metrics.md) - Velocity, commitment accuracy
- [Team Metrics](../metricas/team-metrics.md) - Team performance metrics

---

**Mantenido por**: Engineering Managers + Product Managers  
**Última actualización**: 7 de diciembre de 2025  
**Próxima revisión**: 7 de marzo de 2026  
**Versión**: 1.0
