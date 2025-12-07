# 🔗 Dependency Management - Pre-Planning Check

## 📋 Resumen Ejecutivo

**Problema**: Dependencies entre equipos se descubren durante Sprint Planning o mid-sprint, causando:

- Stories bloqueadas esperando a otro equipo
- Sprint commitments incumplidos
- Re-planning urgente mid-sprint
- Frustración y pérdida de confianza inter-equipos

**Solución**: Pre-Planning Dependency Check ejecutado 1 semana antes de Planning, con checkpoints estructurados.

**Beneficio**: Dependencies identificadas y resueltas ANTES de Planning → sprint fluye sin blockers externos.

---

## 🎯 ¿Qué es una Dependency?

**Definición**:

> Tu equipo necesita que OTRO equipo (o sistema externo) complete trabajo antes de que tú puedas avanzar.

### Tipos de Dependencies

#### 1. **Team-to-Team Dependencies** (Más común)

**Ejemplo**:

- Equipo Frontend necesita API endpoint de equipo Backend
- Equipo Mobile necesita diseños de equipo Diseño
- Equipo Producto necesita infra de equipo DevOps

**Risk**: Alta - requiere coordinación entre equipos con diferentes prioridades

---

#### 2. **External System Dependencies**

**Ejemplo**:

- Third-party API (Stripe, SendGrid, Auth0)
- Vendor delivery (hardware, licenses)
- External approval (legal, compliance, security)

**Risk**: Muy alta - fuera de tu control completamente

---

#### 3. **Internal System Dependencies**

**Ejemplo**:

- Database migration debe completarse antes de feature nueva
- Feature flag debe activarse en producción
- Cache layer debe estar configurado

**Risk**: Media - tu equipo puede controlar, pero requiere planning específico

---

#### 4. **Knowledge/Skill Dependencies**

**Ejemplo**:

- Necesitas training en tecnología nueva
- Necesitas pair programming con especialista
- Necesitas documentación de legacy system

**Risk**: Media - puede resolverse con time-boxing y knowledge transfer

---

## 🔍 Pre-Planning Dependency Check Process

### Timeline: L - 7 días antes de Planning

```
Sprint N Planning: Viernes Week 2
Dependency Check: Viernes Week 1 (L-7 días)

L-7   L-5   L-3   L-1    L (Planning)
 │     │     │     │      │
 └─────┴─────┴─────┴──────┘
Check  Follow-up  Final  Planning
      (if needed) Review
```

---

### Checkpoint 1: Initial Scan (L-7, Viernes, 1 semana antes)

**Owner**: Tech Lead + Product Owner

**Duración**: 30 minutos

**Actividades**:

#### 1. Review Candidate Stories (15 min)

Revisar top 10-15 stories del backlog (priorizadas por PO):

```markdown
Por cada story, preguntar:

1. ¿Requiere trabajo de OTRO equipo?

   - Backend API? → Backend team dependency
   - Diseños? → Diseño team dependency
   - Infra nueva? → DevOps team dependency

2. ¿Requiere sistema externo?

   - Third-party API? → External dependency
   - Vendor? → External dependency

3. ¿Requiere pre-work interno?

   - DB migration? → Internal dependency
   - Feature flag? → Internal dependency

4. ¿Requiere knowledge/skill nuevo?
   - Training? → Knowledge dependency
   - Specialist? → Knowledge dependency
```

#### 2. Crear Dependency Map (10 min)

Template:

```markdown
## Dependency Map - Sprint N (Dec 6-19)

### Team-to-Team Dependencies

| Story ID | Descripción | Blocked By | What Needed          | By When | Status         |
| -------- | ----------- | ---------- | -------------------- | ------- | -------------- |
| TEAM-101 | User login  | Backend    | POST /auth/login API | L-3     | ⚠️ Not Started |
| TEAM-102 | Checkout UI | Diseño     | Mockups finales      | L-5     | ✅ In Progress |

### External Dependencies

| Story ID | Descripción | External System | What Needed   | By When | Status                        |
| -------- | ----------- | --------------- | ------------- | ------- | ----------------------------- |
| TEAM-103 | Payments    | Stripe          | Test API keys | L-1     | ❌ Blocked (waiting approval) |

### Internal Dependencies

| Story ID | Descripción | What Needed  | Owner  | By When | Status       |
| -------- | ----------- | ------------ | ------ | ------- | ------------ |
| TEAM-104 | Analytics   | DB migration | DevOps | L-3     | ✅ Scheduled |

### Knowledge Dependencies

| Story ID | Descripción | Knowledge Needed | Source    | By When | Status           |
| -------- | ----------- | ---------------- | --------- | ------- | ---------------- |
| TEAM-105 | GraphQL API | GraphQL training | Tech Lead | L-2     | ⚠️ Not Scheduled |
```

#### 3. Communicate Dependencies (5 min)

**Slack Message Template**:

```
🔗 Dependency Check - Sprint N Planning (Dec 13)

We have dependencies on:

**Backend Team** (@backend.lead):
- TEAM-101: Need POST /auth/login API by Dec 10 (L-3)
- TEAM-106: Need GET /products?filter=... API by Dec 10 (L-3)

Can you confirm these can be ready? If not, we'll deprioritize stories.

**Diseño Team** (@design.lead):
- TEAM-102: Need final mockups for checkout flow by Dec 8 (L-5)

Status update please?

**DevOps Team** (@devops.lead):
- TEAM-104: Need analytics DB migration by Dec 10 (L-3)

Is this scheduled?

cc @product.owner @scrum.master
```

---

### Checkpoint 2: Follow-up (L-5, Martes, 5 días antes)

**Owner**: Tech Lead

**Duración**: 15 minutos (async updates via Slack)

**Actividades**:

#### 1. Check Status of Dependencies

Revisar Dependency Map, actualizar status:

- ✅ **Confirmed**: Otro equipo confirmó que pueden entregar
- ⚠️ **At Risk**: Otro equipo tiene concerns, pero intentarán
- ❌ **Blocked**: Otro equipo NO puede entregar a tiempo
- 🔄 **In Progress**: Trabajo ya empezó

#### 2. Escalate Blockers

Si hay ❌ Blocked dependencies:

**Option A**: Deprioritize Story

- "Story TEAM-101 depende de Backend API que no estará lista → sacamos del sprint"
- PO re-prioriza backlog

**Option B**: Find Alternative

- "Backend no puede hacer API → podemos usar mock data por ahora?"
- "Diseño no tiene mockups → podemos usar wireframes básicos y refinar después?"

**Option C**: Escalate to Management

- Si story es critical business priority → VP Eng debe resolver
- Típicamente solo para P0 incidents o revenue-critical features

#### 3. Update Dependency Map

```markdown
### Team-to-Team Dependencies

| Story ID | What Needed  | By When | Status L-7     | Status L-5   | Action                 |
| -------- | ------------ | ------- | -------------- | ------------ | ---------------------- |
| TEAM-101 | Backend API  | L-3     | ⚠️ Not Started | ✅ Confirmed | Backend started work   |
| TEAM-102 | Mockups      | L-5     | ✅ In Progress | ✅ Done      | Mockups delivered!     |
| TEAM-107 | DevOps infra | L-3     | ⚠️ Not Started | ❌ Blocked   | **Deprioritize story** |
```

---

### Checkpoint 3: Final Review (L-1, Jueves, 1 día antes de Planning)

**Owner**: Tech Lead + Product Owner

**Duración**: 15 minutos

**Actividades**:

#### 1. Final Status Check

Revisar TODAS las dependencies:

- ✅ **Confirmed**: Story puede ir a Planning con confianza
- ⚠️ **At Risk**: Story puede ir a Planning, pero monitorear closely
- ❌ **Blocked**: Story NO va a Planning, deprioritizar

#### 2. Prepare Contingency Plan

Para dependencies ⚠️ At Risk:

```markdown
## Contingency Plans

**TEAM-101: User Login** (Backend API at risk)

- Plan A: Backend entrega API en L+2 (2 días en sprint) → aceptable
- Plan B: Usamos mock API mientras Backend termina → aceptable
- Plan C: Si L+5 API no está lista → pullamos story del sprint

**TEAM-108: Analytics Dashboard** (Data pipeline at risk)

- Plan A: DevOps entrega pipeline en L+3 → aceptable
- Plan B: Usamos sample data mientras pipeline se completa
- Plan C: Si L+7 no está lista → movemos story a siguiente sprint
```

#### 3. Communicate Final Status

**Slack Update**:

```
🔗 Dependency Check - FINAL STATUS (Planning mañana)

✅ **Ready for Planning** (5 stories):
- TEAM-102: Checkout UI (diseños delivered ✅)
- TEAM-103: Payments (Stripe keys approved ✅)
- TEAM-104: Analytics (DB migration scheduled ✅)
- TEAM-109: Profile page (no dependencies)
- TEAM-110: Bug fixes (no dependencies)

⚠️ **At Risk** (2 stories, con contingency plan):
- TEAM-101: User Login (Backend API in progress, Plan B ready)
- TEAM-108: Analytics Dashboard (Data pipeline at risk, Plan B ready)

❌ **Blocked - REMOVED from Planning** (1 story):
- TEAM-107: Real-time notifications (DevOps infra no disponible)

@product.owner please adjust Planning agenda accordingly.
cc @team
```

---

## 📊 Dependency Risk Matrix

### Cómo Evaluar Risk

```
Risk = Impact × Likelihood of Failure

Impact: ¿Qué tan crítico es para el sprint?
- High: Sprint goal depende de esto
- Medium: Nice to have pero sprint puede succeed sin esto
- Low: Bonus feature

Likelihood of Failure: ¿Qué probabilidad hay de que falle?
- High: Otro equipo no confirmó, external approval uncertain
- Medium: Otro equipo confirmó pero tiene track record de delays
- Low: Otro equipo confirmó y es confiable
```

### Risk Prioritization

```markdown
| Dependency            | Impact | Likelihood | Risk Score   | Action                                     |
| --------------------- | ------ | ---------- | ------------ | ------------------------------------------ |
| Backend API for Login | High   | Medium     | **HIGH**     | Daily check-in, contingency plan mandatory |
| Diseño mockups        | Medium | Low        | **MEDIUM**   | Weekly check-in suficiente                 |
| Training en GraphQL   | Low    | Low        | **LOW**      | Monitor pasivamente                        |
| Legal approval        | High   | High       | **CRITICAL** | Escalate to VP, daily updates              |
```

**Risk Scores**:

- **CRITICAL** (High×High): Escalate to management, daily updates, block story if not resolved
- **HIGH** (High×Medium o Medium×High): Daily check-in, contingency plan ready
- **MEDIUM** (Medium×Medium o High×Low): Weekly check-in
- **LOW** (Low×Any): Pasivo monitoring

---

## 🚨 Escalation Path

### Level 1: Team-to-Team (Default)

**When**: Dependency entre 2 equipos con mismo reporting line

**Process**:

1. Tech Lead de equipo bloqueado → contacta Tech Lead de equipo blocker
2. Slack: `@backend.lead need help with TEAM-101 dependency, can we sync?`
3. Sync call: 15 min, resolver timeline o alternativas
4. Update Dependency Map

**Timeline**: Resolver en 1-2 días

---

### Level 2: Cross-Department

**When**: Dependency entre equipos de diferentes departments (ej: Eng + Marketing)

**Process**:

1. Tech Lead → escala a Engineering Manager
2. Eng Manager → contacta Manager del otro department
3. Managers resuelven prioridades
4. Feedback loop a Tech Leads

**Timeline**: Resolver en 2-3 días

---

### Level 3: Executive

**When**: Dependency crítica bloqueada, impacta business goals

**Process**:

1. Engineering Manager → escala a VP Engineering
2. VP Eng → resuelve con otros VPs (VP Product, VP Ops, etc.)
3. Executive decision: re-prioritize work, add resources, o postpone feature

**Timeline**: Resolver en 1 día (urgent)

**Example**:

- Revenue-critical feature para board meeting
- Compliance deadline (legal requirement)
- P0 production incident

---

## 🎭 Roles y Responsabilidades

### Tech Lead

**L-7 (Initial Scan)**:

- ✅ Review top 10-15 stories con Product Owner
- ✅ Identificar dependencies (team, external, internal, knowledge)
- ✅ Crear Dependency Map
- ✅ Comunicar dependencies a otros equipos via Slack

**L-5 (Follow-up)**:

- ✅ Revisar status updates de otros equipos
- ✅ Actualizar Dependency Map
- ✅ Escalar blockers a Eng Manager si necesario
- ✅ Proponer alternativas para dependencies bloqueadas

**L-1 (Final Review)**:

- ✅ Final status check con PO
- ✅ Preparar contingency plans para dependencies at-risk
- ✅ Comunicar final status al equipo
- ✅ Remover stories bloqueadas del Planning scope

**Durante Sprint**:

- ✅ Monitor dependencies at-risk daily
- ✅ Ejecutar contingency plan si dependency falla
- ✅ Comunicar al equipo si story debe pullarse mid-sprint

---

### Product Owner

**L-7 (Initial Scan)**:

- ✅ Priorizar top 10-15 stories para dependency check
- ✅ Confirmar business priority de cada story
- ✅ Participar en dependency identification

**L-5 (Follow-up)**:

- ✅ Decidir si deprioritizar stories bloqueadas
- ✅ Re-ordenar backlog basado en dependency status

**L-1 (Final Review)**:

- ✅ Aprobar final list de stories para Planning
- ✅ Preparar Planning agenda con stories dependency-free
- ✅ Comunicar a stakeholders si features críticas se postponen

---

### Otros Tech Leads (Blocker Teams)

**Responsabilidad**:

- ✅ Responder a dependency requests en <24h
- ✅ Confirmar timeline realista (no over-promise)
- ✅ Escalar a su manager si no pueden cumplir
- ✅ Comunicar proactivamente si timeline cambia

**Good Citizenship**:

- ✅ Si otro equipo depende de ti → prioriza ese work
- ✅ Si no puedes cumplir → comunica ASAP (no esperar a L-1)
- ✅ Si tienes blockers → pide ayuda temprano

---

### Engineering Manager

**When Escalated**:

- ✅ Resolver conflictos de prioridades entre equipos
- ✅ Re-asignar resources si es necesario
- ✅ Escalar a VP si es cross-department o critical
- ✅ Comunicar resolution a Tech Leads

---

## 📊 Metrics

### Metric #1: Dependency Identification Rate

**Formula**:

```
(Dependencies identificadas en L-7 / Total dependencies en sprint) × 100
```

**Target**: >80%

**Insight**:

- <60% → dependencies se descubren mid-sprint (reactive)
- > 80% → proceso funciona, somos proactive

---

### Metric #2: Dependency Resolution Rate

**Formula**:

```
(Dependencies resueltas antes de Planning / Total dependencies) × 100
```

**Target**: >90%

**Insight**:

- <70% → bloqueamos muchas stories por dependencies
- > 90% → proceso efectivo, good collaboration entre equipos

---

### Metric #3: Mid-Sprint Blockers por Dependencies

**Formula**:

```
# Stories bloqueadas mid-sprint esperando otro equipo
```

**Target**: 0 por sprint

**Insight**:

- > 2 → dependency check no está siendo efectivo
- 0 → excelente planning y coordination

---

### Metric #4: Sprint Commitment Accuracy

**Formula**:

```
(Story points completados / Story points committed) × 100
```

**Target**: >85%

**Insight**:

- Dependencies impactan velocity
- Si accuracy <70% y muchas dependencies → mejorar dependency management

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup

**Semana 1**:

- [ ] Tech Lead crea template de Dependency Map (Confluence o Excel)
- [ ] Tech Lead + PO revisan este documento (30 min)
- [ ] Comunicar proceso a otros Tech Leads
- [ ] Acordar SLA: Responder dependency requests en <24h

**Semana 2**:

- [ ] Trial run: Ejecutar Dependency Check para próximo sprint
- [ ] L-7: Initial scan
- [ ] L-5: Follow-up
- [ ] L-1: Final review
- [ ] Retrospective: ¿Funcionó? ¿Qué ajustar?

---

### Sprint 1-3: Iterate

- [ ] Ejecutar proceso consistentemente cada sprint
- [ ] Trackear metrics (identification rate, resolution rate, mid-sprint blockers)
- [ ] Ajustar timeline si es necesario (ej: ¿L-10 en vez de L-7?)

---

### Sprint 4+: Steady State

- [ ] Proceso es hábito
- [ ] Dependency resolution rate >90%
- [ ] Mid-sprint blockers = 0
- [ ] Equipos confían en collaboration

---

## ✅ Success Criteria

### Mes 1

- ✅ Dependency Map creado cada sprint
- ✅ Dependencies identificadas >60% antes de Planning

### Mes 2-3

- ✅ Dependency resolution rate >80%
- ✅ Mid-sprint blockers por dependencies <2 por sprint

### Mes 4+

- ✅ Dependency resolution rate >90%
- ✅ Mid-sprint blockers = 0
- ✅ Equipos proactivamente comunican dependencies
- ✅ Sprint commitment accuracy >85%

---

## 🔗 Links Relacionados

- [Ceremonias: Sprint Planning](README.md#sprint-planning) - Donde dependencies impactan
- [Ceremonias: Backlog Refinement](README.md#backlog-refinement) - Donde se identifican dependencies
- [Definition of Ready](definition-of-ready.md) - DoR incluye "no blockers conocidos"
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis de dependencies

---

## 📚 Ejemplos

### ✅ Ejemplo: Dependency Bien Manejada

```markdown
## Story: TEAM-101 - User Login con Google OAuth

**Dependency Identificada** (L-7):

- Backend Team debe crear POST /auth/google endpoint
- Estimado: 3 story points, 2 días de trabajo
- By When: L-3 (Dec 10)

**L-7 Communication**:
Tech Lead Frontend → Tech Lead Backend (Slack):
"Hey @backend.lead, para Sprint N necesitamos Google OAuth endpoint.
Can you deliver by Dec 10? API contract here: [link]"

**L-5 Status**:
Backend Lead: "✅ Confirmed. Backend dev started work yesterday.
On track para Dec 10."

**L-1 Final Check**:
Backend Lead: "✅ Done. Endpoint deployed to staging.
Postman collection here: [link]. Ready para testing."

**Durante Sprint**:

- Frontend team integra sin blockers
- Story completes on time
- 🎉 Success!
```

---

### ❌ Ejemplo: Dependency Mal Manejada (Antipattern)

```markdown
## Story: TEAM-202 - Real-time Notifications

**L-7**: Tech Lead no identifica dependency (❌ error #1)

- Story va a Planning sin dependency check

**Sprint Day 2**: Developer empieza a trabajar

- Descubre que necesita WebSocket server de DevOps team
- "Oh, DevOps no tiene esto en roadmap" (❌ error #2)

**Sprint Day 3**: Tech Lead contacta DevOps

- DevOps: "Necesitamos 2 sprints para setup infra"
- Story bloqueada (❌ error #3)

**Sprint Day 5**: Sprint Re-planning

- Story removida del sprint
- Developer re-asignado a otro work (context switch)
- Sprint commitment incumplido
- PO frustrado, stakeholders frustrados

**Root Cause**: Dependency no identificada en L-7 check

**How to Prevent**:

- L-7: Tech Lead debe preguntar "¿Qué infra necesita esto?"
- L-7: Identificar WebSocket dependency
- L-7: Consultar con DevOps
- L-5: DevOps confirma "No podemos en este sprint"
- L-1: Story removida ANTES de Planning
- Result: Sprint commitment realistic, no mid-sprint surprises
```

---

## 🚫 Antipatterns

### ❌ Antipattern #1: "We'll figure it out during the sprint"

**Síntoma**: Dependency conocida pero no hay plan

**Por Qué Falla**: Otro equipo puede no tener capacity, story se bloquea

**Solución**: NO aceptar story en Planning sin dependency confirmation

---

### ❌ Antipattern #2: Dependencies ocultas en sub-tasks

**Síntoma**: Story parece independiente, pero sub-task tiene dependency

**Por Qué Falla**: Dependency se descubre mid-sprint cuando dev empieza sub-task

**Solución**: En Backlog Refinement, preguntar "¿Qué necesitamos de otros equipos para CADA sub-task?"

---

### ❌ Antipattern #3: Over-optimism en timelines

**Síntoma**: "Backend dice que lo tendrán listo" (pero sin commitment)

**Por Qué Falla**: Backend tiene sus propias prioridades, tu dependency no es top priority para ellos

**Solución**: Pedir confirmation escrita (Slack, Jira comment) con timeline específico

---

### ❌ Antipattern #4: No tener Plan B

**Síntoma**: Dependency única sin alternativa

**Por Qué Falla**: Si dependency falla → story muere

**Solución**: Siempre tener contingency plan (mock data, manual workaround, deprioritize)

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Tech Lead + Product Owner  
**Review Cycle**: Trimestral
