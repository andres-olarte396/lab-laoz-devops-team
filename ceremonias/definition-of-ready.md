# ✅ Definition of Ready (DoR) - Criterios de Aceptación para User Stories

## 📋 Resumen Ejecutivo

**Problema**: User stories llegan a Sprint Planning sin suficiente detalle, causando:

- Estimaciones incorrectas (±50% error)
- Trabajo bloqueado mid-sprint esperando clarificaciones
- Scope creep cuando se descubren requerimientos ocultos
- Re-work por malentendidos entre Producto y Desarrollo

**Solución**: Checklist estructurado (Definition of Ready) aplicado en Backlog Refinement antes de Sprint Planning.

**Beneficio**: Stories "ready" → estimaciones precisas, 0 blockers por falta de info, sprint fluye sin interrupciones.

---

## 🎯 ¿Qué es Definition of Ready?

**Definición**:

> Criterios que una User Story debe cumplir ANTES de ser considerada para Sprint Planning.

**Analogía**:

- DoR = "Ingredientes listos antes de cocinar"
- DoD = "Platillo terminado y servido"

Si los ingredientes no están listos (DoR), el chef (dev team) no puede cocinar eficientemente.

**Ownership**:

- **Product Owner**: Responsable de que stories cumplan DoR
- **Team**: Valida DoR en Backlog Refinement
- **Scrum Master**: Facilita y hace enforcement

---

## 📝 DoR Checklist Completo

### ✅ Nivel 1: Información Básica (Obligatorio)

```markdown
User Story Template:

**Como** [tipo de usuario]
**Quiero** [objetivo/necesidad]
**Para** [beneficio/razón de negocio]

**Acceptance Criteria** (formato Given/When/Then):

1. **Given** [contexto/precondición]
   **When** [acción del usuario]
   **Then** [resultado esperado]
2. **Given** [...]
   **When** [...]
   **Then** [...]

(Mínimo 3 AC, máximo 8)
```

**Criterios**:

- [ ] **Título descriptivo**: Max 60 caracteres, describe el valor

  - ✅ Bueno: "Usuario puede filtrar productos por precio y categoría"
  - ❌ Malo: "Implementar filtros"

- [ ] **User Story en formato estándar**: Como/Quiero/Para completo

  - Sin "Como developer quiero..." (esos son tasks técnicos)

- [ ] **Acceptance Criteria claros**: Mínimo 3, formato Given/When/Then

  - Cada AC debe ser testeable
  - Cubren happy path + edge cases + error handling

- [ ] **Business Value claro**: Por qué esto importa al negocio/usuario
  - Impacto en revenue, engagement, UX, compliance, etc.

---

### ✅ Nivel 2: Diseño y UX (Para stories con UI)

- [ ] **Mockups/Wireframes disponibles**:

  - Figma link o screenshots en Jira
  - Desktop + Mobile (si aplica)
  - Estados: Default, Hover, Active, Disabled, Error, Loading

- [ ] **Design handoff completo**:

  - Spacing, typography, colors especificados
  - Assets exportados (iconos, imágenes)
  - Interactions documentadas (animations, transitions)

- [ ] **Edge cases visuales definidos**:

  - ¿Qué pasa con textos muy largos?
  - ¿Qué pasa si no hay data?
  - ¿Qué muestra durante loading?

- [ ] **Responsive behavior claro**:
  - Breakpoints: Mobile (<768px), Tablet (768-1024px), Desktop (>1024px)
  - ¿Cómo cambia layout en cada breakpoint?

---

### ✅ Nivel 3: Técnico y Arquitectura (Para stories complejas)

- [ ] **API contracts definidos** (si aplica):

  - Endpoints: URL, método (GET/POST/etc), params
  - Request/Response schemas (JSON examples)
  - Error codes esperados (400, 404, 500, etc.)

- [ ] **Dependencies identificadas**:

  - ¿Depende de otras stories? (marcar en Jira)
  - ¿Requiere infra nueva? (DB, cache, queue, etc.)
  - ¿Requiere third-party services? (Stripe, SendGrid, etc.)

- [ ] **Data model claro**:

  - ¿Qué tablas/colecciones se afectan?
  - ¿Hay migrations necesarias?
  - ¿Hay data existente que migrar?

- [ ] **Performance requirements**:

  - Latency: <200ms, <500ms, <1s?
  - Throughput: requests/sec esperados
  - Scale: 100 users, 10K users, 1M users?

- [ ] **Security & compliance**:
  - ¿Maneja PII (Personally Identifiable Information)?
  - ¿Requiere autenticación/autorización?
  - ¿GDPR, HIPAA, SOC2 compliance aplica?

---

### ✅ Nivel 4: Testing y QA

- [ ] **Test scenarios identificados**:

  - Happy path (mínimo 1)
  - Edge cases (mínimo 2-3)
  - Error scenarios (mínimo 2)
  - Ejemplos escritos en AC

- [ ] **Test data disponible**:

  - ¿Hay test users/accounts?
  - ¿Hay sample data en staging?
  - ¿Se puede generar data fácilmente?

- [ ] **Accessibility requirements** (si aplica):

  - WCAG 2.1 Level AA compliance
  - Keyboard navigation
  - Screen reader compatibility
  - Color contrast ratios

- [ ] **Browser/Device support**:
  - Chrome, Firefox, Safari, Edge?
  - iOS Safari, Android Chrome?
  - Versiones mínimas soportadas

---

### ✅ Nivel 5: Otros

- [ ] **Story size apropiado**:

  - Estimado en 1-13 story points
  - Si >13 → dividir en sub-stories
  - Completable en 1 sprint (2 semanas)

- [ ] **No blockers conocidos**:

  - No esperando decisiones de management
  - No esperando budget approval
  - No esperando third-party vendor

- [ ] **Equipo tiene skills necesarios**:
  - Si requiere skill nuevo (ej: GraphQL) → spike story primero
  - Si requiere especialista ausente → postponer

---

## 🔍 Criterios INVEST

**Mnemotecnia para validar calidad de User Stories**:

### **I**ndependent (Independiente)

- ✅ Story puede implementarse sin depender de otras
- ✅ Puede priorizarse y re-ordenarse libremente
- ❌ "Implementar login" depende de "Crear DB de usuarios"

**Cómo lograrlo**:

- Identificar dependencies en Backlog Refinement
- Re-ordenar backlog para resolver dependencies primero
- Si es inevitable, marcar como "Blocked by TEAM-XXX" en Jira

### **N**egotiable (Negociable)

- ✅ Detalles de implementación son flexibles
- ✅ Team puede proponer alternativas técnicas
- ❌ "Debe usar PostgreSQL porque el PO lo dijo"

**Cómo lograrlo**:

- Story describe QUÉ (outcome), no CÓMO (implementation)
- Ejemplo: "Usuario puede guardar favoritos" (no "Implementar Redis cache para favoritos")

### **V**aluable (Valioso)

- ✅ Entrega valor al usuario final o negocio
- ✅ Stakeholder pagaría por esta feature
- ❌ "Refactorizar código legacy" (técnicamente necesario pero no valuable para usuario)

**Cómo validarlo**:

- Pregunta: "¿Qué pasaría si NO hacemos esto?"
- Si la respuesta es "Nada cambia para el usuario" → no es valuable

**Tech debt exceptions**:

- Puede ser valuable si: mejora performance, reduce bugs, habilita features futuras

### **E**stimable (Estimable)

- ✅ Team tiene suficiente info para estimar (±50% accuracy)
- ❌ "Integrar con third-party API" (sin documentación de la API)

**Cómo lograrlo**:

- Si no es estimable → hacer spike story primero (time-boxed research)
- Spike output = documento con findings + estimate

### **S**mall (Pequeño)

- ✅ Completable en 1 sprint (2 semanas)
- ✅ 1-13 story points
- ❌ "Rediseñar toda la app" (épica, no story)

**Cómo lograrlo**:

- Dividir en vertical slices (cada slice entrega valor end-to-end)
- Ejemplo: "Login completo" → "Login con email/password" + "Login con Google OAuth" + "Remember me"

### **T**estable (Testeable)

- ✅ Acceptance Criteria son binarios (pass/fail)
- ✅ QA puede escribir test cases sin ambiguedad
- ❌ "Mejorar performance" (¿cuánto? ¿cómo medir?)

**Cómo lograrlo**:

- AC deben incluir métricas: "<200ms latency", "99% uptime", "0 accessibility errors"

---

## 🔄 Proceso: Backlog Refinement (2 Sesiones)

### Sesión 1: Pre-Refinement (1 semana antes de Sprint Planning)

**Objetivo**: Product Owner prepara stories para revisión del equipo

**Duración**: N/A (trabajo async del PO)

**Actividades**:

1. **PO crea User Stories en Jira**

   - Usar template de User Story
   - Escribir 3-8 Acceptance Criteria
   - Agregar mockups/wireframes si aplica

2. **PO auto-evalúa contra DoR checklist**

   - Marcar items completados
   - Identificar gaps (ej: falta API contract)

3. **PO triage stories**

   - **Ready for Refinement**: >80% de DoR completo
   - **Needs Work**: <50% de DoR completo (postponer)
   - **Needs Spike**: No estimable, requiere research

4. **PO comunica en Slack** (3 días antes de Refinement)

   ```
   📋 Backlog Refinement Prep

   **Sesión**: Viernes 10am (1h)
   **Stories a Refinar**: 8 stories (~50 story points)

   Please review:
   - TEAM-101: User can filter products by price ⭐ (priority)
   - TEAM-102: Checkout flow optimization
   - TEAM-103: Email notifications for orders
   - ...

   Jira filter: [link]

   Come prepared with questions! 🚀
   ```

---

### Sesión 2: Team Refinement (Viernes, 1 semana antes de Planning)

**Objetivo**: Team valida DoR, hace preguntas, estima esfuerzo

**Duración**: 1 hora (max 2h si backlog complejo)

**Participantes**:

- Product Owner (presenta stories)
- Tech Lead (valida aspectos técnicos)
- 2-3 Developers (estimación)
- QA Lead (valida testabilidad)
- Designer (si hay UI changes)

**Agenda** (1h total):

#### 1. Review de DoR Checklist (10 min)

- Facilitador recuerda criterios DoR
- "Hoy validamos 8 stories, meta es que 5+ estén ready para Planning"

#### 2. Story-by-Story Review (40 min, ~5min por story)

**Por cada story**:

**PO Presenta** (2 min):

- Lee User Story en voz alta
- Explica business value y contexto
- Muestra mockups si aplica

**Team Q&A** (2 min):

- Devs hacen preguntas técnicas
- QA pregunta sobre edge cases
- Designer clarifica interacciones

**DoR Validation** (1 min):

- Team vota: ✅ Ready / ⚠️ Needs Minor Changes / ❌ Not Ready
- Si ❌ → identificar qué falta (PO toma nota)

**Quick Estimation** (opcional, 30 seg):

- Planning poker rápido: 1, 2, 3, 5, 8, 13
- Si hay discrepancia grande (ej: 2 vs 8) → discutir brevemente
- Estimate final se hace en Sprint Planning, esto es ballpark

#### 3. Prioritization (10 min)

- Team ordena stories por:
  - Business value (PO input)
  - Technical dependencies (Tech Lead input)
  - Risk/uncertainty (Team input)
- Top 5 stories = candidates para próximo sprint

---

### Output de Refinement

**Stories Categorized**:

1. **Ready for Planning** (5-8 stories, ~40-50 points)

   - 100% DoR completo
   - Team entiende scope
   - No blockers conocidos
   - → Van a Sprint Planning

2. **Needs Minor Work** (2-3 stories)

   - 80% DoR completo
   - PO puede completar en 1-2 días
   - → Revisar en daily standup, podrían ir a Planning

3. **Not Ready** (1-2 stories)

   - <50% DoR completo
   - → Vuelve a backlog, re-refine en 2 semanas

4. **Spike Needed** (0-1 stories)
   - No estimable, requiere research
   - → Crear spike story (2-5 points, time-boxed 2-3 días)
   - Spike output = documento con findings
   - → Re-refine cuando spike complete

---

## 🚫 Gatekeeper: Sprint Planning

**Regla Estricta**:

> Solo stories con DoR completo pueden entrar a Sprint Planning.

**Enforcement**:

1. **Pre-Planning Check** (1 día antes)

   - Tech Lead revisa Jira filter: `label = ready-for-planning`
   - Si <5 stories ready → escalar a PO urgentemente
   - PO tiene 24h para completar DoR o postponer stories

2. **Durante Planning**

   - Si story sin DoR completo se propone → Scrum Master la rechaza
   - "Esta story no cumple DoR, no puede entrar al sprint"
   - Exception: Solo si PO puede completar DoR en <15min en la sesión misma

3. **Post-Planning**
   - Sprint backlog = solo stories con DoR completo
   - 0 stories "we'll figure it out mid-sprint"

**Por Qué Es Crítico**:

- Estimaciones precisas requieren info completa
- Evita blockers mid-sprint
- Respeta el tiempo del equipo (no gastar 4h en Planning discutiendo detalles que PO debió preparar)

---

## 📊 Métricas de DoR

### Métrica #1: DoR Completion Rate

**Fórmula**:

```
(Stories ready for Planning / Stories refinadas) * 100
```

**Target**: >70%

**Tracking**:

- Por sprint
- Trend de últimos 6 sprints

**Red Flags**:

- <50% → PO no está preparando stories adecuadamente
- 100% constante → DoR puede estar demasiado laxo, revisar criterios

---

### Métrica #2: Mid-Sprint Blockers por Falta de Info

**Fórmula**:

```
# Stories bloqueadas esperando clarificación de PO
```

**Target**: 0 por sprint

**Red Flags**:

- > 2 blockers → DoR no está siendo enforced en Planning
- Blockers recurrentes en mismo tipo de info (ej: siempre falta API contract) → agregar ese criterio a DoR checklist

---

### Métrica #3: Estimation Accuracy

**Fórmula**:

```
| Estimación inicial - Story points reales | / Estimación inicial
```

**Target**: <30% variance

**Tracking**:

- Stories que se re-estiman mid-sprint (red flag)
- Stories que spillean a siguiente sprint por subestimación

**Insight**:

- Baja accuracy → DoR insuficiente, team no tenía info completa para estimar

---

### Métrica #4: Time Spent in Refinement

**Fórmula**:

```
Horas totales de refinement por sprint
```

**Target**: 1-2 horas por sprint (para equipo de 5-7 personas)

**Red Flags**:

- > 3 horas → Stories demasiado complejas o PO no preparó adecuadamente
- <30 min → DoR no se está validando seriamente

---

## 🎭 Roles y Responsabilidades

### Product Owner

**Pre-Refinement**:

- ✅ Crear user stories con template estándar
- ✅ Escribir 3-8 Acceptance Criteria (Given/When/Then)
- ✅ Auto-evaluar contra DoR checklist (marcar 80%+ antes de Refinement)
- ✅ Coordinar con Designer para mockups
- ✅ Coordinar con Tech Lead para API contracts (si aplica)
- ✅ Comunicar stories a revisar 3 días antes de Refinement

**Durante Refinement**:

- ✅ Presentar cada story (2 min): contexto, business value, mockups
- ✅ Responder preguntas del team
- ✅ Tomar notas de gaps identificados
- ✅ Comprometerse a completar gaps en timeline (1-2 días)

**Post-Refinement**:

- ✅ Completar gaps en stories "Needs Minor Work"
- ✅ Marcar stories ready con label `ready-for-planning`
- ✅ Actualizar prioridades en backlog

---

### Tech Lead

**Pre-Refinement**:

- ✅ Revisar stories técnicamente complejas con PO (async)
- ✅ Definir API contracts si hay integraciones
- ✅ Identificar dependencies técnicas

**Durante Refinement**:

- ✅ Validar aspectos técnicos del DoR
- ✅ Hacer preguntas sobre arquitectura, performance, security
- ✅ Proponer alternativas técnicas si aplica
- ✅ Identificar si story requiere spike

**Post-Refinement**:

- ✅ Crear spike stories si necesario
- ✅ Ordenar stories por dependencies técnicas
- ✅ Pre-Planning check (1 día antes): validar que 5+ stories están ready

---

### QA Lead

**Durante Refinement**:

- ✅ Validar que AC son testeables
- ✅ Preguntar por edge cases y error scenarios
- ✅ Verificar que hay test data disponible
- ✅ Identificar si requiere automation compleja

**Post-Refinement**:

- ✅ Preparar test plan draft para stories ready
- ✅ Setup test data en staging si es necesario

---

### Designer (UX/UI)

**Pre-Refinement**:

- ✅ Crear mockups/wireframes para stories con UI changes
- ✅ Hacer design handoff (spacing, colors, assets)
- ✅ Documentar interactions y responsive behavior

**Durante Refinement**:

- ✅ Presentar diseños y rationale
- ✅ Responder preguntas de implementación
- ✅ Clarificar edge cases visuales

---

### Development Team

**Durante Refinement**:

- ✅ Hacer preguntas para entender scope
- ✅ Identificar complejidades técnicas
- ✅ Validar que tienen info suficiente para estimar
- ✅ Quick estimation (ballpark)

**Post-Refinement**:

- ✅ Revisar stories async antes de Planning
- ✅ Preparar preguntas para Planning si algo no está claro

---

### Scrum Master / Facilitador

**Pre-Refinement**:

- ✅ Recordar a PO deadline para preparar stories (1 semana antes)
- ✅ Enviar calendario de Refinement y Planning

**Durante Refinement**:

- ✅ Facilitar sesión (timebox, mantener focus)
- ✅ Asegurar que DoR checklist se valida para cada story
- ✅ Documentar output (Ready / Needs Work / Not Ready / Spike)

**Sprint Planning**:

- ✅ **Gatekeeper**: Rechazar stories sin DoR completo
- ✅ Enforcement estricto de la regla

---

## 🚀 Implementation Roadmap

### Sprint 0: Setup (2 semanas)

**Semana 1**:

- [ ] Tech Lead + PO + Scrum Master revisan este documento (1h)
- [ ] Customizar DoR checklist para tu equipo
  - Quitar criterios no aplicables (ej: accessibility si no es requerimiento)
  - Agregar criterios específicos de tu stack/dominio
- [ ] Crear Jira labels: `ready-for-planning`, `needs-refinement`, `needs-spike`
- [ ] Crear filtro en Jira para Refinement

**Semana 2**:

- [ ] PO practica crear 3-5 stories con nuevo template
- [ ] Designer hace design handoff para 2 stories
- [ ] Tech Lead revisa y da feedback
- [ ] Primera sesión de Refinement (trial run)

---

### Sprint 1-2: Pilot (4 semanas)

- [ ] Aplicar DoR process end-to-end
- [ ] Refinement session cada viernes
- [ ] Sprint Planning solo acepta stories ready
- [ ] Trackear métricas:
  - DoR completion rate
  - Mid-sprint blockers por falta de info
  - Estimation accuracy

---

### Sprint 3+: Iterate & Optimize

- [ ] Revisar métricas en retro
- [ ] Ajustar DoR checklist basado en learnings
  - ¿Qué criterios faltan?
  - ¿Qué criterios son overkill?
- [ ] DoR completion rate >70% consistentemente
- [ ] Mid-sprint blockers = 0

---

## ✅ Success Criteria

### Mes 1

- ✅ DoR checklist definido y comunicado al equipo
- ✅ 100% de stories en Planning tienen label `ready-for-planning`
- ✅ DoR completion rate >50% (first time, target bajo)

### Mes 2-3

- ✅ DoR completion rate >70%
- ✅ Mid-sprint blockers por falta de info = 0-1 por sprint
- ✅ Estimation accuracy <30% variance

### Mes 4+

- ✅ DoR completion rate >80%
- ✅ Team confía en que stories tienen info suficiente
- ✅ Sprint Planning es más rápido (2h → 1.5h) porque no hay discusiones de detalles
- ✅ Velocity estable (±10%) porque estimaciones son precisas

---

## 🔗 Links Relacionados

- [Ceremonias: Backlog Refinement](README.md#backlog-refinement) - Ceremonia donde se aplica DoR
- [Ceremonias: Sprint Planning](README.md#sprint-planning) - Gatekeeper de DoR
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis completo
- [Tech Debt Budget](tech-debt-budget.md) - Cómo priorizar tech debt vs features
- [QA Estimation Guide](qa-estimation-guide.md) - Cómo incluir QA effort en estimates

---

## 📚 Ejemplos

### ✅ Ejemplo de Story con DoR Completo

```markdown
**TEAM-456: Usuario puede filtrar productos por precio y categoría**

**Como** comprador en la tienda online
**Quiero** filtrar productos por rango de precio y categorías
**Para** encontrar rápidamente productos que se ajusten a mi presupuesto e intereses

**Business Value**:

- Reduce tiempo de búsqueda de 5min a <1min
- Aumenta conversión de 3% a 5% (A/B test results)
- Feature request #1 en customer feedback (67 votos)

**Acceptance Criteria**:

1. **Given** estoy en la página de productos
   **When** selecciono rango de precio "$50-$100" y categoría "Electrónicos"
   **Then** veo solo productos de Electrónicos entre $50-$100, ordenados por relevancia

2. **Given** he aplicado filtros
   **When** selecciono "Clear filters"
   **Then** todos los filtros se resetean y veo todos los productos

3. **Given** no hay productos que matcheen mis filtros
   **When** aplico filtros muy restrictivos
   **Then** veo mensaje "No products found. Try adjusting filters" + sugerencias

4. **Given** estoy en mobile
   **When** toco "Filters" button
   **Then** se abre bottom sheet con filtros, puedo aplicar y ver "Apply (24 results)"

**Mockups**: [Figma link]

- Desktop: Filter sidebar (left), product grid (right)
- Mobile: Bottom sheet con filters, sticky "Apply" button

**API Contract**:
```

GET /api/products?category=electronics&minPrice=50&maxPrice=100

Response:
{
"products": [...],
"totalCount": 24,
"appliedFilters": { "category": "electronics", "priceRange": "50-100" }
}

```

**Dependencies**:
- ✅ None (can implement standalone)

**Estimate**: 5 story points (2-3 días dev + 1 día QA)

**DoR Checklist**:
- ✅ User story formato estándar
- ✅ 4 Acceptance Criteria (happy path, clear, empty state, mobile)
- ✅ Business value claro (metrics!)
- ✅ Mockups completos (desktop + mobile)
- ✅ API contract definido
- ✅ No dependencies
- ✅ Testeable (QA puede escribir test cases)
- ✅ Size apropiado (5 points, ~1 semana)
```

---

### ❌ Ejemplo de Story SIN DoR (Needs Work)

```markdown
**TEAM-457: Mejorar búsqueda de productos**

**Como** usuario
**Quiero** mejor búsqueda
**Para** encontrar cosas más rápido

**Acceptance Criteria**:

- Búsqueda debe ser más rápida
- Resultados más relevantes

**DoR Gaps**:

- ❌ User story demasiado vaga ("mejorar búsqueda" - qué significa?)
- ❌ AC no son testeables (qué es "más rápido"? <200ms? <1s?)
- ❌ No hay mockups (UI no está definida)
- ❌ No hay API contract
- ❌ No se puede estimar (scope unclear)

**Action**: PO debe re-escribir como stories específicas:

- Story 1: "Autocompletado de búsqueda muestra sugerencias en <200ms"
- Story 2: "Búsqueda incluye typo correction (ej: 'tleefono' → 'teléfono')"
- Story 3: "Búsqueda filtra por categoría y precio simultáneamente"
```

---

**Versión**: 1.0  
**Última Actualización**: 2024-12-06  
**Owner**: Product Owner + Scrum Master  
**Review Cycle**: Trimestral
