# Product Owner

## 📋 Visión General

El Product Owner (PO) es responsable de la **ejecución táctica del backlog** en un contexto Agile/Scrum, maximizando el valor del producto trabajando de cerca con el equipo de desarrollo. A diferencia del Product Manager (más estratégico), el PO se enfoca en **sprint-to-sprint execution**, refinamiento de historias, y acceptance de trabajo completado.

**Nota**: En algunas empresas, **Product Owner = Product Manager** (mismo rol). En otras (especialmente grandes), están separados: PM (estrategia) + PO (ejecución).

## 🎯 Responsabilidades

### Backlog Management

**Principales tareas**:
- Crear y mantener product backlog (Jira, Azure DevOps)
- Escribir user stories claras y detalladas
- Priorizar backlog basado en value y dependencies
- Refinar user stories (grooming sessions)
- Asegurar que backlog esté "ready" para sprints

**Backlog structure**:
```yaml
Ready for Development (Sprint-ready):
  - User Story 1 (refined, estimated, acceptance criteria)
  - User Story 2

Next (Being refined):
  - User Story 3 (needs more detail)
  - User Story 4 (blocked, dependencies)

Future (Icebox):
  - User Story 5 (low priority)
  - User Story 6 (ideas, not committed)
```

**Definition of Ready** (DoR):
- User story está claramente escrita
- Acceptance criteria definidos (GIVEN/WHEN/THEN)
- Dependencies identificadas y resueltas
- Design mockups disponibles (si aplica)
- Estimado por el equipo (story points)

---

### User Story Writing

**Principales tareas**:
- Escribir user stories en formato estándar
- Definir acceptance criteria (GIVEN/WHEN/THEN)
- Incluir edge cases y error handling
- Attachments (mockups, specs, wireframes)
- Tagging y metadata (epics, labels, components)

**User story template**:
```markdown
As a [user type],
I want [feature/capability],
So that [benefit/value]

Acceptance Criteria:
- GIVEN [context/precondition]
  WHEN [action/event]
  THEN [expected outcome]

- GIVEN [another context]
  WHEN [another action]
  THEN [another outcome]

Edge Cases:
- What if [scenario]?
- How to handle [error case]?

Design:
- [Link to Figma mockups]

Technical Notes:
- API endpoint: /api/feature
- Database: New table `feature_table`
```

**Example** (real user story):
```
Title: User can reset password via email

As a registered user,
I want to reset my password via email,
So that I can regain access if I forget my password.

Acceptance Criteria:
- GIVEN I'm on the login page
  WHEN I click "Forgot password?" link
  THEN I'm redirected to password reset page

- GIVEN I'm on password reset page
  WHEN I enter my email and click "Send reset link"
  THEN I receive an email with a reset link within 2 minutes

- GIVEN I receive the reset email
  WHEN I click the reset link
  THEN I'm redirected to a page to set a new password

- GIVEN I'm on the new password page
  WHEN I enter a valid password (8+ chars, 1 uppercase, 1 number) and click "Reset"
  THEN my password is updated and I'm logged in automatically

Edge Cases:
- If email doesn't exist, show generic message (security)
- Reset link expires after 24 hours
- Reset link can only be used once

Design:
- [Figma link]

Technical:
- POST /api/auth/password-reset
- Email template: password_reset.html
```

---

### Sprint Planning & Execution

**Principales tareas**:
- Facilitar sprint planning (select stories para sprint)
- Daily standups (optional, depende de empresa)
- Remove blockers para el equipo
- Scope management (evitar scope creep)
- Sprint goal definition

**Sprint cadence** (2-week sprint típico):
```
Week 1:
  - Monday: Sprint Planning (2-4 hours)
    - Select stories from backlog
    - Define sprint goal
    - Estimate capacity
  - Tuesday-Friday: Development
    - Daily standups (15 min)
    - PO available for questions

Week 2:
  - Monday-Thursday: Development
    - PO testing completed stories
  - Thursday: Sprint Review (1 hour)
    - Demo completed work
  - Friday: Sprint Retrospective (1 hour)
    - What went well, what to improve
  - Friday afternoon: Backlog Refinement (1-2 hours)
    - Prepare stories for next sprint
```

**Sprint goal example**:
- "Enable users to export reports to PDF"
- "Improve checkout conversion by implementing guest checkout"
- "Fix top 5 bugs affecting user experience"

---

### Acceptance & Testing

**Principales tareas**:
- Revisar y aceptar user stories completadas
- Manual testing (UAT - User Acceptance Testing)
- Verificar acceptance criteria cumplidos
- Identify bugs y edge cases
- Decisión: Accept, Reject, or Request changes

**Definition of Done** (DoD):
- Code completed y merged
- Unit tests pass (>80% coverage)
- Manual testing por PO: ✅ Passed
- Acceptance criteria met: ✅ All
- Documentation updated (if needed)
- No critical bugs
- Design QA pass (matches mockups)
- Deployed to staging environment

**Testing workflow**:
1. Developer completes story → moves to "Ready for Testing"
2. PO tests in staging environment
3. PO verifies each acceptance criterion
4. If pass → move to "Done", if fail → back to "In Progress" con comments
5. If Done → story goes to production in next release

---

### Stakeholder Communication

**Principales tareas**:
- Sprint demos (show completed work)
- Progress updates (to PM, leadership)
- Feature requests communication (from Sales, Support)
- Release notes (user-facing communication)
- Manage expectations (timeline, scope)

**Communication cadence**:
- **Daily**: Engineering team (standups, Slack)
- **Weekly**: Sprint progress update (written)
- **Bi-weekly**: Sprint review demo (stakeholders)
- **Ad-hoc**: Feature request triage (Sales, Support)

---

### Release Management

**Principales tareas**:
- Coordinar releases (con DevOps/Engineering)
- Release notes writing (user-facing)
- Rollout planning (phased rollout, feature flags)
- Post-release monitoring (bugs, metrics)
- Hotfix prioritization

**Release cadence** (depende de empresa):
- **Continuous Deployment**: Every merge to main → production (startup)
- **Weekly releases**: Every Friday
- **Bi-weekly**: Aligned with sprint cadence
- **Monthly**: Larger enterprises

**Release notes template**:
```markdown
# Release v2.5.0 - December 5, 2024

## New Features
- 🎉 **Export to PDF**: Users can now export reports to PDF format
- 🔔 **Notifications**: Receive email notifications for important updates

## Improvements
- ⚡ Improved dashboard load time by 40%
- 🎨 Redesigned settings page for better usability

## Bug Fixes
- 🐛 Fixed issue where users couldn't upload large files
- 🐛 Resolved crash when clicking "Save" multiple times

## Known Issues
- Export to Excel not working on Safari (fix planned for v2.5.1)
```

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Mid to Senior (2-10 años de experiencia)

**Progresión típica**:
```
Junior Product Owner / Associate PO (0-2 años)
    - Tareas: Escribir user stories, testing, backlog support
    ↓
Product Owner (2-5 años)
    - Tareas: Full backlog ownership, sprint planning, acceptance
    ↓
Senior Product Owner (5-8 años)
    - Tareas: Complex products, multiple teams, mentoring
    ↓
Lead Product Owner (8-10 años)
    - Manage: 2-3 POs (if scaled Agile)
    ↓
Product Manager (lateral move)
    - Transition from execution (PO) → strategy (PM)
```

---

### Skills Requeridas

#### Agile/Scrum (Critical)

**Must have**:
- ✅ **Scrum framework**: Sprints, ceremonies, artifacts
- ✅ **Backlog management**: Prioritization, refinement
- ✅ **User story writing**: Clear, testable, valuable
- ✅ **Acceptance criteria**: GIVEN/WHEN/THEN format
- ✅ **Sprint planning**: Capacity, velocity, sprint goal
- ✅ **Definition of Done (DoD)**: Quality standards

**Certifications** (nice to have):
- 🔶 **CSPO** (Certified Scrum Product Owner) - Scrum Alliance
- 🔶 **PSPO** (Professional Scrum Product Owner) - Scrum.org
- 🔶 **SAFe PO/PM** (Scaled Agile Framework)

---

#### Product Skills (Medium)

**Must have**:
- ✅ **Requirements gathering**: Understand user needs
- ✅ **Prioritization**: Value vs effort, MoSCoW
- ✅ **Testing**: UAT, manual testing, bug identification
- ✅ **Analytics basics**: Understand product metrics

**Nice to have**:
- 🔶 **User research**: Interviews, usability testing (más PM responsibility)
- 🔶 **Product strategy**: Roadmap, vision (más PM responsibility)

---

#### Technical Skills (Basic)

**Must have**:
- ✅ **Jira / Azure DevOps**: Backlog tools proficiency
- ✅ **Understanding of SDLC**: How software is built
- ✅ **API basics**: REST, integrations (conversational)
- ✅ **Testing**: Manual testing, edge cases

**Nice to have**:
- 🔶 **SQL basics**: Query data for validation
- 🔶 **Postman / API testing**: Test APIs manually
- 🔶 **Browser DevTools**: Inspect elements, network tab

---

#### Soft Skills (Critical)

**Must have**:
- ✅ **Communication**: Clear, concise, written + oral
- ✅ **Collaboration**: Work with Eng, Design, QA, PM
- ✅ **Decision-making**: Prioritization, scope management
- ✅ **Problem-solving**: Remove blockers, find solutions
- ✅ **Stakeholder management**: Manage expectations
- ✅ **Adaptability**: Respond to changing priorities

---

### Stack Tecnológico

El PO usa principalmente **Agile tools** y **backlog management platforms**:

#### Backlog & Project Management
```yaml
Primary: Jira (most common), Azure DevOps, Linear
Alternatives: Monday.com, Asana, ClickUp, Shortcut
Kanban boards: Trello, Notion (smaller teams)
```

#### Documentation
```yaml
Confluence (Jira integration), Notion, Google Docs
Miro (workshops, user story mapping)
```

#### Design Collaboration
```yaml
Figma (view designs, comment, handoff specs)
Zeplin (legacy, design specs)
```

#### Testing
```yaml
Manual testing: Staging environments, QA tools
Bug tracking: Jira, Bugzilla
API testing: Postman (basic)
```

#### Analytics (basic visibility)
```yaml
Google Analytics, Mixpanel, Amplitude (dashboards)
Product usage: Pendo, FullStory
```

#### Communication
```yaml
Slack, Microsoft Teams
Zoom, Google Meet (sprint reviews, planning)
Loom (async video updates)
```

---

## 📊 Métricas de Éxito

### Sprint Performance

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Sprint Commitment Accuracy** | >80% stories completed | Por sprint |
| **Velocity Stability** | ±15% variance | Por sprint |
| **Sprint Goal Achievement** | >90% | Por sprint |
| **Backlog Health** | >2 sprints ready (refined) | Semanal |

### Story Quality

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Stories Returned to Dev** | <10% (due to unclear requirements) | Por sprint |
| **Acceptance Rate (First Pass)** | >85% | Por sprint |
| **Average Story Cycle Time** | <5 days (from In Progress → Done) | Semanal |
| **Bug Escape Rate** | <5 bugs per sprint (found post-release) | Por sprint |

### Team Collaboration

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Team Satisfaction** | >4/5 (clarity, support) | Trimestral |
| **Blocker Resolution Time** | <24 hours | Semanal |
| **Backlog Refinement Attendance** | 100% | Semanal |

### Product Impact (indirect, shared with PM)

| Métrica | Target | Influencia |
|---------|--------|------------|
| **Feature Adoption** | >30% users | Media |
| **Bug Rate** | <5 critical bugs/month | Alta (quality) |
| **Release Frequency** | On-time releases | Alta |

---

## 🔄 Interacciones con Otros Equipos

### Con Engineering Team

**Frecuencia**: Daily  
**Modo**: **Collaboration** (partnership muy cercano)

**Actividades**:
- Daily standups (progress, blockers)
- Sprint planning (story selection, capacity)
- Backlog refinement (estimate, clarify stories)
- Ad-hoc questions (clarifications durante development)
- Sprint review (demo completed work)
- Sprint retrospective (process improvement)

**Ratio**: 1 PO : 5-8 Engineers (Scrum team típico)

**Tools**: Jira, Slack, Zoom

---

### Con Product Manager (si separado del PO)

**Frecuencia**: Weekly  
**Modo**: **Collaboration** + **Reporting**

**Actividades**:
- Roadmap translation (PM strategy → PO backlog)
- Feature prioritization (PM defines priority, PO sequences)
- User story creation (PM provides requirements, PO writes stories)
- Sprint progress updates (PO reports to PM)
- Stakeholder alignment

**División**:
- **PM**: Strategy, vision, roadmap, stakeholder management
- **PO**: Execution, backlog, sprint planning, acceptance

---

### Con QA / Test Engineers

**Frecuencia**: Daily  
**Modo**: **Collaboration**

**Actividades**:
- Test planning (test cases, scenarios)
- Bug triage (prioritize bugs)
- UAT collaboration (PO + QA testing together)
- Definition of Done alignment
- Regression testing coordination

**Tools**: Jira (bug tracking), TestRail (test management)

---

### Con UX/UI Designers

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Receive design mockups (Figma handoff)
- Clarify design specs (edge cases, states)
- Design QA (verify implementation matches design)
- Feedback loop (user issues → design improvements)

**Tools**: Figma, Slack

---

### Con Scrum Master (si existe rol separado)

**Frecuencia**: Daily  
**Modo**: **Collaboration**

**Actividades**:
- Facilitate ceremonies (SM facilita, PO participa)
- Remove impediments (SM + PO jointly)
- Process improvement (retrospectives)
- Team coaching (Agile practices)

**División**:
- **PO**: What to build (product value)
- **Scrum Master**: How to work (process, Agile coaching)

**Nota**: En muchas empresas, no hay Scrum Master separado; PO o Engineering Manager hace esas tareas.

---

### Con Stakeholders (Sales, Support, Marketing)

**Frecuencia**: Bi-weekly  
**Modo**: **Communication**

**Actividades**:
- Sprint demos (show completed work)
- Feature requests triage (evaluate, prioritize)
- Release notes communication
- Timeline updates (when will X be ready)

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: Product Owner → Product Manager

```
Product Owner (2-5 años)
    ↓
Senior Product Owner (5-8 años)
    ↓
Product Manager (lateral move)
    - Transition: Execution (PO) → Strategy (PM)
    - Aprender: Market analysis, product strategy, roadmapping
```

#### Opción 2: Stay in PO Track (Large Orgs)

```
Product Owner (2-5 años)
    ↓
Senior Product Owner (5-8 años)
    - Complex products, multiple scrum teams
    ↓
Lead Product Owner (8-10 años)
    - Scaled Agile (SAFe), coordinate multiple POs
```

#### Opción 3: Scrum Master / Agile Coach

```
Product Owner (2-5 años)
    ↓
Scrum Master
    - Focus: Process, team coaching (not product)
    ↓
Agile Coach
    - Enterprise agile transformation
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Dominar Jira/Azure DevOps (backlog management)
- [ ] Get CSPO o PSPO certification
- [ ] Escribir 100+ user stories (practice clarity)
- [ ] Facilitar 10+ sprint planning sessions
- [ ] Aprender SQL básico (para validar data)

**Próximos 1-2 años**:
- [ ] Own full product backlog (not just features)
- [ ] Aprender product analytics (Mixpanel, Amplitude)
- [ ] Desarrollar stakeholder management skills
- [ ] Transition hacia Product Manager role (si interesa)
- [ ] Mentoring de Junior PO

**Próximos 3-5 años** (hacia PM o Lead PO):
- [ ] Product strategy (roadmap, vision)
- [ ] Market analysis (competitive intelligence)
- [ ] P&L understanding (business acumen)
- [ ] Scaled Agile (SAFe, multiple teams)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"User Stories Applied"** - Mike Cohn (user story writing)
- 📚 **"Agile Estimating and Planning"** - Mike Cohn (sprint planning, velocity)
- 📚 **"Scrum: The Art of Doing Twice the Work in Half the Time"** - Jeff Sutherland
- 📚 **"The Professional Product Owner"** - Don McGreal & Ralph Jocham
- 📚 **"Inspired"** - Marty Cagan (si quieres transicionar a PM)

#### Certifications

- **CSPO** (Certified Scrum Product Owner) - Scrum Alliance (~$1k, 2-day course)
- **PSPO** (Professional Scrum Product Owner) - Scrum.org (~$200, exam only)
- **SAFe POPM** (SAFe Product Owner/Product Manager) - Scaled Agile

#### Comunidades

- **Scrum Alliance**: Events, local user groups
- **Scrum.org**: Resources, forums
- **Product Owner Community (Slack)**: Discussions, best practices
- **Agile Alliance**: Conferences, resources

---

## 📝 Herramientas del Día a Día

### Backlog Management

| Tool | Uso | Nivel |
|------|-----|-------|
| **Jira** | Backlog, sprint planning, tracking | Advanced |
| **Azure DevOps** | Alternative to Jira (Microsoft shops) | Advanced |
| **Linear** | Modern alternative (startups) | Intermediate |
| **Miro** | User story mapping, workshops | Intermediate |

### Documentation

| Tool | Uso |
|------|-----|
| **Confluence** | User stories, requirements, knowledge base |
| **Notion** | Lightweight alternative to Confluence |
| **Google Docs** | Collaborative documents |

### Design & Testing

| Tool | Uso |
|------|-----|
| **Figma** | View designs, comment, specs |
| **Postman** | API testing (basic) |
| **Browser DevTools** | Inspect elements, debug |

### Communication

| Tool | Uso |
|------|-----|
| **Slack / Teams** | Team communication |
| **Zoom / Google Meet** | Sprint ceremonies |
| **Loom** | Async video updates |

---

## 🚀 Ejemplo de Semana Típica

### Lunes (Sprint Planning)
- **9:00-10:00**: Prep for sprint planning (review refined backlog)
- **10:00-13:00**: Sprint Planning (select stories, estimate, define sprint goal)
- **14:00-15:00**: Update Jira (move stories to sprint, assign)
- **15:00-17:00**: Deep work: Write user stories para próximos sprints

### Martes-Jueves (Sprint Execution)
**Daily**:
- **9:00-9:15**: Daily standup (progress, blockers)
- **9:15-10:00**: Answer developer questions (Slack, ad-hoc meetings)
- **10:00-12:00**: Testing completed stories (UAT in staging)
- **14:00-15:00**: Backlog refinement prep (refine stories para próximo sprint)
- **15:00-17:00**: Stakeholder sync (triage feature requests, updates)

### Jueves (Sprint Review)
- **9:00-12:00**: Testing remaining stories (crunch time)
- **14:00-15:00**: Sprint Review prep (demo script)
- **15:00-16:00**: Sprint Review (demo completed work a stakeholders)
- **16:00-17:00**: Retrospective (what went well, improvements)

### Viernes (Backlog Refinement)
- **9:00-9:15**: Daily standup
- **9:15-12:00**: Backlog Refinement session con Engineering (estimate, clarify stories)
- **14:00-16:00**: Deep work: Write user stories, research features
- **16:00-17:00**: Week wrap-up, release notes (if deploying)

**Sprint execution** (planning, standups, testing): ~40%  
**User story writing**: ~25%  
**Stakeholder communication**: ~15%  
**Backlog refinement**: ~15%  
**Admin**: ~5%

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- 2-3+ años de experiencia (puede ser QA, BA, Junior PM, Engineering → PO)
- Understanding de Agile/Scrum (ideal: CSPO/PSPO certification)
- Experience escribiendo requirements (user stories, specs)
- Collaboration skills (work well con Engineering)
- Testing mindset (catch bugs, validate acceptance criteria)

✅ **Puedes**:
- Escribir user stories claras con acceptance criteria
- Facilitar sprint planning sessions
- Priorizar backlog basado en value
- Test software manually (UAT)
- Communicate con stakeholders (demos, updates)

✅ **Te gusta**:
- Hands-on execution (not pure strategy)
- Working closely con Engineering (daily collaboration)
- Agile ceremonies (sprints, standups, reviews)
- Testing & quality (ensure things work)
- Tactical problem-solving (remove blockers, clarify requirements)

---

## 🆚 Product Owner vs Product Manager

| Aspecto | Product Owner | Product Manager |
|---------|---------------|-----------------|
| **Focus** | Execution (sprint-to-sprint) | Strategy (quarterly, annual) |
| **Horizon** | 1-2 sprints ahead | 6-12 months ahead |
| **Primary Activity** | Backlog management, user stories | Roadmap, vision, market analysis |
| **Stakeholders** | Engineering team, Scrum Master | C-suite, Sales, Marketing, Customers |
| **Ceremonies** | Sprint planning, standups, reviews | OKR reviews, executive demos, roadmap planning |
| **Metrics** | Velocity, sprint commitment | NPS, revenue, feature adoption |
| **Ratio to Engineers** | 1:5-8 | 1:7-10 |
| **Typical in** | Scrum/Agile orgs (separate roles) | Startups, small teams (PM = PO) |

**Nota**: En muchas startups y small teams, **PM y PO son el mismo rol** (Product Manager hace ambas tareas).

---

## 🔗 Links Relacionados

- [Product Manager](product-manager.md) - Estrategia y visión
- [Business Analyst](business-analyst.md) - Análisis de requisitos
- [Scrum Master](../desarrollo/tech-lead.md) - Facilitación Agile
- [Equipo de Producto](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: Lead Product Owner / Product Manager