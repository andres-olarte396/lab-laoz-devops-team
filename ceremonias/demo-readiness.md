# 🎬 Demo Readiness - Smoke Tests & Backup Plan

## 📋 Resumen Ejecutivo

**Problema**: Demos en Sprint Review fallan por:

- Demo environment down o broken
- Data de test incorrecta o missing
- "Funciona en mi laptop pero no en staging"
- Last-minute discoveries de bugs críticos

**Solución**: **Demo Readiness Process** con smoke tests L-1 (día antes) y backup plan.

**Beneficio**:

- 0 demos rotos en Sprint Reviews
- Confidence alta al presentar
- Professional image ante stakeholders
- Backup plan si algo sale mal

---

## 🎯 Demo Readiness Checklist

### L-1: Day Before Sprint Review

#### 1. **Environment Smoke Test** (30 min)

**Owner**: Developer presentando + QA

**Activities**:

✅ **Verify Demo Environment is UP**

```bash
# Health check
curl https://staging.app.com/health
# Expected: 200 OK

# Database connectivity
curl https://staging.app.com/api/status
# Expected: {"db": "connected", "cache": "connected"}
```

✅ **Test CADA Feature Flow End-to-End**

Por cada feature en demo:

**Example: User Login con Google OAuth**

```
Test Steps:
1. Open https://staging.app.com
2. Click "Login with Google"
3. Enter test account: demo@example.com / Demo123!
4. Authorize in Google consent screen
5. Verify redirect to app
6. Verify user logged in (see username in header)

✅ Expected: Login successful
❌ Actual: Redirect fails in Safari

→ Bug found L-1 → Fix urgently or remove from demo
```

**Test ALL paths**:

- Happy path
- 1-2 edge cases (if demoing error handling)
- Cross-browser (if relevant): Chrome, Safari, Firefox

---

#### 2. **Test Data Verification** (15 min)

✅ **Verify Test Accounts Exist**

```sql
-- Example
SELECT * FROM users WHERE email = 'demo@example.com';
-- Expected: 1 row
```

✅ **Verify Sample Data**

```
Check:
- Products table: >100 products para filtering demo
- Orders table: 10 sample orders para dashboard demo
- Test credit cards: 4242 4242 4242 4242 (Stripe test)
```

✅ **Reset Demo Data if Needed**

```bash
# Script to reset staging data
./scripts/seed-demo-data.sh

# Verify
curl https://staging.app.com/api/products?limit=10
# Expected: 10 products con realistic data
```

---

#### 3. **Performance Check** (10 min)

✅ **Test Load Time**

```
Open Chrome DevTools → Network tab
Load https://staging.app.com

Check:
- Page load: <3 segundos (acceptable para demo)
- API calls: <500ms per endpoint

⚠️ If >5 segundos → Investigate (cache issue? DB query slow?)
```

---

#### 4. **Visual Check** (10 min)

✅ **Cross-Browser Visual Regression**

Test en:

- Chrome (primary)
- Safari (if stakeholders use Mac)
- Mobile (if demoing mobile features)

**Red Flags**:

- UI broken (CSS no carga)
- Images missing
- Layout roto en mobile

---

#### 5. **Pre-Record Backup Video** (20 min)

**WHY**: Si staging crashea during demo → show video como backup

**How**:

1. Use Loom o QuickTime para screen recording
2. Record demo flow completo (5-10 min)
3. Narrate: "Aquí el usuario hace login..."
4. Save video en Google Drive + link en Slack

**Backup Plan**:

```
Si staging falla durante Sprint Review:
→ Tech Lead dice: "Staging está teniendo issues,
   tenemos pre-recorded video del feature funcionando"
→ Show video (2-3 min)
→ Offer to demo in-person post-Review para stakeholders
```

---

### Morning of Sprint Review (T-2h before)

#### 6. **Final Smoke Test** (15 min)

**Owner**: Developer presenting

**Activities**:

✅ **Re-test Critical Path**

- Login flow: ✅ Works
- Product filtering: ✅ Works
- Checkout: ✅ Works

✅ **Check Staging Status**

```bash
curl https://staging.app.com/health
# Expected: 200 OK
```

**If ❌ Staging is down**:

1. Alert DevOps immediately: "@devops.lead staging down!"
2. Estimate time to fix: <1h → wait, >1h → use backup video
3. Communicate to stakeholders: "We'll use pre-recorded demo due to staging issues"

---

## 🎬 Demo Best Practices

### Setup Your Demo Script (L-2)

**Template**:

```markdown
## Demo Script: User Login con Google OAuth

**Time**: 5 min total (3 min demo + 2 min Q&A)

**Business Context** (30 seg):
"Antes: Users tenían que crear password, alta fricción, 40% drop-off.
Ahora: Login con Google, 1 click, target es 60% de users usan OAuth."

**Live Demo** (2 min):

1. **Show Before State** (30 seg):

   - "Esta es la pantalla de login actual" (screenshot)
   - "User debe ingresar email, password, confirmar password"

2. **Show After State - OAuth Flow** (1 min):

   - Navigate to https://staging.app.com
   - Click "Login with Google" button
   - Google consent screen appears
   - Click "Allow"
   - **[WAIT for redirect - 2 segundos]**
   - User logged in → show username in header
   - "Login completado en 3 clicks vs 7 antes"

3. **Edge Case Demo** (30 seg) - Optional:
   - "Si user cancela OAuth → vuelve a login con mensaje claro"
   - Click "Login with Google" → Click "Cancel" → Show error message

**Key Talking Points**:

- ✅ Secure: No passwords stored, Google handles auth
- ✅ Fast: 1 click login
- ✅ User-friendly: 80% of users ya tienen Google account

**Q&A Prep** (anticipar preguntas):

- Q: "¿Qué pasa con users que no tienen Google?"
  A: "Traditional email/password sigue disponible, OAuth es optional"
- Q: "¿Security concerns?"
  A: "OAuth 2.0 standard, mismo protocolo que Gmail, YouTube"
```

---

### During Demo: Presentation Tips

**1. Slow Down**

- ❌ "Y aquí hago click y login funciona" (demasiado rápido)
- ✅ "Voy a hacer click en 'Login with Google'... [CLICK]...
  ahora Google nos pide autorización... [WAIT]...
  y ahora estamos logged in"

**2. Narrate Your Actions**

- Stakeholders no saben qué estás haciendo si no narras
- "Ahora voy a filtrar productos por precio..."

**3. Handle Delays Gracefully**

- Si API tarda 3 segundos: "Esto está cargando, en producción será <1 segundo con cache"
- No quedarte en silencio awkward

**4. Show, Don't Tell**

- ❌ "El botón es azul" → ✅ [Mover cursor al botón azul]
- ❌ "Hay mensaje de error" → ✅ [Scroll para que sea visible en screen]

---

## 🚨 Troubleshooting: Broken Demos

### Scenario 1: Feature Works pero UI Broken

**Example**: CSS no carga, botón invisible

**Immediate Action**:

1. Hard refresh: Ctrl+Shift+R (puede ser cache issue)
2. Si persiste → usar backup video
3. Post-demo: Fix CSS, re-deploy

**Prevention**:

- L-1 smoke test debió atrapar esto
- Add visual regression test en CI/CD

---

### Scenario 2: API Returns Error

**Example**: 500 Internal Server Error al hacer login

**Immediate Action**:

1. Check Staging logs: `kubectl logs pod/api-server`
2. Si es quick fix (<5 min) → fix y retry
3. Si no → backup video

**Prevention**:

- L-1 smoke test
- Staging monitoring (alert si 500 errors spike)

---

### Scenario 3: Test Data Missing

**Example**: No hay productos para demo de filtering

**Immediate Action**:

1. Run seed script: `./scripts/seed-demo-data.sh`
2. Verify: `curl /api/products?limit=10`
3. Si no funciona → backup video

**Prevention**:

- L-1 verify test data
- Automate: Seed script runs nightly en staging

---

### Scenario 4: Staging Completamente Down

**Example**: DNS no resuelve, server crashed

**Immediate Action**:

1. Alert DevOps: "@devops.lead staging down!"
2. Check status page: https://status.staging.app.com
3. Estimate fix time:
   - <10 min → delay demo 10 min
   - > 10 min → use backup video

**Prevention**:

- Staging uptime monitoring (99% SLA)
- Weekly staging health check

---

## 📊 Métricas

### Metric #1: Demo Success Rate

**Formula**:

```
(Sprint Reviews con 0 broken demos / Total Sprint Reviews) × 100
```

**Target**: 100%

**Red Flags**:

- <90% → Demo readiness process no se está siguiendo

---

### Metric #2: Backup Video Usage Rate

**Formula**:

```
(Sprint Reviews donde usamos backup video / Total) × 100
```

**Target**: <10%

**Insight**:

- 0% → Great! Staging siempre funciona
- <10% → Acceptable (occasional staging issues)
- > 20% → Staging es unreliable, needs investment

---

### Metric #3: Stakeholder Confidence (Survey)

**Question**: "¿Demos fueron smooth y professional?" (1-5)

**Target**: >4.0

---

## 🎭 Roles y Responsabilidades

### Developer (Presenter)

**L-2**:

- ✅ Escribir demo script (business context + steps)
- ✅ Ensayar demo (15 min run-through con team member)

**L-1**:

- ✅ Smoke test environment (30 min)
- ✅ Verify test data
- ✅ Pre-record backup video
- ✅ Alert team si hay issues

**Morning of Review (T-2h)**:

- ✅ Final smoke test (15 min)
- ✅ Verify staging up

**During Review**:

- ✅ Present demo confidently
- ✅ Narrate actions
- ✅ Use backup video si staging fails

---

### QA

**L-1**:

- ✅ Help smoke test (verify test scenarios)
- ✅ Validate test data correctness

---

### DevOps

**L-1**:

- ✅ Verify staging uptime (99%+ last 7 days)
- ✅ On-call durante Sprint Review (si staging crashea)

**Morning of Review**:

- ✅ Monitor staging health

---

### Tech Lead

**L-1**:

- ✅ Verify all presenters han hecho smoke test
- ✅ Verify backup videos existen

**During Review**:

- ✅ Backup presenter si primary falta
- ✅ Troubleshoot si demo fails (call DevOps, switch to video)

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup

- [ ] Create smoke test checklist
- [ ] Setup staging monitoring (uptime, error rate)
- [ ] Create seed script para demo data
- [ ] Train team en Loom/QuickTime para backup videos

---

### Sprint 1-3: Pilot

- [ ] Enforce L-1 smoke test policy
- [ ] Track demo success rate
- [ ] Iterate basado en failures

---

### Sprint 4+: Optimize

- [ ] Demo success rate 100%
- [ ] Backup video usage <10%
- [ ] Stakeholder confidence >4.0

---

## ✅ Success Criteria

### Mes 1

- ✅ 100% of demos have L-1 smoke test
- ✅ Demo success rate >90%

### Mes 2-3

- ✅ Demo success rate 100%
- ✅ Backup videos exist para todos los demos
- ✅ Staging uptime >99%

### Mes 4+

- ✅ Process es hábito (team doesn't forget)
- ✅ Stakeholders confían en demos (no sorpresas)

---

## 🔗 Links Relacionados

- [Ceremonias: Sprint Review](README.md#sprint-review) - Ceremonia donde se presenta
- [Stakeholder Matrix](stakeholder-matrix.md) - Audiencia para demos
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis

---

## 📚 Antipatterns

### ❌ Antipattern #1: "It Works on My Machine"

**Síntoma**: Dev no testa en staging, solo localhost

**Por Qué Falla**: Staging puede tener config diferente, breaking demo

**Solución**: L-1 smoke test MUST ser en staging environment

---

### ❌ Antipattern #2: No Backup Plan

**Síntoma**: Staging crashes, presenter improvisa excusas

**Por Qué Falla**: Looks unprofessional, stakeholders pierden confianza

**Solución**: ALWAYS have backup video pre-recorded

---

### ❌ Antipattern #3: Last-Second Testing

**Síntoma**: Testing staging 10 minutos before Sprint Review

**Por Qué Falla**: No hay tiempo para fix si hay issues

**Solución**: L-1 (day before) is MINIMUM, L-2 is better

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Tech Lead + Development Team  
**Review Cycle**: Trimestral
