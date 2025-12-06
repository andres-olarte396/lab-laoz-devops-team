# Workflows Inter-Equipos

Este directorio documenta los flujos de trabajo que cruzan múltiples equipos y requieren coordinación entre diferentes áreas de la organización.

## 📋 Tabla de Contenidos

- [Feature Development Workflow](#feature-development-workflow)
- [Sprint Planning Cross-Team](#sprint-planning-cross-team)
- [Incident Response & Postmortem](#incident-response--postmortem)
- [Release Management](#release-management)
- [Onboarding de Nuevos Empleados](#onboarding-de-nuevos-empleados)

---

## 🚀 Feature Development Workflow

**Equipos involucrados**: Producto, Diseño, Desarrollo, DevOps, QA

### Fase 1: Discovery (Semanas N-2 a N-1)

| Paso | Responsable | Entregable | Duración |
|------|-------------|------------|----------|
| 1. Identificación de problema u oportunidad | Product Manager | Problem Statement | 1-2 días |
| 2. User Research (si es necesario) | UX Researcher + PM | Research Insights | 3-5 días |
| 3. Validación de viabilidad técnica | Tech Lead + Solution Architect | Technical Feasibility Doc | 1-2 días |
| 4. Estimación de complejidad | Tech Lead + Engineering Manager | T-Shirt Sizing (S/M/L/XL) | 1 día |
| 5. Priorización | Product Manager | Decision: Go/No-Go | 1 día |

**Entregable de fase**: Validated Idea lista para diseño e implementación

---

### Fase 2: Design (Semana N-1)

| Paso | Responsable | Entregable | Duración |
|------|-------------|------------|----------|
| 1. User Flows | UX Designer | User Flow Diagrams | 2-3 días |
| 2. Wireframes | UX Designer | Low-fidelity Wireframes | 2-3 días |
| 3. Design Review con Producto y Dev | UX Designer + PM + Tech Lead | Feedback incorporado | 1 día |
| 4. UI Design | UI Designer | High-fidelity Mockups | 3-4 días |
| 5. Design QA y Handoff | UI Designer + Frontend Dev | Figma Dev Mode specs | 1 día |

**Entregable de fase**: Diseños finales aprobados y especificaciones técnicas

**Modo de interacción**: Collaboration entre Diseño, Producto, y Desarrollo

---

### Fase 3: Development (Semana N)

| Paso | Responsable | Entregable | Duración |
|------|-------------|------------|----------|
| 1. Sprint Planning | Product Owner + Dev Team | Sprint Backlog con tasks | 2h |
| 2. Architecture Spike (features complejas) | Tech Lead + Solution Architect | ADR si necesario | 1-2 días |
| 3. Backend Implementation | Backend Developer | API endpoints + tests | Variable |
| 4. Frontend Implementation | Frontend Developer | UI components + tests | Variable |
| 5. Integration | Full-Stack Developer | Integración E2E | 1-2 días |
| 6. Code Review | Tech Lead + Peers | Approved PR | Continuo |
| 7. QA Testing | QA Engineer | Test results | 2-3 días |

**Entregable de fase**: Feature implementada, testeada, lista para deploy

**Modo de interacción**: 
- Desarrollo internamente (Collaboration)
- Desarrollo + Diseño (Collaboration para ajustes)
- Desarrollo + DevOps (X-as-a-Service para CI/CD)

---

### Fase 4: Deployment (Semana N)

| Paso | Responsable | Entregable | Duración |
|------|-------------|------------|----------|
| 1. Merge a main/develop | Tech Lead | Code en rama principal | 1h |
| 2. CI/CD Pipeline | Platform Engineer (DevOps) | Build & Tests pasados | Auto (15-30min) |
| 3. Deploy a Staging | CI/CD automatizado | Staging environment | Auto (10-20min) |
| 4. Smoke Tests en Staging | QA Engineer | Validation checklist | 1-2h |
| 5. UAT (User Acceptance Testing) | Product Owner + QA | UAT approval | 1-2 días |
| 6. Deploy a Production | DevOps + Tech Lead | Production deployment | 30min-2h |
| 7. Monitoring & Validation | SRE + Tech Lead | Health checks + metrics | 24-48h |

**Entregable de fase**: Feature en producción, monitoreada, estable

**Modo de interacción**: 
- DevOps (X-as-a-Service para infraestructura)
- DevOps + Desarrollo (Collaboration si hay issues)

---

### Fase 5: Post-Launch (Semana N+1)

| Paso | Responsable | Entregable | Duración |
|------|-------------|------------|----------|
| 1. Monitoring de métricas de negocio | Data Analyst + PM | Metrics dashboard | Continuo |
| 2. User Feedback collection | Product Manager | User feedback report | 1-2 semanas |
| 3. Bug fixing (si necesario) | Development Team | Hotfixes | Variable |
| 4. Retrospective | Scrum Master + Team | Retrospective action items | 1h |
| 5. Documentation update | Tech Lead | Updated docs | 1-2 días |

**Entregable de fase**: Feature estabilizada, documentada, con learnings capturados

---

## 📊 Diagrama de Flujo Completo

```
[Problem/Opportunity] 
    ↓
[Discovery: Research + Feasibility] (PM + Research + Tech Lead)
    ↓
[Design: Flows + Wireframes + UI] (UX/UI Designer)
    ↓
[Development: Backend + Frontend + Integration] (Dev Team)
    ↓
[Testing: QA + UAT] (QA + PO)
    ↓
[Deployment: Staging → Production] (DevOps + Tech Lead)
    ↓
[Monitoring: Metrics + Feedback] (Data Analyst + PM + SRE)
    ↓
[Retrospective + Documentation] (Team)
```

---

## 🎯 Sprint Planning Cross-Team

**Frecuencia**: Cada 2 semanas (inicio de sprint)  
**Duración**: 2-4 horas  
**Participantes**: Product Owner, Tech Lead, Development Team, Design Lead, DevOps Lead

### Agenda

| Tiempo | Actividad | Responsable | Objetivo |
|--------|-----------|-------------|----------|
| 0-30min | Sprint Review anterior | Product Owner | Cerrar sprint anterior |
| 30-60min | Priorities para próximo sprint | Product Owner | Alineación de prioridades |
| 60-120min | Capacity Planning | Tech Lead + Engineering Manager | Disponibilidad del equipo |
| 120-180min | Task Breakdown | Development Team | Stories → Tasks |
| 180-210min | Dependencies & Blockers | Tech Lead + DevOps Lead | Identificar riesgos |
| 210-240min | Sprint Goal & Commitment | Product Owner + Team | Compromiso final |

### Entregables

- **Sprint Goal**: Objetivo claro del sprint en 1-2 frases
- **Sprint Backlog**: User Stories con tasks y estimaciones
- **Dependency Map**: Dependencias con otros equipos identificadas
- **Capacity Plan**: Disponibilidad de cada team member

### Modos de Interacción

- **Desarrollo + Producto**: Collaboration (tight partnership)
- **Desarrollo + Diseño**: Collaboration (para features con UX)
- **Desarrollo + DevOps**: X-as-a-Service (infraestructura) + Facilitating (nuevas capacidades)
- **Desarrollo + Arquitectura**: Facilitating (para features complejas)

---

## 🚨 Incident Response & Postmortem

**Equipos involucrados**: DevOps (SRE), Desarrollo (Tech Lead + Developers), Producto (PM), Comunicación

### Proceso de Incident Response

#### 1. Detección (T+0min)

| Acción | Responsable | Tool | SLA |
|--------|-------------|------|-----|
| Alert triggered | Monitoring system | Azure Monitor / Grafana | Auto |
| On-call notification | SRE / Platform Engineer | PagerDuty / Opsgenie | <5min |
| Incident acknowledged | On-call SRE | PagerDuty | <10min |

#### 2. Triage (T+10min)

| Acción | Responsable | Entregable | SLA |
|--------|-------------|------------|-----|
| Severity assessment | On-call SRE | Severity: P0/P1/P2/P3 | <15min |
| Impact analysis | On-call SRE | Users affected, services down | <15min |
| Escalation (si P0/P1) | On-call SRE | Tech Lead + Engineering Manager notified | <20min |
| War room creation | On-call SRE | Slack channel #incident-YYYYMMDD-NNNN | <20min |

**Severity Levels**:
- **P0 (Critical)**: Sistema completamente caído, pérdida de datos, todos los usuarios afectados
- **P1 (High)**: Funcionalidad core afectada, >20% usuarios afectados
- **P2 (Medium)**: Funcionalidad no-core afectada, <20% usuarios afectados
- **P3 (Low)**: Bug menor, workaround disponible, <5% usuarios afectados

#### 3. Mitigation (T+20min - variable)

| Acción | Responsable | Entregable | SLA |
|--------|-------------|------------|-----|
| Root cause investigation | On-call SRE + Tech Lead | Hypothesis | <30min |
| Implement fix or rollback | Developer + SRE | Hotfix or rollback | <1h (P0), <4h (P1) |
| Deploy fix to production | DevOps + Tech Lead | Deployment | <2h (P0), <8h (P1) |
| Verify resolution | QA + SRE | Health checks pass | <30min post-deploy |

#### 4. Communication (Continuo)

| Stakeholder | Frecuencia | Canal | Responsable |
|-------------|-----------|-------|-------------|
| Engineering Team | Cada 15-30min | Slack #incident channel | On-call SRE |
| Product Manager | Cada 30-60min | Slack DM + incident channel | Tech Lead |
| Customer Support | Cada 30-60min | Slack #customer-support | Product Manager |
| Executives (P0/P1) | Cada 1-2h | Email + Slack | Engineering Manager |
| Customers (si afecta visiblemente) | Cada 1-2h | Status page | Product Manager |

#### 5. Resolution & Closing (T+variable)

| Acción | Responsable | Entregable | SLA |
|--------|-------------|------------|-----|
| Confirm fix stable | SRE | 24-48h monitoring | Variable |
| Close incident | On-call SRE | Incident closed in tool | Post-stabilization |
| Schedule postmortem | Engineering Manager | Calendar invite | Within 48h |

---

### Postmortem Process

**Timing**: Dentro de 48 horas del incidente  
**Duración**: 1-2 horas  
**Participantes**: On-call SRE, Tech Lead, Developers involucrados, Product Manager, Engineering Manager

#### Agenda del Postmortem

| Sección | Tiempo | Responsable | Objetivo |
|---------|--------|-------------|----------|
| 1. Timeline de eventos | 15min | On-call SRE | Reconstruir qué pasó y cuándo |
| 2. Root Cause Analysis | 30min | Tech Lead + SRE | Identificar causa raíz (5 Whys) |
| 3. What Went Well | 10min | Team | Reconocer buenas prácticas |
| 4. What Went Wrong | 20min | Team | Identificar fallos (sin culpar) |
| 5. Action Items | 20min | Engineering Manager | Crear tasks para prevenir recurrencia |
| 6. Priorización de action items | 15min | Engineering Manager + PM | Decidir qué se hace cuándo |

#### Postmortem Document Template

```markdown
# Postmortem: [Incident Title]

**Incident ID**: INC-2025-01-15-001  
**Date**: 2025-01-15  
**Severity**: P1  
**Duration**: 2h 35min (10:23 AM - 12:58 PM UTC)  
**Impact**: 35% of users unable to access checkout, ~$12K revenue loss

## Summary (1-2 paragraphs)

Brief description of what happened, impact, and resolution.

## Timeline

| Time (UTC) | Event | Actor |
|------------|-------|-------|
| 10:23 | Alert: API response time >5s | Monitoring |
| 10:28 | On-call SRE acknowledged | @jane |
| 10:35 | Identified: Database connection pool exhausted | @jane |
| ... | ... | ... |

## Root Cause

The database connection pool was set to 50 connections (default), but after the recent feature release, concurrent user load increased from avg 200 to 450. The connection pool became exhausted, causing timeouts.

## 5 Whys Analysis

1. Why did the checkout fail? → API timeouts
2. Why API timeouts? → Database connection pool exhausted
3. Why pool exhausted? → More concurrent users than pool size
4. Why more concurrent users? → New feature increased engagement
5. Why wasn't this anticipated? → Load testing didn't simulate realistic concurrency

## What Went Well ✅

- Alert triggered within 5 minutes
- On-call responded quickly
- Rollback executed smoothly
- Communication to stakeholders was clear

## What Went Wrong ❌

- No load testing before release
- Connection pool size not reviewed
- No monitoring on connection pool utilization
- Rollback plan wasn't documented

## Action Items

| Action | Owner | Priority | Due Date | Status |
|--------|-------|----------|----------|--------|
| Increase DB connection pool to 200 | @john | P0 | 2025-01-16 | ✅ Done |
| Add connection pool metrics to Grafana | @jane | P1 | 2025-01-20 | In Progress |
| Implement load testing in CI/CD | @mike | P1 | 2025-01-30 | Not Started |
| Document rollback procedures | @sarah | P2 | 2025-02-15 | Not Started |
| Review capacity planning for all services | @team | P2 | 2025-02-28 | Not Started |

## Lessons Learned

- Always load test before major releases
- Monitor resource utilization proactively
- Document rollback procedures in advance
```

**Modo de interacción**: Collaboration entre DevOps, Desarrollo, y Producto

---

## 📦 Release Management

**Equipos involucrados**: Desarrollo, DevOps, Producto, QA

### Release Cadence Options

| Tipo de Release | Frecuencia | Cuándo Usar | Riesgo |
|----------------|-----------|-------------|--------|
| **Continuous Deployment** | Cada commit a main | Startups, equipos maduros con fuerte testing | Bajo (con CI/CD robusto) |
| **Daily Releases** | 1x por día | Scale-ups con buen CI/CD | Bajo-Medio |
| **Sprint-based** | Cada 2 semanas | Medium companies, equipos en crecimiento | Medio |
| **Monthly** | 1x por mes | Enterprise, sistemas legacy | Alto (batch size grande) |
| **Quarterly** | 4x por año | Sistemas críticos con extensa validación | Muy Alto |

**Recomendación**: Tender hacia releases más frecuentes = menor riesgo por release

---

### Release Process (Sprint-based)

#### Semana N: Development

- Lunes: Sprint Planning
- Martes-Jueves: Development + Code Reviews
- Viernes: Feature Freeze (no new features, solo bug fixes)

#### Semana N+1: Testing & Release

| Día | Actividad | Responsable | Entregable |
|-----|-----------|-------------|------------|
| Lunes | QA Testing en Staging | QA Engineer | Test results |
| Martes | UAT (User Acceptance Testing) | Product Owner + QA | UAT sign-off |
| Miércoles | Release Notes preparation | Product Manager | Release notes draft |
| Miércoles | Pre-release checklist | Tech Lead + DevOps | Checklist completed |
| Jueves | Deploy to Production (AM) | DevOps + Tech Lead | Production deployment |
| Jueves | Smoke tests post-deploy | QA + SRE | Validation complete |
| Jueves-Viernes | Monitoring & hotfixes | SRE + Dev Team | Stable release |

---

### Pre-Release Checklist

**Technical**:
- [ ] All tests passing (unit, integration, E2E)
- [ ] Code coverage >80%
- [ ] No critical or high security vulnerabilities
- [ ] Performance benchmarks met
- [ ] Database migrations tested
- [ ] Rollback plan documented
- [ ] Feature flags configured (if applicable)
- [ ] Monitoring dashboards updated

**Product**:
- [ ] UAT completed and signed off
- [ ] Release notes written
- [ ] Customer support briefed
- [ ] Marketing materials ready (if needed)
- [ ] Beta users tested (if applicable)

**DevOps**:
- [ ] Infrastructure capacity reviewed
- [ ] Backup completed
- [ ] On-call schedule confirmed
- [ ] Incident response plan ready
- [ ] Deployment runbook updated

---

### Release Communication Plan

| Stakeholder | Timing | Channel | Content |
|-------------|--------|---------|---------|
| Engineering Team | 24h before | Slack #engineering | Technical details, timeline |
| Product Team | 48h before | Slack #product | Feature list, UAT status |
| Customer Support | 48h before | Slack #support + email | What's new, known issues, FAQs |
| Executives | 1 week before | Email | High-level summary, business impact |
| Customers | Day of release | Email + in-app | What's new, benefits, docs |

---

### Post-Release Activities

**Day 1 (Release Day)**:
- [ ] Monitor error rates, response times, user activity
- [ ] Be available for hotfixes
- [ ] Collect initial feedback

**Week 1**:
- [ ] Monitor business metrics (engagement, conversion, etc.)
- [ ] Collect user feedback
- [ ] Fix critical bugs
- [ ] Update documentation based on learnings

**Week 2**:
- [ ] Sprint Retrospective (include release process review)
- [ ] Update release runbook with learnings
- [ ] Plan improvements for next release

---

## 👤 Onboarding de Nuevos Empleados

**Duración**: 1-2 semanas para setup inicial, 1-3 meses para full productivity  
**Equipos involucrados**: HR, Engineering Manager, Tech Lead, DevOps, Producto, Diseño

### Day 1: Welcome & Setup

| Tiempo | Actividad | Responsable | Entregable |
|--------|-----------|-------------|------------|
| 9:00-10:00 | Welcome & HR paperwork | HR | Contracts signed |
| 10:00-11:00 | Team introductions | Engineering Manager | Meet the team |
| 11:00-12:00 | Equipment setup | IT / DevOps | Laptop, accounts |
| 12:00-13:00 | Lunch with team | Assigned buddy | Social connection |
| 13:00-14:00 | Code repository access | DevOps | GitHub access granted |
| 14:00-15:00 | Development environment setup | Tech Lead | Local dev env running |
| 15:00-16:00 | Company culture & values | Engineering Manager | Culture deck reviewed |
| 16:00-17:00 | Q&A and first day recap | Assigned buddy | Questions answered |

---

### Week 1: Foundations

#### Technical Setup (Dev Team)

- [ ] **Day 1**: Laptop, IDE, Git, access to repositories
- [ ] **Day 2**: Clone main repo, run app locally
- [ ] **Day 2**: Access to staging environment
- [ ] **Day 3**: First commit (e.g., update README with your name)
- [ ] **Day 4**: Code review of first small PR
- [ ] **Day 5**: Fix first "good first issue" bug

**Responsable**: Tech Lead + Assigned Buddy (Senior Developer)

#### Documentation Reading

- [ ] **Day 1**: This documentation repo (Team structure, roles)
- [ ] **Day 1**: [equipos/README.md](../equipos/README.md) - Team Topologies model
- [ ] **Day 2**: Your team's README (Development, DevOps, Product, Design, or Architecture)
- [ ] **Day 2**: Your specific role document
- [ ] **Day 3**: [stacks/README.md](../stacks/README.md) - Technology stacks
- [ ] **Day 4**: [workflows/README.md](README.md) - This document
- [ ] **Day 5**: [ceremonias/README.md](../ceremonias/README.md) - Agile ceremonies

**Responsable**: New hire (self-paced) + Buddy (Q&A)

#### Meetings & People

- [ ] **Day 1**: 1:1 with Engineering Manager (30min)
- [ ] **Day 2**: 1:1 with Tech Lead (30min)
- [ ] **Day 2**: Meet Product Manager for your squad (30min)
- [ ] **Day 3**: Meet QA Engineer (if applicable) (30min)
- [ ] **Day 3**: Meet Designer working with your squad (30min)
- [ ] **Day 4**: Shadow a Daily Standup
- [ ] **Day 5**: Shadow a Sprint Planning or Backlog Refinement

**Responsable**: Engineering Manager (scheduling)

---

### Week 2: First Contributions

#### Goals

- [ ] Complete your first meaningful user story (small feature or bug fix)
- [ ] Participate actively in Daily Standup
- [ ] Do at least 2 code reviews for teammates
- [ ] Pair program with a senior developer for 2-4 hours
- [ ] Deploy a change to staging environment

#### Milestones

- **Day 6-7**: Pick a story from backlog (with Tech Lead guidance)
- **Day 8-9**: Implement and test
- **Day 10**: Code review and iterate
- **Day 11**: Deploy to staging, validate, create PR
- **Day 12**: PR approved, merged, deployed to production

#### Check-in

- [ ] **End of Week 2**: 1:1 with Engineering Manager (How's it going? Any blockers?)

**Responsable**: Tech Lead + Buddy

---

### Month 1: Ramp Up

#### Goals

- [ ] Own 2-3 user stories per sprint
- [ ] Understand the product domain deeply
- [ ] Start contributing to design discussions
- [ ] Shadow an incident response (if one occurs)
- [ ] Give feedback in Sprint Retrospective

#### Activities

- **Week 3-4**: 
  - Take on stories with medium complexity
  - Participate in Design Reviews
  - Learn the deployment process hands-on
  - Read architecture documentation (ADRs if available)

#### Check-in

- [ ] **End of Month 1**: 1:1 with Engineering Manager (30-day review)
- [ ] Feedback: What's going well? What's challenging?
- [ ] Set goals for Month 2-3

**Responsable**: Engineering Manager

---

### Month 2-3: Full Productivity

#### Goals

- [ ] Operate at full productivity (same velocity as team average)
- [ ] Own entire features end-to-end
- [ ] Mentor newer team members (if applicable)
- [ ] Contribute to technical discussions and decisions
- [ ] Identify and propose improvements to processes or codebase

#### Activities

- **Month 2**:
  - Lead a user story from planning through deployment
  - Participate in Architecture Review (for complex features)
  - Start learning adjacent areas (e.g., Frontend dev learns Backend basics)

- **Month 3**:
  - Fully autonomous on typical stories
  - Proactively identify tech debt and improvements
  - Contribute to knowledge sharing (tech talks, documentation)

#### Check-in

- [ ] **End of Month 3**: 1:1 with Engineering Manager (90-day review)
- [ ] Formal performance review
- [ ] Career development discussion
- [ ] Confirmation of successful onboarding

**Responsable**: Engineering Manager

---

### Role-Specific Onboarding Paths

#### For Developers

- **Week 1**: Environment setup, first commit, good first issue
- **Week 2**: First feature deployed to production
- **Month 1**: Full sprint contribution, understand domain
- **Month 2-3**: Own features end-to-end, mentor others

#### For Product Managers

- **Week 1**: Meet all stakeholders, understand product vision, read user research
- **Week 2**: Shadow user interviews, review product metrics, understand roadmap
- **Month 1**: Own backlog refinement, write first user stories, lead discovery sessions
- **Month 2-3**: Own a product area, drive sprint planning, define OKRs

#### For Designers

- **Week 1**: Understand design system, meet dev team, access Figma
- **Week 2**: Shadow user research, review existing designs, first design contribution
- **Month 1**: Own design for a feature, participate in Design Critique, handoff to dev
- **Month 2-3**: Lead design for new features, contribute to design system

#### For DevOps / Platform Engineers

- **Week 1**: Access to cloud accounts, understand infrastructure, read runbooks
- **Week 2**: Shadow on-call rotation, participate in incident postmortem
- **Month 1**: Own small infrastructure changes, improve monitoring/alerting
- **Month 2-3**: On-call rotation, own platform improvements, enable dev teams

---

### Onboarding Checklist (Manager's Copy)

**Pre-Day 1 (1 week before)**:
- [ ] Laptop ordered and configured
- [ ] Accounts created (email, Slack, GitHub, Jira, cloud)
- [ ] Add to relevant Slack channels
- [ ] Assign an onboarding buddy (senior team member)
- [ ] Schedule Day 1 agenda
- [ ] Prepare welcome kit (swag, handbook, etc.)

**Day 1**:
- [ ] Welcome meeting
- [ ] Equipment handover
- [ ] Team introductions
- [ ] 1:1 with manager (30min)
- [ ] Buddy assigned and introduced

**Week 1**:
- [ ] Development environment set up
- [ ] First commit merged
- [ ] Documentation reading completed
- [ ] Meet key stakeholders (PM, Design, DevOps lead)
- [ ] Attend first ceremonies (Standup, Planning)

**Week 2**:
- [ ] First user story completed and deployed
- [ ] Participated in code reviews
- [ ] 1:1 check-in with manager

**Month 1**:
- [ ] Contributing to sprints regularly
- [ ] Comfortable with dev workflow
- [ ] Knows the product domain
- [ ] 30-day review with manager

**Month 3**:
- [ ] Fully productive
- [ ] 90-day review with manager
- [ ] Performance feedback
- [ ] Career development plan

---

## 📊 Workflow Metrics

### Feature Development Metrics

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Cycle Time** (Idea → Production) | <2 sprints (4 weeks) | Jira/Linear time tracking |
| **Lead Time for Changes** (Code → Production) | <1 día | DORA metric, CI/CD logs |
| **Deployment Frequency** | >1x por día (ideal) | CI/CD deployment logs |
| **Change Failure Rate** | <15% | Incidents caused by deployments |
| **Design to Dev Handoff Time** | <2 días | Figma handoff → dev start |
| **Code Review Turnaround** | <4 horas | GitHub PR metrics |
| **QA Cycle Time** | <2 días | Jira time in "QA" status |

### Incident Response Metrics

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **MTTD** (Mean Time to Detect) | <5min | Alert timestamp - incident start |
| **MTTA** (Mean Time to Acknowledge) | <10min | Acknowledge time - alert time |
| **MTTR** (Mean Time to Resolve) | <1h (P0), <4h (P1) | Resolution time - incident start |
| **Incident Frequency** | Trending down | Count per week/month |
| **Postmortem Completion Rate** | 100% (P0/P1) | Postmortems done / incidents |
| **Action Item Completion Rate** | >80% | Completed action items / total |

### Release Metrics

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Release Success Rate** | >95% | Successful releases / total releases |
| **Rollback Rate** | <5% | Rollbacks / total releases |
| **Hotfix Rate** | <10% | Hotfixes / total releases |
| **Release Frequency** | 2x per month (baseline) | Deployments to production |
| **Release Preparation Time** | <1 día | Time spent on release checklist |

### Onboarding Metrics

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Time to First Commit** | <3 días | Day 1 → first merged PR |
| **Time to First Feature** | <2 semanas | Day 1 → first story deployed |
| **Time to Full Productivity** | <3 meses | Manager assessment |
| **90-Day Retention** | >95% | Employees staying >90 days |
| **Onboarding Satisfaction** | >4/5 | Survey after Month 1 |

---

## 🔗 Links Relacionados

- [Equipos](../equipos/README.md) - Estructura organizacional
- [Ceremonias](../ceremonias/README.md) - Ceremonias ágiles
- [Comunicación](../comunicacion/README.md) - Estrategia de comunicación
- [DORA Metrics](https://dora.dev/) - DevOps Research & Assessment

---

**Última actualización**: Enero 2025  
**Mantenido por**: Engineering Manager + Tech Leads