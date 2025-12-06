# Estrategia de Comunicación

Este directorio documenta la estrategia de comunicación organizacional para equipos de tecnología, incluyendo estructura de canales, matriz de escalación, y prácticas de reporting.

## 📋 Tabla de Contenidos

- [Principios de Comunicación](#principios-de-comunicación)
- [Estructura de Canales](#estructura-de-canales)
- [Matriz de Escalación](#matriz-de-escalación)
- [Reporting y Métricas](#reporting-y-métricas)
- [Comunicación Asíncrona](#comunicación-asíncrona)
- [Prácticas de Documentación](#prácticas-de-documentación)

---

## 🎯 Principios de Comunicación

### 1. Default to Async

**Prioridad**: Async > Sync

**Por qué**:

- Respeta el tiempo de deep work de todos
- Permite trabajar en zonas horarias diferentes
- Crea registro escrito automáticamente
- Reduce interrupciones

**Cuándo usar async**:

- ✅ Updates de progreso
- ✅ Decisiones que no son urgentes
- ✅ Compartir información
- ✅ Code reviews
- ✅ Feedback no crítico

**Cuándo usar sync (meetings)**:

- ⚠️ Brainstorming complejo
- ⚠️ Resolver conflictos
- ⚠️ Decisiones urgentes
- ⚠️ Onboarding
- ⚠️ Incidentes críticos

---

### 2. Write Things Down

**Principio**: Si no está escrito, no existe.

**Prácticas**:

- Decisiones importantes → Documentar en Confluence/Notion
- Decisiones de arquitectura → ADR (Architecture Decision Record)
- Acuerdos de reuniones → Meeting notes en docs compartidos
- Procesos → README.md en repo correspondiente

**Beneficios**:

- Onboarding más fácil (nueva gente lee en vez de preguntar)
- Reduce repetir misma info 10 veces
- Evita "juego de teléfono" (información se distorsiona)
- Auditable (sabemos quién decidió qué y cuándo)

---

### 3. Public by Default, Private when Necessary

**Regla**: Comunicación en canales públicos por defecto, DMs solo cuando es personal.

**Por qué**:

- Transparencia organizacional
- Otros pueden aprender de conversaciones
- Reduce silos de información
- Facilita que otros contribuyan

**Cuándo usar canales públicos**:

- ✅ Preguntas técnicas
- ✅ Updates de proyectos
- ✅ Decisiones de producto
- ✅ Bugs y issues

**Cuándo usar DMs**:

- 🔒 Feedback 1:1 sensible
- 🔒 Temas de HR (salarios, performance)
- 🔒 Información confidencial
- 🔒 Coordinar regalos/sorpresas para alguien

---

### 4. Overcommunicate Context, Not Just Conclusions

**Mal** ❌:

> "Vamos a cambiar a microservices."

**Bien** ✅:

> "**Context**: Nuestro monolito tarda 2h en deployar y bloquea a 3 equipos. **Problema**: No podemos iterar rápido. **Solución**: Extraer módulo de Orders a microservicio. **Trade-off**: Más complejidad operacional, pero equipos autónomos. **Decisión**: Go. **Siguiente**: Tech Lead escribe ADR esta semana."

**Por qué**:

- Otros entienden el razonamiento, no solo la conclusión
- Pueden cuestionar si el context cambia
- Facilita discusiones constructivas

---

### 5. Bias Toward Action

**Principio**: En caso de duda, hacer algo es mejor que paralysis.

**Práctica**:

- No esperar consenso perfecto (imposible con >10 personas)
- Decisiones reversibles → Decidir rápido, iterar
- Decisiones irreversibles → Tomar más tiempo, consultar más gente
- Si después de 2 días de discusión no hay consenso → Decision maker (PM, Tech Lead, EM) decide

---

## 📱 Estructura de Canales

### Slack / Microsoft Teams

#### Canales Generales

| Canal        | Propósito                          | Quién publica | Frecuencia         |
| ------------ | ---------------------------------- | ------------- | ------------------ |
| **#general** | Anuncios de empresa, celebraciones | Everyone      | Bajo (1-2/semana)  |
| **#random**  | Memes, conversación casual         | Everyone      | Alto (varias/día)  |
| **#wins**    | Celebrar logros del equipo         | Everyone      | Medio (3-5/semana) |

---

#### Canales de Equipos

| Canal             | Propósito                                         | Miembros                           | Actividad  |
| ----------------- | ------------------------------------------------- | ---------------------------------- | ---------- |
| **#engineering**  | Todo el equipo de Engineering                     | All Developers, QA, DevOps, EM     | Alta       |
| **#development**  | Equipo de Development (Frontend, Backend, Mobile) | Developers, Tech Leads             | Alta       |
| **#devops**       | Equipo de DevOps/Platform                         | DevOps, SRE, Cloud Engineers       | Media      |
| **#product**      | Equipo de Producto                                | PMs, POs, BAs, Data Analysts       | Alta       |
| **#design**       | Equipo de Diseño                                  | Designers, Researchers             | Media      |
| **#architecture** | Equipo de Arquitectura                            | Architects, Tech Leads             | Baja-Media |
| **#qa**           | Quality Assurance                                 | QA Engineers, Automation Engineers | Media      |

**Qué se postea en cada canal**:

**#engineering**:

- ✅ Anuncios que afectan a todos (nuevo stack, proceso, tool)
- ✅ RFCs (Request for Comments) técnicos
- ✅ Post-mortems de incidentes
- ✅ Celebrar releases grandes
- ❌ No: Debugging de bugs específicos (usar canales específicos)

**#development**:

- ✅ Preguntas técnicas (code, arquitectura)
- ✅ Code review requests urgentes
- ✅ Breaking changes en APIs
- ✅ Nuevas librerías/frameworks
- ❌ No: Product decisions (usar #product)

**#devops**:

- ✅ Cambios en infraestructura
- ✅ Alertas y outages (también integrar monitoring tools)
- ✅ Deploy announcements
- ✅ On-call schedule
- ❌ No: Application code issues (a menos que sea infra-related)

**#product**:

- ✅ Roadmap updates
- ✅ User research findings
- ✅ Feature proposals
- ✅ Sprint goals
- ❌ No: Technical implementation details

**#design**:

- ✅ Design reviews / critiques
- ✅ Design system updates
- ✅ Figma file shares
- ✅ User research shareouts
- ❌ No: Final designs (esos van a #development para handoff)

---

#### Canales por Proyecto/Squad

| Canal                        | Propósito                     | Duración                         |
| ---------------------------- | ----------------------------- | -------------------------------- |
| **#squad-checkout**          | Equipo trabajando en checkout | Permanente                       |
| **#squad-mobile**            | Equipo de mobile app          | Permanente                       |
| **#project-oauth-migration** | Migración a OAuth 2.0         | Temporal (archivado post-launch) |

**Naming convention**: `#squad-[nombre]` o `#project-[nombre]`

**Cuándo crear un canal de proyecto**:

- Proyecto dura >2 semanas
- Involucra >3 personas
- Necesita coordinación frecuente

**Cuándo NO crear un canal de proyecto**:

- Proyecto <1 semana (usar thread en #development)
- Solo 1-2 personas (usar DM)
- Ya existe un squad que lo cubre

---

#### Canales de Operaciones

| Canal           | Propósito                         | Integraciones                   | Notificaciones         |
| --------------- | --------------------------------- | ------------------------------- | ---------------------- |
| **#incidents**  | Incidentes de producción activos  | PagerDuty, Monitoring           | @channel para P0/P1    |
| **#deploys**    | Deploy notifications              | CI/CD (GitHub Actions, Jenkins) | Silencioso (solo info) |
| **#alerts**     | Alertas automáticas (no críticas) | Grafana, Datadog, Azure Monitor | Silencioso             |
| **#monitoring** | Dashboards y métricas             | Grafana snapshots, reports      | Silencioso             |

**Reglas de #incidents**:

- Solo para incidentes activos P0/P1
- Crear thread por incidente
- Format: `🚨 [P0] Production API down - All users affected`
- Actualizar cada 15-30min con status
- Resolver y cerrar thread cuando fixed
- Postmortem linked al thread

---

#### Canales de Integración

| Canal                  | Integración                      | Propósito                      | Notificaciones              |
| ---------------------- | -------------------------------- | ------------------------------ | --------------------------- |
| **#github**            | GitHub                           | PRs, merges, releases          | Filtrado (solo main branch) |
| **#jira**              | Jira                             | Story updates, sprint changes  | Filtrado (solo important)   |
| **#ci-cd**             | GitHub Actions / Azure Pipelines | Build status, test failures    | Solo failures               |
| **#customer-feedback** | Zendesk, Intercom                | User feedback, support tickets | Críticos solo               |

---

### Email

**Cuándo usar email en vez de Slack**:

| Situación                                            | Tool          | Por qué                                 |
| ---------------------------------------------------- | ------------- | --------------------------------------- |
| Updates internos rápidos                             | Slack         | Menos formal, más rápido                |
| Comunicación con stakeholders externos               | Email         | Más formal, auditable                   |
| Decisiones importantes que necesitan registro formal | Email + Slack | Email para record, Slack para discusión |
| Contratos, legal, HR                                 | Email         | Requerimiento legal                     |
| All-hands announcements                              | Email + Slack | Asegurar que todos lo vean              |

---

## 🚨 Matriz de Escalación

### Niveles de Severidad

| Nivel             | Descripción                                                            | Response Time | Escalation Path                                     |
| ----------------- | ---------------------------------------------------------------------- | ------------- | --------------------------------------------------- |
| **P0 - Critical** | Sistema completamente caído, pérdida de datos, >50% usuarios afectados | <15min        | On-call SRE → Tech Lead → Engineering Manager → CTO |
| **P1 - High**     | Funcionalidad core afectada, 20-50% usuarios afectados                 | <1h           | On-call SRE → Tech Lead → Engineering Manager       |
| **P2 - Medium**   | Funcionalidad no-core afectada, <20% usuarios afectados                | <4h           | On-call SRE → Tech Lead                             |
| **P3 - Low**      | Bug menor, workaround disponible, <5% usuarios afectados               | <1 day        | Developer → Tech Lead                               |
| **P4 - Trivial**  | Cosmético, no afecta funcionalidad                                     | Backlog       | Product Owner → Developer                           |

---

### Escalation Paths por Tipo

#### 1. Incidentes Técnicos

```
[Incident Detected]
    ↓
[On-call SRE] (acknowledge <10min)
    ↓
¿P0/P1?
    ├─ Sí → [Notify Tech Lead + Engineering Manager]
    │        ↓
    │        [Create war room #incident-YYYYMMDD-NNN]
    │        ↓
    │        [Notify Product Manager + Customer Support]
    │        ↓
    │        ¿>2h sin resolver?
    │             ├─ Sí → [Escalate to CTO]
    │             └─ No → [Continue mitigation]
    └─ No (P2/P3) → [SRE + Developer fix]
```

**Contactos**:

- **On-call SRE**: Ver rotación en PagerDuty
- **Tech Lead**: @tech-lead-channel en Slack
- **Engineering Manager**: @engineering-manager
- **CTO**: @cto (solo para P0 >2h)

---

#### 2. Decisiones de Producto

```
[Product Decision Needed]
    ↓
[Product Owner / PM]
    ↓
¿Afecta roadmap o múltiples equipos?
    ├─ Sí → [Head of Product / VP Product]
    │        ↓
    │        ¿Strategic decision?
    │             ├─ Sí → [CEO / Executives]
    │             └─ No → [Head of Product decide]
    └─ No → [PO decide con Tech Lead input]
```

**Contactos**:

- **Product Owner**: @po-squad-nombre
- **Product Manager**: @pm-nombre
- **Head of Product**: @head-of-product
- **VP Product**: @vp-product (solo decisiones estratégicas)

---

#### 3. Decisiones de Arquitectura

```
[Architecture Decision Needed]
    ↓
[Tech Lead]
    ↓
¿Afecta múltiples sistemas o es irreversible?
    ├─ Sí → [Solution Architect]
    │        ↓
    │        [RFC (Request for Comments)]
    │        ↓
    │        ¿Organization-wide impact?
    │             ├─ Sí → [Enterprise Architect + CTO]
    │             └─ No → [Solution Architect decide]
    └─ No → [Tech Lead decide con equipo]
```

**Proceso**:

1. Tech Lead identifica necesidad
2. Escribe RFC (1-2 páginas)
3. Share en #architecture para comments (3-5 días)
4. Arquitecto revisa y aprueba/rechaza/pide cambios
5. Decision → ADR (Architecture Decision Record)

---

#### 4. Problemas de Seguridad

```
[Security Issue Detected]
    ↓
[Developer / DevOps]
    ↓
¿Critical vulnerability (CVE >7.0, data exposure)?
    ├─ Sí (P0) → [Security Engineer IMMEDIATELY]
    │             ↓
    │             [Notify CTO + Legal]
    │             ↓
    │             [Incident response plan]
    │             ↓
    │             ¿Data breach?
    │                  ├─ Sí → [Legal + PR + Notify users]
    │                  └─ No → [Fix + Postmortem]
    └─ No (P2/P3) → [Security Engineer]
                      ↓
                      [Triage and schedule fix]
```

**Contactos**:

- **Security Engineer**: @security-team en Slack + <security@company.com>
- **CTO**: Solo para P0 security
- **Legal**: <legal@company.com> (solo si hay data breach o regulatorio)

---

#### 5. Problemas de Performance

```
[Performance Issue]
    ↓
[Developer / SRE]
    ↓
¿Afecta >20% usuarios o SLA?
    ├─ Sí → [Treat as Incident P1/P2]
    │        ↓
    │        [Follow incident escalation path]
    └─ No → [Create Performance Task]
             ↓
             [Tech Lead prioriza en backlog]
```

---

### Response Time SLAs

| Severity | Acknowledge | Initial Response | Resolution Target | Communication Frequency |
| -------- | ----------- | ---------------- | ----------------- | ----------------------- |
| **P0**   | <10min      | <15min           | <2h               | Every 15-30min          |
| **P1**   | <30min      | <1h              | <8h               | Every 1-2h              |
| **P2**   | <2h         | <4h              | <2 days           | Once per day            |
| **P3**   | <1 day      | <1 day           | <1 week           | As needed               |
| **P4**   | Backlog     | Backlog          | Next sprint       | Not urgent              |

---

## 📊 Reporting y Métricas

### Daily Updates

**Quién**: Development teams  
**Cuándo**: Daily Standup  
**Dónde**: Slack #squad-[nombre] o herramienta de standup (Geekbot)  
**Formato**: What I did yesterday, What I'll do today, Blockers

**No necesita reportarse más allá del equipo** (Engineering Manager lee si quiere)

---

### Sprint Reports

**Quién**: Tech Lead + Product Owner  
**Cuándo**: Fin de cada sprint  
**Dónde**: Confluence/Notion + Slack #engineering  
**Audiencia**: Engineering team + stakeholders

**Template**:

```markdown
# Sprint [N] Report - [Squad Name]

**Sprint Goal**: [What we aimed to achieve]

## ✅ Completed

- [Feature 1] - Impact: [business value]
- [Feature 2] - Impact: [business value]
- [Bug fixes] - [N] bugs fixed

## ⚠️ In Progress (carried to next sprint)

- [Feature 3] - Reason: [blocker or underestimation]

## 📊 Metrics

- Velocity: [X] story points (avg last 3 sprints: [Y])
- Completion rate: [Z]% (committed vs completed)
- Deployment frequency: [N] deploys this sprint
- Incidents: [M] (P0: 0, P1: 1, P2: 3)

## 🎯 Next Sprint Preview

- Sprint Goal: [Next goal]
- Top priorities: [List 3-5]
```

**Distribución**:

- Post en #engineering (Slack)
- Link en Confluence sprint page
- Email a stakeholders (opcional, solo si piden)

---

### Weekly Executive Summary

**Quién**: Engineering Manager + Head of Product  
**Cuándo**: Viernes EOD  
**Dónde**: Email a Executives + Confluence  
**Audiencia**: CEO, CTO, VP Product, VP Sales

**Template**:

```markdown
# Engineering Weekly Update - [Week of Jan 15-19, 2025]

## 🎯 Highlights

- ✅ [Major feature] shipped to 100% users, [metric] improved by X%
- ✅ Infrastructure migration 60% complete (on track for Feb 1)
- ⚠️ [Known issue] affecting [Y]% users, fix deploying Monday

## 📈 Key Metrics

| Metric               | This Week  | Last Week  | Target   |
| -------------------- | ---------- | ---------- | -------- |
| Deployment Frequency | 15 deploys | 12 deploys | >10/week |
| MTTR                 | 45min      | 1.2h       | <1h      |
| System Uptime        | 99.95%     | 99.89%     | >99.9%   |
| Active Incidents     | 0          | 1 (P2)     | 0        |

## 🚀 In Progress

- [Project A] - 70% complete (on track)
- [Project B] - 40% complete (1 week delay due to [reason])

## 🚧 Blockers & Risks

- [Blocker 1] - Impact: [X], Need: [Y], Owner: [Z]

## 📅 Next Week Focus

- Ship [Feature X]
- Complete [Infrastructure Y]
- Hire 2 Backend Developers (3 final interviews scheduled)
```

**Frequency**: Semanal (Viernes)  
**Response expected**: No (unless executives have questions)

---

### Monthly All-Hands Presentation

**Quién**: CTO + Engineering Manager  
**Cuándo**: Primer viernes de cada mes  
**Dónde**: All-hands meeting (Zoom + grabación)  
**Audiencia**: Toda la empresa

**Contenido** (15min):

1. **Major achievements** del mes (2min)
2. **Product launches** y business impact (3min)
3. **Engineering metrics** (DORA, uptime, velocity) (3min)
4. **Team updates** (new hires, promotions) (2min)
5. **Roadmap preview** próximos 1-2 meses (3min)
6. **Q&A** (5min)

**Formato**: Slides (Google Slides), visualmente atractivo, no muy técnico

---

### Quarterly Business Review (QBR)

**Quién**: CTO + VP Product + VP Sales  
**Cuándo**: Final de cada quarter  
**Dónde**: Board meeting (presencial) + documento escrito  
**Audiencia**: Board of Directors, Investors, Executives

**Contenido** (30min presentación + 30min Q&A):

1. **Q[N] Objectives & Results** (OKRs)

   - Qué nos propusimos
   - Qué logramos (% completion)
   - Qué no logramos y por qué

2. **Engineering Metrics**

   - DORA metrics (Deployment Frequency, Lead Time, MTTR, Change Failure Rate)
   - System uptime
   - Tech debt ratio
   - Team velocity trend

3. **Product Releases**

   - Major features shipped
   - Business impact (revenue, users, engagement)

4. **Team Growth**

   - Headcount: start vs end of quarter
   - New hires, attrition
   - Key promotions

5. **Challenges & Learnings**

   - What went wrong (incidents, delays)
   - How we addressed it
   - Improvements implemented

6. **Q[N+1] Roadmap**
   - Strategic priorities next quarter
   - Resource allocation
   - Risks and dependencies

**Formato**: Documento escrito (15-20 páginas) + Slide deck (20-30 slides)

---

### Incident Reports (Postmortems)

**Quién**: On-call SRE + Tech Lead  
**Cuándo**: Within 48h del incidente P0/P1  
**Dónde**: Confluence + Slack #incidents  
**Audiencia**: Engineering team + impacted stakeholders

**Template**: Ver [Workflows - Incident Response & Postmortem](../workflows/README.md#incident-response--postmortem)

**Distribución**:

- P0: Email a toda Engineering + Executives
- P1: Post en #engineering + #incidents
- P2: Post en #incidents solo

---

## 📝 Comunicación Asíncrona

### Principios de Async Communication

1. **Write clearly**: Assume el lector no puede hacer follow-up questions inmediatamente
2. **Provide context**: No asumir que todos tienen el mismo contexto que tú
3. **Be specific**: "Podemos hablar?" → "¿Tienes 15min hoy para revisar el diseño del endpoint de auth?"
4. **Set expectations**: "No es urgente, responde cuando puedas" vs "Necesito respuesta antes de 5pm"
5. **Use threads**: Mantener conversaciones organizadas

---

### Templates de Mensajes Async

#### Request for Feedback (RFC)

```markdown
📋 **RFC: [Título de la propuesta]**

**Context**: [Por qué estamos considerando esto]

**Proposal**: [Qué proponemos hacer]

**Alternatives Considered**:

- Option A: [Pros/Cons]
- Option B: [Pros/Cons]

**Recommendation**: [Cuál preferimos y por qué]

**Timeline**: [Cuándo necesitamos decidir]

**Feedback requested by**: [Fecha]

React with:

- ✅ if you support
- ❓ if you have questions
- ⚠️ if you have concerns

Comments appreciated! 👇
```

---

#### Status Update

```markdown
🚀 **Update: [Project Name]**

**Progress**: [X]% complete

**Completed this week**:

- ✅ [Task 1]
- ✅ [Task 2]

**In progress**:

- 🔄 [Task 3] - ETA: [Date]
- 🔄 [Task 4] - ETA: [Date]

**Blockers**:

- 🚧 [Blocker 1] - Need: [X], Owner: [@person]

**Next week**:

- [ ] [Task 5]
- [ ] [Task 6]

**Questions/Help needed**: [Si aplica]
```

---

#### Decision Made

```markdown
✅ **Decision: [Título]**

**What we decided**: [Decisión clara en 1 frase]

**Why**: [Razonamiento en 2-3 bullets]

- Reason 1
- Reason 2

**Who was involved**: [@person1] [@person2] [@person3]

**Next steps**:

1. [Action 1] - Owner: [@person] - Due: [Date]
2. [Action 2] - Owner: [@person] - Due: [Date]

**Documentation**: [Link to ADR/Confluence doc]
```

---

### Response Time Expectations (Async)

| Channel                   | Response Time         | Explanation                 |
| ------------------------- | --------------------- | --------------------------- |
| **Slack message**         | <4h during work hours | Best effort, not guaranteed |
| **Slack @mention**        | <2h during work hours | Higher priority             |
| **Slack @channel**        | <1h                   | Only for important/urgent   |
| **Email**                 | <24h                  | Formal communication        |
| **PR review request**     | <1 business day       | Blocking work               |
| **Slack DM from manager** | <2h                   | 1:1 stuff usually important |

**Out of hours**: No response expected (unless on-call for incidents)

---

## 📚 Prácticas de Documentación

### Dónde Documentar Qué

| Tipo de Documento              | Tool                                         | Ejemplo                                                                    |
| ------------------------------ | -------------------------------------------- | -------------------------------------------------------------------------- |
| **Decisiones de Arquitectura** | ADRs (Architecture Decision Records) en repo | "ADR-003: Adopt Microservices for Order Management"                        |
| **Procesos de equipo**         | README.md en este repo                       | [Workflows](../workflows/README.md), [Ceremonias](../ceremonias/README.md) |
| **Documentación de código**    | Inline comments + README en cada repo        | "This function calculates..."                                              |
| **API documentation**          | OpenAPI/Swagger + Postman collections        | API specs auto-generated                                                   |
| **Runbooks operacionales**     | Confluence + links en código                 | "How to deploy to production"                                              |
| **Product specs**              | Confluence/Notion                            | "PRD: Checkout redesign"                                                   |
| **Design specs**               | Figma + Confluence                           | Figma files + design rationale                                             |
| **Meeting notes**              | Confluence/Notion                            | "Sprint Planning 2025-01-15"                                               |
| **OKRs y Roadmap**             | Confluence/Notion + Google Sheets            | Quarterly goals                                                            |

---

### Documentation Quality Standards

**Good documentation tiene**:

- ✅ **Clear title** que describe el contenido
- ✅ **Date** de creación y última actualización
- ✅ **Owner** (quién lo mantiene actualizado)
- ✅ **Table of contents** para docs >1 página
- ✅ **Context** (por qué este doc existe)
- ✅ **Examples** cuando sea posible
- ✅ **Links** a recursos relacionados

**Bad documentation**:

- ❌ Sin fecha (no sabemos si está desactualizado)
- ❌ Sin owner (nadie se hace responsable)
- ❌ Muy técnico sin contexto (solo expertos entienden)
- ❌ Desorganizado (wall of text)
- ❌ Duplicado (misma info en 5 lugares diferentes)

---

### Documentation Maintenance

**Revisión trimestral** (cada 3 meses):

- [ ] Engineering Manager revisa índice de documentación
- [ ] Archivar docs obsoletos (mover a carpeta "Archive")
- [ ] Actualizar docs desactualizados
- [ ] Identificar gaps (qué falta documentar)

**Ownership**:

- Cada documento debe tener un owner (persona o equipo)
- Owner es responsable de mantenerlo actualizado
- Si el owner cambia de rol, reasignar ownership

---

## 🎯 Communication Metrics

| Métrica                                     | Target                   | Cómo Medir                     | Acción si bajo              |
| ------------------------------------------- | ------------------------ | ------------------------------ | --------------------------- |
| **Slack Response Time (during work hours)** | <4h (median)             | Slack analytics                | Recordar expectations       |
| **PR Review Time**                          | <1 business day          | GitHub metrics                 | Más reviewers, reminders    |
| **Documentation Freshness**                 | >80% updated in last 6mo | Manual audit quarterly         | Deprecate old docs          |
| **Meeting Load**                            | <20% of work time        | Calendar analysis              | Cancel/consolidate meetings |
| **Async vs Sync Ratio**                     | >60% async               | Message count vs meeting hours | Push more to async          |

---

## 🔗 Links Relacionados

- [Workflows](../workflows/README.md) - Procesos inter-equipos
- [Ceremonias](../ceremonias/README.md) - Ceremonias ágiles
- [Equipos](../equipos/README.md) - Estructura organizacional

---

**Última actualización**: Enero 2025  
**Mantenido por**: Engineering Manager + Head of Product
