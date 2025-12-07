# 🎤 Standup Facilitation - Ownership & Async Model

## 📋 Resumen Ejecutivo

**Problema**: Daily Standups sin facilitador claro resulta en:

- Meetings que duran 30+ minutos (target: 15min)
- Discussions técnicas profundas (no es el propósito)
- Solo devs hablan, QA/Designer quedan callados
- "Round-robin status updates" sin coordinación real

**Solución**: **Facilitación estructurada** con 3 modelos + **Async Standup Hybrid** (3 días async + 2 días sync).

**Beneficio**:

- Standups son eficientes (15min max)
- Focus en blockers, no status updates
- Team coordinado sin waste de tiempo
- Flexibility para trabajo remoto/distribuido

---

## 🎯 Responsabilidades del Facilitador

### Durante Daily Standup (15 min)

**1. Timebox Enforcement** (⏱️ Critical)

- Start on time (ej: 9:30am sharp)
- 1-2 min por persona MAX
- Cut off discussions: "Let's take this offline"
- End on time (9:45am)

**2. Format Structure**

- Enforce 3 questions:
  1. ¿Qué hiciste ayer? (30 seg)
  2. ¿Qué harás hoy? (30 seg)
  3. ¿Tienes blockers? (30 seg - si hay blocker, 1 min extra)

**3. Blocker Management**

- Capture blockers en tiempo real
- Assign owner para resolver
- Follow up: "Yesterday's blocker (API down) - resolved?"

**4. Inclusión**

- Asegurar que TODOS hablan (dev, QA, designer, PO)
- Si alguien está callado: "@maria, any updates?"

**5. Post-Standup**

- Facilitate "parking lot" discussions (offline)
- Update Jira board con blockers
- Slack summary para remote attendees

---

## 📝 3 Modelos de Facilitación

### **Modelo A: Tech Lead Permanente** (Tradicional)

**Cómo Funciona**:

- Tech Lead facilita TODOS los standups
- Permanent role, no rotation

**Pros**:

- ✅ Consistencia (mismo facilitador siempre)
- ✅ Tech Lead tiene context completo del sprint
- ✅ Puede identificar technical blockers rápidamente

**Cons**:

- ❌ Tech Lead single point of failure (vacaciones, sick days)
- ❌ Team no desarrolla facilitation skills
- ❌ Puede convertirse en "report to Tech Lead" (anti-pattern)

**Best For**: Equipos nuevos, junior teams

---

### **Modelo B: Weekly Rotation** (Recomendado)

**Cómo Funciona**:

- Cada semana, un team member diferente facilita
- Rotation schedule publicado en Confluence
- Incluye devs, QA, designer (NO solo devs)

**Rotation Example**:

```
Week 1: Alice (Frontend Dev)
Week 2: Bob (Backend Dev)
Week 3: Charlie (QA Lead)
Week 4: Diana (Designer)
Week 5: Tech Lead
Week 6: [repeat]
```

**Pros**:

- ✅ Ownership compartido (no recae en 1 persona)
- ✅ Team members desarrollan facilitation skills
- ✅ Evita "report to boss" dynamic
- ✅ Resilience (si facilitador falta, próximo en rotation toma over)

**Cons**:

- ❌ Requires onboarding (cómo facilitar bien)
- ❌ Puede ser inconsistente si facilitadores tienen diferentes styles

**Best For**: Equipos maduros, quieren distribuir responsabilidad

**Implementation**:

- Sprint 0: Tech Lead demuestra facilitation (2 semanas)
- Sprint 1: First rotation, Tech Lead da feedback
- Sprint 2+: Rotation autónoma

---

### **Modelo C: Dedicated Scrum Master** (Formal)

**Cómo Funciona**:

- Scrum Master (rol dedicado) facilita TODAS las ceremonias
- Scrum Master NO es developer (full-time role)

**Pros**:

- ✅ Professional facilitation (trained Scrum Master)
- ✅ Devs se enfocan 100% en development
- ✅ Scrum Master puede coach team en Agile practices

**Cons**:

- ❌ Costo: Requiere contratar Scrum Master
- ❌ Scrum Master puede no tener technical context profundo
- ❌ Overkill para equipos pequeños (<5 personas)

**Best For**:

- Equipos grandes (8+ personas)
- Múltiples equipos (1 Scrum Master para 2-3 equipos)
- Organización con budget para Scrum Masters

---

## 🔄 Async Standup Hybrid Model

### Problema con Standups 100% Síncronos

**Pain Points**:

- 15 min × 5 días = 75 min/semana = 5h/mes waste si solo son status updates
- Time zones (equipos distribuidos: NYC, Bangalore, London)
- Interrupciones: Developers en flow state deben parar para standup

**¿Cuándo es necesario sync standup?**

- Planning (Lunes): Alinear en sprint goals
- Mid-sprint check-in (Miércoles): Detectar risks early
- Blockers críticos: Necesitan discusión inmediata

---

### Solución: 3 Async + 2 Sync Días

**Weekly Schedule**:

```
Lunes:    🎤 SYNC Standup (15 min)  - Sprint alignment
Martes:   💬 ASYNC (Slack)          - Status update solo
Miércoles: 🎤 SYNC Standup (15 min)  - Mid-sprint check
Jueves:   💬 ASYNC (Slack)          - Status update solo
Viernes:  🎤 SYNC Standup (15 min)  - Sprint wrap-up, ready for Review

Total: 45 min sync/semana (vs 75 min en modelo tradicional)
Ahorro: 30 min/semana = 2h/mes = 24h/año por equipo
```

---

### Async Standup Process (Martes y Jueves)

**Owner**: Cada team member

**Timeline**: By 10am (o start of day)

**Template en Slack** (#team-standup channel):

```
📅 Async Standup - Dec 10, 2024

**Yesterday**:
- ✅ Completed: TEAM-101 (User login frontend)
- 🚧 In Progress: TEAM-102 (Product filtering UI)

**Today**:
- 🎯 Focus: Finish TEAM-102, start TEAM-103 (Checkout flow)
- ⏰ Estimate: TEAM-102 ready for QA by EOD

**Blockers**:
- ❌ None

**Questions/Help Needed**:
- ❔ @backend.lead can you review API contract for TEAM-103?

**Mood**: 😊 (emoji: 😊 Good / 😐 Meh / 😟 Struggling)
```

**Benefits**:

- ✅ No interrumpir flow state
- ✅ Escribir forces clarity (mejor que verbalizar rápido)
- ✅ Time zone friendly
- ✅ Async = people respond when they can

**Facilitator Role** (even en async):

- Monitor Slack channel by 11am
- Tag blockers: "@tech.lead @alice mentioned API blocker, can you help?"
- If critical blocker → call emergency sync: "Let's hop on Zoom for 10 min"

---

### Sync Standup (Lunes, Miércoles, Viernes)

**Same format as traditional standup**:

- 15 min max
- 3 questions per person
- Focus en coordinación y blockers

**Lunes Focus**: Sprint alignment

- "Este sprint entregamos X, Y, Z"
- Dependencies identificadas

**Miércoles Focus**: Risk detection

- "¿Vamos on track para sprint goals?"
- "¿Algún story en riesgo de spillear?"

**Viernes Focus**: Sprint wrap-up

- "¿Qué está ready para Sprint Review?"
- "¿Qué falta para cerrar el sprint?"

---

## 📊 Métricas de Standup Effectiveness

### Metric #1: Standup Duration

**Target**: ≤15 min (avg de últimos 10 standups)

**Red Flags**:

- > 20 min → Facilitator no hace timebox enforcement
- > 30 min → Team está haciendo technical discussions (wrong forum)

---

### Metric #2: Blocker Resolution Time

**Formula**:

```
Avg días desde blocker identificado → blocker resuelto
```

**Target**: <1 día

**Red Flag**:

- > 3 días → Blockers no tienen ownership, mueren silenciosamente

---

### Metric #3: Attendance Rate

**Formula**:

```
(Attendees / Total team) × 100
```

**Target**: >90%

**Red Flag**:

- <80% → Standups no están agregando valor, team los skip

---

### Metric #4: Team Satisfaction (Survey)

**Question**: "¿Daily standups son útiles?" (1-5 scale)

**Target**: >3.5

**Red Flag**:

- <2.5 → Standups son waste, team los odia

---

## 🎭 Roles y Responsabilidades

### Facilitador (rotación o permanente)

**Pre-Standup**:

- ✅ Review Jira board (identificar work en progress, blockers)
- ✅ Prepare agenda si hay topics especiales (ej: dependency con otro team)

**Durante Standup**:

- ✅ Start on time (no esperar late arrivals >2 min)
- ✅ Enforce 1-2 min per persona
- ✅ Cut off technical discussions: "Let's park this, discuss offline"
- ✅ Capture blockers (write them down)
- ✅ End on time (15 min max)

**Post-Standup**:

- ✅ Update Jira con blockers
- ✅ Facilitate parking lot discussions (offline)
- ✅ Slack summary para remote/absentees

---

### Team Members

**Durante Standup**:

- ✅ Prepararse (saber qué dirán en <2 min)
- ✅ Focus en COORDINATION, no detailed status update
- ✅ Escalate blockers inmediatamente (no esperar 3 días)

**Async Standups**:

- ✅ Post update by 10am en #team-standup
- ✅ Monitor channel para blockers de otros team members

---

### Tech Lead (aún si no facilita)

**Durante Standup**:

- ✅ Listen para technical risks
- ✅ Assign owners a blockers
- ✅ Identify dependencies entre team members

**Post-Standup**:

- ✅ Resolver blockers técnicos
- ✅ Escalate blockers externos (ej: dependency con otro team)

---

## 🚀 Implementation Roadmap

### Sprint 0: Decide Modelo

**Week 1**:

- [ ] Tech Lead + team discuten 3 modelos
- [ ] Votar: A (Tech Lead), B (Rotation), C (Scrum Master)
- [ ] Decide async hybrid: Yes/No

**Week 2**:

- [ ] Comunicar decision al team
- [ ] Si rotation: Crear rotation schedule
- [ ] Si async: Setup #team-standup Slack channel

---

### Sprint 1-2: Pilot

- [ ] Ejecutar nuevo modelo
- [ ] Track metrics: duration, blocker resolution time
- [ ] Survey team: ¿Les gusta? ¿Qué mejorar?

---

### Sprint 3+: Optimize

- [ ] Ajustar basado en feedback
- [ ] Standup duration <15 min consistentemente
- [ ] Team satisfaction >3.5

---

## ✅ Success Criteria

### Mes 1

- ✅ Modelo seleccionado y comunicado
- ✅ Standups duran ≤15 min (90% del tiempo)
- ✅ Attendance >85%

### Mes 2-3

- ✅ Blocker resolution <1 día (avg)
- ✅ Si rotation: Team members confident facilitando
- ✅ Si async hybrid: Team usa Slack channel consistentemente

### Mes 4+

- ✅ Standup duration <15 min (100% del tiempo)
- ✅ Team satisfaction >3.5
- ✅ Blockers identificados early (no surprises en Sprint Review)

---

## 🔗 Links Relacionados

- [Ceremonias: Daily Standup](README.md#daily-standup) - Ceremonia principal
- [Dependency Management](dependency-management.md) - Cómo manejar blockers cross-team
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

## 📚 Antipatterns

### ❌ Antipattern #1: Status Report to Manager

**Síntoma**: Team members miran al Tech Lead al hablar (no al team)

**Por Qué Falla**: Standup se siente como "report to boss", no team coordination

**Solución**: Facilitator dice: "Háblale al TEAM, no a mí"

---

### ❌ Antipattern #2: Technical Deep Dives

**Síntoma**: Standup dura 40 min discutiendo arquitectura

**Por Qué Falla**: Standup es para coordinación, NO para problem-solving

**Solución**: Facilitator interrumpe: "This is important, let's discuss offline con @alice y @bob after standup"

---

### ❌ Antipattern #3: No Blockers Reportados

**Síntoma**: Team siempre dice "No blockers" pero sprint spillea

**Por Qué Falla**: Team no escala blockers por miedo o no entienden qué es blocker

**Solución**: Facilitator pregunta proactivamente: "@charlie, TEAM-101 está en progress 3 días, ¿hay algo bloqueándote?"

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Tech Lead / Scrum Master  
**Review Cycle**: Trimestral
