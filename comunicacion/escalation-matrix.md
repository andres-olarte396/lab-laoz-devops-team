# Escalation Matrix - Matriz de Escalación Cross-Team

## 📋 Resumen Ejecutivo

**Problema**: Developer bloqueado por DevOps → Espera 2 días porque no sabe cómo escalar. Product y Engineering no se ponen de acuerdo en prioridades → Proyecto se retrasa. Design y Frontend tienen visiones diferentes → Feature queda a medio hacer.

**Solución**: **Escalation matrix clara** con niveles definidos, time-boxing estricto, y decision makers claros para cada tipo de conflicto.

**Beneficio**:
- Blockers resueltos rápido (<4 horas vs 2+ días)
- Decisiones tomadas (no paralysis por análisis)
- Transparencia (todos saben cómo escalar)
- Menos frustr

ación (proceso claro para resolver conflictos)

---

## 🎯 Principios de Escalación

### 1. Bias Toward Resolution

**Regla**: Tomar decisión imperfecta hoy > Decisión perfecta en 2 semanas

**Por qué**: 
- Velocity es más importante que perfección
- Decisiones se pueden revertir (código se puede cambiar)
- Paralysis cuesta más que una decisión subóptima

---

### 2. Time-Boxing Estricto

**Regla**: Cada nivel tiene tiempo máximo

| Nivel | Time Box | Qué pasa si se excede |
|-------|----------|----------------------|
| Nivel 1 (Individual) | 30 min - 2 horas | Auto-escala a Nivel 2 |
| Nivel 2 (Lead/Manager) | 2 horas - 1 día | Auto-escala a Nivel 3 |
| Nivel 3 (Director/VP) | 1 día | Decisión forzada |

**Si time-box se excede → Automatic escalation** (no optional)

---

### 3. Document Decisions

**Regla**: Toda decisión escalada se documenta

**Dónde**:
- Decisiones técnicas → ADR (Architecture Decision Record)
- Decisiones de producto → Product brief
- Decisiones organizacionales → Confluence

**Por qué**:
- Evita re-litigar misma decisión 10 veces
- Onboarding más fácil (nuevos miembros entienden por qué)
- Auditable (sabemos quién decidió qué y cuándo)

---

## 🔀 Escalation Paths by Scenario

### Scenario 1: Technical Blocker (Development ↔ DevOps)

**Example**: Developer necesita nueva database, DevOps dice "tardaremos 2 semanas en provisionar"

---

#### Nivel 1: Individual Contributor (30 min - 2 horas)

**Actors**: Developer ↔ DevOps Engineer

**Process**:
1. Developer postea en #devops:
   ```markdown
   Need help: I need a PostgreSQL database for new feature
   
   Context:
   - Feature: User analytics dashboard
   - Timeline: Need DB by Friday (3 days)
   - Requirements: ~10GB storage, read replicas
   
   Can we spin this up? @devops-team
   ```

2. DevOps Engineer responde:
   - ✅ "Yes, can do in 1 day" → Problem solved
   - ⚠️ "Need 2 weeks, we're at capacity" → Escalate a Nivel 2

**Time box**: 2 horas (si no hay respuesta → ping DevOps Lead)

---

#### Nivel 2: Lead/Manager (2 horas - 1 día)

**Actors**: Tech Lead ↔ DevOps Lead

**Process**:
1. Tech Lead escalates:
   ```markdown
   @devops-lead Need help prioritizing:
   
   Developer needs DB for user analytics (launches next Friday).
   DevOps says 2-week wait due to capacity.
   
   Options:
   1. Delay launch 2 weeks (bad - committed to stakeholders)
   2. Use managed DB (Azure Database for PostgreSQL) - faster
   3. Re-prioritize DevOps backlog
   
   Can we sync 15 min to decide? @devops-lead
   ```

2. Tech Lead + DevOps Lead sync call (15 min):
   - Discuss tradeoffs
   - Pick solution (e.g., use managed DB for now, migrate later)
   - Document decision

3. Decision:
   - ✅ Agreed solution → Unblocked
   - ❌ Still disagreement → Escalate a Nivel 3

**Time box**: 1 día (if no resolution → auto-escalate)

---

#### Nivel 3: Engineering Manager (1 día)

**Actors**: Engineering Manager (Decision Maker)

**Process**:
1. Engineering Manager reviews options
2. Makes decision (final, non-negotiable)
3. Documents rationale

**Decision** (example):
```markdown
DECISION: Use Azure managed PostgreSQL for now

RATIONALE:
- Launching on time is critical (committed to CEO)
- DevOps capacity is low (2 other P0 projects)
- Managed DB is acceptable (performance ok, cost +$200/month)
- We'll migrate to self-hosted later (Q2 2026)

OWNER: @developer (provision managed DB)
DEADLINE: Wednesday
FOLLOW-UP: Tech debt ticket to migrate (Q2 2026)

Decision maker: @engineering-manager
Date: 2025-12-07
```

**Time box**: 1 día (decision MUST be made)

---

### Scenario 2: Scope/Timeline Conflict (Product ↔ Engineering)

**Example**: Product wants 10 features in Q1, Engineering says "we can only do 5"

---

#### Nivel 1: Product Owner ↔ Tech Lead (1 hora)

**Process**:
1. Product Owner presents roadmap:
   - 10 features planned for Q1
   - All are "high priority"

2. Tech Lead responds with capacity:
   - Team velocity: 40 story points/sprint
   - Q1 = 6 sprints = 240 points
   - 10 features = ~400 points
   - **Conclusion**: Can only do 5-6 features

3. Options:
   - ✅ Product re-prioritizes (pick top 5) → Resolved
   - ❌ Product says "all 10 are must-haves" → Escalate

**Time box**: 1 hora

---

#### Nivel 2: Product Manager ↔ Engineering Manager (4 horas)

**Process**:
1. PM + EM sync (1 hour meeting):
   - Review each feature:
     - Business value (revenue impact, customer requests)
     - Technical complexity (story points)
     - Dependencies (other features, external teams)

2. Prioritization exercise:
   - Use RICE framework (Reach, Impact, Confidence, Effort)
   - Rank features 1-10
   - Cutline at team capacity (e.g., top 6 features)

3. Decision:
   - ✅ Agreed on top 6 → Resolved
   - ❌ Still disagree (PM says "need all 10") → Escalate

**Time box**: 4 horas (sync call + async alignment)

---

#### Nivel 3: CPO ↔ CTO (1 día)

**Actors**: Chief Product Officer ↔ Chief Technology Officer

**Process**:
1. CPO + CTO review:
   - Business strategy (what do we need to win?)
   - Engineering capacity (realistic estimate)
   - Options:
     - Cut scope (do fewer features)
     - Add capacity (hire contractors)
     - Extend timeline (Q1 → Q1 + Q2)

2. Decision (example):
   ```markdown
   DECISION: Top 6 features in Q1, remaining 4 in Q2
   
   RATIONALE:
   - Engineering capacity is realistic (can't do 10)
   - Top 6 features drive 80% of revenue impact
   - Remaining 4 can wait (nice-to-have, not critical)
   
   ALTERNATIVE CONSIDERED:
   - Hire 2 contractors ($50K/month)
   - REJECTED: Onboarding would take 1 month, net negative
   
   OWNER: @product-manager (re-plan roadmap)
   DEADLINE: Monday
   
   Decision makers: CPO + CTO
   Date: 2025-12-07
   ```

**Time box**: 1 día (decision MUST be made by end of day)

---

### Scenario 3: Design vs Engineering Feasibility

**Example**: Design proposes complex animation, Frontend says "will take 2 weeks, not worth it"

---

#### Nivel 1: Designer ↔ Frontend Developer (1 hora)

**Process**:
1. Designer shares Figma design:
   - Complex animation (parallax scroll effect)
   - Looks amazing

2. Frontend Developer reviews:
   - Estimates: 2 weeks (40 hours)
   - Technical complexity: High (performance issues on mobile)
   - Recommendation: Simplified version (2 days instead)

3. Options:
   - ✅ Designer agrees to simplified version → Resolved
   - ❌ Designer insists on original design → Escalate

**Time box**: 1 hora (pair on alternative designs)

---

#### Nivel 2: Lead Designer ↔ Tech Lead (4 horas)

**Process**:
1. Lead Designer + Tech Lead review:
   - User impact: Is complex animation critical to UX?
   - Technical feasibility: Can we do it without performance hit?
   - Alternatives: Simpler animation that achieves 80% of impact?

2. Prototype/spike (2-4 hours):
   - Frontend Developer builds quick POC
   - Lead Designer reviews POC
   - Measure performance (Lighthouse score)

3. Decision:
   - ✅ POC is acceptable → Use simplified version
   - ❌ POC is not acceptable → Escalate

**Time box**: 4 horas

---

#### Nivel 3: Design Manager ↔ Engineering Manager (1 día)

**Process**:
1. Design Manager + Engineering Manager review:
   - Strategic alignment: Does this feature support product strategy?
   - Cost/benefit: Is 2 weeks worth it for this animation?
   - User research: Do users care about this animation?

2. Decision (example):
   ```markdown
   DECISION: Use simplified animation (2 days), not complex (2 weeks)
   
   RATIONALE:
   - User testing shows animation is "nice to have", not critical
   - 2 weeks is too expensive (opportunity cost: 2 other features)
   - Simplified version achieves 80% of visual impact
   
   ALTERNATIVE CONSIDERED:
   - Delay other features to fit complex animation
   - REJECTED: Other features have higher business priority
   
   OWNER: @frontend-developer (implement simplified)
   DEADLINE: Friday
   
   Decision makers: Design Manager + Engineering Manager
   Date: 2025-12-07
   ```

**Time box**: 1 día

---

### Scenario 4: Architecture vs Speed (Tech Debt vs Features)

**Example**: Architect wants to refactor to microservices, Product wants to ship features fast

---

#### Nivel 1: Solution Architect ↔ Tech Lead (Discussion)

**Process**:
1. Solution Architect proposes:
   - Refactor monolith → microservices
   - Benefits: Better scalability, team independence
   - Cost: 3 months of engineering time

2. Tech Lead responds:
   - Product roadmap: 10 features committed for Q1
   - Refactor would block all feature work
   - Recommendation: Incremental migration (strangler pattern)

3. Options:
   - ✅ Architect agrees to incremental approach → Resolved
   - ❌ Architect insists on full rewrite → Escalate

**Time box**: Discussion (no time box at this level, this is strategic)

---

#### Nivel 2: Enterprise Architect ↔ Engineering Manager (Alignment)

**Process**:
1. Enterprise Architect + EM align:
   - Technical vision (where do we want to be in 2 years?)
   - Business constraints (what do we need to ship now?)
   - Migration strategy:
     - Option A: Full rewrite (3 months, blocks features)
     - Option B: Incremental (strangler pattern, 6-12 months, parallel with features)
     - Option C: Stay monolith (ship features now, refactor later)

2. Decision:
   - ✅ Agreed on Option B (incremental) → Resolved
   - ❌ Still disagree → Escalate to CTO

**Time box**: 1-2 weeks (strategic discussion, not urgent)

---

#### Nivel 3: CTO (Strategic Decision)

**Process**:
1. CTO reviews:
   - Technical debt impact (is monolith slowing us down?)
   - Business priorities (do we need to ship features fast?)
   - Long-term vision (where is company going?)

2. Decision (example):
   ```markdown
   DECISION: Incremental migration (strangler pattern) over 12 months
   
   RATIONALE:
   - Monolith is slowing us down (deploy frequency low, incidents high)
   - Full rewrite is too risky (3 months without features = lost revenue)
   - Incremental migration balances speed + quality
   
   PLAN:
   - 20% of each sprint dedicated to migration
   - Migrate 1 service per quarter
   - Full migration complete by Q4 2026
   
   OWNER: @enterprise-architect (migration roadmap)
   DEADLINE: Next week (present detailed plan)
   
   Decision maker: CTO
   Date: 2025-12-07
   ```

**Time box**: 1 semana (strategic, but needs decision)

---

## 📊 Escalation Matrix (Summary Table)

| Scenario | Nivel 1 | Nivel 2 | Nivel 3 | Time Box Total |
|----------|---------|---------|---------|----------------|
| **Dev ↔ DevOps** | IC ↔ IC (2h) | TL ↔ DevOps Lead (1d) | EM (1d) | 2 días |
| **Product ↔ Eng** | PO ↔ TL (1h) | PM ↔ EM (4h) | CPO ↔ CTO (1d) | 2 días |
| **Design ↔ Eng** | Designer ↔ Dev (1h) | Lead Designer ↔ TL (4h) | Design Manager ↔ EM (1d) | 2 días |
| **Arch ↔ Speed** | Architect ↔ TL (discuss) | EA ↔ EM (2wks) | CTO (1wk) | 3 semanas |

---

## 🎭 RACI: Escalation Responsibilities

| Actividad | IC | Lead | Manager | Director/VP |
|-----------|----|----|---------|-------------|
| **Identify blocker** | R | I | I | I |
| **Attempt Nivel 1 resolution** | A/R | C | I | I |
| **Escalate to Nivel 2** | R | I | I | I |
| **Facilitate Nivel 2** | C | A/R | C | I |
| **Escalate to Nivel 3** | I | R | I | I |
| **Make final decision (Nivel 3)** | I | I | A/R | A/R |
| **Document decision** | I | C | R | R |
| **Communicate decision** | I | C | R | A |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 📝 Escalation Templates

### Template: Escalation Request

**Slack Message** (when escalating from Nivel 1 → Nivel 2):
```markdown
@tech-lead Need help resolving blocker:

**Issue**: [Brief description]
**Blocker**: [What's blocking us]
**Tried**: [What we already tried]
**Options**: 
1. [Option A]
2. [Option B]

**Impact**: [Why this is urgent]
**Deadline**: [When we need decision]

Can we sync 15 min to decide? [Calendly link]
```

---

### Template: Decision Record (ADR)

**Architecture Decision Record** (for Nivel 3 decisions):
```markdown
# ADR-XXX: [Decision Title]

**Date**: YYYY-MM-DD
**Status**: Proposed | Accepted | Rejected | Superseded
**Deciders**: @username, @username
**Consulted**: @team

## Context
[What is the issue we're trying to solve?]

## Decision
[What did we decide to do?]

## Rationale
[Why did we make this decision?]

## Consequences
**Positive**:
- [Good outcome 1]
- [Good outcome 2]

**Negative**:
- [Tradeoff 1]
- [Tradeoff 2]

## Alternatives Considered
**Option A**: [Description]
- Pros: [...]
- Cons: [...]
- Why rejected: [...]

**Option B**: [Description]
- Pros: [...]
- Cons: [...]
- Why rejected: [...]

## Implementation
**Owner**: @username
**Deadline**: YYYY-MM-DD
**Success Criteria**: [How we'll know this worked]

## Follow-Up
- [ ] [Action item 1]
- [ ] [Action item 2]
```

---

## ⏱️ Time-Boxing Best Practices

### Auto-Escalation Triggers

**Automatic escalation si**:
- Time box exceeded (sin decisión tomada)
- Blocker impacta >3 personas
- Deadline critical (<48 horas)
- Revenue risk (potential loss >$10K)

**How to auto-escalate**:
```markdown
⚠️ **AUTO-ESCALATION** (Time box exceeded)

**Issue**: [Brief description]
**Nivel 1 attempts**: [What was tried]
**Outcome**: No resolution after [X hours]

Escalating to @tech-lead for Nivel 2 decision.

**Deadline**: [Critical date]
**Impact**: [Who's blocked]
```

---

## 📊 Escalation Metrics

### Metrics to Track

| Metric | Target | Red Flag |
|--------|--------|----------|
| **Time to resolution (avg)** | <4 horas | >1 día |
| **Escalations to Nivel 3** | <10/quarter | >20/quarter |
| **Decision documentation** | 100% | <80% |
| **Blocker recurrence** | 0 (same issue) | >2 same issue |
| **Team satisfaction** | >4/5 | <3/5 |

**How to measure**:
- Quarterly survey (team sentiment)
- Jira/Linear tags (track escalations)
- Post-mortem reviews (escalation effectiveness)

---

## ✅ Success Criteria

### Mes 1
- ✅ Escalation matrix documented y comunicada
- ✅ Team trained (workshop on escalation process)
- ✅ First 5 escalations documented (ADRs)

### Mes 2-3
- ✅ Time to resolution <6 horas (avg)
- ✅ Team satisfaction >3.5/5 (escalation process)
- ✅ 80% decisions documented

### Mes 4+
- ✅ Time to resolution <4 horas (avg)
- ✅ Team satisfaction >4/5
- ✅ 100% Nivel 3 decisions documented
- ✅ Zero "I didn't know how to escalate" complaints

---

## 🔗 Links Relacionados

- [Channel Ownership](./channel-ownership.md) - Dónde escalar (canales)
- [Incident Communication](./incident-communication.md) - Escalación durante incidentes
- [Change Management](../procesos/change-management.md) - Escalación de changes
- [Decision Making](../ceremonias/README.md) - Quién decide qué

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (team feedback)
