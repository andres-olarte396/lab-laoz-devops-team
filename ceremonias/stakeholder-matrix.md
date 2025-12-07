# 👥 Stakeholder Matrix - Sprint Review Invitations

## 📋 Resumen Ejecutivo

**Problema**: Sprint Reviews sin stakeholders claros resulta en:

- Demos a audiencia incorrecta (developers presentando a developers)
- Feedback irrelevante o ausente
- Business stakeholders se quejan "no sabíamos de esto"
- Time wasted en demos que nadie necesitaba ver

**Solución**: **Stakeholder Matrix** con niveles de obligación (Mandatory/Recommended/Optional) y proceso estructurado de invitations.

**Beneficio**:

- Audiencia correcta en cada Sprint Review
- Feedback relevante y accionable
- Alignment entre Tech y Business
- Demos tienen impacto y visibilidad

---

## 🎯 Stakeholder Matrix Concept

### 3 Niveles de Stakeholder

```
┌─────────────────────────────────────────────────┐
│ 🔴 MANDATORY (Obligatorio)                     │
│ Deben asistir, demo no procede sin ellos       │
├─────────────────────────────────────────────────┤
│ 🟡 RECOMMENDED (Recomendado)                    │
│ Deberían asistir, aportan valor pero no crítico│
├─────────────────────────────────────────────────┤
│ 🟢 OPTIONAL (Opcional)                          │
│ Pueden asistir si tienen interés                │
└─────────────────────────────────────────────────┘
```

---

## 👥 Stakeholder Roles y Niveles

### 🔴 MANDATORY Stakeholders

#### 1. **Product Owner**

- **Por Qué**: Acepta o rechaza el work done, prioriza siguiente sprint
- **Responsibilities en Review**:
  - ✅ Validar que stories cumplen Acceptance Criteria
  - ✅ Dar feedback inmediato (accept/reject)
  - ✅ Ajustar prioridades para siguiente sprint

**Si No Asiste**: Sprint Review se cancela o postpone

---

#### 2. **Engineering Manager** (del equipo que presenta)

- **Por Qué**: Visibility en progress, puede remover blockers, representa a Engineering en decisiones
- **Responsibilities en Review**:
  - ✅ Entender technical challenges del sprint
  - ✅ Identificar cross-team dependencies
  - ✅ Escalar blockers si necesario

**Si No Asiste**: Tech Lead puede representar, pero es subóptimo

---

#### 3. **Key Business Stakeholder** (varía por feature)

- **Quién**: Depende del feature

  - Revenue feature → CFO o VP Sales
  - Compliance feature → Legal o Compliance Officer
  - Customer-facing → Customer Success Lead

- **Por Qué**: Necesitan ver progress en iniciativas críticas de negocio

**Si No Asiste**:

- Si feature es board-level priority → re-schedule Review
- Si no → proceder, pero enviar recording después

---

### 🟡 RECOMMENDED Stakeholders

#### 4. **Design Lead** (si hubo UI changes)

- **Por Qué**: Validar que implementación sigue diseños
- **Feedback Esperado**:
  - Spacing, colors, typography correctos
  - Interactions como se diseñaron
  - Edge cases visuales manejados

**Si No Asiste**: Designer puede review async via recording

---

#### 5. **Tech Leads de Equipos Relacionados**

- **Ejemplos**:

  - Backend Team (si Frontend team presenta integración)
  - DevOps Team (si cambio requiere infra)
  - Mobile Team (si API nueva afecta mobile)

- **Por Qué**: Awareness de cambios que impactan sus áreas
- **Feedback Esperado**: Identificar integration issues o dependencies

**Si No Asiste**: Send meeting notes + recording

---

#### 6. **Customer Success / Support Lead**

- **Por Qué**: Features afectan customer experience, necesitan saber qué comunicar a clientes
- **Feedback Esperado**:
  - ¿Cómo explico esto a customers?
  - ¿Hay edge cases que causarán support tickets?
  - ¿Necesitamos FAQ o docs?

**Si No Asiste**: Send demo video + release notes

---

### 🟢 OPTIONAL Stakeholders

#### 7. **Marketing Team**

- **Cuándo Invitar**: Feature es customer-facing y market-worthy
- **Feedback Esperado**: "¿Podemos hacer campaign sobre esto?"

---

#### 8. **Sales Team**

- **Cuándo Invitar**: Feature es differentiator competitivo
- **Feedback Esperado**: "¿Cómo sell esto a prospects?"

---

#### 9. **C-Level Executives** (CEO, CTO, CPO)

- **Cuándo Invitar**:
  - Board-level priority feature
  - Company all-hands demo
  - Quarterly review

**Nota**: No invitar a CADA Sprint Review (executives no tienen tiempo)

---

#### 10. **Developers de Otros Equipos** (open invitation)

- **Por Qué**: Knowledge sharing, aprender de otros equipos
- **Open Door Policy**: Cualquier dev puede asistir

---

## 📅 Invitation Process & Timeline

### L-10: Identify Stakeholders (2 semanas antes de Review)

**Owner**: Product Owner + Tech Lead

**Actividades**:

1. **Review Sprint Goal y Features Completadas**

   - "Este sprint entregamos: User login, Product filtering, Checkout flow"

2. **Identify Stakeholders por Feature**

Template:

```markdown
## Sprint 24 Review - Stakeholder Matrix

**Date**: Dec 13, 2024, 2pm-3pm
**Location**: Zoom [link] + Conf Room A

### Features to Demo

#### Feature 1: User Login con Google OAuth

**Business Impact**: Reduce friction en signup (target: +20% conversion)

**Stakeholders**:

- 🔴 MANDATORY:

  - Product Owner (@jane.po)
  - Engineering Manager (@john.em)
  - VP Product (@vp.product) - board priority

- 🟡 RECOMMENDED:

  - Design Lead (@alice.design) - validar UI
  - Customer Success (@cs.lead) - customer impact

- 🟢 OPTIONAL:
  - Marketing (@marketing.lead) - potential campaign

#### Feature 2: Product Filtering

**Business Impact**: Improve search experience (target: reduce search time 50%)

**Stakeholders**:

- 🔴 MANDATORY:

  - Product Owner (@jane.po)
  - Engineering Manager (@john.em)

- 🟡 RECOMMENDED:

  - Backend Tech Lead (@backend.lead) - API integration
  - QA Lead (@qa.lead) - testing feedback

- 🟢 OPTIONAL:
  - Open to all teams
```

3. **Send Save-the-Date** (L-10, 2 semanas antes)

**Slack Message** (to #sprint-reviews channel):

```
📅 Sprint 24 Review - Save the Date

**When**: Dec 13, 2pm-3pm (1h)
**Where**: Zoom [link] + Conf Room A

**What We'll Demo**:
- ✅ User login con Google OAuth (BOARD PRIORITY)
- ✅ Product filtering by price/category
- ✅ Checkout flow optimization

**Mandatory Attendees** (please block calendar):
@jane.po @john.em @vp.product

**Recommended** (please try to attend):
@alice.design @cs.lead @backend.lead @qa.lead

**Optional** (open invitation):
All teams welcome!

Formal invite coming L-7 (1 week before) with agenda.

cc @team
```

---

### L-7: Send Formal Invitation (1 semana antes)

**Owner**: Scrum Master o Tech Lead

**Actividades**:

1. **Create Calendar Invite**

   - Title: "Sprint 24 Review - User Login + Product Filtering"
   - Date/Time: Dec 13, 2pm-3pm
   - Location: Zoom link + Conf Room A
   - Attendees:
     - **Required**: Mandatory stakeholders
     - **Optional**: Recommended + Optional stakeholders

2. **Include Agenda en Calendar Invite**

```markdown
## Sprint 24 Review Agenda

**Total Time**: 1 hour

### Agenda

**1. Sprint Overview** (5 min) - Tech Lead

- Sprint goal recap
- Metrics: Velocity, completion rate

**2. Feature Demos** (40 min)

**Demo 1: User Login con Google OAuth** (15 min)

- Presenter: @developer.alice
- Business context: Reduce signup friction, +20% conversion target
- Live demo: Login flow end-to-end
- Q&A: 5 min

**Demo 2: Product Filtering** (15 min)

- Presenter: @developer.bob
- Business context: Improve search, -50% search time
- Live demo: Filter by price, category, combined
- Q&A: 5 min

**Demo 3: Checkout Optimization** (10 min)

- Presenter: @developer.charlie
- Business context: Reduce cart abandonment -10%
- Live demo: Simplified checkout flow
- Q&A: 3 min

**3. Feedback & Discussion** (10 min)

- Open floor: Questions, concerns, suggestions
- Prioritization for next sprint

**4. Retrospective Highlights** (5 min) - Optional

- What went well
- What to improve
- Action items from retro

### Preparation

- All demos in STAGING environment
- Backup plan: Pre-recorded videos if live demo fails
- Test accounts available for attendees to try

### Attendance

🔴 **Mandatory**: @jane.po @john.em @vp.product
🟡 **Recommended**: @alice.design @cs.lead @backend.lead
🟢 **Optional**: Open to all
```

3. **Send Confirmation Request**

**Slack** (to Mandatory stakeholders individually):

```
Hi @vp.product,

You're invited to Sprint 24 Review (Dec 13, 2pm).

We'll demo **User Login con Google OAuth** - board priority feature.
Your feedback is critical for go/no-go decision.

Can you confirm attendance? If not, we can re-schedule.

Calendar invite: [link]
Agenda: [confluence link]

Thanks!
```

---

### L-3: Confirmation Check (3 días antes)

**Owner**: Scrum Master

**Actividades**:

1. **Check Calendar Responses**

   - ✅ Mandatory stakeholders accepted?
   - ⚠️ Any declines?

2. **Escalate if Mandatory Declines**

**If VP Product declines**:

```
Slack to VP Product:

Hi @vp.product,

I see you declined Sprint 24 Review.

This demo includes **User Login OAuth** (board priority).
We need your sign-off to proceed to production.

Options:
A) Re-schedule to Dec 14 (your availability?)
B) Async review via recording (sub-optimal)
C) Delegate to @product.director with authority to approve

Which works for you?
```

3. **Remind Recommended Stakeholders**

**Slack**:

```
🔔 Reminder: Sprint 24 Review in 3 days

**When**: Dec 13, 2pm-3pm
**Zoom**: [link]

Agenda attached. Looking forward to your feedback!

@alice.design @cs.lead @backend.lead @qa.lead
```

---

### L-1: Final Prep (1 día antes)

**Owner**: Team presenting

**Actividades**:

1. **Smoke Test Demos** (ver [Demo Readiness](demo-readiness.md))

   - Verify staging environment works
   - Test all demo flows
   - Backup: Pre-record videos

2. **Send Final Reminder**

**Slack** (to all attendees):

```
📢 Tomorrow: Sprint 24 Review

**When**: Dec 13, 2pm-3pm (1h)
**Zoom**: [link]
**Conf Room**: Room A (for in-office attendees)

**What to Expect**:
- 3 feature demos (User Login, Filtering, Checkout)
- Live Q&A
- Your feedback shapes next sprint priorities

**Test Accounts** (if you want to try features):
- Username: demo@example.com
- Password: Demo123!

See you tomorrow! 🚀
```

---

### Day 0: Sprint Review Execution

**During Review**:

1. **Record Session** (always)

   - For attendees who couldn't make it
   - For async review by executives
   - For onboarding future team members

2. **Take Notes** (designated note-taker)

   - Feedback per feature
   - Action items
   - Decisions made (go/no-go, prioritization)

3. **Parking Lot** (for deep technical discussions)
   - "Let's discuss infrastructure details offline"
   - Schedule follow-up with specific stakeholders

---

### Post-Review: Follow-up (Same day)

**Owner**: Scrum Master or Tech Lead

**Actividades**:

1. **Send Meeting Notes + Recording**

**Email** (to all invitees + absentees):

```
Subject: Sprint 24 Review - Notes & Recording

Hi team,

Thanks for attending Sprint 24 Review!

**Recording**: [link]
**Slides**: [link]
**Meeting Notes**: [confluence link]

**Key Decisions**:
✅ User Login OAuth approved for production (go-live: Dec 15)
✅ Product Filtering needs design tweaks (alice.design to update mockups)
⚠️ Checkout flow: Legal review required before prod (legal.lead to review by Dec 14)

**Action Items**:
- [ ] @alice.design: Update filter UI (spacing issue) - Due: Dec 14
- [ ] @legal.lead: Review checkout flow compliance - Due: Dec 14
- [ ] @devops.lead: Setup OAuth prod environment - Due: Dec 15

**Feedback Summary**:
- VP Product: "Great progress! OAuth is game-changer for conversion."
- CS Lead: "Need FAQ for customers about Google data privacy" → Action: PO to create
- Backend Lead: "API performance looks good, no concerns"

**Next Sprint Preview**:
Top priorities for Sprint 25:
1. Payment integration (Stripe)
2. Email notifications
3. Admin dashboard

Next Review: Dec 27, 2pm

Questions? Let me know!

Thanks,
Tech Lead
```

2. **Update Jira Stories**

   - Mark approved stories as "Ready for Production"
   - Create follow-up tasks for feedback (ej: "Update filter UI spacing")

3. **Stakeholder Follow-up** (if needed)

**For Absentees** (if they were Mandatory):

```
Slack to @vp.product:

Hi, you missed Sprint 24 Review due to conflict.

Here's 2-min summary:
- User Login OAuth: DONE, ready for prod ✅
- Needs your approval to go-live Dec 15

Recording: [link] (skip to 10:20 for OAuth demo)

Can you approve by EOD? Or should we hold off?
```

---

## 📊 Stakeholder Engagement Metrics

### Metric #1: Attendance Rate

**Formula**:

```
(Stakeholders who attended / Stakeholders invited) × 100
```

**Targets**:

- Mandatory: 100% (or re-schedule)
- Recommended: >70%
- Optional: >30%

**Red Flags**:

- Mandatory <100% → Reviews no tienen decisiones, waste de tiempo
- Recommended <50% → Reviews no tienen feedback relevante

---

### Metric #2: Feedback Quality Score

**Subjetivo, team vota 1-5**:

- 5 = Feedback accionable, decisiones claras (ej: "Approved for prod")
- 3 = Feedback genérico ("Looks good")
- 1 = No feedback o irrelevante

**Target**: Avg >3.5

**Red Flag**:

- Avg <2.5 → Wrong stakeholders en la sala

---

### Metric #3: Action Items per Review

**Formula**:

```
# Action items generados en Sprint Review
```

**Target**: 2-5 action items

**Insight**:

- 0 action items → No feedback útil, waste de tiempo
- > 10 action items → Demo reveló muchos problemas (red flag en quality)

---

### Metric #4: Time to Production (Post-Review)

**Formula**:

```
Days desde Review hasta Production Deploy
```

**Target**: <3 días

**Insight**:

- Si >7 días → Review no está generando decisiones rápidas, blockers post-review

---

## 🎭 Roles y Responsabilidades

### Product Owner

**L-10 (2 semanas antes)**:

- ✅ Identificar business stakeholders (quién DEBE ver qué feature)
- ✅ Confirmar asistencia de Mandatory stakeholders

**Durante Review**:

- ✅ Presentar business context de cada feature
- ✅ Decidir: Approved for prod / Needs changes / Rejected
- ✅ Priorizar feedback para siguiente sprint

**Post-Review**:

- ✅ Comunicar decisiones a stakeholders externos (Sales, Marketing, CS)

---

### Tech Lead / Scrum Master

**L-10**:

- ✅ Crear Stakeholder Matrix con PO
- ✅ Send save-the-date

**L-7**:

- ✅ Send formal calendar invite con agenda

**L-3**:

- ✅ Confirmation check, escalate declines
- ✅ Remind recommended stakeholders

**L-1**:

- ✅ Final reminder
- ✅ Verify demos ready (smoke test)

**Durante Review**:

- ✅ Facilitar sesión (timebox, mantener focus)
- ✅ Take notes (o designar note-taker)
- ✅ Parking lot para deep dives técnicos

**Post-Review**:

- ✅ Send notes + recording
- ✅ Create action items en Jira
- ✅ Follow up con absentees

---

### Developers (Presenters)

**L-3**:

- ✅ Preparar demo script (qué mostrar, qué decir)
- ✅ Ensayar demo (15 min run-through)

**L-1**:

- ✅ Smoke test demo en staging
- ✅ Pre-record backup video

**Durante Review**:

- ✅ Presentar demo (10-15 min por feature)
- ✅ Responder Q&A técnico

---

### Stakeholders (Attendees)

**Durante Review**:

- ✅ Dar feedback específico y accionable
- ✅ Hacer decisiones (approve/reject/needs-work)
- ✅ Identify blockers o concerns

**Post-Review**:

- ✅ Review recording si no pudieron asistir
- ✅ Respond a follow-up actions

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup

**Week 1**:

- [ ] PO + Tech Lead crean Stakeholder Matrix template
- [ ] Identificar stakeholders por tipo de feature
- [ ] Document en Confluence

**Week 2**:

- [ ] Comunicar proceso a stakeholders
- [ ] "From now on, Sprint Reviews tendrán invitations 2 semanas antes"
- [ ] Trial run con próximo Sprint Review

---

### Sprint 1-3: Iterate

- [ ] Ejecutar proceso end-to-end
- [ ] Track attendance rate y feedback quality
- [ ] Ajustar Stakeholder Matrix basado en learnings

---

### Sprint 4+: Optimize

- [ ] Attendance rate >70% (Recommended)
- [ ] Feedback quality score >3.5
- [ ] Process es hábito

---

## ✅ Success Criteria

### Mes 1

- ✅ Stakeholder Matrix creado
- ✅ Invitations enviadas L-10, L-7, L-3
- ✅ Mandatory attendance 100%

### Mes 2-3

- ✅ Recommended attendance >70%
- ✅ Feedback quality score >3.5
- ✅ Action items tracked en Jira

### Mes 4+

- ✅ Stakeholders proactivamente preguntan "Cuándo es la próxima Review?"
- ✅ Business alignment mejorado (stakeholders saben qué está pasando)
- ✅ Faster time-to-production (<3 días post-review)

---

## 🔗 Links Relacionados

- [Ceremonias: Sprint Review](README.md#sprint-review) - Ceremonia principal
- [Demo Readiness](demo-readiness.md) - Cómo preparar demos
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

## 📚 Antipatterns

### ❌ Antipattern #1: Invitar a Todo el Mundo

**Síntoma**: 50 personas invitadas a Sprint Review

**Por Qué Falla**:

- Audiencia demasiado grande → no hay discusión
- Feedback genérico ("looks good")
- Waste de tiempo de executives

**Solución**: Limit a 10-15 stakeholders, categorize por Mandatory/Recommended/Optional

---

### ❌ Antipattern #2: Invitaciones Last-Minute

**Síntoma**: Invitation enviada 1 día antes de Review

**Por Qué Falla**:

- Stakeholders ya tienen calendar bloqueado
- Low attendance
- No feedback relevante

**Solución**: L-10 save-the-date, L-7 formal invite

---

### ❌ Antipattern #3: No Follow-up

**Síntoma**: Review termina, no hay notes ni action items

**Por Qué Falla**:

- Feedback se pierde
- Decisiones no se ejecutan
- Stakeholders dejan de asistir ("waste de tiempo")

**Solución**: Same-day notes + recording + action items en Jira

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Product Owner + Scrum Master  
**Review Cycle**: Trimestral
