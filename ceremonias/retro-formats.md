# 🔄 Retrospective Formats - Rotation Catalog

## 📋 Resumen Ejecutivo

**Problema**: Retrospectivas con mismo formato repetitivo resultan en:

- Fatiga: "Otra vez Start/Stop/Continue..."
- Engagement bajo: Team members no participan activamente
- Feedback superficial: Siempre los mismos comments genéricos
- Pérdida de creatividad: No se descubren insights nuevos

**Solución**: **Format Rotation** - Rotar entre 6+ formatos diferentes para mantener engagement y descubrir insights variados.

**Beneficio**:

- Retrospectivas frescas y engaging
- Diferentes formatos revelan diferentes insights
- Team participation aumenta
- Continuous improvement real

---

## 🎯 Cuándo Rotar Formatos

### Rotation Schedule Recomendado

**Opción A: Sprint-by-Sprint Rotation**

```
Sprint 1: Start/Stop/Continue (baseline)
Sprint 2: Sailboat
Sprint 3: 4 Ls (Liked/Learned/Lacked/Longed For)
Sprint 4: Mad/Sad/Glad
Sprint 5: Timeline
Sprint 6: Five Whys
Sprint 7: [Repeat from Sprint 1]
```

**Opción B: Rotation Basada en Context**

```
Sprint normal: Start/Stop/Continue
Sprint post-release: Timeline (analyze whole release)
Sprint con conflictos: Sailboat (identify anchors)
Sprint con bajo morale: Mad/Sad/Glad (emotions)
Sprint exploratorio: 4 Ls (focus en learning)
Sprint con incident: Five Whys (root cause)
```

---

## 📚 6 Formatos de Retrospectiva

---

## 1️⃣ Start / Stop / Continue (Clásico)

### 📖 Overview

**Cuándo Usar**: Default format, good para equipos nuevos o sprints normales

**Duración**: 1 hora

**Best For**:

- Equipos nuevos a retrospectivas
- Sprints estables sin major incidents

---

### 🎯 Format Structure

**3 Categorías**:

1. **START** (🟢 Green Post-its)

   - ¿Qué deberíamos empezar a hacer?
   - New practices, tools, processes

2. **STOP** (🔴 Red Post-its)

   - ¿Qué deberíamos dejar de hacer?
   - Wasteful activities, antipatterns

3. **CONTINUE** (🟡 Yellow Post-its)
   - ¿Qué funciona bien y debemos mantener?
   - Celebrate wins, reinforce good practices

---

### 🔄 Process (60 min)

**1. Set the Stage** (5 min)

- Facilitator explica el format
- Prime directive: "Todos hicieron lo mejor posible con info/skills/resources que tenían"

**2. Gather Data** (15 min)

- Individual brainstorm: Escribir post-its
- 5 min: START items
- 5 min: STOP items
- 5 min: CONTINUE items
- Silencio (no discutir aún)

**3. Group & Vote** (10 min)

- Todos pegan post-its en pizarra (física o Miro/Mural)
- Agrupar duplicados
- Cada persona: 3 votos (dots) para items más importantes

**4. Discuss Top Items** (25 min)

- Discutir top 5-7 items con más votos
- Por cada item (3-5 min):
  - ¿Por qué es importante?
  - ¿Qué acción específica tomaríamos?
  - ¿Quién sería owner?

**5. Create Action Items** (10 min)

- Convertir discussions en 3-5 action items concretos
- Assign owners, DoD, timeline
- Ver [Retro Action Items](retro-action-items.md)

**6. Close** (5 min)

- Review action items
- Facilitator agradece participation
- Anunciar formato de próxima retro

---

### ✅ Ejemplo Output

```markdown
## Sprint 24 Retro - Start/Stop/Continue

### START (3 items con más votos)

1. ✅ Pair programming para stories complejas (8 votos)
   - Owner: Tech Lead
   - Action: Setup weekly pairing schedule
2. ✅ Weekly tech talks (5 votos)

   - Owner: Alice
   - Action: Schedule first tech talk Dec 15

3. ✅ Automated smoke tests pre-demo (4 votos)
   - Owner: QA Lead
   - Action: Create smoke test script

### STOP (2 items)

1. ❌ Long Planning meetings (6 votos)
   - Owner: Scrum Master
   - Action: Timebox Planning to 2h max
2. ❌ Slack notifications después de 7pm (4 votos)
   - Owner: Team Lead
   - Action: Configure Slack Do Not Disturb

### CONTINUE (3 items - celebrate!)

1. 🎉 Daily standup format (async 3 días) (7 votos)
2. 🎉 Code review within 24h (5 votos)
3. 🎉 Team lunches every Friday (4 votos)
```

---

## 2️⃣ Sailboat (Visual Metaphor)

### 📖 Overview

**Cuándo Usar**: Sprint con blockers o cuando team morale está bajo

**Duración**: 1 hora

**Best For**:

- Identificar blockers (anchors)
- Visualizar goals (island)
- Acknowledge risks (rocks)
- Celebrate momentum (wind)

---

### 🎯 Visual Metaphor

```
         ☁️ WIND (What's helping us?)
            |  |  |
         ⛵ SAILBOAT (Our Team)
            |
          ⚓ ANCHOR (What's slowing us?)

🏝️ ISLAND (Goal)                    ⚠️ ROCKS (Risks)
```

**4 Categorías**:

1. **🏝️ ISLAND** (Goal/Destination)

   - ¿Hacia dónde vamos?
   - Sprint goal, quarterly OKRs, vision

2. **☁️ WIND** (Helping Forces)

   - ¿Qué nos impulsa hacia la isla?
   - Good practices, supportive stakeholders, automation

3. **⚓ ANCHOR** (Slowing Forces)

   - ¿Qué nos frena?
   - Tech debt, blockers, distractions

4. **⚠️ ROCKS** (Risks Ahead)
   - ¿Qué peligros vemos en el horizonte?
   - Upcoming dependencies, turnover, budget cuts

---

### 🔄 Process (60 min)

**1. Set the Stage** (5 min)

- Facilitator dibuja sailboat visual
- Explica metaphor

**2. Gather Data** (20 min)

- Individual brainstorm: 5 min por categoría
- Silencio

**3. Group & Present** (15 min)

- Pegar post-its en visual
- Cada persona presenta 1-2 items top

**4. Discuss** (15 min)

- Focus en **ANCHORS** (¿cómo los removemos?)
- Focus en **ROCKS** (¿cómo los evitamos?)

**5. Action Items** (10 min)

- 2-3 actions para remover anchors
- 1-2 actions para mitigate risks

**6. Close** (5 min)

---

### ✅ Ejemplo Output

```markdown
## Sprint 24 Retro - Sailboat

### 🏝️ ISLAND (Goal)

"Ship User Login OAuth + Product Filtering with 0 P1 bugs"

### ☁️ WIND (5 items)

- Async standup model (saves 2h/week)
- QA joined early (caught bugs before dev complete)
- Backend API ready on time (no dependencies blocker)

### ⚓ ANCHOR (3 items - ACTION NEEDED)

1. **Tech debt in auth module** (6 votos)
   - Action: Dedicate 1 sprint to auth refactor
   - Owner: Tech Lead
2. **Slow CI/CD (20 min build)** (5 votos)

   - Action: Parallelize test suite
   - Owner: DevOps Lead

3. **Unclear requirements from PO** (4 votos)
   - Action: Implement DoR checklist
   - Owner: PO + Scrum Master

### ⚠️ ROCKS (2 items)

1. **Key developer leaving next month** (7 votos)
   - Action: Start knowledge transfer now
   - Owner: Tech Lead
2. **Black Friday coming (3x traffic spike)** (5 votos)
   - Action: Load testing sprint
   - Owner: DevOps
```

---

## 3️⃣ 4 Ls (Liked / Learned / Lacked / Longed For)

### 📖 Overview

**Cuándo Usar**: Focus en learning y growth, good para sprints exploratorios

**Duración**: 1 hora

**Best For**:

- New technology adoption
- Post-training sprints
- Teams focused on continuous learning

---

### 🎯 4 Categorías

1. **LIKED** 💚

   - ¿Qué disfrutaste del sprint?
   - Positive experiences

2. **LEARNED** 📚

   - ¿Qué aprendiste?
   - New skills, insights, discoveries

3. **LACKED** ❌

   - ¿Qué faltó?
   - Missing resources, support, clarity

4. **LONGED FOR** 💭
   - ¿Qué desearías?
   - Aspirations, improvements, wishes

---

### ✅ Ejemplo Output

```markdown
## Sprint 24 Retro - 4 Ls

### LIKED 💚

- Pair programming sessions were fun and productive
- Sprint goal was clear and achievable
- Team lunch on Friday

### LEARNED 📚

- OAuth 2.0 implementation (Alice learned from Bob)
- GraphQL queries optimization (tech talk by Charlie)
- Playwright for E2E testing is faster than Selenium

### LACKED ❌

1. **Clear API documentation** (6 votos)
   - Action: Backend creates OpenAPI spec
   - Owner: Backend Lead
2. **Design mockups early in sprint** (4 votos)
   - Action: Designer delivers mockups in Refinement
   - Owner: Design Lead

### LONGED FOR 💭

1. **Dedicated time for learning** (5 votos)
   - Action: Friday afternoons = learning time (20% rule)
   - Owner: Tech Lead
2. **Better test coverage** (4 votos)
   - Action: 20% capacity to test automation
   - Owner: QA Lead
```

---

## 4️⃣ Mad / Sad / Glad (Emotions)

### 📖 Overview

**Cuándo Usar**: Team morale is low, conflicts, post-incident

**Duración**: 1 hour

**Best For**:

- Processing emotions
- Addressing interpersonal issues
- Post-mortem of difficult sprints

---

### 🎯 3 Categorías

1. **MAD** 😠 (Red)

   - ¿Qué te frustró?
   - Anger, frustration, annoyance

2. **SAD** 😢 (Blue)

   - ¿Qué te decepcionó?
   - Disappointment, missed opportunities

3. **GLAD** 😊 (Green)
   - ¿Qué te alegró?
   - Happiness, satisfaction, wins

---

### 🔄 Process (60 min)

**Special Note**: Emotions can be sensitive

**Facilitator Role**:

- Create safe space: "No judgment, all feelings valid"
- Enforce respect: "No blaming individuals"
- Focus on system, not people

**Process**:

1. Set the Stage (10 min) - Emphasize psychological safety
2. Gather Data (15 min) - Anonymous if needed
3. Group (5 min)
4. Discuss (25 min) - Focus on SAD/MAD (resolve emotions)
5. Action Items (10 min) - Address root causes
6. Close (5 min) - End on GLAD notes (positive)

---

### ✅ Ejemplo Output

```markdown
## Sprint 24 Retro - Mad/Sad/Glad

### MAD 😠

1. **Last-minute requirement changes** (8 votos)

   - Root cause: PO didn't finalize requirements in Refinement
   - Action: Enforce DoR checklist
   - Owner: Scrum Master

2. **Production incident on Friday 6pm** (5 votos)
   - Root cause: Deploy without smoke tests
   - Action: Mandatory smoke tests pre-prod deploy
   - Owner: DevOps

### SAD 😢

1. **Missed sprint goal by 5 points** (6 votos)

   - Root cause: Underestimated QA effort
   - Action: Implement QA-inclusive estimation
   - Owner: QA Lead + Tech Lead

2. **No time for tech debt** (4 votos)
   - Action: 20% tech debt budget starting next sprint
   - Owner: Tech Lead

### GLAD 😊 (Celebrate!)

- OAuth feature shipped on time! 🎉
- Zero P1 bugs this sprint ✅
- Team helped Alice when she was blocked 💚
- Friday team lunch was great 🍕
```

---

## 5️⃣ Timeline (Post-Release Reflection)

### 📖 Overview

**Cuándo Usar**: End of release, major milestone, post-incident

**Duración**: 1.5 hours (longer than usual)

**Best For**:

- Analyzing entire release cycle (multi-sprint)
- Understanding cause-and-effect
- Post-mortem of incidents

---

### 🎯 Visual Timeline

```
Week 1    Week 2    Week 3    Week 4
  |---------|---------|---------|
  ⭐        ⚠️        🐛        🎉
Sprint    Blocker   Bug      Ship!
Start     Found     Fixed
```

**Process**:

1. Draw timeline (X-axis = time, Y-axis = mood/energy)
2. Team members add events (post-its on timeline)
3. Identify patterns:
   - When did energy drop? (Why?)
   - When did energy spike? (What worked?)

---

### ✅ Ejemplo Output

```markdown
## Q4 Release Retro - Timeline

### Week 1-2: High Energy ⬆️

- Sprint started strong
- OAuth implementation smooth
- Good collaboration

### Week 3: Energy Drop ⬇️ (WHY?)

- Blocker: Backend API delayed 5 days
- Design changes required rework
- Team frustrated

**Action**: Improve dependency management (L-7 check)

### Week 4: Recovery ⬆️

- Backend unblocked
- Rapid testing by QA
- Shipped on time! 🎉

**Learning**: Buffer time for dependencies (add 20% contingency)
```

---

## 6️⃣ Five Whys (Root Cause Analysis)

### 📖 Overview

**Cuándo Usar**: Post-incident, recurring problems, need deep analysis

**Duración**: 1 hour

**Best For**:

- Root cause analysis
- Systemic issues (not surface-level)
- Incidents or major bugs

---

### 🎯 Five Whys Process

**Start with Problem Statement**:
"Production went down for 2 hours on Friday"

**Ask "Why?" 5 times**:

1. **Why did prod go down?**
   → Database ran out of connections

2. **Why did DB run out of connections?**
   → Connection pool size was 100, we hit 150 concurrent users

3. **Why didn't we scale connection pool?**
   → We didn't know traffic would spike

4. **Why didn't we know?**
   → No monitoring/alerting on connection pool usage

5. **Why no monitoring?**
   → We didn't prioritize observability (tech debt)

**Root Cause**: Lack of observability investment

**Action Items**:

- Add connection pool monitoring (alert at 80%)
- Increase pool size from 100 → 500
- Quarterly observability review

---

### ✅ Ejemplo Output

```markdown
## Sprint 24 Retro - Five Whys

### Problem: Stories spillearon 3 sprints consecutivos

**Why #1**: ¿Por qué stories spillearon?
→ Estimaciones fueron incorrectas (story de 5 points tomó 13)

**Why #2**: ¿Por qué estimaciones incorrectas?
→ No consideramos QA effort

**Why #3**: ¿Por qué no consideramos QA effort?
→ QA no participó en Planning Poker

**Why #4**: ¿Por qué QA no participó?
→ No estaba claro que QA debía estimar

**Why #5**: ¿Por qué no estaba claro?
→ No tenemos proceso documentado de estimation

**ROOT CAUSE**: Falta de proceso QA-inclusive estimation

**Action Items**:

1. Implement QA-inclusive estimation model
2. QA participa en Planning Poker
3. Document estimation process
```

---

## 🎭 Facilitator Tips

### Cómo Elegir Formato

**Decision Tree**:

```
Sprint normal?
  → Start/Stop/Continue

Blockers importantes?
  → Sailboat

Aprendimos mucho (new tech)?
  → 4 Ls

Team morale bajo / conflicts?
  → Mad/Sad/Glad

Post-release / major milestone?
  → Timeline

Incident o problema recurrente?
  → Five Whys
```

---

### General Facilitation Tips

**1. Prime Directive** (start EVERY retro)

> "Regardless of what we discover, we understand and truly believe
> that everyone did the best job they could, given what they knew
> at the time, their skills and abilities, the resources available,
> and the situation at hand."

**2. Psychological Safety**

- No blaming individuals
- Focus en system, not people
- "What can WE improve?" not "Who messed up?"

**3. Timebox Rigorously**

- Use timer
- Cut off discussions: "Let's continue offline"

**4. Action Items are MANDATORY**

- No retro without action items
- Max 5 action items (more = none get done)

**5. Follow Up**

- Review action items from previous retro (first 10 min)
- Hold team accountable

---

## 📊 Metrics

### Metric #1: Action Item Completion Rate

**Target**: >70% (ver [Retro Action Items](retro-action-items.md))

---

### Metric #2: Team Satisfaction with Retros

**Survey**: "Retrospectivas son valiosas?" (1-5)

**Target**: >3.5

**Red Flag**:

- <2.5 → Retros son waste, no agregan valor

---

### Metric #3: Format Diversity

**Track**: Cuántos formatos diferentes usamos en últimos 6 sprints?

**Target**: Mínimo 3 formatos diferentes

**Red Flag**:

- Solo 1 formato → Fatigue, repetitive

---

## 🚀 Implementation

### Sprint 0

- [ ] Facilitator aprende 6 formatos
- [ ] Crea rotation schedule
- [ ] Comunica a team: "Vamos a rotar formatos"

### Sprint 1-6

- [ ] Ejecutar cada formato 1 vez
- [ ] Survey team: ¿Cuál formato prefieren?

### Sprint 7+

- [ ] Rotation basada en context + team preference

---

## ✅ Success Criteria

- ✅ 3+ formatos usados en últimos 6 sprints
- ✅ Team satisfaction >3.5
- ✅ Action item completion >70%
- ✅ Team members proactivamente sugieren formatos

---

## 🔗 Links Relacionados

- [Retro Action Items](retro-action-items.md) - Accountability system (CRÍTICO)
- [Ceremonias: Retrospective](README.md#retrospective) - Ceremonia principal
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Scrum Master / Facilitator  
**Review Cycle**: Trimestral
