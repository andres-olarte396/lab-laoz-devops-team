# 🧪 QA Estimation Guide - Dev + QA Inclusive Model

## 📋 Resumen Ejecutivo

**Problema**: Estimaciones solo consideran dev effort, ignorando QA, causando:

- Stories "done" pero sin testear (no truly done)
- QA bottleneck al final del sprint (rush testing)
- Bugs escapan a producción (insufficient test time)
- QA trabaja overtime constantemente

**Solución**: **QA-Inclusive Estimation** - Estimar dev effort + QA effort juntos en Sprint Planning, con QA effort típicamente 20-40% del dev effort.

**Beneficio**:

- Stories done = dev complete + QA complete
- QA tiene tiempo suficiente para testing completo
- Menos bugs en producción
- Sprint commitment más realista

---

## 🎯 QA-Inclusive Estimation Model

### Concept

**Old Way** (Dev-Only):

```
Story Points = Dev Effort (solo)
QA testing = "Lo haremos cuando dev termine" (sin planear)
```

**New Way** (QA-Inclusive):

```
Story Points = Dev Effort + QA Effort
QA testing = Planeado explícitamente en estimation
```

---

### Formula Base

```
Total Story Points = Dev Points + QA Points

Donde:
QA Points = Dev Points × QA Factor

QA Factor típico: 0.2 - 0.4 (20% - 40% del dev effort)
```

**Ejemplo**:

```
Story: User login con Google OAuth
Dev effort: 5 points (3 días)
QA factor: 0.3 (30%)
QA effort: 5 × 0.3 = 1.5 points (1 día)
Total: 6.5 points ≈ 7 points
```

---

### Cómo Determinar QA Factor

**QA Factor varía por tipo de story**:

#### 🟢 **Low Complexity** (QA Factor: 0.2 = 20%)

**Ejemplos**:

- Bug fix simple
- Copy changes (texto en UI)
- CSS tweaks (styling)
- Feature flag toggle

**QA Scope**:

- Smoke test: verificar fix funciona
- Regression test: verificar no rompió nada adyacente
- 1-2 browsers, 1 device

**Effort**: 1-2 horas de QA por 1 día de dev

---

#### 🟡 **Medium Complexity** (QA Factor: 0.3 = 30%)

**Ejemplos**:

- CRUD operations (Create/Read/Update/Delete)
- Form validation
- UI flow nuevo (3-5 pantallas)
- API endpoint nuevo

**QA Scope**:

- Functional testing: happy path + edge cases
- Regression testing: áreas relacionadas
- Cross-browser: Chrome, Firefox, Safari
- Cross-device: Desktop + Mobile

**Effort**: 1 día de QA por 2-3 días de dev

---

#### 🔴 **High Complexity** (QA Factor: 0.4 = 40%)

**Ejemplos**:

- Payment integration (Stripe, PayPal)
- Authentication/Authorization changes
- Data migration
- Performance optimization
- Third-party API integration

**QA Scope**:

- Functional testing: comprehensive (happy + edge + error cases)
- Security testing: SQL injection, XSS, auth bypass
- Performance testing: load testing, stress testing
- Integration testing: end-to-end flows
- Regression testing: full suite
- Cross-browser + cross-device completo

**Effort**: 2 días de QA por 3-5 días de dev

---

#### 🔥 **Very High Complexity** (QA Factor: 0.5+ = 50%+)

**Ejemplos**:

- Arquitectura nueva (microservices, event-driven)
- Legacy system migration
- Compliance-critical (GDPR, HIPAA, SOC2)
- Real-time features (WebSockets, notifications)

**QA Scope**:

- Todo lo anterior +
- Chaos engineering (fault injection)
- Penetration testing (security audit)
- Compliance validation
- Multi-environment testing (dev, staging, prod-like)

**Effort**: 3+ días de QA por 5+ días de dev

**Nota**: Stories con QA Factor >0.5 probablemente son demasiado grandes → dividir en sub-stories

---

## 📝 Estimation Process en Sprint Planning

### Pre-Planning: QA Review de Stories (L-1)

**Owner**: QA Lead

**Actividades**:

1. **Review top 10-15 candidate stories**

   - Leer User Story y Acceptance Criteria
   - Identificar complejidad de testing

2. **Estimate QA Effort (rough)**

   - Low/Medium/High complexity
   - QA Factor: 0.2, 0.3, 0.4

3. **Identificar QA Blockers**

   - ¿Hay test data disponible?
   - ¿Necesitamos setup especial (ej: Stripe test account)?
   - ¿Requiere devices específicos?

4. **Communicate a Tech Lead**
   - Slack: "Para TEAM-101, necesitaré Stripe test keys antes de empezar QA"

---

### Durante Sprint Planning: Estimation Conjunta

**Participants**:

- Developers (estiman dev effort)
- QA (estima QA effort)
- Tech Lead (facilita)

**Process (por story)**:

#### Step 1: Dev Estimation (5 min)

**Developers** estiman dev effort:

- Planning Poker: 1, 2, 3, 5, 8, 13
- Converge en dev points (ej: 5 points)

#### Step 2: QA Complexity Assessment (2 min)

**QA Lead** presenta:

- "Esta story es Medium complexity (CRUD + validación)"
- "QA scope: functional + regression + 3 browsers"
- "Estimo QA Factor 0.3 (30%)"

#### Step 3: QA Estimation (2 min)

**QA** estima QA effort:

- QA Points = Dev Points × QA Factor
- Ejemplo: 5 dev points × 0.3 = 1.5 QA points

**Discusión**:

- Devs pueden challenge: "¿Por qué 30%? Parece simple"
- QA explica: "Hay 8 edge cases en validación + cross-browser testing"
- Ajustan si hay consenso

#### Step 4: Total Story Points (1 min)

**Tech Lead** suma:

```
Total = Dev Points + QA Points
Total = 5 + 1.5 = 6.5 ≈ 7 points
```

**Nota**: Redondear a Fibonacci más cercano (1, 2, 3, 5, 8, 13)

---

### Output: Story con QA Estimate

**Jira Story Updated**:

```markdown
**TEAM-101: User login con Google OAuth**

**Estimate**: 7 story points

- Dev effort: 5 points
- QA effort: 2 points (QA Factor: 0.3, Medium complexity)

**QA Scope**:

- ✅ Functional: Login happy path + error cases
- ✅ Regression: Verify existing auth flows still work
- ✅ Cross-browser: Chrome, Firefox, Safari
- ✅ Cross-device: Desktop + Mobile web
- ✅ Security: OAuth token handling, no credentials leak

**QA Prerequisites**:

- Google OAuth test account (DevOps)
- Test users in staging DB (Backend)

**Timeline**:

- Day 1-3: Dev work (5 points)
- Day 4-5: QA testing (2 points)
```

---

## 🔄 QA Workflow Durante el Sprint

### Day 1-3: Dev Work

**Developer**:

- Implementa feature
- Unit tests
- Code review
- Deploy a staging

**QA** (en paralelo):

- Prepara test cases basado en AC
- Setup test data / environment
- Identifica edge cases adicionales

---

### Day 4: Dev → QA Handoff

**Developer** comunica:

```
Slack: @qa.lead
TEAM-101 ready for QA ✅

- Deployed to staging
- Test account: test@example.com / password123
- Known issues: None
- Notes: OAuth consent screen has staging warning (expected)

Jira ticket: [link]
```

**QA Lead** verifica:

- ✅ Story está en staging
- ✅ AC claros y completos
- ✅ Test data disponible
- ✅ No blockers conocidos

**Si NO está ready**:

- QA rechaza: "Missing test data, cannot start QA"
- Dev debe resolver antes de handoff

---

### Day 4-5: QA Testing

**QA** ejecuta test plan:

#### Day 4 AM: Functional Testing

- Happy path (30 min)
- Edge cases (1h)
- Error handling (30 min)

#### Day 4 PM: Cross-Browser Testing

- Chrome: ✅ Pass
- Firefox: ✅ Pass
- Safari: ❌ Fail - OAuth redirect broken

**Bug Found** → QA crea bug ticket:

```
**BUG-456: OAuth redirect fails in Safari**

Severity: High
Blocks: TEAM-101

Steps to Reproduce:
1. Open Safari
2. Click "Login with Google"
3. Authorize in Google
4. Redirect to app

Expected: User logged in
Actual: Stuck on redirect page

Browser: Safari 15.6
OS: macOS Ventura
```

**Developer** fixes bug (2h)

#### Day 5 AM: Regression Testing

- Re-test Safari: ✅ Pass
- Verify existing auth flows: ✅ Pass

#### Day 5 PM: Final Sign-off

- All tests passed
- No blockers
- QA marks story as **Done** ✅

---

## 📊 QA Capacity Planning

### Calculate QA Capacity per Sprint

**Formula**:

```
QA Capacity (points) = # QA Engineers × Points per Person per Sprint

Typical: 1 QA = 10-15 points/sprint (depende de team size)
```

**Ejemplo**:

```
Team:
- 5 Developers: 50 dev points/sprint
- 2 QA Engineers: 20 QA points/sprint

Si QA Factor promedio = 0.3:
- Dev work: 50 points → requiere 50 × 0.3 = 15 QA points
- QA capacity: 20 points
- Sobrante: 5 points para automation o exploratory testing ✅
```

---

### Red Flag: QA Bottleneck

**Síntoma**:

```
Sprint Capacity:
- Dev: 50 points
- QA: 10 points (solo 1 QA en team de 5 devs)

Si QA Factor = 0.3:
- Dev work 50 points → requiere 15 QA points
- QA capacity: 10 points
- Deficit: -5 points ❌
```

**Resultado**:

- Stories quedan "dev done" pero no QA done
- QA bottleneck al final del sprint
- Stories spillean a siguiente sprint

**Solución**:

1. **Hire more QA**: Ratio típico 1 QA por 3-4 devs
2. **Reduce dev capacity**: Commit a solo 35 dev points (requiere 10.5 QA points)
3. **Automation**: Devs escriben tests automatizados → reduce QA effort

---

## 🤖 QA Automation Strategy

### Objetivo: Reducir QA Factor Long-Term

**Sin Automation**:

```
QA Factor = 0.3-0.4 (30-40% del dev effort)
```

**Con Automation**:

```
QA Factor = 0.15-0.25 (15-25% del dev effort)
```

**Ahorro**: 50% reduction en QA manual effort

---

### Qué Automatizar (Prioridad)

#### 1. **Regression Tests** (Prioridad: 🔥 Alta)

**Por Qué**: Se ejecutan CADA sprint, high ROI

**Ejemplos**:

- Login flow (se toca frecuentemente)
- Checkout flow (revenue-critical)
- User registration

**Tools**:

- E2E: Playwright, Cypress
- API: Postman, REST Assured

**ROI**:

- Manual: 2h cada sprint × 26 sprints/año = 52h/año
- Automation: 8h setup + 0.5h maintenance/sprint × 26 = 21h/año
- Ahorro: 31h/año (60% reducción)

---

#### 2. **Smoke Tests** (Prioridad: 🔥 Alta)

**Por Qué**: Se ejecutan CADA deploy (múltiples veces/día)

**Ejemplos**:

- Homepage carga
- Critical endpoints responden 200 OK
- DB connectivity

**Tools**:

- Smoke test suite en CI/CD
- Health check endpoints

**ROI**:

- Manual: 15 min × 5 deploys/día × 250 días = 312h/año
- Automation: 4h setup + 1h maintenance/mes × 12 = 16h/año
- Ahorro: 296h/año (95% reducción)

---

#### 3. **Happy Path Tests** (Prioridad: 🟡 Media)

**Por Qué**: Ejecutan frecuentemente, pero menos críticos que regression

**Ejemplos**:

- CRUD operations estándar
- Form submissions

**Tools**:

- Unit tests (devs escriben)
- Integration tests

---

#### 4. **Edge Cases** (Prioridad: 🟢 Baja)

**Por Qué**: Menos frecuentes, automation ROI bajo

**Estrategia**: Mantener manual, pero documentar en test cases

**Ejemplos**:

- "¿Qué pasa si user ingresa emoji en username?"
- "¿Qué pasa si network se cae mid-transaction?"

---

### QA Automation Budget (20% Rule)

**Regla**:

> Dedicar 20% de QA capacity a automation (similar a tech debt budget)

**Ejemplo**:

```
Sprint Capacity:
- QA: 20 points total
- Manual testing: 16 points (80%)
- Automation: 4 points (20%)
```

**Automation Work**:

- Escribir E2E tests para regression suite
- Mantener tests existentes (fix flaky tests)
- CI/CD integration

**Long-term**:

- Automation coverage crece gradualmente
- Manual QA effort decrece
- QA Factor baja de 0.3 a 0.2 → más capacity para exploratory testing

---

## 📊 Métricas de QA

### Métrica #1: QA Coverage

**Formula**:

```
(Stories con QA complete / Total stories) × 100
```

**Target**: 100%

**Red Flag**:

- <90% → Stories están bypassing QA (technical debt)

---

### Métrica #2: Bug Escape Rate

**Formula**:

```
(Bugs encontrados en prod / Total bugs) × 100
```

**Target**: <10%

**Insight**:

- <10% → QA está catching mayoría de bugs
- > 20% → QA testing insuficiente o rushed

---

### Métrica #3: QA Bottleneck Index

**Formula**:

```
(Stories bloqueadas esperando QA / Total stories) × 100
```

**Target**: <15%

**Red Flag**:

- > 25% → QA capacity insuficiente, necesitan más QAs o automation

---

### Métrica #4: Test Automation Coverage

**Formula**:

```
(Test cases automatizados / Total test cases) × 100
```

**Target**: >60% (regression + smoke tests)

**Tracking**:

- Trend: debería subir gradualmente
- Goal: 80% automation para regression tests

---

## 🎭 Roles y Responsabilidades

### QA Lead

**Pre-Planning**:

- ✅ Review candidate stories para estimar QA effort
- ✅ Identificar QA blockers (test data, setup)
- ✅ Preparar QA Factor estimates (Low/Med/High complexity)

**Sprint Planning**:

- ✅ Participar en estimation (votar QA points)
- ✅ Validar que QA capacity es suficiente
- ✅ Rechazar sprint commitment si QA capacity insuficiente

**Durante Sprint**:

- ✅ Ejecutar test plan por story
- ✅ Comunicar bugs a developers inmediatamente
- ✅ Sign-off stories cuando QA complete

**Automation**:

- ✅ Dedicar 20% de capacity a test automation
- ✅ Priorizar regression tests y smoke tests

---

### Developers

**Sprint Planning**:

- ✅ Estimar dev effort
- ✅ Colaborar con QA en total estimate

**Durante Sprint**:

- ✅ Escribir unit tests (no QA responsability)
- ✅ Handoff a QA con environment ready y test data
- ✅ Fix bugs encontrados por QA con prioridad

**Automation**:

- ✅ Escribir integration tests cuando corresponda
- ✅ Ayudar QA a setup automation framework

---

### Tech Lead

**Sprint Planning**:

- ✅ Facilitar estimation conjunta (dev + QA)
- ✅ Verificar que QA capacity es suficiente
- ✅ Ajustar sprint scope si QA bottleneck detectado

**Durante Sprint**:

- ✅ Monitor QA bottleneck (stories esperando QA)
- ✅ Re-priorizar si QA está sobrecargado

---

### Product Owner

**Sprint Planning**:

- ✅ Aceptar que estimates incluyen QA effort
- ✅ Entender que "Done" = dev done + QA done

**Durante Sprint**:

- ✅ No presionar para skipear QA por urgencia
- ✅ Priorizar bugs encontrados por QA

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup

**Week 1**:

- [ ] QA Lead + Tech Lead revisan este documento
- [ ] Comunicar a team: "Vamos a estimar dev + QA juntos"
- [ ] Crear template de QA Scope en Jira stories

**Week 2**:

- [ ] QA Lead identifica QA Factor para tipos comunes de stories
- [ ] Trial run: Estimar 5 stories con QA-inclusive model

---

### Sprint 1-3: Pilot

- [ ] Sprint Planning: Estimar todas stories con dev + QA points
- [ ] Track QA bottleneck: ¿Stories esperando QA?
- [ ] Retrospective: ¿QA capacity fue suficiente?

---

### Sprint 4+: Optimize

- [ ] Ajustar QA Factors basado en actuals
- [ ] QA automation: 20% capacity dedicado
- [ ] Metrics review: Bug escape rate, QA coverage

---

## ✅ Success Criteria

### Mes 1

- ✅ 100% de stories estimadas con dev + QA points
- ✅ QA coverage >90%

### Mes 2-3

- ✅ QA bottleneck <15% de stories
- ✅ Bug escape rate <15%
- ✅ Test automation >40%

### Mes 4+

- ✅ QA capacity match dev capacity (no bottleneck)
- ✅ Bug escape rate <10%
- ✅ Test automation >60%
- ✅ QA Factor baja gradualmente (automation effect)

---

## 🔗 Links Relacionados

- [Ceremonias: Sprint Planning](README.md#sprint-planning) - Donde se hace estimation
- [Definition of Ready](definition-of-ready.md) - Test scenarios parte del DoR
- [Tech Debt Budget](tech-debt-budget.md) - Automation es tech debt investment
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

## 📚 Ejemplos

### ✅ Ejemplo: Story con QA-Inclusive Estimate

```markdown
**TEAM-201: Product filtering by price and category**

**Total Estimate**: 8 story points

- Dev effort: 5 points (3 días)
- QA effort: 3 points (2 días) - QA Factor: 0.6 (High complexity)

**QA Complexity: High** (0.4 factor, but +20% for cross-browser)

**QA Scope**:
✅ Functional Testing (1 día):

- Filter by price range: $0-50, $50-100, $100+
- Filter by category: Electronics, Clothing, Home
- Combined filters: price + category
- Clear filters
- Empty results state
- URL persistence (filter params in URL)

✅ Cross-Browser Testing (0.5 día):

- Chrome, Firefox, Safari (desktop)
- iOS Safari, Android Chrome (mobile)

✅ Performance Testing (0.5 día):

- Filter 10,000 products: <500ms response
- Load test: 100 concurrent users

**QA Prerequisites**:

- 10,000 sample products in staging DB
- Price data populated correctly
- Category taxonomy complete

**Timeline**:

- Day 1-3: Dev implementation (5 points)
- Day 4-5: QA testing (3 points)

**Automation Plan** (Sprint N+1):

- E2E test for happy path (1 point)
- Performance test in CI/CD (1 point)
```

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: QA Lead + Tech Lead  
**Review Cycle**: Trimestral
