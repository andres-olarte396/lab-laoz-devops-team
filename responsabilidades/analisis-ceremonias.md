# Análisis de Responsabilidades: Ceremonias Ágiles

## 📋 Resumen Ejecutivo

Este documento analiza los **vacíos, overlaps, y mejoras** en las ceremonias ágiles definidas en [`/ceremonias/README.md`](../ceremonias/README.md), identificando responsabilidades poco claras y proponiendo soluciones concretas para optimizar las ceremonias del equipo.

**Fecha de análisis**: Diciembre 6, 2025  
**Scope**: Daily Standup, Sprint Planning, Backlog Refinement, Sprint Review, Sprint Retrospective  
**Base**: [Ceremonias Ágiles actuales](../ceremonias/README.md) (839 líneas)

---

## 📂 Contexto: Ceremonias Actuales Definidas

Las ceremonias actuales (definidas en [`/ceremonias/README.md`](../ceremonias/README.md)) establecen:

### Calendario de Sprints (2 semanas)

```yaml
Semana 1:
  - Daily Standup: Lunes-Viernes 15min
  - Backlog Refinement: Martes + Viernes 1h

Semana 2:
  - Daily Standup: Lunes-Viernes 15min
  - Sprint Planning: Lunes 2-4h (inicio de sprint)
  - Sprint Review: Jueves 1h
  - Sprint Retrospective: Viernes 1h
```

### Ceremonias Definidas Actualmente

#### 1. Daily Standup (15 min)

- **Participantes**: Dev Team (obligatorio), PO/TL (recomendado)
- **Formato**: 3 preguntas (Ayer/Hoy/Blockers)
- **Facilitador**: Tech Lead o Scrum Master
- **Opción async**: Slack bot para equipos distribuidos

#### 2. Sprint Planning (2-4 horas)

- **Parte 1**: Sprint Goal + Prioridades (45-60min)
- **Parte 2**: Capacity Planning (30min)
- **Parte 3**: Story Selection & Breakdown (60-120min)
- **Participantes**: PO, Dev Team, Tech Lead (obligatorio)

#### 3. Backlog Refinement (1 hora, 2x/sprint)

- **Objetivo**: Preparar stories para próximo sprint
- **Actividades**: Story breakdown, estimation, clarification
- **Participantes**: PO, Tech Lead, Dev Team

#### 4. Sprint Review (1 hora)

- **Objetivo**: Demo de features completadas
- **Participantes**: Todo el equipo + stakeholders opcionales
- **Formato**: Demos + Q&A + Feedback

#### 5. Sprint Retrospective (1 hora)

- **Objetivo**: Mejora continua del proceso
- **Formato**: What went well / What didn't / Action items
- **Participantes**: Dev Team, PO, Tech Lead (obligatorio)

### Gaps Detectados en Definición Actual

Aunque las ceremonias están **bien documentadas**, **NO definen claramente**:

- ❌ Qué hacer si Tech Lead no puede facilitar (backup)
- ❌ Cómo manejar dependencies cross-team en Planning
- ❌ Proceso para priorizar tech debt vs features
- ❌ Cómo involucrar a QA en estimation (evitar bottleneck)
- ❌ Definition of Ready para stories (cuándo está ready para Planning)
- ❌ Quiénes son "stakeholders" en Sprint Review (cómo invitar)
- ❌ **CRÍTICO**: Cómo hacer follow-up de action items de Retro
- ❌ Qué hacer con emergency work mid-sprint (bugs P0/P1)
- ❌ Cómo evitar que Design handoff bloquee desarrollo

Este análisis aborda estos **vacíos específicos** con soluciones concretas.

---

## 🔍 Hallazgos Principales

### ✅ Fortalezas Detectadas

1. **Calendario bien estructurado**: Sprints de 2 semanas con ceremonias claramente espaciadas
2. **Roles definidos**: Participación clara (obligatorio, recomendado, opcional)
3. **Time-boxing claro**: Duraciones específicas para cada ceremonia
4. **Async standup option**: Flexibilidad para equipos distribuidos

### ⚠️ Vacíos Identificados

| #   | Vacío                                         | Impacto                                              | Severidad |
| --- | --------------------------------------------- | ---------------------------------------------------- | --------- |
| 1   | **Scrum Master rol no asignado**              | No hay facilitador claro si Tech Lead no puede       | 🟡 Media  |
| 2   | **Backlog Refinement: Ownership poco claro**  | PO vs PM - quién lidera, quién estima                | 🟡 Media  |
| 3   | **Sprint Review: Stakeholders no definidos**  | ¿Quién debe asistir? ¿Cómo se invita?                | 🟡 Media  |
| 4   | **Retrospective: Action items sin follow-up** | Mejoras identificadas no se implementan              | 🔴 Alta   |
| 5   | **Cross-team dependencies en Planning**       | No hay proceso para coordinar con otros equipos      | 🔴 Alta   |
| 6   | **Tech debt en Sprint Planning**              | No hay % reservado, siempre se prioriza features     | 🟡 Media  |
| 7   | **QA involucrado tarde en Planning**          | QA no estima testing effort, causa overcommit        | 🟡 Media  |
| 8   | **Design handoff timing**                     | Designs llegan mid-sprint, bloquean desarrollo       | 🔴 Alta   |
| 9   | **Emergency work mid-sprint**                 | No hay proceso para bugs P0/P1 que llegan mid-sprint | 🟡 Media  |
| 10  | **Velocity tracking inconsistente**           | No hay owner, no se usa para planning                | 🟢 Baja   |

---

## 📊 Análisis Detallado por Ceremonia

### 1. Daily Standup

#### Vacíos Detectados

**1.1. Scrum Master rol no asignado claramente**

**Problema**:

- Documento dice "Tech Lead o Scrum Master"
- Muchos equipos no tienen Scrum Master dedicado
- Si Tech Lead está de vacaciones, ¿quién facilita?
- No hay rotación clara

**Impacto**:

- Standup se salta cuando Tech Lead no está
- Formato inconsistente (cada facilitador lo hace diferente)
- Nadie hace time-keeping (se excede 15 minutos)

**Solución propuesta**:

```yaml
Standup Facilitation Model:

Opción 1: Tech Lead como facilitador permanente
  Primary: Tech Lead
  Backup (si TL de vacaciones/enfermo):
    - Senior Developer (pre-designado cada sprint)
    - Rotación semanal entre Senior Devs

  Responsibilities del facilitador:
    - Llegar 2 minutos antes (setup Zoom/room)
    - Timeboxing (cut off discusiones >2 min)
    - Anotar blockers en Jira/Linear
    - Facilitar parking lot post-standup
    - Actualizar standup board (si físico)

Opción 2: Rotación semanal (para equipos senior)
  Rotation: Cada developer facilita 1 semana
  Benefits:
    - Ownership compartido
    - Desarrolla facilitation skills
    - No depende de 1 persona
  Drawbacks:
    - Inconsistencia (cada quien lo hace diferente)
    - Juniors pueden no saber manejar discusiones

  Best for: Equipos de 5-7 developers, todos senior (3+ años)

Opción 3: Scrum Master dedicado (equipos grandes)
  Required if: Team >10 personas
  Scrum Master responsibilities:
    - Facilitar todas las ceremonias
    - Coaching en Agile practices
    - Remover impediments
    - Metrics tracking (velocity, burndown)
```

**Recomendación**: Opción 1 para mayoría de equipos (Tech Lead + backup rotation)

---

**1.2. Async Standup: Falta seguimiento de blockers**

**Problema**:

- Async standup (Slack bot) funciona para updates
- Pero blockers no se resuelven tan rápido (no hay discusión inmediata)
- No hay "parking lot" para discusiones async

**Impacto**:

- Blockers duran >1 día porque no hay urgency
- Equipo no se siente sincronizado

**Solución propuesta**:

```yaml
Async Standup con Blocker Resolution:

Tool: Slack bot (Geekbot) + Blocker Thread

Process:
  1. Bot pregunta 3 preguntas (8-9 AM)
  2. Cada persona responde antes de 10 AM
  3. Bot crea thread summary a las 10 AM

  4. Si alguien reporta blocker:
     - Bot automáticamente crea thread dedicado
     - Bot tagea al Tech Lead + persona relevante
     - Expectativa: Respuesta en <2 horas

  5. Si blocker no resuelto en 4 horas:
     - Escalación automática a Engineering Manager
     - Quick sync call (15 min) forzado

  6. Blocker resolution tracked en Jira (auto-created ticket)

Hybrid approach (recomendado):
  - Async standup 3 días/semana (Lunes, Miércoles, Viernes)
  - Sync standup 2 días/semana (Martes, Jueves)
  - Balance: Flexibilidad + Resolución rápida de blockers
```

---

### 2. Sprint Planning

#### Vacíos Detectados

**2.1. Cross-team dependencies no manejadas**

**Problema**:

- Equipo A planea feature que depende de API de Equipo B
- No hay proceso para coordinar entre equipos en Planning
- Dependencias se descubren mid-sprint (bloqueos)

**Impacto**:

- Sprint goals no se cumplen (bloqueados por otros equipos)
- Re-planning mid-sprint (desperdicio de tiempo)
- Frustración entre equipos

**Solución propuesta**:

```yaml
Pre-Planning Dependency Check (1 semana antes de Planning):

Lunes (1 semana antes):
  1. Product Owner lista top 10 stories para próximo sprint
  2. Tech Lead revisa cada story:
     - ¿Tiene dependencias externas? (otros equipos, third-party APIs)
     - ¿Requiere infra changes? (DevOps)
     - ¿Requiere diseños? (Design team)

  3. Si hay dependencias:
     - Tech Lead crea ticket de coordinación
     - Tagea al Tech Lead del otro equipo
     - Async o quick sync call (15 min) para confirmar

Miércoles (5 días antes):
  4. Tech Lead valida que dependencias están resueltas:
     ✅ Otro equipo confirma que su parte estará ready
     ✅ Designs están completos (no WIP)
     ✅ Infra changes programados

  5. Si dependencia no confirmada:
     - Story se mueve a backlog (no entra en planning)
     - O se busca alternativa (workaround, mock API)

Viernes (3 días antes):
  6. Final check: Todas las stories en planning tienen:
     - ✅ Designs completos (si requieren)
     - ✅ Dependencies confirmadas
     - ✅ Acceptance criteria claros

Sprint Planning Day:
  - Parte 1 incluye "Dependency Review" (15 min):
    - Tech Lead confirma que todas las dependencies están OK
    - Si algo cambió, story se saca del sprint

Post-Planning:
  - Tech Lead envía email a equipos con dependencias:
    "Equipo B: Necesitamos API X ready para Day 5 del sprint. Confirm?"
```

---

**2.2. Tech Debt no priorizado sistemáticamente**

**Problema**:

- Planning siempre prioriza features (presión de Product/Business)
- Tech debt se acumula indefinidamente
- No hay % reservado para tech debt, refactors, upgrades

**Impacto**:

- Codebase se degrada (velocity baja con el tiempo)
- Developer frustration (siempre trabajando en deuda técnica)
- Incidentes aumentan (código frágil)

**Solución propuesta**:

```yaml
Tech Debt Budget Model:

Opción 1: Fixed percentage (20% rule)
  - 20% de cada sprint reservado para tech debt
  - ~8 story points de 40 total
  - No negociable (policy de Engineering)

  Implementation:
    - Sprint Planning Parte 1: PO presenta features
    - Sprint Planning Parte 2:
      - Equipo selecciona features (hasta 80% capacity)
      - Tech Lead presenta top 3 tech debt items
      - Equipo vota cuál trabajar (20% restante)

Opción 2: Dedicated Tech Debt Sprints (quarterly)
  - 1 sprint completo cada quarter dedicado a tech debt
  - No features nuevas (solo critical bugs)
  - Tech Lead define roadmap de tech debt

  Best for: Productos maduros con mucha deuda acumulada

Opción 3: Hybrid (recomendado)
  - 10% de cada sprint para tech debt pequeño
  - 1 sprint completo cada 6 meses para tech debt grande

Tech Debt Prioritization:
  - Tech Lead mantiene "Tech Debt Backlog" en Jira
  - Categorías:
    - 🔴 Critical: Security, performance, stability (prioridad 1)
    - 🟡 Important: Upgrade dependencies, refactors (prioridad 2)
    - 🟢 Nice-to-have: Code cleanup, minor refactors (prioridad 3)

  - Cada sprint: Tech Lead presenta top 3 critical items
  - Equipo decide cuál trabajar basado en:
    - Impact (reduce incidents, improve velocity)
    - Effort (story points)
    - Risk (qué pasa si no lo hacemos)
```

---

**2.3. QA effort no estimado en Planning**

**Problema**:

- Developers estiman development time
- QA testing time no se considera
- Features "completas" en desarrollo esperan días en QA queue

**Impacto**:

- Sprint commitment inaccurato (features no "done done" al final)
- QA bottleneck (todo llega en Day 8-9 del sprint)
- Bugs found late (no time para fix antes de sprint end)

**Solución propuesta**:

```yaml
QA-Inclusive Estimation Model:

Story Point breakdown:
  Development: X points
  QA Testing: Y points (typically 20-40% of dev time)
  Total: X + Y points

Example:
  Story: "User can reset password"
  - Backend API: 3 points
  - Frontend UI: 2 points
  - QA Testing: 2 points (test cases, manual testing, automation)
  - Total: 7 points

Sprint Planning Parte 3: QA Planning (30 min)
  After dev stories selected:
  1. QA Engineer revisa cada story
  2. Identifica testing complexity:
     - Simple (CRUD): +1 point
     - Medium (flows, integrations): +2 points
     - Complex (payments, security): +3-5 points

  3. QA creates testing tasks:
     - Write test cases
     - Manual testing (exploratory)
     - Automated test scripts (if applicable)

  4. Capacity check:
     - ¿QA tiene capacidad para testear todas las stories?
     - Si no: Reducir commitment o agregar QA capacity

Definition of Ready (incluye QA):
  ✅ Acceptance criteria clara (testable)
  ✅ Test cases estimados (QA reviewed story)
  ✅ Testing environment available
  ✅ Test data available

QA Parallel Work (evitar bottleneck):
  - Day 1-2: QA escribe test cases mientras dev trabaja
  - Day 3-5: QA hace exploratory testing en staging (si feature parcial ready)
  - Day 6-8: QA hace regression testing
  - Day 9-10: Buffer para re-testing después de bug fixes
```

---

### 3. Backlog Refinement

#### Vacíos Detectados

**3.1. Product Owner vs Product Manager ownership**

**Problema**:

- ¿Quién lidera Refinement? ¿PO o PM?
- Si hay ambos roles: Confusion sobre quién presenta stories
- Si solo hay PM: ¿PM hace refinement técnico?

**Impacto**:

- Stories mal definidas (faltan acceptance criteria)
- Technical feasibility no discutida
- Estimaciones incorrectas

**Solución propuesta**:

```yaml
Refinement Ownership por Estructura:

Scenario 1: Team tiene PO dedicado
  Leader: Product Owner
  PM involvement: Opcional (solo para context de roadmap)

  PO responsibilities:
    - Presentar stories del backlog
    - Clarificar acceptance criteria
    - Priorizar dentro del sprint scope
    - Responder preguntas de negocio

  Tech Lead responsibilities:
    - Hacer preguntas técnicas
    - Identificar edge cases
    - Estimar complejidad (con equipo)
    - Identificar dependencias técnicas

Scenario 2: Team tiene PM (sin PO dedicado)
  Leader: Product Manager (wearing PO hat)
  Support: Tech Lead (co-facilitator)

  PM responsibilities:
    - Context de roadmap (why estas stories)
    - Business requirements
    - User personas, use cases

  Tech Lead responsibilities:
    - Break down stories en tasks técnicas
    - Estimación
    - Feasibility discussion
    - Acceptance criteria técnica

  Split de tiempo:
    - 40% PM presenta (context, requirements)
    - 60% Tech Lead facilita (breakdown, estimation)

Scenario 3: Large team (PM + multiple POs)
  PM: Strategic refinement (quarterly, roadmap-level)
  PO: Tactical refinement (bi-weekly, sprint-level)

  PM Quarterly Refinement (1x/quarter, 2 hours):
    - Presenta roadmap próximos 3-6 meses
    - Epics breakdown en features
    - Tech Lead da T-shirt sizing (S/M/L/XL)

  PO Bi-Weekly Refinement (2x/sprint, 1 hour):
    - Presenta stories para próximos 1-2 sprints
    - Detailed acceptance criteria
    - Team da story point estimation
```

---

**3.2. Stories no "Ready" para Planning**

**Problema**:

- Refinement no asegura que stories estén "Ready"
- En Planning, se pierde tiempo discutiendo stories mal definidas
- No hay Definition of Ready clara

**Impacto**:

- Sprint Planning toma >4 horas (debería ser 2-3h)
- Stories se completan mid-sprint porque faltan details
- Re-work y desperdicio

**Solución propuesta**:

```yaml
Definition of Ready (DoR):

Una story está "Ready" para Planning si cumple:

✅ 1. INVEST criteria:
  - Independent: No depende de otras stories en mismo sprint
  - Negotiable: Details pueden ajustarse
  - Valuable: Entrega valor al usuario o negocio
  - Estimable: Equipo puede estimar (tiene suficiente info)
  - Small: Cabe en 1 sprint (max 8-13 points)
  - Testable: Tiene acceptance criteria clara

✅ 2. Acceptance Criteria clara:
  - Formato "Given/When/Then" (Gherkin style)
  - Ejemplo:
    Given: User is logged in
    When: User clicks "Reset Password"
    Then: Email is sent within 2 minutes
    And: User sees confirmation message

✅ 3. Designs completos (si aplica):
  - High-fidelity mockups en Figma
  - Interactive prototype (para flows complejos)
  - Design handoff completo (specs, assets)

✅ 4. Dependencies identificadas:
  - ¿Requiere API de otro equipo? (confirmado que estará ready)
  - ¿Requiere infra changes? (DevOps notificado)
  - ¿Requiere third-party integration? (API keys, sandbox access)

✅ 5. Technical spike completado (si necesario):
  - Proof of concept hecho
  - Unknowns resueltos
  - Approach técnico acordado

Refinement Process con DoR:

Refinement Session 1 (week before Planning):
  1. PO presenta stories (30 min)
  2. Team hace preguntas, identifica gaps (20 min)
  3. PO asigna "Ready" label a stories que cumplen DoR (10 min)

Between Refinement 1 y Planning:
  4. PO completa gaps:
     - Escribe acceptance criteria faltante
     - Confirma dependencies
     - Obtiene designs (si faltan)

  5. Tech Lead hace spike si hay unknowns técnicos

Refinement Session 2 (2-3 days before Planning):
  6. Re-review de stories (30 min)
  7. Final estimation (30 min)
  8. Mark stories como "Ready for Planning"

Sprint Planning:
  - Solo se discuten stories marcadas "Ready"
  - Si story no está Ready → Se saca del sprint
  - Goal: Planning en <3 horas (no 4-5h)
```

---

### 4. Sprint Review

#### Vacíos Detectados

**4.1. Stakeholders no definidos claramente**

**Problema**:

- ¿Quién debe asistir a Sprint Review?
- ¿Cómo se invita a stakeholders externos (Sales, Marketing, CS)?
- ¿Qué pasa si stakeholders clave no pueden asistir?

**Impacto**:

- Reviews con poca audiencia (solo equipo interno)
- Feedback de stakeholders llega tarde (después de release)
- Re-work porque no se validó con usuarios/business

**Solución propuesta**:

```yaml
Sprint Review Stakeholder Matrix:

Obligatorio (Must Attend):
  - Product Owner / Product Manager
  - Development Team (presentan su trabajo)
  - QA Engineer (valida que features funcionan)
  - Tech Lead (facilita, Q&A técnico)

Altamente Recomendado (Should Attend):
  - UX/UI Designer (valida que diseño se implementó bien)
  - Engineering Manager (context de roadmap)
  - Customer Success Lead (representa voz del cliente)

Opcional pero Valioso (Nice to Have):
  - Sales Engineer (valida features para demos a clientes)
  - Marketing (para launch communications)
  - Data Analyst (discute metrics tracking)
  - C-suite (CEO, CPO, CTO) - para releases grandes

Stakeholder Invitation Process:

2 semanas antes:
  - PO identifica stakeholders relevantes para features del sprint
  - Ejemplo: Si sprint incluye "Checkout optimization" → Invite Sales, CS

1 semana antes:
  - PO envía calendar invite con:
      - Agenda (qué features se demostrarán)
      - Objetivo (qué feedback se busca)
      - Duration (1 hora max)

3 días antes:
  - PO envía reminder con preview:
      - Screenshots o video corto (1-2 min)
      - Context: Problem solved, user impact

Día de Review:
  - Recording automático (para stakeholders que no pudieron asistir)
  - Q&A notes documentadas en Confluence

Post-Review:
  - Recording + notes enviados a stakeholders ausentes
  - Feedback deadline: 48 horas post-review

Format de Review (1 hora):
  0-5 min: PO presenta sprint goal y context
  5-40 min: Demos (cada feature 3-5 min)
  40-55 min: Q&A y feedback
  55-60 min: Wrap-up, next steps
```

---

**4.2. Demo environment no confiable**

**Problema**:

- Demos fallan porque staging está roto
- "Demo effect" (funciona en dev, falla en demo)
- No hay smoke tests antes de review

**Impacto**:

- Tiempo perdido en review (debugging en vivo)
- Stakeholders pierden confianza
- Equipo se ve mal

**Solución propuesta**:

```yaml
Demo Readiness Process:

Day before Review (Thursday):
  1. QA runs smoke tests en staging (1 hora)
     - Happy paths de todas las features a demostrar
     - Edge cases críticos

  2. Si staging está roto:
     - DevOps fix immediately (priority P1)
     - Si no fixable: Demo en local environment (backup plan)

  3. Developers preparan demo script:
     - ¿Qué usuario/data usar?
     - Step-by-step flow
     - Screenshots de fallback (si demo falla en vivo)

Morning of Review (Friday 8 AM):
  4. Final smoke test (30 min)
     - QA re-valida staging
     - Developers practican demo (dry-run)

  5. Backup plan si staging down:
     - Use recorded video (pre-grabado day before)
     - Or demo en local con screen share

During Review:
  6. If demo fails:
     - Switch to recorded video (no intentar fix en vivo)
     - Explain issue (transparencia)
     - Show alternative proof (screenshots, video)

Demo Environment Best Practices:
  - Staging should mirror production (same infra)
  - Separate demo database (no production data)
  - Automated smoke tests (run every 2 hours)
  - Monitoring alerts for staging (detect issues early)
```

---

### 5. Sprint Retrospective

#### Vacíos Detectados (CRÍTICO)

**5.1. Action items sin follow-up**

**Problema**:

- Retro identifica mejoras ("Mejorar code review speed")
- Action items se documentan
- **Nadie hace follow-up**: Action items se olvidan
- Próxima retro: Mismos problemas

**Impacto**:

- Equipo pierde confianza en retrospectives (waste of time)
- Problemas se repiten sprint tras sprint
- Frustración y cinismo

**Solución propuesta** (IMPLEMENTAR URGENTE):

```yaml
Retrospective Action Item Accountability:

Durante Retro (Last 15 min):
  1. Equipo vota top 3 action items (más impacto)
  2. Para cada action item:
     - Assign Owner (persona específica, no "el equipo")
     - Define Definition of Done (¿Cómo sabemos que está hecho?)
     - Set Timeline (próximo sprint, 2 sprints, etc.)

  Example:
    ❌ Bad: "Mejorar code reviews"
    ✅ Good:
      Action: "Reduce code review time from 2 days to <8 hours"
      Owner: Sarah (Tech Lead)
      DoD: 80% of PRs reviewed within 8 hours (measured in GitHub)
      Timeline: Next sprint (2 weeks)

Post-Retro (same day):
  3. Tech Lead creates Jira tickets para cada action item:
     - Label: "retro-action"
     - Assigned to owner
     - Due date según timeline

  4. Tech Lead adds action items al Sprint Backlog:
     - Treated como user stories (tienen story points)
     - Commitment: At least 1 action item per sprint

Weekly Check-in (During Standups):
  5. Viernes standup: Quick update on action items
     - Owner reports progress (1 min cada uno)
     - If blocked: Escalate immediately

Next Retro (2 weeks later):
  6. First agenda item: Review previous action items (15 min)
     - ✅ Completed: Celebrate, measure impact
     - 🔄 In Progress: Continue, adjust timeline
     - ❌ Not Started: Why? Re-prioritize or drop

  7. Metrics tracking:
     - % of action items completed (target: >70%)
     - If <50%: Root cause analysis (too many items? Unrealistic? Lack of ownership?)

Action Item Retirement:
  - If action item no completado en 3 sprints:
    - Re-evaluate: ¿Sigue siendo importante?
    - If yes: Escalar (Engineering Manager involvement)
    - If no: Close (don't carry dead weight)

Accountability Escalation:
  - If owner consistently no completa action items:
    - 1:1 con Engineering Manager (coaching)
    - Re-assign to someone con más capacity
```

**Esto es CRÍTICO**: Retrospectives sin follow-up son waste of time. Implementar este proceso immediately.

---

**5.2. Retro format repetitivo (fatiga)**

**Problema**:

- Siempre mismo formato ("What went well / What didn't")
- Equipo se aburre, participa menos
- Insights superficiales

**Impacto**:

- Baja participación
- No se descubren root causes
- Retros se vuelven checkbox exercise

**Solución propuesta**:

```yaml
Retrospective Format Rotation (cada sprint diferente):

Sprint 1: Start/Stop/Continue
  - Start: ¿Qué deberíamos empezar a hacer?
  - Stop: ¿Qué deberíamos dejar de hacer?
  - Continue: ¿Qué está funcionando bien?

Sprint 2: Sailboat Retrospective
  - ⛵ Sailboat = Equipo
  - 💨 Wind = Qué nos impulsa (positivo)
  - ⚓ Anchor = Qué nos frena (negativo)
  - 🏝️ Island = Nuestro goal
  - 🪨 Rocks = Riesgos adelante

Sprint 3: 4 Ls (Liked, Learned, Lacked, Longed For)
  - Liked: Qué nos gustó
  - Learned: Qué aprendimos
  - Lacked: Qué nos faltó
  - Longed For: Qué deseamos para el futuro

Sprint 4: Mad/Sad/Glad
  - 😠 Mad: Qué nos frustró
  - 😢 Sad: Qué nos decepcionó
  - 😊 Glad: Qué nos alegró

Sprint 5: Timeline Retrospective
  - Draw timeline del sprint
  - Team marca eventos significativos (highs/lows)
  - Discuss patterns

Sprint 6: Five Whys (Root Cause Analysis)
  - Pick el problema más votado
  - Ask "Why?" 5 veces para llegar a root cause
  - Example:
    Problem: "PRs tardan 2 días en revisarse"
    Why? → "Reviewers están ocupados"
    Why? → "Muchas features en paralelo"
    Why? → "Overcommitment en planning"
    Why? → "Pressure de Product para entregar rápido"
    Why? → "No hay alignment en capacity vs roadmap"
    Root cause: Falta capacity planning colaborativo (PM + EM)

Facilitator Rotation:
  - Tech Lead no siempre facilita
  - Rotar facilitator cada sprint (desarrolla skills)
  - External facilitator (Scrum Master, EM) cada quarter (fresh perspective)
```

---

## 🎯 Recomendaciones Priorizadas

### Críticas (Implementar AHORA - próximos 7 días)

1. **Retrospective Action Item Accountability System**

   - **Owner**: Tech Lead (cada equipo)
   - **Effort**: 2 horas (setup Jira template + training)
   - **Impact**: ⭐⭐⭐⭐⭐ (multiplica efectividad de retros)

2. **Definition of Ready (DoR) para Planning**
   - **Owner**: Product Owner + Tech Lead
   - **Effort**: 1 sprint (documentar + validar con equipo)
   - **Impact**: ⭐⭐⭐⭐ (reduce planning time 30-40%)

### Alta Prioridad (Implementar en próximos 30 días)

3. **Pre-Planning Dependency Check Process**

   - **Owner**: Tech Lead
   - **Effort**: 2 sprints (pilot + refine)
   - **Impact**: ⭐⭐⭐⭐ (reduce blockers mid-sprint 50%+)

4. **Tech Debt Budget (20% rule)**

   - **Owner**: Engineering Manager + Tech Lead
   - **Effort**: 1 sprint (policy + process)
   - **Impact**: ⭐⭐⭐⭐ (mejora velocity long-term)

5. **QA-Inclusive Estimation Model**

   - **Owner**: QA Engineer + Tech Lead
   - **Effort**: 2 sprints (change habit)
   - **Impact**: ⭐⭐⭐ (reduce QA bottleneck)

6. **Sprint Review Stakeholder Matrix**
   - **Owner**: Product Manager
   - **Effort**: 1 semana (documentar + comunicar)
   - **Impact**: ⭐⭐⭐ (mejor feedback loop)

### Media Prioridad (Implementar en próximos 60 días)

7. **Standup Facilitation Model** (definir backup)

   - **Owner**: Tech Lead
   - **Effort**: 1 sprint
   - **Impact**: ⭐⭐ (evita standup skips)

8. **Demo Readiness Process**

   - **Owner**: QA Engineer + DevOps
   - **Effort**: 2 sprints
   - **Impact**: ⭐⭐⭐ (reduce demo failures)

9. **Retro Format Rotation**
   - **Owner**: Tech Lead (facilitator)
   - **Effort**: Ongoing (cada sprint diferente)
   - **Impact**: ⭐⭐ (mejora engagement)

### Baja Prioridad (Nice to have)

10. **Velocity Tracking Dashboard**
    - **Owner**: Engineering Manager
    - **Effort**: 1 semana (Jira/Linear config)
    - **Impact**: ⭐ (útil para long-term planning)

---

## 📋 RACI: Responsabilidades de Ceremonias

### Daily Standup

| Actividad                | TL  | Dev | QA  | PO/PM | EM  | DevOps |
| ------------------------ | --- | --- | --- | ----- | --- | ------ |
| **Facilitar standup**    | R/A | C   | C   | I     | I   | I      |
| **Participar (updates)** | R   | R   | R   | C     | I   | C      |
| **Timeboxing**           | R/A | I   | I   | I     | I   | I      |
| **Anotar blockers**      | R/A | C   | C   | I     | I   | C      |
| **Resolver blockers**    | A   | R   | R   | C     | C   | R      |

### Sprint Planning

| Actividad                 | TL  | Dev | QA  | PO/PM | EM  | Design |
| ------------------------- | --- | --- | --- | ----- | --- | ------ |
| **Presentar prioridades** | C   | C   | I   | R/A   | C   | I      |
| **Definir Sprint Goal**   | C   | C   | C   | R/A   | C   | I      |
| **Capacity planning**     | R/A | C   | C   | C     | C   | I      |
| **Story breakdown**       | R   | R   | C   | C     | I   | C      |
| **Estimation**            | A   | R   | R   | I     | I   | I      |
| **Dependency check**      | R/A | C   | C   | C     | I   | C      |
| **Commitment decision**   | A   | C   | C   | C     | C   | I      |

### Backlog Refinement

| Actividad                       | TL  | Dev | QA  | PO/PM | Design |
| ------------------------------- | --- | --- | --- | ----- | ------ |
| **Presentar stories**           | C   | I   | I   | R/A   | C      |
| **Clarify acceptance criteria** | C   | C   | C   | R/A   | C      |
| **Technical feasibility**       | R/A | R   | C   | C     | C      |
| **Estimation**                  | A   | R   | R   | I     | I      |
| **Definition of Ready check**   | R   | C   | C   | A     | C      |

### Sprint Review

| Actividad                       | TL  | Dev | QA  | PO/PM | Stakeholders | EM  |
| ------------------------------- | --- | --- | --- | ----- | ------------ | --- |
| **Facilitar Review**            | R/A | C   | C   | C     | I            | I   |
| **Presentar features**          | A   | R   | C   | C     | I            | I   |
| **Validar acceptance criteria** | C   | C   | R   | A     | I            | I   |
| **Recopilar feedback**          | C   | C   | C   | R/A   | R            | C   |
| **Invitar stakeholders**        | C   | I   | I   | R/A   | I            | C   |

### Sprint Retrospective

| Actividad                    | TL  | Dev | QA  | PO/PM | EM  |
| ---------------------------- | --- | --- | --- | ----- | --- |
| **Facilitar Retro**          | R/A | C   | C   | C     | C   |
| **Participar (insights)**    | R   | R   | R   | R     | C   |
| **Identificar action items** | C   | R   | R   | R     | C   |
| **Assign owners**            | A   | C   | C   | C     | C   |
| **Follow-up action items**   | R/A | R   | R   | R     | C   |
| **Escalate blockers**        | C   | C   | C   | C     | R/A |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 📈 Métricas de Éxito

Para validar que las mejoras funcionan:

| Métrica                             | Baseline   | Target         | Frecuencia        | Owner  |
| ----------------------------------- | ---------- | -------------- | ----------------- | ------ |
| **Retro action items completed**    | No medido  | >70%           | Por sprint        | TL     |
| **Sprint commitment accuracy**      | No medido  | >80%           | Por sprint        | TL     |
| **Planning duration**               | ~4 horas   | <3 horas       | Por sprint        | PO/PM  |
| **Cross-team blockers**             | No medido  | <2 per sprint  | Por sprint        | TL     |
| **Stories marked "Ready"**          | No medido  | >90%           | Por refinement    | PO     |
| **QA bottleneck (stories waiting)** | No medido  | <3 stories     | Por sprint        | QA     |
| **Demo failures (staging issues)**  | Anecdótico | <1 per quarter | Por review        | DevOps |
| **Sprint goal achieved**            | No medido  | >75%           | Por sprint        | PO/TL  |
| **Velocity stability (±%)**         | No medido  | ±20%           | Rolling 3 sprints | TL     |
| **Team satisfaction (ceremonies)**  | No medido  | >4/5           | Trimestral        | EM     |

---

## 🔗 Links Relacionados

### Documentos de Análisis

- [Análisis de Comunicación](analisis-comunicacion.md) - Gaps en estrategia de comunicación
- [RACI Matrix](RACI.md) - Responsabilidades generales por rol

### Ceremonias Actuales (Base del Análisis)

- [**Ceremonias Ágiles: Documento Principal**](../ceremonias/README.md) - Daily, Planning, Refinement, Review, Retro (839 líneas)

### Otros Procesos Organizacionales

- [Comunicación](../comunicacion/README.md) - Estrategia de comunicación, canales, escalación
- [Workflows](../workflows/README.md) - Procesos de desarrollo y colaboración

### Documentos a Crear (Basados en Recomendaciones)

Estos documentos deberían crearse en `/ceremonias/` para complementar las ceremonias:

1. `ceremonias/retro-action-items.md` - **CRÍTICO**: Accountability system (Recomendación #1)
2. `ceremonias/definition-of-ready.md` - DoR checklist y process completo (Recomendación #2)
3. `ceremonias/dependency-management.md` - Pre-planning dependency check (Recomendación #3)
4. `ceremonias/tech-debt-budget.md` - Policy del 20% + priorización (Recomendación #4)
5. `ceremonias/qa-estimation-guide.md` - QA-inclusive estimation model (Recomendación #5)
6. `ceremonias/stakeholder-matrix.md` - Sprint Review invitations process (Recomendación #6)
7. `ceremonias/standup-facilitation.md` - Modelo de facilitación y backups (Recomendación #7)
8. `ceremonias/demo-readiness.md` - Demo environment smoke tests (Recomendación #8)
9. `ceremonias/retro-formats.md` - 6+ formatos de retrospective (Recomendación #9)

---

**Última actualización**: Diciembre 6, 2025  
**Próxima revisión**: Marzo 2025  
**Owner**: Engineering Manager + Tech Leads

---

## 📝 Apéndice: Templates

### Template: Retrospective Action Item

```markdown
## Action Item: [Título claro y accionable]

**Identified in**: Sprint XX Retrospective (YYYY-MM-DD)

**Problem Statement**:
[Descripción del problema en 2-3 frases]

**Action**:
[Qué específicamente vamos a hacer]

**Owner**: [Nombre específico]

**Definition of Done**:

- [ ] [Criteria 1]
- [ ] [Criteria 2]
- [ ] [Criteria 3]

**Timeline**: [Next sprint / 2 sprints / End of quarter]

**Success Metrics**:
[Cómo mediremos que funcionó]

**Status Updates**:

- Week 1: [Update]
- Week 2: [Update]
```

### Template: Definition of Ready Checklist

```markdown
## Story: [Story Title]

### Definition of Ready Checklist

- [ ] **INVEST criteria met**

  - [ ] Independent
  - [ ] Negotiable
  - [ ] Valuable
  - [ ] Estimable
  - [ ] Small (<13 points)
  - [ ] Testable

- [ ] **Acceptance Criteria** (Given/When/Then format)

  - [ ] Happy path defined
  - [ ] Edge cases identified
  - [ ] Error handling specified

- [ ] **Designs** (if applicable)

  - [ ] High-fidelity mockups in Figma
  - [ ] Design handoff complete
  - [ ] Assets exported

- [ ] **Dependencies**

  - [ ] No blocking dependencies OR dependencies confirmed ready
  - [ ] Infrastructure changes identified (DevOps notified)
  - [ ] Third-party integrations planned (API keys obtained)

- [ ] **Technical Spike** (if needed)
  - [ ] POC completed
  - [ ] Approach agreed upon
  - [ ] Unknowns resolved

**Ready for Planning**: ☐ Yes ☐ No

**Sign-off**:

- Product Owner: [Name] - [Date]
- Tech Lead: [Name] - [Date]
```

---

**End of Analysis**
