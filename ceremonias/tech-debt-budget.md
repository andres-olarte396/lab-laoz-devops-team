# 🔧 Tech Debt Budget - 20% Rule & Prioritization

## 📋 Resumen Ejecutivo

**Problema**: Tech debt crece sin control porque:

- "Siempre hay features más urgentes"
- Tech debt no tiene prioridad visible en backlog
- No hay tiempo dedicado explícitamente
- Eventualmente: código unmaintainable, velocity colapsa

**Solución**: **20% Rule** - Dedicar 20% de sprint capacity a tech debt, explícitamente planeado en Sprint Planning.

**Beneficio**:

- Tech debt se paga incrementalmente
- Codebase se mantiene saludable long-term
- Velocity se mantiene estable (no decay)
- Team morale mejora (devs no sufren legacy hell)

---

## 🎯 ¿Qué es Tech Debt?

**Definición**:

> Código o arquitectura subóptima que funciona HOY pero tendrá costo futuro en mantenimiento, features, o performance.

**Analogía Financiera**:

- Feature work = Ingresos
- Tech debt = Préstamo bancario
- Intereses = Tiempo extra que toma cada nueva feature por culpa del debt

**No Todo Código Imperfecto es Tech Debt**:

- ✅ **Es Tech Debt**: Código que SABES que causará problemas futuros
- ❌ **No es Tech Debt**: Código que simplemente no te gusta estéticamente

---

## 📊 Tipos de Tech Debt

### 1. **Code Quality Debt**

**Ejemplos**:

- Código duplicado (DRY violations)
- Funciones >200 líneas (god functions)
- Clases >1000 líneas (god classes)
- Cyclomatic complexity >15
- 0 tests (código legacy sin coverage)

**Síntomas**:

- Bugs recurrentes en mismo código
- Developers evitan tocar ese código
- "Nadie entiende cómo funciona esto"

**Impacto**:

- Velocity baja: cada feature requiere más tiempo
- Bug rate alta: cambios rompen cosas inesperadas

---

### 2. **Architecture Debt**

**Ejemplos**:

- Monolito que debería ser microservices
- Tight coupling entre módulos
- No separation of concerns
- Database schema mal diseñada (N+1 queries)

**Síntomas**:

- "Para agregar feature X, tenemos que tocar 15 archivos"
- "No podemos escalar porque todo está acoplado"
- "Deploy de un microservice requiere deploy de todos"

**Impacto**:

- Scalability limitada
- Deploy risk alto (cambio pequeño → impacto grande)
- Onboarding lento (arquitectura compleja)

---

### 3. **Test Debt**

**Ejemplos**:

- Code coverage <60%
- Tests flaky (pasan/fallan aleatoriamente)
- 0 integration tests
- 0 E2E tests
- Tests toman >30min en CI/CD

**Síntomas**:

- "No podemos refactorizar porque romperíamos algo"
- "Tests fallan pero los ignoramos"
- "CI/CD toma 2h, nadie lo usa"

**Impacto**:

- Confidence en deployments baja
- Regression bugs en producción
- Refactoring riesgoso

---

### 4. **Infrastructure Debt**

**Ejemplos**:

- Servers con OS desactualizado (security risk)
- Manual deployment (no CI/CD)
- 0 monitoring/alerting
- Hard-coded configs (no environment variables)
- DB backup manual

**Síntomas**:

- "Deploy toma 3h porque es manual"
- "No sabemos si prod está down hasta que user reporta"
- "DB crasheó y no teníamos backup reciente"

**Impacto**:

- Downtime frecuente
- Security vulnerabilities
- Deploy risk alto

---

### 5. **Dependency Debt**

**Ejemplos**:

- Libraries 2+ major versions desactualizadas
- CVEs (security vulnerabilities) en dependencies
- Deprecated APIs siendo usadas
- Unsupported frameworks (ej: Angular 1.x)

**Síntomas**:

- `npm audit` muestra 50 vulnerabilities
- Dependabot PRs ignorados por meses
- "No podemos actualizar porque rompería todo"

**Impacto**:

- Security risk (exploits públicos)
- No puedes usar features nuevas de libraries
- Eventualmente: rewrite completo necesario

---

## 💰 The 20% Rule

### Concepto

**Regla**:

> Dedicar 20% de sprint capacity a tech debt, CADA sprint.

**Ejemplo**:

- Sprint capacity: 50 story points
- Tech debt budget: 10 story points (20%)
- Feature work: 40 story points (80%)

**Rationale**:

- 20% es sostenible long-term (no impacta feature delivery drásticamente)
- Compound effect: 20% cada sprint → código mejora gradualmente
- Previene "tech debt bankruptcy" (rewrite completo)

---

### 3 Opciones de Implementación

#### **Opción A: Porcentaje Fijo por Sprint** (Recomendado)

**Cómo Funciona**:

- Cada Sprint Planning, reserve 20% de capacity para tech debt
- Tech Lead + devs seleccionan tech debt items de backlog
- Tech debt tiene MISMA prioridad que features

**Pros**:

- ✅ Predecible: siempre hay tiempo para tech debt
- ✅ Sostenible: no genera sprint "especiales"
- ✅ Compound effect: mejora continua

**Cons**:

- ❌ Si hay feature ultra-urgente, PO puede presionar para saltarse

**Best For**: Equipos con tech debt moderado, quieren prevenir crecimiento

---

#### **Opción B: Sprints Dedicados Periódicos**

**Cómo Funciona**:

- Cada N sprints (ej: cada 5 sprints), 1 sprint completo para tech debt
- Sprint 1-4: 100% features
- Sprint 5: 100% tech debt (hardening sprint)

**Pros**:

- ✅ Focus total en tech debt (no context switching)
- ✅ Puede hacer refactorings grandes (ej: arquitectura)

**Cons**:

- ❌ Tech debt crece durante sprints 1-4
- ❌ PO puede cancelar hardening sprint si hay urgencia
- ❌ Devs pueden "aguantar" problemas esperando hardening sprint

**Best For**: Equipos con tech debt alto, necesitan sprints de "catch-up"

---

#### **Opción C: Hybrid (20% + Hardening Sprints)**

**Cómo Funciona**:

- Sprints normales: 20% tech debt
- Cada trimestre: 1 sprint hardening (100% tech debt)

**Pros**:

- ✅ Mejora continua (20% cada sprint)
- ✅ Puede hacer refactorings grandes (hardening sprint)
- ✅ Flexible

**Cons**:

- ❌ Más complejo de planear
- ❌ Requiere disciplina para mantener 20% + hardening

**Best For**: Equipos maduros, tech debt bajo control, quieren optimizar

---

### Nuestra Recomendación: **Opción A (20% Fijo)**

**Por Qué**:

- Sostenible long-term
- Predecible para PO y stakeholders
- Previene tech debt bankruptcy
- Mejora continua sin "special sprints"

**Cómo Empezar**:

1. Sprint 1: Comunica a PO "vamos a dedicar 20% a tech debt"
2. Sprint Planning: Reserve 20% de capacity
3. Tech Lead selecciona tech debt items (ver Prioritization)
4. Track separately en Jira (label `tech-debt`)

---

## 🎯 Cómo Priorizar Tech Debt

### Framework: Impact × Effort Matrix

```
          │ Low Effort │ High Effort │
──────────┼────────────┼─────────────┤
High      │ ⭐ QUICK   │ 🎯 STRATEGIC│
Impact    │   WINS     │   BET       │
──────────┼────────────┼─────────────┤
Low       │ 🔧 NICE    │ ❌ AVOID    │
Impact    │   TO HAVE  │             │
```

### Cuadrante 1: ⭐ Quick Wins (High Impact, Low Effort)

**Prioridad**: **MÁXIMA** - Hacer primero

**Ejemplos**:

- Actualizar dependency con CVE crítico (2h)
- Agregar index a DB table lenta (1h)
- Agregar monitoring a endpoint crítico (3h)
- Documentar API endpoint confuso (2h)

**Criterio**:

- ✅ Impacto: Mejora velocity, reduce bugs, o mejora performance
- ✅ Esfuerzo: <1 día (8h)
- ✅ ROI: Inmediato

**Tip**: Siempre llena sprint con Quick Wins primero

---

### Cuadrante 2: 🎯 Strategic Bets (High Impact, High Effort)

**Prioridad**: **ALTA** - Planear cuidadosamente

**Ejemplos**:

- Migrar monolito a microservices (3 meses)
- Rewrite legacy module con 0 tests (2 sprints)
- Setup CI/CD pipeline (1 sprint)
- Database schema migration (1 sprint)

**Criterio**:

- ✅ Impacto: Transformacional (habilita features futuras, 10x mejora)
- ⚠️ Esfuerzo: >1 sprint
- ✅ ROI: Long-term

**Cómo Manejar**:

- Dividir en incremental steps (vertical slices)
- No hacerlo todo en 1 sprint
- Ejemplo: "Microservice migration" → "Extract auth service" (sprint 1) → "Extract payments" (sprint 2)

---

### Cuadrante 3: 🔧 Nice to Have (Low Impact, Low Effort)

**Prioridad**: **MEDIA** - Hacer si sobra tiempo

**Ejemplos**:

- Renombrar variables confusas (1h)
- Formatting de código (30min)
- Agregar comments a código (2h)

**Criterio**:

- ⚠️ Impacto: Mejora marginal (code readability)
- ✅ Esfuerzo: <4h
- ⚠️ ROI: Bajo

**Cuándo Hacer**:

- Developer tiene 2-3h libres en sprint
- Onboarding new hire (good first tasks)
- NO priorizar sobre Quick Wins o Strategic Bets

---

### Cuadrante 4: ❌ Avoid (Low Impact, High Effort)

**Prioridad**: **EVITAR** - No hacer nunca

**Ejemplos**:

- Reescribir código que funciona bien solo porque "no me gusta"
- Over-engineering (agregar abstracción innecesaria)
- Premature optimization

**Criterio**:

- ❌ Impacto: No mejora velocity, no reduce bugs
- ❌ Esfuerzo: Alto
- ❌ ROI: Negativo (waste de tiempo)

**Red Flag**: "Sería cool hacer X" (pero no hay beneficio concreto)

---

## 📝 Tech Debt Backlog Management

### Crear Tech Debt Items en Jira

**Template**:

```markdown
**Title**: [TECH DEBT] Fix N+1 query in /products endpoint

**Type**: Technical Debt

**Label**: tech-debt, performance

**Description**:

### Problem

/products endpoint hace N+1 queries a database:

- 1 query: SELECT \* FROM products
- N queries: SELECT \* FROM categories WHERE id = ?

Con 100 products → 101 queries → 2 segundos de latency

### Impact

- High: P95 latency = 2s (target: <200ms)
- Affects: 10,000 requests/day
- User experience: Página de productos carga lento

### Proposed Solution

Use JOIN en query inicial:
SELECT p._, c._ FROM products p LEFT JOIN categories c ON p.category_id = c.id

Estimado: 3h (change query + test)

### Expected Outcome

- Latency: 2s → <200ms (10x improvement)
- DB load: 101 queries → 1 query

### Effort

3 story points (4-6h)

### Priority Quadrant

⭐ Quick Win (High Impact, Low Effort)
```

---

### Priorizar Tech Debt Backlog

**Sprint Planning Process**:

1. **Pre-Planning** (L-1):

   - Tech Lead revisa Tech Debt backlog
   - Categoriza items en Impact×Effort matrix
   - Selecciona top 5-10 candidates

2. **Sprint Planning**:

   - Reserve 20% capacity (ej: 10 de 50 points)
   - Tech Lead presenta top 3-5 tech debt items
   - Team vota: cuáles hacer este sprint?
   - Commit a 2-3 items (total ~10 points)

3. **Durante Sprint**:
   - Tech debt tiene MISMA prioridad que features
   - No postponer tech debt por "feature urgente"
   - Si feature urgente llega → remove otra feature, NO tech debt

---

### Tech Debt Backlog Hygiene

**Weekly Review** (15 min, Tech Lead):

- Agregar nuevos tech debt items identificados
- Re-priorizar basado en impact
- Marcar items obsoletos (código refactored o deleted)

**Quarterly Review** (1h, Tech Lead + team):

- Revisar todos tech debt items
- Categorizar por tipo (code, architecture, test, infra, dependency)
- Identificar patterns: "Siempre tenemos test debt → invertir en testing framework"

---

## 📊 Métricas de Tech Debt

### Métrica #1: Tech Debt Ratio

**Fórmula**:

```
Tech Debt Story Points / Total Story Points × 100
```

**Target**: 15-25% (promedio de últimos 6 sprints)

**Insight**:

- <10% → No estamos invirtiendo suficiente en tech debt
- 15-25% → Saludable
- > 30% → Tech debt está fuera de control (red flag)

---

### Métrica #2: Code Coverage

**Fórmula**:

```
(Líneas de código con tests / Total líneas) × 100
```

**Target**: >70% (>80% ideal)

**Tracking**:

- CI/CD report de coverage
- Trend: debería subir gradualmente

**Red Flag**:

- Coverage bajando → estamos agregando código sin tests

---

### Métrica #3: Dependency Security Score

**Fórmula**:

```
# CVEs (vulnerabilities) en dependencies
```

**Target**: 0 Critical, 0 High, <5 Medium

**Tools**:

- `npm audit` (Node.js)
- `pip-audit` (Python)
- Dependabot (GitHub)

**Red Flag**:

- > 10 Critical/High CVEs → security risk inminente

---

### Métrica #4: Build/Test Time

**Fórmula**:

```
Tiempo total de CI/CD pipeline (min)
```

**Target**: <15 min (ideal: <10 min)

**Tracking**:

- CI/CD logs
- Trend: debería mantenerse estable o bajar

**Red Flag**:

- Build time creciendo → infra debt o test debt

---

### Métrica #5: Velocity Stability

**Fórmula**:

```
Std Dev de velocity de últimos 6 sprints
```

**Target**: <15% variance

**Insight**:

- High variance → tech debt está afectando predictability
- Stable velocity → tech debt bajo control

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup

**Week 1**:

- [ ] Tech Lead + PO alinean en 20% rule
- [ ] Comunicar a team: "Vamos a dedicar 20% a tech debt cada sprint"
- [ ] Crear Jira label `tech-debt`
- [ ] Crear Jira filter: `label = tech-debt AND status != Done`

**Week 2**:

- [ ] Tech Lead + team identifican top 20 tech debt items
- [ ] Categorizar en Impact×Effort matrix
- [ ] Estimate tech debt items (story points)

---

### Sprint 1-3: Pilot

- [ ] Sprint Planning: Reserve 20% capacity para tech debt
- [ ] Commit a 2-3 tech debt items (~10 points)
- [ ] Track separately: Tech debt velocity vs feature velocity
- [ ] Retrospective: ¿20% es suficiente? ¿Muy poco? ¿Mucho?

---

### Sprint 4+: Optimize

- [ ] Ajustar % basado en feedback (ej: 15% si tech debt bajo, 25% si alto)
- [ ] Metrics review: Coverage, CVEs, build time
- [ ] Quarterly: Strategic tech debt initiatives (architecture changes)

---

## ✅ Success Criteria

### Mes 1

- ✅ 20% de sprint capacity dedicado a tech debt
- ✅ Tech debt backlog priorizado
- ✅ 2-3 tech debt items completados por sprint

### Mes 2-3

- ✅ Code coverage aumenta +5-10%
- ✅ CVEs: 0 Critical, <5 High
- ✅ Build time estable (<15 min)

### Mes 4+

- ✅ Velocity estable (±10% variance)
- ✅ Team morale: "Codebase está mejorando"
- ✅ Onboarding: Nuevos devs pueden ser productivos más rápido
- ✅ Bug rate baja (menos regression bugs)

---

## 🎭 Roles y Responsabilidades

### Tech Lead

**Pre-Sprint**:

- ✅ Revisar tech debt backlog semanalmente
- ✅ Categorizar nuevos items en Impact×Effort matrix
- ✅ Seleccionar top 3-5 candidates para próximo sprint

**Sprint Planning**:

- ✅ Reserve 20% capacity para tech debt
- ✅ Presentar tech debt items al team
- ✅ Facilitar votación: cuáles hacer?

**Durante Sprint**:

- ✅ Proteger tech debt budget (no dejarlo caer por features urgentes)
- ✅ Monitor progress de tech debt items

**Post-Sprint**:

- ✅ Review métricas: coverage, CVEs, build time
- ✅ Comunicar wins en retro: "Mejoramos coverage de 65% a 72%"

---

### Product Owner

**Sprint Planning**:

- ✅ Aceptar 20% tech debt budget (no presionar por 100% features)
- ✅ Entender business value de tech debt (velocity long-term)

**Durante Sprint**:

- ✅ No re-priorizar features sobre tech debt mid-sprint
- ✅ Si feature urgente llega → remove otra feature, no tech debt

**Stakeholder Communication**:

- ✅ Explicar a stakeholders por qué 20% tech debt es investment
- ✅ "80% features + 20% tech debt = velocidad sostenible"

---

### Development Team

**Identificar Tech Debt**:

- ✅ Agregar tech debt items a backlog cuando encuentran problemas
- ✅ Estimar tech debt items en Planning Poker

**Durante Sprint**:

- ✅ Trabajar tech debt items con misma dedicación que features
- ✅ No considerar tech debt "menos importante"

**Code Review**:

- ✅ Sugerir tech debt items cuando ven código problemático
- ✅ No crear nuevo tech debt (write tests, follow standards)

---

## 🔗 Links Relacionados

- [Ceremonias: Sprint Planning](README.md#sprint-planning) - Donde se planea tech debt
- [Ceremonias: Retrospective](README.md#retrospective) - Donde se identifica tech debt
- [Definition of Ready](definition-of-ready.md) - Tech debt items también necesitan DoR
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

## 📚 Ejemplos de Tech Debt Items

### ✅ Ejemplo: Quick Win

```markdown
**[TECH DEBT] Add monitoring to /checkout endpoint**

**Problem**:
/checkout endpoint procesa 5,000 transactions/día pero no tiene monitoring.
Si falla, solo nos enteramos cuando customer reporta.

**Impact**:

- High: Revenue-critical endpoint
- Currently: 0 visibility, MTTR >2h

**Solution**:

- Add Datadog APM instrumentation
- Alert si error rate >1% o latency >2s

**Effort**: 2 story points (3h)

**Priority**: ⭐ Quick Win (High Impact, Low Effort)
```

---

### ✅ Ejemplo: Strategic Bet

```markdown
**[TECH DEBT] Migrate authentication to Auth0**

**Problem**:
Custom auth implementation (3,000 lines) tiene:

- 12 security vulnerabilities
- No MFA support
- No SSO support
- Hard to maintain

**Impact**:

- High: Security risk + feature blocker
- Currently: 2 security incidents/año

**Solution**:

- Migrate to Auth0 (managed service)
- Remove 3,000 lines of custom code
- Gain MFA, SSO out-of-box

**Effort**: 13 story points (2 sprints)

**Priority**: 🎯 Strategic Bet (High Impact, High Effort)

**Plan**:
Sprint 1: Auth0 setup + migrate 50% of users
Sprint 2: Migrate remaining 50% + deprecate old auth
```

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Tech Lead  
**Review Cycle**: Trimestral
