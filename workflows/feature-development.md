# Feature Development Workflow - Flujo Completo de Desarrollo de Features

> **Owner**: Engineering Manager + Product Manager  
> **Última actualización**: 7 de diciembre de 2025  
> **Próxima revisión**: 7 de marzo de 2026

---

## 📋 Resumen Ejecutivo

Este documento describe el flujo completo de desarrollo de una feature desde la **idea inicial** hasta **producción**, atravesando 4 fases: **Discovery**, **Design**, **Development**, y **Deployment**.

**Equipos involucrados**: Producto, Diseño, Desarrollo, DevOps, QA  
**Duración típica**: 3-4 semanas (Discovery: 1 semana, Design: 1 semana, Development: 1-2 semanas, Deployment: 1 día)  
**Modo de interacción**: Collaboration (equipos trabajan juntos activamente)

---

## 🎯 Objetivos

- **Claridad**: Todos saben qué fase estamos, quién hace qué
- **Eficiencia**: Minimizar handoffs y re-trabajo
- **Calidad**: Validación temprana (Discovery y Design antes de código)
- **Visibilidad**: Stakeholders informados en cada fase
- **Escalabilidad**: Proceso funciona para 1 squad o 10 squads en paralelo

---

## 📊 Overview del Workflow

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  DISCOVERY  │───▶│   DESIGN    │───▶│ DEVELOPMENT │───▶│ DEPLOYMENT  │
│             │    │             │    │             │    │             │
│ Product/UX  │    │ Design Team │    │  Dev Team   │    │ DevOps/QA   │
│  1 semana   │    │  1 semana   │    │  1-2 sem    │    │   1 día     │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
     │                    │                  │                   │
     ▼                    ▼                  ▼                   ▼
Problem Statement    Wireframes +        Code + Tests       Production
+ Tech Feasibility   UI Mockups         + Code Review        + Monitoring
```

**Timeline total**: Sprint N-2 (Discovery) → Sprint N-1 (Design) → Sprint N (Development) → Sprint N (Deployment)

---

## 🔍 Fase 1: Discovery (Semanas N-2 a N-1)

**Objetivo**: Validar que la idea es valiosa, viable, y factible antes de diseñar o desarrollar.

### Paso 1.1: Identificación de Problema u Oportunidad

**Responsable**: Product Manager  
**Duración**: 1-2 días  
**Entregable**: Problem Statement

**Actividades**:
1. Identificar problema o oportunidad de negocio
2. Definir hipótesis de valor: ¿Por qué esto importa?
3. Identificar usuarios afectados (segmento, cantidad)
4. Definir success metrics (¿cómo sabemos que funciona?)

**Template - Problem Statement**:
```markdown
## Problem Statement

**Problema**: [Descripción clara del problema que resolvemos]
**Usuarios afectados**: [Segmento + cantidad] (ej: "500 enterprise customers")
**Impacto actual**: [Qué pasa hoy sin esta solución]
**Valor esperado**: [Qué mejora si lo resolvemos]

**Success Metrics**:
- Metric 1: [Baseline → Target] (ej: "Conversion 15% → 25%")
- Metric 2: [...]

**Hipótesis**: Si implementamos [solución], entonces [usuarios] podrán [beneficio], 
lo que resultará en [métrica de negocio].
```

**Ejemplo**:
```markdown
## Problem Statement

**Problema**: Usuarios abandonan checkout porque el proceso de pago toma 5 pasos (3 pantallas).
**Usuarios afectados**: 10,000 usuarios/mes intentan comprar, 60% abandonan en checkout.
**Impacto actual**: Perdemos $200K/mes en ventas potenciales.
**Valor esperado**: Reducir abandono de 60% a 30% = +$100K/mes en revenue.

**Success Metrics**:
- Abandono en checkout: 60% → 30% (en 2 meses)
- Tiempo en checkout: 3 min → 1 min
- Conversión total: 15% → 25%

**Hipótesis**: Si simplificamos checkout a 1 pantalla con autofill, 
entonces usuarios completarán compra más rápido, 
lo que reducirá abandono en 50%.
```

**Output**: ✅ Problem Statement aprobado por PM + EM

---

### Paso 1.2: User Research (si es necesario)

**Responsable**: UX Researcher + Product Manager  
**Duración**: 3-5 días (opcional)  
**Entregable**: Research Insights

**Cuándo hacer research**:
- ✅ Nueva feature sin datos existentes
- ✅ Cambio mayor en UX existente
- ✅ Problema complejo con múltiples soluciones posibles
- ❌ Mejora incremental obvia (ej: "botón más grande")
- ❌ Bug fix o tech debt

**Actividades**:
1. **User interviews**: 5-8 usuarios (30-45 min cada uno)
   - Entender pain points actuales
   - Validar hipótesis de problema
   - Explorar soluciones preferidas
2. **Surveys** (opcional): Encuesta a 50-100 usuarios para datos cuantitativos
3. **Analytics review**: Revisar funnels, heatmaps, session recordings
4. **Competitive analysis**: ¿Cómo lo resuelven competidores?

**Template - Research Insights**:
```markdown
## Research Insights

**Método**: [User interviews / Surveys / Analytics]
**Participantes**: [Cantidad + perfil] (ej: "8 enterprise users, 3 SMB users")
**Fecha**: [Rango de fechas]

### Key Findings

1. **Finding 1**: [Insight con quote o dato]
   - Quote: "[Usuario dijo...]"
   - Impact: [Por qué importa]

2. **Finding 2**: [...]

### Recommendations

- **Do**: [Qué incluir en solución]
- **Don't**: [Qué evitar]
- **Consider**: [Ideas para futuro]

### Next Steps

- [ ] Validar con Product Manager
- [ ] Incorporar en diseño
```

**Output**: ✅ Research Insights documentado

---

### Paso 1.3: Validación de Viabilidad Técnica

**Responsable**: Tech Lead + Solution Architect  
**Duración**: 1-2 días  
**Entregable**: Technical Feasibility Document

**Objetivo**: Asegurar que podemos construir la solución técnicamente antes de diseñar.

**Actividades**:
1. **Spike técnico** (si es necesario): 2-4 horas investigando
   - ¿Tenemos APIs necesarias?
   - ¿Existen limitaciones de plataforma?
   - ¿Necesitamos librerías nuevas?
2. **Identificar dependencies**:
   - ¿Depende de otro equipo?
   - ¿Necesitamos infraestructura nueva?
3. **Identificar riesgos técnicos**:
   - Performance (¿puede causar latencia?)
   - Security (¿expone datos sensibles?)
   - Scalability (¿funciona con 10x usuarios?)

**Template - Technical Feasibility**:
```markdown
## Technical Feasibility

**Feature**: [Nombre de feature]
**Reviewer**: [Tech Lead name]
**Date**: [Fecha]

### ✅ Viable

- [x] Tenemos APIs/infraestructura necesaria
- [x] No hay limitaciones de plataforma
- [x] Performance acceptable (<200ms latency)
- [x] Security review OK (no expone PII)

### ⚠️ Risks Identified

| Riesgo | Severidad | Mitigación |
|--------|-----------|------------|
| [Riesgo 1] | HIGH/MED/LOW | [Cómo mitigamos] |

### 🛠️ Technical Approach (High-Level)

**Architecture**:
[Diagrama simple o descripción de componentes]

**Key Components**:
1. Frontend: [Qué cambia]
2. Backend: [Nuevos endpoints, DB changes]
3. Infrastructure: [Si necesita nuevos servicios]

**Estimated Complexity**: [S / M / L / XL]

### 📋 Dependencies

- [ ] Dependency 1: [Equipo X debe entregar API Y]
- [ ] Dependency 2: [...]

### 🚦 Decision

- ✅ **GO**: Proceed to Design phase
- ⚠️ **CONDITIONAL GO**: Proceed if [condición]
- ❌ **NO-GO**: Not feasible because [razón]
```

**Ejemplo**:
```markdown
## Technical Feasibility - Simplified Checkout

**Reviewer**: Jane Doe (Tech Lead)  
**Date**: Dec 1, 2025

### ✅ Viable

- [x] Stripe API supports one-page checkout
- [x] Address autofill available (Google Places API)
- [x] Performance OK (checkout page <500ms)
- [x] Security: PCI compliance maintained

### ⚠️ Risks Identified

| Riesgo | Severidad | Mitigación |
|--------|-----------|------------|
| Google Places API quota (10K/day) | MEDIUM | Upgrade to paid tier ($50/mo) |
| Browser autofill conflicts | LOW | Disable browser autofill, use custom |

### 🛠️ Technical Approach

**Frontend**: Single-page React form with Stripe Elements
**Backend**: Merge 3 endpoints into 1 (`POST /api/checkout/complete`)
**Infrastructure**: No changes needed

**Estimated Complexity**: M (Medium, 5-8 story points)

### 📋 Dependencies

- [x] None (all APIs available)

### 🚦 Decision

- ✅ **GO**: Proceed to Design phase
```

**Output**: ✅ Technical Feasibility aprobado por Tech Lead

---

### Paso 1.4: Estimación de Complejidad

**Responsable**: Tech Lead + Engineering Manager  
**Duración**: 1 día  
**Entregable**: T-Shirt Sizing (S/M/L/XL)

**Objetivo**: Entender esfuerzo antes de commitear recursos.

**Escala de T-Shirt Sizing**:
- **XS** (1-2 story points): 1-2 días de 1 developer
- **S** (3-5 puntos): 3-5 días de 1 developer
- **M** (5-8 puntos): 1-2 semanas de 1 developer
- **L** (8-13 puntos): 2-3 semanas de 1 developer o 1 semana de 2 developers
- **XL** (13-21 puntos): >3 semanas, considerar dividir en épica

**Factores a considerar**:
- Complejidad técnica (nuevas tecnologías?)
- Tamaño de código (líneas de código estimadas)
- Testing effort (unit + integration + E2E)
- Dependencies (esperas a otros equipos?)
- Risk (probabilidad de re-trabajo)

**Template**:
```markdown
## Estimation - T-Shirt Sizing

**Feature**: [Nombre]
**Estimators**: [Tech Lead + 2 senior devs]

**Size**: M (Medium)

**Breakdown**:
- Frontend: S (3-5 días)
- Backend: S (3-5 días)
- Testing: XS (1-2 días)
- Code Review + QA: XS (1-2 días)

**Total**: 8-14 días → Fits in 1 sprint (2 semanas)

**Assumptions**:
- Stripe API already integrated
- No infrastructure changes
- QA can test in parallel

**Dependencies**: None
```

**Output**: ✅ T-Shirt Size definido

---

### Paso 1.5: Priorización (Go/No-Go Decision)

**Responsable**: Product Manager  
**Duración**: 1 día  
**Entregable**: Go/No-Go Decision

**Criterios de Priorización**:
1. **Business Value**: ¿Cuánto revenue/impact genera?
2. **User Impact**: ¿Cuántos usuarios afecta?
3. **Effort**: ¿Cuánto cuesta construir? (T-shirt size)
4. **Strategic Alignment**: ¿Está en roadmap?
5. **Urgency**: ¿Es blocker para algo más?

**Framework - RICE Score**:
```
RICE = (Reach × Impact × Confidence) / Effort

Reach: Usuarios afectados por trimestre (ej: 10,000)
Impact: 3 (Massive) / 2 (High) / 1 (Medium) / 0.5 (Low)
Confidence: 100% / 80% / 50% (% de certeza que funciona)
Effort: Story points o persona-meses
```

**Ejemplo**:
```
Feature: Simplified Checkout

Reach: 10,000 users/quarter
Impact: 3 (Massive - revenue directo)
Confidence: 80% (research + tech feasibility validan hipótesis)
Effort: 8 story points

RICE = (10,000 × 3 × 0.8) / 8 = 3,000

(Score >1,000 = High Priority)
```

**Decision Template**:
```markdown
## Go/No-Go Decision

**Feature**: [Nombre]
**RICE Score**: [Score]

### ✅ GO - Proceed to Design

**Rationale**:
- High business value ($100K/mes potential)
- Technically feasible (no blockers)
- Fits in 1 sprint (M size)
- Strategic alignment (checkout optimization is Q1 OKR)

**Next Steps**:
1. Assign to Design team (Jane Doe, UX Designer)
2. Target: Designs ready by Dec 15
3. Development start: Sprint 42 (Dec 18)

**Stakeholders to inform**:
- Engineering team (#engineering)
- Sales team (#product-updates)
```

**Output**: ✅ Go/No-Go decision documentada

---

### 📋 Checklist de Salida - Fase Discovery

Antes de pasar a Design, validar:

- [ ] **Problem Statement** escrito y aprobado (PM)
- [ ] **User Research** completado (si aplica) (UX Researcher)
- [ ] **Technical Feasibility** validado (Tech Lead)
- [ ] **T-Shirt Sizing** estimado (Tech Lead + EM)
- [ ] **Go/No-Go Decision** tomada (PM)
- [ ] **Stakeholders informados** (#product-updates, #engineering)
- [ ] **Jira Epic creada** con links a docs

**Duración total Fase 1**: 5-7 días

---

## 🎨 Fase 2: Design (Semana N-1)

**Objetivo**: Diseñar la solución visualmente antes de escribir código.

### Paso 2.1: User Flows

**Responsable**: UX Designer  
**Duración**: 2-3 días  
**Entregable**: User Flow Diagrams

**Objetivo**: Mapear el journey completo del usuario a través de la feature.

**Actividades**:
1. Identificar entry points (¿cómo llega usuario a esta feature?)
2. Mapear happy path (flujo ideal sin errores)
3. Mapear edge cases (errores, validaciones, estados vacíos)
4. Identificar decision points (if/else en UX)

**Tools**: Figma (FigJam), Miro, Whimsical

**Template**:
```
[Entry] → [Screen 1] → [Decision?] → [Screen 2A / 2B] → [Success]
                             ↓
                         [Error State]
```

**Ejemplo - Simplified Checkout**:
```
User clicks "Checkout" 
  ↓
Single-page Checkout Form
  - Email (autofill if logged in)
  - Address (Google Places autofill)
  - Payment (Stripe card element)
  ↓
Click "Complete Purchase"
  ↓
Payment processing (loading spinner)
  ↓
Success? ───YES──→ Order Confirmation Page
    │
    NO (error)
    ↓
  Error Message (inline, retry)
```

**Output**: ✅ User flows aprobados por PM + Tech Lead

---

### Paso 2.2: Wireframes (Low-Fidelity)

**Responsable**: UX Designer  
**Duración**: 2-3 días  
**Entregable**: Low-Fidelity Wireframes

**Objetivo**: Diseñar estructura y layout sin colores/estilos finales.

**Fidelidad**: Gris, boxes, placeholder text  
**Tool**: Figma (Wireframe kit)

**Qué incluir**:
- Layout de componentes (header, form, buttons)
- Contenido (texto, labels, placeholders)
- Interacciones básicas (qué pasa al click)
- Estados (loading, error, empty, success)

**Ejemplo - Checkout Wireframe**:
```
┌────────────────────────────────────┐
│  [Logo]        Your Cart (3 items) │
├────────────────────────────────────┤
│                                    │
│  Contact Information               │
│  ┌──────────────────────────────┐  │
│  │ email@example.com            │  │
│  └──────────────────────────────┘  │
│                                    │
│  Shipping Address                  │
│  ┌──────────────────────────────┐  │
│  │ Start typing address...      │  │
│  └──────────────────────────────┘  │
│                                    │
│  Payment                           │
│  ┌──────────────────────────────┐  │
│  │ Card Number                  │  │
│  └──────────────────────────────┘  │
│                                    │
│  ┌──────────────────────────────┐  │
│  │ Complete Purchase ($125.00)  │  │
│  └──────────────────────────────┘  │
└────────────────────────────────────┘
```

**Output**: ✅ Wireframes revisados por PM, Tech Lead, Frontend Dev

---

### Paso 2.3: Design Review con Producto y Desarrollo

**Responsable**: UX Designer (facilitador)  
**Duración**: 1 día (1 reunión de 1 hora)  
**Entregable**: Feedback incorporado en wireframes

**Participantes**:
- UX Designer (presenta)
- PM (valida que resuelve problema)
- Tech Lead (valida viabilidad técnica)
- Frontend Developer (valida implementabilidad)
- QA Engineer (valida testability)

**Agenda (60 min)**:
1. **Context** (5 min): Recap de problema y solución
2. **User Flows** (10 min): Walkthrough de flows
3. **Wireframes** (20 min): Walkthrough de pantallas
4. **Feedback** (20 min): Todos dan feedback
5. **Action Items** (5 min): Qué cambiar antes de UI design

**Feedback Categories**:
- 🟢 **Approved**: No cambios necesarios
- 🟡 **Minor Changes**: Ajustes menores (1-2 horas)
- 🔴 **Major Changes**: Rediseño necesario (1-2 días)

**Output**: ✅ Wireframes aprobados con feedback incorporado

---

### Paso 2.4: UI Design (High-Fidelity Mockups)

**Responsable**: UI Designer  
**Duración**: 3-4 días  
**Entregable**: High-Fidelity Mockups

**Objetivo**: Diseño final pixel-perfect con colores, tipografía, iconos.

**Actividades**:
1. Aplicar design system (colores, spacing, typography)
2. Crear todos los estados (default, hover, active, disabled, error, loading)
3. Diseñar responsive (desktop, tablet, mobile)
4. Añadir micro-interactions (animaciones, transitions)
5. Accessibility review (contrast ratio WCAG AA)

**Tools**: Figma (con design system/component library)

**Qué incluir**:
- Mockups de todas las pantallas (desktop + mobile)
- Estados de cada componente
- Specs de spacing, colors, typography (Figma Dev Mode)
- Prototipo interactivo (para user testing si aplica)

**Checklist - UI Design Quality**:
- [ ] Colores siguen design system
- [ ] Typography consistente (font sizes, line heights)
- [ ] Spacing usa 8px grid
- [ ] Contrast ratio >4.5:1 (WCAG AA)
- [ ] Mobile responsive (320px min width)
- [ ] Loading states diseñados
- [ ] Error states diseñados
- [ ] Empty states diseñados

**Output**: ✅ UI mockups finales en Figma

---

### Paso 2.5: Design QA y Handoff

**Responsable**: UI Designer + Frontend Developer  
**Duración**: 1 día  
**Entregable**: Figma Dev Mode Specs + Assets

**Actividades**:
1. **Design QA**: Revisar consistency (spacing, colores, typography)
2. **Export assets**: Icons, images optimizados (SVG, PNG @2x)
3. **Dev Mode**: Activar Figma Dev Mode para specs
4. **Handoff meeting**: 30 min con Frontend Dev para Q&A
5. **Documentation**: Escribir notas de implementación

**Figma Dev Mode Specs**:
- CSS properties (colors, spacing, typography)
- Component variants (states)
- Responsive breakpoints
- Animations/transitions specs

**Handoff Checklist**:
- [ ] Figma link compartido con Frontend Dev
- [ ] Dev Mode activado
- [ ] Assets exportados y en repo
- [ ] Implementación notes escritas
- [ ] Edge cases documentados
- [ ] Accessibility requirements listados

**Output**: ✅ Design handoff completo, Frontend Dev puede empezar

---

### 📋 Checklist de Salida - Fase Design

Antes de pasar a Development, validar:

- [ ] **User Flows** aprobados (UX Designer)
- [ ] **Wireframes** aprobados por PM + Tech Lead (UX Designer)
- [ ] **UI Mockups** finales en Figma (UI Designer)
- [ ] **Responsive designs** (desktop, tablet, mobile) (UI Designer)
- [ ] **Design QA** completado (consistency check) (UI Designer)
- [ ] **Figma Dev Mode** activado con specs (UI Designer)
- [ ] **Assets** exportados (icons, images) (UI Designer)
- [ ] **Handoff meeting** con Frontend Dev realizado (UI Designer + Dev)
- [ ] **Accessibility** validado (WCAG AA contrast) (UI Designer)

**Duración total Fase 2**: 7-10 días

---

## 💻 Fase 3: Development (Semana N)

**Objetivo**: Implementar la feature con código, tests, y code review.

### Paso 3.1: Implementation Planning

**Responsable**: Tech Lead + Assigned Developers  
**Duración**: 0.5 día (Planning meeting)  
**Entregable**: Technical Plan + Jira Stories

**Actividades**:
1. **Story Breakdown**: Dividir epic en stories implementables
2. **Technical Design**: Definir arquitectura (componentes, APIs, DB schema)
3. **Task Assignment**: Asignar stories a developers
4. **Definition of Done**: Qué debe cumplir cada story para estar "Done"

**Story Breakdown Template**:
```markdown
## Epic: Simplified Checkout

### Story 1: Frontend - Checkout Form Component
**Points**: 5
**Owner**: Jane (Frontend Dev)
**Tasks**:
- [ ] Create CheckoutForm.tsx component
- [ ] Integrate Stripe Elements
- [ ] Implement Google Places autofill
- [ ] Add form validation
- [ ] Write unit tests (Jest + React Testing Library)
- [ ] Responsive styling (mobile + desktop)

**DoD**:
- [ ] Code reviewed and approved
- [ ] Unit tests passing (>80% coverage)
- [ ] Figma design implemented pixel-perfect
- [ ] Accessibility: keyboard navigation works
- [ ] No console errors/warnings

### Story 2: Backend - Checkout API
**Points**: 5
**Owner**: John (Backend Dev)
**Tasks**:
- [ ] Create POST /api/checkout/complete endpoint
- [ ] Integrate Stripe payment processing
- [ ] Add order creation logic
- [ ] Add error handling (payment failed, validation)
- [ ] Write unit tests + integration tests
- [ ] Add API documentation (Swagger)

**DoD**:
- [ ] Code reviewed and approved
- [ ] Tests passing (>80% coverage)
- [ ] API documented in Swagger
- [ ] Error handling tested
- [ ] Performance <500ms

### Story 3: Integration + E2E Testing
**Points**: 3
**Owner**: QA Engineer
**Tasks**:
- [ ] Frontend + Backend integration testing
- [ ] E2E test with Cypress (happy path)
- [ ] E2E test error scenarios (card declined)
- [ ] Load testing (100 concurrent users)

**DoD**:
- [ ] E2E tests passing
- [ ] Load test: <2s P95 latency
- [ ] No critical bugs
```

**Output**: ✅ Stories creadas en Jira, asignadas a developers

---

### Paso 3.2: Implementation

**Responsable**: Assigned Developers (Frontend, Backend, Mobile)  
**Duración**: 5-10 días  
**Entregable**: Code en feature branch

**Best Practices**:
1. **Branches**: `feature/simplified-checkout` (branch por epic)
2. **Commits**: Commits pequeños y frecuentes con mensajes claros
   - `feat(checkout): add autofill for address field`
   - `fix(checkout): handle Stripe card decline error`
3. **Tests**: Escribir tests mientras desarrollas (no al final)
4. **Daily Updates**: Actualizar Jira tickets diariamente
5. **Pair Programming**: Para features complejas, pair 2-3 horas/día

**Checklist por Developer**:
- [ ] Código implementado según diseño
- [ ] Unit tests escritos (>80% coverage)
- [ ] Integration tests (si aplica)
- [ ] Linter passing (ESLint, Prettier)
- [ ] No warnings en consola
- [ ] Performance OK (frontend <3s load, backend <500ms)
- [ ] Accessibility (WCAG AA) - keyboard navigation, screen reader
- [ ] Security review (no secrets hardcoded, input validation)

**Output**: ✅ Feature branch con código completo y tests

---

### Paso 3.3: Code Review

**Responsable**: Tech Lead + Senior Developers  
**Duración**: 1-2 días  
**Entregable**: Approved Pull Request

**Code Review Checklist**:

**Funcionalidad**:
- [ ] Código cumple requirements de story
- [ ] Edge cases manejados (errores, validaciones, empty states)
- [ ] No regresiones (features existentes funcionan)

**Code Quality**:
- [ ] Código legible (nombres claros, no "magic numbers")
- [ ] DRY (Don't Repeat Yourself) - no duplicación
- [ ] SOLID principles seguidos
- [ ] Comentarios donde necesario (no obviedades)

**Testing**:
- [ ] Unit tests cubren casos principales + edge cases
- [ ] Tests son determinísticos (no flaky tests)
- [ ] Coverage >80% (lines, branches)

**Performance**:
- [ ] No N+1 queries
- [ ] No loops innecesarios
- [ ] Assets optimizados (images comprimidas)
- [ ] Lazy loading donde aplica

**Security**:
- [ ] Input validation (prevent XSS, SQL injection)
- [ ] No secrets hardcoded
- [ ] Authentication/authorization checks
- [ ] HTTPS para APIs sensibles

**Accessibility**:
- [ ] Semantic HTML (no divs para todo)
- [ ] ARIA labels donde necesario
- [ ] Keyboard navigation funciona
- [ ] Color contrast WCAG AA

**Process**:
1. Developer crea PR con descripción detallada
2. Automated checks run (linter, tests, build)
3. Tech Lead asigna 2 reviewers (1 senior, 1 peer)
4. Reviewers revisan en <24h
5. Developer hace cambios según feedback
6. Re-review si cambios mayores
7. Tech Lead aprueba y merges

**Output**: ✅ PR approved y merged a `main`

---

### Paso 3.4: QA Testing

**Responsable**: QA Engineer  
**Duración**: 1-3 días  
**Entregable**: QA Sign-off

**Testing Types**:

**1. Functional Testing** (Manual):
- [ ] Happy path funciona (user puede completar checkout)
- [ ] Edge cases (errores, validaciones)
- [ ] Cross-browser (Chrome, Firefox, Safari, Edge)
- [ ] Cross-device (desktop, tablet, mobile)

**2. Regression Testing**:
- [ ] Features existentes funcionan (no rompimos nada)
- [ ] Automated regression suite passing

**3. Integration Testing**:
- [ ] Frontend + Backend integran correctamente
- [ ] Third-party APIs funcionan (Stripe, Google Places)

**4. Performance Testing**:
- [ ] Page load <3s (Lighthouse score >80)
- [ ] API response <500ms (P95)
- [ ] No memory leaks (Chrome DevTools)

**5. Accessibility Testing**:
- [ ] Keyboard navigation (Tab, Enter, Esc)
- [ ] Screen reader (NVDA, VoiceOver)
- [ ] Color contrast (WCAG AA)

**6. Security Testing** (básico):
- [ ] XSS attempts blocked
- [ ] SQL injection attempts blocked
- [ ] HTTPS enforced

**Bug Severity Classification**:
- **P0 (Blocker)**: Feature no funciona, bloquea deployment
- **P1 (Critical)**: Error mayor pero workaround existe
- **P2 (Major)**: Bug evidente pero no bloquea uso
- **P3 (Minor)**: Cosmético, no afecta funcionalidad

**QA Sign-off Criteria**:
- **PASS**: 0 P0 bugs, 0 P1 bugs, <3 P2 bugs
- **CONDITIONAL PASS**: 1-2 P1 bugs con mitigación plan
- **FAIL**: >1 P0 bugs o >3 P1 bugs

**Output**: ✅ QA Sign-off aprobado, ready for deployment

---

### 📋 Checklist de Salida - Fase Development

Antes de pasar a Deployment, validar:

- [ ] **Code implementado** según diseño (Developers)
- [ ] **Unit tests** escritos y passing (>80% coverage) (Developers)
- [ ] **Code review** aprobado (Tech Lead + Reviewers)
- [ ] **PR merged** a `main` branch (Tech Lead)
- [ ] **QA testing** completado (QA Engineer)
- [ ] **QA sign-off** aprobado (0 P0/P1 bugs) (QA Engineer)
- [ ] **Performance validated** (<3s load, <500ms API) (QA + DevOps)
- [ ] **Security review** básico pasado (Tech Lead)
- [ ] **Accessibility tested** (keyboard, screen reader) (QA)
- [ ] **Documentation** actualizada (README, API docs) (Developers)

**Duración total Fase 3**: 7-14 días

---

## 🚀 Fase 4: Deployment (Fin de Semana N)

**Objetivo**: Desplegar a producción de forma segura y monitorear.

### Paso 4.1: Staging Deployment

**Responsable**: DevOps / Platform Engineer  
**Duración**: 0.5 día  
**Entregable**: Feature live en Staging

**Actividades**:
1. Deploy a staging environment (auto via CI/CD)
2. Smoke tests automáticos (Cypress E2E)
3. Manual QA validation en staging
4. Performance testing en staging (load test)
5. Stakeholder demo (PM muestra a execs/sales)

**Checklist - Staging**:
- [ ] Deployment exitoso (no errors en logs)
- [ ] Smoke tests passing (Cypress)
- [ ] QA manual validation OK
- [ ] Performance OK (load test passing)
- [ ] Stakeholder demo realizado

**Output**: ✅ Feature validada en Staging, ready for Production

---

### Paso 4.2: Production Deployment

**Responsable**: DevOps Lead + Tech Lead  
**Duración**: 1-4 horas  
**Entregable**: Feature live en Production

**Deployment Strategy** (elegir según riesgo):

**1. Blue-Green Deployment** (Zero downtime, fácil rollback):
```
[Current: Blue (100% traffic)] 
         ↓
[Deploy: Green (0% traffic)] → Validate
         ↓
[Switch: Green (100% traffic)] → Monitor
         ↓
Rollback available: Switch back to Blue
```

**2. Canary Deployment** (Gradual rollout):
```
[Deploy: Canary (5% traffic)] → Monitor 30min
         ↓ No errors?
[Increase: 25% traffic] → Monitor 1h
         ↓ No errors?
[Increase: 50% traffic] → Monitor 2h
         ↓ No errors?
[Full rollout: 100% traffic]
```

**3. Feature Flag** (Instant rollback sin redeploy):
```
[Deploy code with flag OFF] → Code in prod, feature hidden
         ↓
[Enable flag for 5% users] → Monitor
         ↓
[Enable flag for 100% users] → Full rollout

Rollback: Toggle flag OFF (instant)
```

**Deployment Checklist**:
- [ ] **Pre-Deployment**:
  - [ ] Notify #engineering y #product-updates (30 min antes)
  - [ ] Freeze other deployments (deployment window)
  - [ ] On-call engineer ready (PagerDuty)
  - [ ] Rollback plan documented
  
- [ ] **During Deployment**:
  - [ ] Deployment executing (CI/CD pipeline)
  - [ ] Monitoring dashboards open (Grafana/DataDog)
  - [ ] No errors en logs (CloudWatch/Splunk)
  - [ ] Health checks passing
  
- [ ] **Post-Deployment** (primeros 30 min):
  - [ ] Smoke tests passing en production
  - [ ] Error rate <0.1% (normal baseline)
  - [ ] Latency P95 <500ms (normal)
  - [ ] CPU/Memory normal (<80%)
  - [ ] No alerts disparados (PagerDuty silencio)

**Output**: ✅ Feature live en Production

---

### Paso 4.3: Post-Deployment Monitoring

**Responsable**: DevOps + Tech Lead + PM  
**Duración**: 24-48 horas  
**Entregable**: Stability Report

**Monitoring - First 24h**:

**Hour 0-1** (Critical window):
- Monitor cada 5 minutos
- Error rate, latency, CPU, memory
- User feedback (#customer-feedback, support tickets)

**Hour 1-4**:
- Monitor cada 15 minutos
- Validate business metrics (conversion, usage)

**Hour 4-24**:
- Monitor cada 1 hora
- Compare metrics vs baseline

**Hour 24-48**:
- Monitor diario
- Full analysis de impact

**Metrics to Monitor**:

**Technical Metrics**:
- Error rate (target: <0.1%)
- API latency (target: P95 <500ms)
- Page load time (target: <3s)
- CPU/Memory usage (target: <80%)

**Business Metrics**:
- Conversion rate (checkout completion)
- Abandonment rate
- Revenue
- User engagement

**User Feedback**:
- Support tickets (any new issues?)
- In-app feedback (NPS, surveys)
- Social media mentions

**Rollback Triggers** (deploy FAILED, rollback):
- ❌ Error rate >1% (10x baseline)
- ❌ Latency P95 >2s (4x target)
- ❌ CPU >95% sustained
- ❌ Critical bugs (checkout no funciona)
- ❌ Revenue drop >20%

**Output**: ✅ Stability Report after 48h

**Stability Report Template**:
```markdown
## Post-Deployment Stability Report

**Feature**: Simplified Checkout
**Deployment Date**: Dec 18, 2025
**Report Date**: Dec 20, 2025 (48h post-deploy)

### ✅ Success Metrics

**Technical**:
- Error rate: 0.05% (target <0.1%) ✅
- API latency: P95 = 320ms (target <500ms) ✅
- Page load: 2.1s (target <3s) ✅
- Zero downtime ✅

**Business**:
- Conversion rate: 18% → 23% (+27% improvement) 🎉
- Abandonment: 60% → 35% (-41% improvement) 🎉
- Revenue: +$15K in 48h 💰

**User Feedback**:
- 12 positive mentions (#customer-feedback)
- 2 bug reports (P3 minor cosmetic issues)
- NPS: +8 points

### 🐛 Issues Found

| Issue | Severity | Status |
|-------|----------|--------|
| Autofill no funciona en Safari | P3 | Fixed in hotfix |
| Mobile keyboard covers button | P3 | Scheduled for next sprint |

### 📊 Conclusion

**Status**: ✅ **STABLE** - Feature performing above expectations

**Next Steps**:
- Monitor for 1 week
- Address P3 bugs in next sprint
- Expand to international markets (Phase 2)
```

**Output**: ✅ Stability validated, feature graduation

---

### 📋 Checklist de Salida - Fase Deployment

Feature considerada **DONE** cuando:

- [ ] **Staging deployment** exitoso y validado (DevOps)
- [ ] **Production deployment** exitoso (DevOps + Tech Lead)
- [ ] **Smoke tests** passing en production (QA)
- [ ] **Monitoring** normal (error rate, latency, CPU/memory) (DevOps)
- [ ] **Business metrics** improving (conversion, revenue) (PM)
- [ ] **User feedback** positivo (no critical issues) (PM + Customer Success)
- [ ] **Stability report** completado (48h post-deploy) (DevOps + PM)
- [ ] **Stakeholders notificados** (#product-updates) (PM)
- [ ] **Release notes** publicados (PM)
- [ ] **Documentation** actualizada (Knowledge Base) (PM)

**Duración total Fase 4**: 1 día deployment + 2 días monitoring = 3 días

---

## 🎭 RACI Matrix - Feature Development

| Actividad | PM | UX/UI | Tech Lead | Dev | QA | DevOps |
|-----------|----|----|-----------|-----|----|----|
| **Discovery Phase** | | | | | | |
| Problem Statement | **R/A** | C | C | I | I | I |
| User Research | C | **R/A** | I | I | I | I |
| Tech Feasibility | C | I | **R/A** | C | I | I |
| Estimation | C | I | **R/A** | C | I | I |
| Go/No-Go Decision | **A/R** | C | C | I | I | I |
| **Design Phase** | | | | | | |
| User Flows | C | **R/A** | C | I | I | I |
| Wireframes | C | **R/A** | C | C | I | I |
| UI Mockups | C | **R/A** | I | C | I | I |
| Design Handoff | I | **R** | C | **A** | I | I |
| **Development Phase** | | | | | | |
| Story Breakdown | C | I | **A** | **R** | C | I |
| Implementation | I | I | C | **R/A** | I | I |
| Code Review | I | I | **A** | **R** | I | I |
| QA Testing | I | I | C | C | **R/A** | I |
| **Deployment Phase** | | | | | | |
| Staging Deploy | I | I | C | I | C | **R/A** |
| Production Deploy | C | I | **A** | I | C | **R** |
| Monitoring | **A** | I | C | I | C | **R** |
| Release Notes | **R/A** | I | C | I | I | I |

**Leyenda**:
- **R** (Responsible): Ejecuta la tarea
- **A** (Accountable): Responsable final, aprueba
- **C** (Consulted): Se consulta su opinión
- **I** (Informed): Se mantiene informado

---

## 📊 Métricas de Éxito del Workflow

### Métricas de Eficiencia
- **Lead Time**: Idea → Production (<4 semanas para features M)
- **Cycle Time**: Development Start → Deployed (<2 semanas)
- **Re-work Rate**: % features que requieren re-diseño (<10%)
- **Time in Review**: Code review + QA (<3 días)

### Métricas de Calidad
- **Bug Escape Rate**: Bugs encontrados en producción vs QA (<5%)
- **Deployment Success Rate**: % deployments sin rollback (>95%)
- **Test Coverage**: Unit + integration tests (>80%)
- **Performance**: P95 latency <500ms (100% features)

### Métricas de Colaboración
- **Handoff Efficiency**: Tiempo entre fases (<2 días)
- **Stakeholder Satisfaction**: PM + EM rating (>4/5)
- **Team Velocity**: Story points por sprint (trend up)

---

## 🚨 Antipatrones Comunes (Qué Evitar)

### ❌ Antipatrón 1: "Empezar a codear sin diseño"
**Síntoma**: Developer empieza sin mockups finales  
**Consecuencia**: Re-trabajo, diseño inconsistente  
**Solución**: Bloquear development hasta Design handoff completo

### ❌ Antipatrón 2: "Saltar discovery"
**Síntoma**: PM dice "ya sé lo que usuarios quieren, no necesito research"  
**Consecuencia**: Construir feature que nadie usa  
**Solución**: Mandatory research para features >M size

### ❌ Antipatrón 3: "QA al final del sprint"
**Síntoma**: QA recibe feature día 9 de sprint de 10 días  
**Consecuencia**: QA bottleneck, bugs no detectados  
**Solución**: QA involucrado desde planning, testing en paralelo

### ❌ Antipatrón 4: "Deploy viernes tarde"
**Síntoma**: Deploy 5pm viernes, equipo se va  
**Consecuencia**: Issue en producción sin on-call  
**Solución**: Deploy lunes-jueves, deployment freeze viernes

### ❌ Antipatrón 5: "No monitorear post-deploy"
**Síntoma**: Deploy y olvidar, revisar métricas 1 semana después  
**Consecuencia**: Issues no detectados por días  
**Solución**: Mandatory 48h monitoring con on-call ready

---

## 🔗 Links Relacionados

### Documentación Interna
- [Ceremonias: Sprint Planning](../ceremonias/sprint-planning.md) - Cómo planear sprint
- [Workflows: Incident Response](incident-response.md) - Qué hacer si deploy falla
- [Workflows: Release Management](release-management.md) - Release train y versioning
- [Comunicación: Stakeholder Updates](../comunicacion/external-stakeholders.md) - Cómo comunicar releases
- [Plantillas: User Story Template](../plantillas/user-story-template.md) - Template de stories

### Equipos y Roles
- [Equipo de Producto](../equipos/producto/README.md) - Roles PM/PO
- [Equipo de Diseño](../equipos/diseno/README.md) - Roles UX/UI
- [Equipo de Desarrollo](../equipos/desarrollo/README.md) - Roles Dev/QA
- [Equipo de DevOps](../equipos/devops/README.md) - Roles DevOps/SRE

### Procesos Relacionados
- [Procesos: CI/CD Pipeline](../procesos/cicd-pipeline.md) - Automated deployment
- [Procesos: Deployment Procedures](../procesos/deployment-procedures.md) - Blue-Green, Canary
- [Procesos: Post-Mortem](../procesos/post-mortem.md) - Si algo sale mal

---

**Mantenido por**: Engineering Manager + Product Manager  
**Última actualización**: 7 de diciembre de 2025  
**Próxima revisión**: 7 de marzo de 2026  
**Versión**: 1.0
