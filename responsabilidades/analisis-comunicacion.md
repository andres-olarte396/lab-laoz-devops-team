# Análisis de Responsabilidades: Comunicación

## 📋 Resumen Ejecutivo

Este documento analiza los **vacíos, overlaps, y mejoras** en la estrategia de comunicación organizacional definida en [`/comunicacion/README.md`](../comunicacion/README.md), identificando responsabilidades poco claras y proponiendo soluciones concretas.

**Fecha de análisis**: Diciembre 6, 2025  
**Scope**: Canales de comunicación, matriz de escalación, reporting, documentación  
**Base**: [Estrategia de Comunicación actual](../comunicacion/README.md) (807 líneas)

---

## 📂 Contexto: Estrategia de Comunicación Actual

La estrategia actual (definida en [`/comunicacion/README.md`](../comunicacion/README.md)) establece:

### Principios Definidos

1. **Default to Async**: Comunicación asíncrona como default (Slack, docs)
2. **Write Things Down**: Documentar decisiones (ADRs, meeting notes)
3. **Public by Default**: Canales públicos > DMs privados
4. **Overcommunicate Context**: Compartir el "por qué", no solo el "qué"
5. **Bias Toward Action**: Decidir y ejecutar, no paralysis por análisis

### Estructura de Canales Actual

- **Canales Generales**: #general, #random, #wins
- **Canales por Equipo**: #engineering, #development, #devops, #product, #design, #architecture, #qa
- **Canales por Proyecto**: #squad-checkout, #squad-mobile, #project-X
- **Canales de Incidentes**: #incidents, #on-call
- **Canales de Proceso**: #deployments, #releases, #rfc (Request for Comments)

### Gaps Detectados en Definición Actual

Aunque la estrategia define **QUÉ** canales existen y **PRINCIPIOS** de comunicación, **NO define**:

- ❌ Quién es responsable de cada canal (ownership)
- ❌ Cómo escalar issues entre equipos (cross-team escalation)
- ❌ Cómo comunicar incidentes severos (incident communication process)
- ❌ Quién mantiene documentación técnica (documentation ownership)
- ❌ Cómo comunicar a stakeholders no-técnicos (translation framework)
- ❌ Cómo hacer onboarding de comunicación (new hire guide)

Este análisis aborda estos **vacíos específicos**.

---

## 🔍 Hallazgos Principales

### ✅ Fortalezas Detectadas

1. **Principios claros de comunicación async-first**: Bien definidos
2. **Estructura de canales por equipo**: Clara separación (development, devops, product, design)
3. **Principio "write things down"**: Enfatiza documentación
4. **Bias toward action**: Evita paralysis por análisis

### ⚠️ Vacíos Identificados

| #   | Vacío                                                | Impacto                                       | Severidad |
| --- | ---------------------------------------------------- | --------------------------------------------- | --------- |
| 1   | **Responsables de canales no definidos**             | Canales sin moderación/cleanup                | 🟡 Media  |
| 2   | **Escalación cross-team poco clara**                 | Delays en resolver blockers entre equipos     | 🔴 Alta   |
| 3   | **Ownership de documentación técnica**               | Docs desactualizados, sin owner               | 🟡 Media  |
| 4   | **Comunicación de incidentes severos**               | Confusión en crisis (quién comunica, a quién) | 🔴 Alta   |
| 5   | **Onboarding de comunicación**                       | Nuevos miembros no saben dónde comunicar      | 🟡 Media  |
| 6   | **Comunicación con stakeholders externos**           | Sales, Marketing, C-suite (no cubierto)       | 🟡 Media  |
| 7   | **Archiving/cleanup de canales**                     | Canales antiguos acumulan ruido               | 🟢 Baja   |
| 8   | **Translation de decisiones técnicas → no-técnicas** | Stakeholders no-técnicos no entienden updates | 🟡 Media  |
| 9   | **Comunicación de Security/Compliance issues**       | No hay canal ni proceso                       | 🔴 Alta   |
| 10  | **Feedback loops de comunicación**                   | No hay proceso para mejorar estrategia        | 🟢 Baja   |

---

## 📊 Análisis Detallado por Área

### 1. Canales de Comunicación

#### Vacíos Detectados

**1.1. Responsables de canales no definidos**

**Problema**:

- Canales como `#engineering`, `#development`, `#product` no tienen owners claros
- No hay quien haga cleanup de mensajes antiguos
- No hay moderación (spam, off-topic)
- No hay quien actualice el "topic" del canal con info relevante

**Impacto**:

- Canales se vuelven ruidosos y difíciles de seguir
- Información importante se pierde en el ruido
- Nuevos miembros no saben qué se postea dónde

**Solución propuesta**:

```yaml
Channel Ownership:
  #engineering:
    Owner: Engineering Manager
    Backup: Tech Lead (rotation)
    Responsibilities:
      - Moderar discusiones (mantener on-topic)
      - Pin mensajes importantes
      - Actualizar channel topic mensualmente
      - Cleanup de threads antiguos (cada trimestre)

  #development:
    Owner: Tech Lead (rotation mensual)
    Backup: Senior Developer
    Responsibilities:
      - Mantener technical standards en discusiones
      - Facilitar code review requests
      - Coordinar RFCs (Request for Comments)

  #devops:
    Owner: DevOps Lead / SRE Lead
    Backup: On-call DevOps Engineer (weekly rotation)
    Responsibilities:
      - Coordinar incident response
      - Comunicar cambios de infraestructura
      - Post-mortems de incidentes

  #product:
    Owner: Product Manager (Senior)
    Backup: Product Owner
    Responsibilities:
      - Facilitar roadmap discussions
      - Coordinar con stakeholders
      - Priorización de requests

  #design:
    Owner: Lead Designer (UX or Product Designer)
    Backup: Senior UX Researcher
    Responsibilities:
      - Facilitar design critiques
      - Coordinar research shareouts
      - Design system updates
```

---

**1.2. Falta canal de Security/Compliance**

**Problema**:

- No hay canal dedicado para temas de seguridad
- Compliance issues (GDPR, HIPAA, SOC2) no tienen canal
- Vulnerabilidades se discuten en canales públicos (riesgo)

**Impacto**:

- Vulnerabilidades pueden ser expuestas públicamente
- Compliance issues no se priorizan
- Auditorías difíciles sin historial claro

**Solución propuesta**:

```yaml
Nuevo canal: #security-private
  Type: Private channel
  Members:
    - CTO / VP Engineering
    - Security Engineer (si existe)
    - DevOps Lead / SRE
    - Compliance Officer (si existe)
    - Tech Leads (read-only)

  Purpose:
    - Reportar vulnerabilidades (CVEs, security scans)
    - Discutir patches y remediations
    - Compliance updates (GDPR, HIPAA, SOC2)
    - Security audits y penetration tests
    - Incident response para security breaches

  Process:
    - Vulnerabilidades críticas: Report en <1 hora
    - Vulnerabilidades altas: Report en <24 horas
    - Compliance issues: Report en <48 horas

Nuevo canal: #security (público)
  Purpose:
    - Security awareness (training, tips)
    - Security best practices
    - Tool updates (1Password, SSO)
    - General security discussions (no vulnerabilities específicas)
```

---

**1.3. Comunicación con stakeholders externos**

**Problema**:

- No hay canales para comunicación con Sales, Marketing, Customer Success
- Updates de producto no llegan a stakeholders externos
- Feedback de clientes no llega a Engineering/Product

**Impacto**:

- Sales promete features que no existen
- Marketing lanza campaigns sin coordinar con Product
- Customer feedback se pierde

**Solución propuesta**:

```yaml
Nuevos canales:

#product-updates (público, read-only para no-tech):
  Purpose: Comunicar releases y roadmap a Sales/Marketing/CS
  Posting rights: Product Manager, Engineering Manager
  Subscribers: Sales, Marketing, CS, Executives
  Frequency: Semanal (viernes)
  Format:
    - Release notes (qué shipped esta semana)
    - Roadmap preview (próximas 2-4 semanas)
    - Known issues y workarounds

#customer-feedback (público):
  Purpose: Centralizar feedback de clientes
  Posting rights: Sales, CS, Support
  Subscribers: Product, Engineering, Design
  Process:
    - CS postea top 5 customer requests (mensual)
    - Product Manager triages y responde
    - Critical bugs escalados a #development

#sales-engineering (privado):
  Purpose: Coordinar entre Sales y Engineering
  Members: Sales Engineers, Solution Architects, Tech Leads
  Use cases:
    - RFPs (Request for Proposals) técnicos
    - Customer demos (technical feasibility)
    - Custom integrations (scoping)
```

---

### 2. Matriz de Escalación

#### Vacíos Detectados

**2.1. Escalación cross-team poco clara**

**Problema**:

- ¿Qué hacer si Development está bloqueado por DevOps?
- ¿Qué hacer si Product no puede decidir prioridad entre 2 equipos?
- ¿Quién desbloquea si Design y Engineering no están de acuerdo?

**Impacto**:

- Blockers duran días porque nadie escala
- Equipos pierden tiempo esperando decisiones
- Frustración y conflictos

**Solución propuesta**:

```yaml
Escalación Intra-Team (dentro del mismo equipo):
  Nivel 1: Individual Contributor
    - Intenta resolver (15-30 minutos)
    - Si no puede → Escala a Nivel 2

  Nivel 2: Tech Lead / Lead Designer / Product Manager
    - Time-box: 1-2 horas
    - Facilita discusión, propone solución
    - Si no hay consenso → Escala a Nivel 3

  Nivel 3: Engineering Manager / Design Manager / Product Director
    - Time-box: 4 horas
    - Toma decisión final (decision maker)
    - Documenta rationale

Escalación Cross-Team (entre equipos):
  Scenario 1: Development bloqueado por DevOps
    Nivel 1: Developer ↔ DevOps Engineer (30 min)
    Nivel 2: Tech Lead ↔ DevOps Lead (2 horas)
    Nivel 3: Engineering Manager decide prioridad

  Scenario 2: Product vs Engineering (scope/timeline)
    Nivel 1: Product Owner ↔ Tech Lead (1 hora)
    Nivel 2: Product Manager ↔ Engineering Manager (4 horas)
    Nivel 3: CPO (Chief Product Officer) ↔ CTO

  Scenario 3: Design vs Engineering (feasibility)
    Nivel 1: Designer ↔ Frontend Developer (1 hora)
    Nivel 2: Lead Designer ↔ Tech Lead (4 horas)
    Nivel 3: Design Manager ↔ Engineering Manager

  Scenario 4: Arquitectura vs Speed (tech debt vs features)
    Nivel 1: Solution Architect ↔ Tech Lead (discusión)
    Nivel 2: Enterprise Architect ↔ Engineering Manager
    Nivel 3: CTO (decision final)

Time-boxing rules:
  - Nivel 1: 30 min - 2 horas
  - Nivel 2: 2 horas - 1 día
  - Nivel 3: 1 día máximo → Decisión forzada
```

---

**2.2. Incidentes severos: Comunicación poco clara**

**Problema**:

- ¿Quién comunica el incidente a stakeholders?
- ¿Quién actualiza a clientes?
- ¿Quién coordina con C-suite?
- ¿Cómo se comunica severidad (P0, P1, P2)?

**Impacto**:

- Caos durante incidentes críticos
- Clientes no saben qué está pasando
- C-suite se entera por Twitter, no por equipo interno

**Solución propuesta**:

```yaml
Incident Communication Process:

Severidad P0 (Outage total, revenue-impacting):
  Incident Commander (IC): On-call SRE/DevOps Lead
  Communication Lead: Engineering Manager o designado

  Timeline:
    T+0 (detección):
      - IC crea incident channel (#incident-YYYY-MM-DD-description)
      - IC invita: DevOps, Tech Leads, EM, Product Manager

    T+15 min:
      - Communication Lead postea en #engineering:
        "🚨 P0 Incident: [brief description]. Investigating. Updates every 15min."
      - Communication Lead notifica a CTO via Slack/Phone

    T+30 min:
      - Communication Lead envía email a stakeholders internos:
        Subject: "P0 Incident Update - [Product Name]"
        Body: Status, Impact, ETA (si disponible), Next update time

    T+30 min (si clientes afectados):
      - Communication Lead coordina con Customer Success
      - CS postea en status page (e.g., status.empresa.com)
      - CS envía email a clientes afectados (template pre-aprobado)

    Cada 15-30 min:
      - IC postea update en incident channel
      - Communication Lead resume en #engineering

    Post-resolution:
      - IC declara "incident resolved" en incident channel
      - Communication Lead postea all-clear en #engineering
      - CS actualiza status page
      - Post-mortem scheduled dentro de 48 horas

Severidad P1 (Degradación parcial):
  - Similar a P0, pero updates cada 1 hora (no 15 min)
  - Status page update recomendado, no obligatorio
  - Email a stakeholders a T+1 hora (no T+30min)

Severidad P2 (Minor issue, no customer-facing):
  - IC: Engineer que detectó el issue
  - No incident channel (usar #devops)
  - Update en #devops cada 2-4 horas
  - No comunicación externa
```

---

### 3. Documentation Ownership

#### Vacíos Detectados

**3.1. Documentación técnica sin owner**

**Problema**:

- READMEs en repos no tienen owner
- Confluence docs están desactualizados
- ADRs (Architecture Decision Records) sin follow-up
- Runbooks de on-call sin mantener

**Impacto**:

- Onboarding lento (docs incorrectos)
- Debugging difícil (runbooks desactualizados)
- Decisiones pasadas se olvidan (ADRs abandonados)

**Solución propuesta**:

```yaml
Documentation Ownership Model:

Tipo: Repository README.md
  Owner: Tech Lead del equipo que mantiene el repo
  Review frequency: Trimestral
  Process:
    - Cada quarter, Tech Lead revisa README
    - Actualiza setup instructions, architecture diagram
    - Valida que links funcionen
    - Agrega/actualiza troubleshooting section

Tipo: ADRs (Architecture Decision Records)
  Owner: Solution Architect o Tech Lead que propuso ADR
  Review frequency: Anual
  Process:
    - ADR se escribe al tomar decisión
    - ADR se revisa 6-12 meses después
    - Si decisión cambió, ADR se marca "superseded" con link a nuevo ADR

Tipo: Runbooks (On-call playbooks)
  Owner: DevOps Lead / SRE Lead
  Co-owners: On-call rotation (todos contribuyen)
  Review frequency: Post-incident (immediate)
  Process:
    - Cada vez que on-call usa runbook, anota mejoras
    - Cada incident post-mortem actualiza runbook relevante
    - Quarterly review: DevOps Lead valida todos los runbooks

Tipo: API Documentation
  Owner: Backend Tech Lead
  Review frequency: Cada release
  Process:
    - API changes requieren actualizar docs (en PR)
    - CI/CD valida que docs estén en sync con código (Swagger, OpenAPI)
    - Quarterly audit: Tech Lead valida ejemplos funcionen

Tipo: Confluence / Internal Wiki
  Owner: Engineering Manager
  Delegate: Tech Writer (si existe) o Senior Developer
  Review frequency: Mensual
  Process:
    - Cada página tiene "Last reviewed" date
    - Páginas no revisadas en >6 meses se marcan "stale"
    - Páginas stale >1 año se archivan o borran
```

---

**3.2. Translation de decisiones técnicas a stakeholders no-técnicos**

**Problema**:

- Executives, Sales, Marketing no entienden updates técnicos
- "We migrated to microservices" → ¿Qué significa para el negocio?
- Decisiones técnicas no tienen business rationale claro

**Impacto**:

- Stakeholders no-técnicos se sienten excluidos
- Falta de buy-in para iniciativas técnicas (tech debt, refactors)
- Decisiones técnicas se cuestionan porque no se entienden

**Solución propuesta**:

```yaml
Technical → Business Translation Framework:

Template para comunicar decisiones técnicas:

## [Technical Decision Name]

### 🎯 Business Impact (2-3 frases)
- ¿Qué significa esto para el negocio?
- ¿Cómo afecta a clientes, revenue, growth?

Ejemplo:
  ❌ "We're migrating to microservices architecture"
  ✅ "We're splitting our application into smaller pieces so teams can
      ship features faster without blocking each other. This will reduce
      time-to-market from 2 weeks to 3 days for most features."

### 📊 Key Metrics
- Metric a mejorar (e.g., deploy frequency, page load time)
- Baseline actual vs Target
- Timeline

Ejemplo:
  - Deploy frequency: 1x/week → 5x/week (target in 3 months)
  - Page load time: 3s → 1.5s (target in 6 months)

### 💰 Cost / Effort
- Engineering time: X weeks
- Infrastructure cost: $Y/month
- ROI: Z% efficiency gain

Ejemplo:
  - Engineering: 8 weeks (2 developers full-time)
  - Infra cost: +$500/month (Kubernetes cluster)
  - ROI: 40% faster feature delivery = 6 more features/quarter

### ⚠️ Risks
- ¿Qué puede salir mal?
- Mitigation plan

Ejemplo:
  - Risk: Temporary slowdown during migration (2-3 weeks)
  - Mitigation: Migrate one service at a time, keep old system running

### 📅 Timeline
- Week 1-2: [Phase 1]
- Week 3-6: [Phase 2]
- Week 7-8: [Phase 3]

### ❓ FAQ
- Preguntas comunes que stakeholders tendrán

Responsable de translation:
  - Tech Lead escribe versión técnica
  - Product Manager o Engineering Manager traduce a business language
  - Ambas versiones se publican (technical en Confluence, business en Slack)
```

---

### 4. Comunicación de Onboarding

#### Vacíos Detectados

**4.1. Nuevos miembros no saben dónde comunicar**

**Problema**:

- No hay guía de "dónde postear qué"
- Nuevos miembros hacen preguntas en canales incorrectos
- No saben cómo escalar issues

**Impacto**:

- Frustración de nuevos miembros
- Ruido en canales (off-topic posts)
- Tiempo perdido dirigiendo gente a canales correctos

**Solución propuesta**:

```yaml
Communication Onboarding Checklist:

Día 1:
  ☐ Agregar a canales obligatorios:
    - #general, #engineering, #team-specific (e.g., #development)
  ☐ Leer "Communication Guide" en Confluence
  ☐ Revisar lista de canales y sus propósitos

Semana 1:
  ☐ Hacer primera pregunta en canal correcto (con ayuda de buddy)
  ☐ Postear en #wins tu primer PR mergeado
  ☐ Asistir a Daily Standup (observar formato)

Semana 2:
  ☐ Participar activamente en Daily Standup
  ☐ Hacer code review request en #development
  ☐ Escalar tu primer blocker (practice)

Resources creados:
  - "Communication Guide" (Confluence):
    - Channel directory (qué se postea dónde)
    - Escalation matrix (cómo escalar issues)
    - Slack etiquette (do's and don'ts)
    - Examples (good vs bad messages)

  - Channel topic updates:
    - Cada canal tiene topic claro: "For X, post Y. For Z, use #other-channel"
```

---

## 🎯 Recomendaciones Priorizadas

### Alta Prioridad (Implementar en próximos 30 días)

1. **Definir Channel Owners** para canales principales (#engineering, #development, #devops, #product, #design)
   - **Owner**: Engineering Manager
   - **Effort**: 2 horas (documentar + comunicar)
2. **Crear Incident Communication Process** (P0/P1/P2)
   - **Owner**: DevOps Lead + Engineering Manager
   - **Effort**: 1 semana (documentar + training)
3. **Crear canal #security-private** para vulnerabilidades
   - **Owner**: CTO o Security Engineer
   - **Effort**: 1 día (setup + permissions)
4. **Documentar Escalation Matrix** (cross-team)
   - **Owner**: Engineering Manager
   - **Effort**: 1 semana (workshop + documentar)

### Media Prioridad (Implementar en próximos 60 días)

5. **Crear "Communication Onboarding Guide"** en Confluence
   - **Owner**: Tech Lead + EM
   - **Effort**: 1 semana
6. **Implementar Documentation Ownership Model**
   - **Owner**: Tech Leads (cada equipo)
   - **Effort**: 2 semanas (audit + assign owners)
7. **Crear canales externos** (#product-updates, #customer-feedback, #sales-engineering)
   - **Owner**: Product Manager
   - **Effort**: 1 semana (setup + templates)
8. **Technical → Business Translation Framework**
   - **Owner**: Product Manager + Engineering Manager
   - **Effort**: 2 semanas (template + training)

### Baja Prioridad (Implementar en próximos 90 días)

9. **Channel Cleanup Process** (archivar canales viejos)
   - **Owner**: Engineering Manager
   - **Effort**: Trimestral, 2 horas
10. **Feedback Loop** para estrategia de comunicación (quarterly survey)
    - **Owner**: Engineering Manager
    - **Effort**: Trimestral, 1 día

---

## 📋 RACI: Responsabilidades de Comunicación

| Actividad                             | EM  | Tech Lead | DevOps Lead | PM  | Design Lead |
| ------------------------------------- | --- | --------- | ----------- | --- | ----------- |
| **Channel moderation (#engineering)** | A/R | C         | C           | I   | I           |
| **Channel moderation (#development)** | I   | A/R       | I           | I   | I           |
| **Channel moderation (#devops)**      | I   | C         | A/R         | I   | I           |
| **Channel moderation (#product)**     | I   | I         | I           | A/R | C           |
| **Channel moderation (#design)**      | I   | I         | I           | C   | A/R         |
| **Incident communication (P0)**       | A/R | C         | R           | I   | I           |
| **Technical → Business translation**  | A   | C         | I           | R   | I           |
| **Documentation ownership (tech)**    | A   | R         | R           | I   | I           |
| **Communication onboarding**          | R   | R         | C           | C   | C           |
| **Escalation decisions (cross-team)** | A/R | C         | C           | C   | C           |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 📈 Métricas de Éxito

Para medir si las mejoras funcionan:

| Métrica                                    | Baseline   | Target     | Frecuencia     |
| ------------------------------------------ | ---------- | ---------- | -------------- |
| **Time to resolve cross-team blockers**    | No medido  | <4 horas   | Mensual        |
| **% of incidents con comunicación clara**  | No medido  | >90%       | Por incident   |
| **Onboarding satisfaction (comunicación)** | No medido  | >4/5       | Por nuevo hire |
| **% documentation actualizada**            | No medido  | >80%       | Trimestral     |
| **Channel noise complaints**               | Anecdótico | <5/quarter | Trimestral     |

---

## 🔗 Links Relacionados

### Documentos de Análisis

- [Análisis de Ceremonias](analisis-ceremonias.md) - Gaps en ceremonias ágiles
- [RACI Matrix](RACI.md) - Responsabilidades generales por rol

### Estrategia Actual (Base del Análisis)

- [**Comunicación: Estrategia General**](../comunicacion/README.md) - Principios, canales, escalación, reporting (807 líneas)

### Otros Procesos Organizacionales

- [Ceremonias Ágiles](../ceremonias/README.md) - Daily, Planning, Refinement, Review, Retro
- [Workflows](../workflows/README.md) - Procesos de desarrollo y colaboración

### Documentos a Crear (Basados en Recomendaciones)

Estos documentos deberían crearse en `/comunicacion/` para completar la estrategia:

1. `comunicacion/channel-ownership.md` - Responsables de cada canal (Recomendación #1)
2. `comunicacion/incident-communication.md` - Proceso P0/P1/P2 completo (Recomendación #2)
3. `comunicacion/security-channels.md` - Setup de #security-private y #security (Recomendación #3)
4. `comunicacion/escalation-matrix.md` - Cross-team escalation detallada (Recomendación #4)
5. `comunicacion/onboarding-guide.md` - Communication guide para nuevos hires (Recomendación #5)
6. `comunicacion/documentation-ownership.md` - Owners de docs técnicos (Recomendación #6)
7. `comunicacion/external-stakeholders.md` - Canales para Sales/Marketing/CS (Recomendación #7)
8. `comunicacion/translation-framework.md` - Technical→Business translation templates (Recomendación #8)

---

**Última actualización**: Diciembre 6, 2025  
**Próxima revisión**: Marzo 2025  
**Owner**: Engineering Manager
