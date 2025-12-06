# Product Manager

## 📋 Visión General

El Product Manager (PM) es responsable de la **estrategia, visión, y roadmap del producto**, actuando como puente entre negocio, usuarios, y tecnología. Define **qué** construir y **por qué**, mientras que Engineering define **cómo** y Diseño define **la experiencia**. Es el "CEO del producto" (aunque sin autoridad directa sobre equipos).

## 🎯 Responsabilidades

### Product Strategy & Vision

**Principales tareas**:
- Definir product vision (2-3 años)
- Desarrollar product strategy (cómo alcanzar la visión)
- Market analysis y competitive intelligence
- Identificar oportunidades de mercado
- Alineación con business objectives

**Entregables**:
- Product Vision Document (1-pager: misión, visión, valores)
- Product Strategy (3-5 year roadmap, high-level)
- Market Analysis (TAM/SAM/SOM, competitive landscape)
- Business Case (ROI, revenue impact, cost-benefit)

**Frameworks**:
- **North Star Metric**: Métrica única que indica success (ej: DAU, revenue, feature adoption)
- **OKRs** (Objectives & Key Results): Quarterly goals
- **Porter's 5 Forces**: Competitive analysis
- **Blue Ocean Strategy**: Encontrar mercados sin competencia

---

### Product Roadmap

**Principales tareas**:
- Crear y mantener product roadmap (trimestral, anual)
- Priorización de features (value vs effort)
- Secuencing de initiatives (qué primero, qué después)
- Comunicar roadmap a stakeholders
- Ajustar roadmap basado en feedback y data

**Roadmap structure**:
```yaml
Now (Current Quarter):
  - Feature A (in development)
  - Feature B (in design)

Next (Next Quarter):
  - Feature C (discovery)
  - Feature D (planned)

Later (Future):
  - Feature E (ideas, not committed)
  - Feature F (exploring)
```

**Priorización frameworks**:
- **RICE**: Reach × Impact × Confidence / Effort
- **MoSCoW**: Must have, Should have, Could have, Won't have
- **Kano Model**: Basic needs, Performance needs, Delighters
- **Value vs Effort**: 2×2 matrix (quick wins, strategic, fill-ins, time sinks)

---

### Stakeholder Management

**Principales tareas**:
- Comunicar con C-suite (CEO, CTO, CFO)
- Presentar product updates (demos, progress)
- Manage expectations (timeline, scope, trade-offs)
- Influir en decisiones sin autoridad directa
- Conflict resolution entre stakeholders

**Stakeholders típicos**:
- **Executive team**: Budget, strategy, approvals
- **Sales**: Feature requests, customer needs
- **Marketing**: Go-to-market, positioning
- **Customer Success**: User feedback, pain points
- **Engineering**: Feasibility, capacity
- **Design**: User experience, usability

**Communication cadence**:
- **Weekly**: Engineering + Design sync
- **Bi-weekly**: Stakeholder updates (written)
- **Monthly**: Executive demos
- **Quarterly**: OKR reviews, roadmap planning

---

### Discovery & User Research

**Principales tareas**:
- Customer interviews (problem discovery)
- User research collaboration (con UX Researcher)
- Feature validation (prototypes, MVPs)
- Analytics analysis (behavioral data)
- Competitive research

**Discovery process**:
1. **Problem definition**: ¿Qué problema resolver? (jobs-to-be-done)
2. **User research**: Interviews, surveys, analytics
3. **Ideation**: Brainstorming, design sprints
4. **Prototyping**: Low-fi → High-fi
5. **Validation**: Usability testing, beta testing, A/B tests
6. **Decision**: Build, pivot, kill

**Methods**:
- **Jobs-to-be-done**: ¿Qué "job" está contratando nuestro producto para hacer?
- **User Story Mapping**: Visualizar user journey y features
- **Opportunity Solution Tree**: Connect business outcomes → opportunities → solutions

---

### Feature Definition & Requirements

**Principales tareas**:
- Escribir PRDs (Product Requirements Documents)
- Definir user stories (As a [user], I want [feature], so that [benefit])
- Acceptance criteria (GIVEN/WHEN/THEN)
- Edge cases y error handling
- Success metrics (KPIs por feature)

**PRD structure** (Product Requirements Document):
```markdown
# Feature: [Name]

## Problem Statement
- What problem are we solving?
- Who has this problem?
- How do we know? (data, research)

## Goals & Success Metrics
- North Star Metric impact: +X%
- KPI 1: Target
- KPI 2: Target

## User Stories
- As a [user type], I want [feature], so that [benefit]

## Requirements
### Functional Requirements
- Must have (P0)
- Should have (P1)
- Nice to have (P2)

### Non-Functional Requirements
- Performance: <Xms load time
- Security: Authentication, authorization
- Scalability: Support X users

## Out of Scope
- What we're NOT building (explicitly)

## Design Mocks
- Link to Figma

## Technical Considerations
- Dependencies, APIs, integrations

## Launch Plan
- Beta testing, rollout strategy, go-to-market
```

---

### Metrics & Analytics

**Principales tareas**:
- Definir product metrics (KPIs)
- Analizar product performance (dashboards)
- A/B test design & interpretation
- Funnel analysis (conversion optimization)
- Cohort analysis (retention, churn)

**Product metrics framework**:
- **Acquisition**: CAC (Customer Acquisition Cost), signups, traffic
- **Activation**: % users reaching "aha moment"
- **Engagement**: DAU/MAU ratio, session duration, feature adoption
- **Retention**: Week 1, Month 1, Month 3 retention curves
- **Revenue**: MRR/ARR, ARPU, LTV
- **Referral**: NPS, viral coefficient

**Tools**:
- Google Analytics, Mixpanel, Amplitude (behavioral analytics)
- Tableau, Looker (data visualization)
- Optimizely, VWO (A/B testing)

---

### Go-to-Market (GTM)

**Principales tareas**:
- Launch planning (beta, rollout, full launch)
- Pricing strategy (con Business team)
- Positioning & messaging (con Marketing)
- Sales enablement (training, collateral)
- Customer communication (release notes, emails)

**Launch checklist**:
- [ ] Beta testing (internal + external)
- [ ] Rollout plan (% users, phased rollout)
- [ ] Marketing materials (landing page, blog post, social)
- [ ] Sales training (demos, pitch deck)
- [ ] Customer communication (email, in-app notifications)
- [ ] Support training (FAQs, troubleshooting)
- [ ] Metrics tracking (dashboards ready)

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Mid to Senior (3-12+ años de experiencia)

**Progresión típica**:
```
Associate Product Manager (0-2 años)
    - Tareas: Small features, learning, support Senior PM
    ↓
Product Manager (3-5 años)
    - Tareas: Feature ownership, roadmap, stakeholder management
    ↓
Senior Product Manager (5-8 años)
    - Tareas: Product area ownership, strategy, mentoring
    ↓
Lead Product Manager (8-10 años)
    - Manage: 2-3 PMs (dotted line o direct)
    ↓
Director of Product (10-12 años)
    - Manage: 5-10 PMs, multiple products
    ↓
VP of Product / CPO (Chief Product Officer) (12+ años)
    - Manage: Entire product org (20-50+ PMs)
```

---

### Skills Requeridas

#### Product Skills (Critical)

**Must have**:
- ✅ **Product strategy**: Vision, roadmap, OKRs
- ✅ **Priorización**: RICE, value/effort, MoSCoW
- ✅ **User research**: Interviews, usability testing (collaboration con UX)
- ✅ **Analytics**: Metrics, A/B testing, funnel analysis
- ✅ **Requirements**: PRDs, user stories, acceptance criteria
- ✅ **Go-to-market**: Launch planning, pricing, positioning

**Nice to have**:
- 🔶 **UX design basics**: Wireframing, prototyping (not primary)
- 🔶 **Technical knowledge**: SQL, APIs, architecture (depends on product)
- 🔶 **Growth marketing**: SEO, conversion optimization

---

#### Business Skills (High)

**Must have**:
- ✅ **Business acumen**: P&L, revenue models, unit economics
- ✅ **Market analysis**: TAM/SAM/SOM, competitive intelligence
- ✅ **ROI analysis**: Business case, cost-benefit
- ✅ **Stakeholder management**: C-suite, sales, marketing
- ✅ **Strategic thinking**: 1-3 year planning

---

#### Technical Skills (Medium)

**Must have** (varies by product):
- ✅ **SQL basics**: Query analytics databases
- ✅ **APIs understanding**: Integration, webhooks
- ✅ **Architecture basics**: Understand tech constraints
- ✅ **Agile/Scrum**: Sprint planning, backlog management

**Nice to have**:
- 🔶 **Coding basics**: Python, JavaScript (not required, but helpful)
- 🔶 **Data science basics**: Statistical significance, regression

---

#### Soft Skills (Critical)

**Must have**:
- ✅ **Communication**: Presentations, writing (PRDs, emails)
- ✅ **Influence**: Persuade without authority
- ✅ **Leadership**: Inspire teams, drive execution
- ✅ **Empathy**: User needs, team needs
- ✅ **Decision-making**: Trade-offs, prioritization
- ✅ **Conflict resolution**: Mediate stakeholders
- ✅ **Storytelling**: Narrative, vision communication

---

### Stack Tecnológico

El PM usa principalmente **product management tools** y **analytics platforms**:

#### Product Management
```yaml
Roadmapping: ProductPlan, Aha!, Roadmunk, Productboard
Backlog: Jira, Linear, Asana, Monday.com
Documentation: Confluence, Notion, Google Docs
Collaboration: Slack, Microsoft Teams, Zoom
```

#### Analytics & Data
```yaml
Product Analytics: Mixpanel, Amplitude, Heap, Pendo
Web Analytics: Google Analytics, Adobe Analytics
A/B Testing: Optimizely, VWO, LaunchDarkly
Data Viz: Tableau, Looker, Metabase
SQL Tools: Mode, Redash, DataGrip
```

#### Research & Feedback
```yaml
User Research: UserTesting.com, Maze, Lookback
Surveys: Typeform, SurveyMonkey, Qualtrics
Customer Feedback: Productboard, Canny, UserVoice
NPS: Delighted, Wootric
```

#### Design Collaboration
```yaml
Figma (view designs, comment)
Miro (workshops, brainstorming)
```

---

## 📊 Métricas de Éxito

### Product Performance

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **North Star Metric** | +15-30% QoQ | Trimestral |
| **Feature Adoption** | >30% users in 1 month | Por feature |
| **User Retention** | >40% Month 1, >20% Month 3 | Mensual |
| **NPS (Net Promoter Score)** | >30 (good), >50 (excellent) | Trimestral |
| **Revenue Impact** | $X ARR/MRR contribution | Mensual |

### Delivery & Execution

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Roadmap Accuracy** | >70% features shipped on time | Trimestral |
| **Sprint Velocity** | Stable (not decreasing) | Sprint |
| **Feature Success Rate** | >60% features hit KPI targets | Trimestral |
| **Time to Market** | Reduce by 10% YoY | Anual |

### Stakeholder Satisfaction

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Engineering Satisfaction** | >4/5 (clarity, collaboration) | Trimestral |
| **Design Satisfaction** | >4/5 | Trimestral |
| **Sales Satisfaction** | >4/5 (product-market fit) | Trimestral |
| **Executive Satisfaction** | >4/5 (strategy, execution) | Trimestral |

---

## 🔄 Interacciones con Otros Equipos

### Con Engineering Team

**Frecuencia**: Daily to Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Sprint planning (backlog prioritization)
- Daily standups (blockers, progress)
- Feature kickoffs (requirements, context)
- Feasibility discussions (tech constraints)
- Trade-off decisions (scope, timeline, quality)

**Ratio**: 1 PM : 7-10 Engineers (típico)

**Tools**: Jira, Slack, Sprint planning meetings

---

### Con Design Team

**Frecuencia**: Daily to Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Feature definition (requirements → wireframes)
- Design reviews (feedback, iteration)
- User research planning (what to research)
- Prototype validation (usability testing)
- Design QA (pre-launch)

**Tools**: Figma (commenting), Miro (workshops), Slack

---

### Con Data Team (Analysts, Data Scientists)

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Metrics definition (KPIs por feature)
- Dashboard creation (product analytics)
- A/B test design & analysis
- Funnel analysis (conversion optimization)
- Cohort analysis (retention, churn)

**Tools**: SQL, Mixpanel, Tableau, Slack

---

### Con Marketing Team

**Frecuencia**: Weekly to Bi-weekly  
**Modo**: **Collaboration**

**Actividades**:
- Go-to-market planning (launches)
- Positioning & messaging (product value props)
- Content creation (blog posts, case studies)
- Demand generation (feature marketing)
- Customer education (webinars, tutorials)

**Tools**: Confluence, Slack, GTM documents

---

### Con Sales Team

**Frecuencia**: Weekly to Bi-weekly  
**Modo**: **Collaboration** + **X-as-a-Service** (enablement)

**Actividades**:
- Feature requests (customer needs)
- Sales enablement (training, demos)
- Competitive intelligence (what customers compare us to)
- Pricing discussions (packaging, tiers)
- Deal support (custom feature requests)

**Tools**: Salesforce, Slack, Demo calls

---

### Con Customer Success

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Customer feedback (pain points, feature requests)
- Churn analysis (why customers leave)
- Feature adoption (help customers use new features)
- Beta testing (recruit power users)
- Customer interviews (research)

**Tools**: Zendesk, Intercom, Slack

---

### Con C-Suite (CEO, CTO, CFO)

**Frecuencia**: Monthly to Quarterly  
**Modo**: **Reporting** + **Strategy**

**Actividades**:
- Product strategy reviews
- Roadmap alignment (priorities)
- Budget discussions (headcount, tools)
- Business metrics (revenue, retention, NPS)
- Strategic initiatives (new markets, pivots)

**Tools**: Executive presentations, OKR reviews, QBRs

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: IC Product Track (menos común, más common en Big Tech)

```
Product Manager (3-5 años)
    ↓
Senior Product Manager (5-8 años)
    ↓
Staff Product Manager (8-12 años)
    - Scope: Multiple products, strategic
    ↓
Principal Product Manager (12+ años)
    - Scope: Product vision, company-wide impact
```

#### Opción 2: Management Track (más común)

```
Product Manager (3-5 años)
    ↓
Senior Product Manager (5-8 años)
    ↓
Lead Product Manager (8-10 años)
    - Manage: 2-3 PMs
    ↓
Director of Product (10-12 años)
    - Manage: 5-10 PMs, product area
    ↓
VP of Product (12-15 años)
    - Manage: Product org (15-30 PMs)
    ↓
Chief Product Officer (CPO) (15+ años)
    - C-suite, entire product strategy
```

#### Opción 3: Founder / CEO

```
Senior Product Manager (5-8 años)
    ↓
Startup Founder / CEO
    - Leveraging product + business skills
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Ship 2-3 features end-to-end (discovery → launch)
- [ ] Aprender SQL (básico para analytics)
- [ ] Dominar product analytics (Mixpanel/Amplitude)
- [ ] Desarrollar stakeholder management skills
- [ ] Crear portfolio de PRDs y roadmaps

**Próximos 1-2 años**:
- [ ] Own product area (no solo features)
- [ ] Launch major product initiative (strategic impact)
- [ ] Desarrollar business acumen (P&L understanding)
- [ ] Public speaking (product demos, conferences)
- [ ] Mentoring de APM (Associate PM)

**Próximos 3-5 años** (hacia Senior/Director):
- [ ] Product strategy (multi-year vision)
- [ ] P&L ownership (revenue responsibility)
- [ ] Cross-functional leadership (influence org)
- [ ] Thought leadership (blog, conferences, Twitter)
- [ ] Team management (if management track)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"Inspired"** - Marty Cagan (product management bible)
- 📚 **"The Lean Startup"** - Eric Ries (build-measure-learn)
- 📚 **"Hooked"** - Nir Eyal (behavior design)
- 📚 **"Crossing the Chasm"** - Geoffrey Moore (product-market fit)
- 📚 **"The Mom Test"** - Rob Fitzpatrick (customer interviews)
- 📚 **"Continuous Discovery Habits"** - Teresa Torres (discovery)
- 📚 **"Escaping the Build Trap"** - Melissa Perri (outcome-focused PM)

#### Cursos & Certificaciones

- **Reforge**: Product Strategy, Growth, Retention (top-tier, $2k+)
- **Product School**: Product Management certifications
- **Pragmatic Institute**: Certified Product Manager
- **Coursera**: "Digital Product Management" specialization

#### Comunidades

- **Product School**: Events, webinars
- **Mind the Product**: Conferences, community
- **Product Hunt**: Product discovery, trends
- **Lenny's Newsletter**: Product management insights (Lenny Rachitsky)
- **Product Management Slack communities**: PM Hangout, Women in Product

---

## 📝 Herramientas del Día a Día

### Product Management

| Tool | Uso | Nivel |
|------|-----|-------|
| **Jira / Linear** | Backlog, sprint planning, task tracking | Advanced |
| **Confluence / Notion** | PRDs, documentation, knowledge base | Advanced |
| **ProductPlan / Aha!** | Roadmapping, strategic planning | Intermediate |
| **Miro** | Workshops, brainstorming, user story mapping | Intermediate |

### Analytics & Data

| Tool | Uso |
|------|-----|
| **Mixpanel / Amplitude** | Product analytics, funnels, cohorts |
| **Google Analytics** | Web analytics, traffic, conversion |
| **Tableau / Looker** | Data visualization, dashboards |
| **SQL** (Mode, DataGrip) | Ad-hoc queries, data exploration |

### Research & Feedback

| Tool | Uso |
|------|-----|
| **UserTesting.com** | Usability testing, user interviews |
| **Typeform** | Surveys, feedback collection |
| **Productboard / Canny** | Feature requests, customer feedback |
| **Delighted** | NPS surveys |

### Collaboration

| Tool | Uso |
|------|-----|
| **Slack** | Team communication |
| **Zoom / Google Meet** | Meetings, demos |
| **Figma** | Design collaboration (commenting) |
| **Loom** | Video updates, async communication |

---

## 🚀 Ejemplo de Semana Típica

### Lunes
- **9:00-10:00**: Sprint planning con Engineering (prioritize backlog)
- **10:00-11:00**: Review analytics (weekend metrics, dashboards)
- **11:00-12:00**: 1:1 con Design Lead (feature kickoff)
- **14:00-15:00**: Customer interview (discovery research)
- **15:00-17:00**: Deep work: Write PRD para nueva feature

### Martes
- **9:00-9:30**: Daily standup con Engineering
- **9:30-11:00**: Stakeholder meeting (Sales feedback, feature requests)
- **11:00-12:00**: A/B test review con Data Analyst
- **14:00-16:00**: Roadmap planning (Q2 priorities)
- **16:00-17:00**: 1:1 con Engineering Manager (capacity planning)

### Miércoles
- **9:00-10:00**: Product demo a Executive team (monthly update)
- **10:00-12:00**: Deep work: Competitive analysis (research competitors)
- **14:00-15:00**: Design review (mockups feedback)
- **15:00-17:00**: User research synthesis con UX Researcher (affinity diagram)

### Jueves
- **9:00-9:30**: Daily standup
- **9:30-11:00**: Go-to-market planning con Marketing (launch next feature)
- **11:00-12:00**: Customer Success sync (churn analysis, feedback)
- **14:00-15:30**: OKR review (quarterly progress check)
- **15:30-17:00**: Deep work: Write executive summary (strategy doc)

### Viernes
- **9:00-10:00**: Product team sync (all PMs, share learnings)
- **10:00-11:00**: Backlog grooming con Engineering (refine stories)
- **11:00-12:00**: 1:1 con VP Product (career development)
- **14:00-16:00**: Deep work: Roadmap updates, planning next quarter
- **16:00-17:00**: Week wrap-up, Slack catch-up, admin

**Strategic work** (vision, roadmap, strategy): ~30%  
**Execution** (sprint planning, PRDs, backlog): ~25%  
**Stakeholder management** (meetings, alignment): ~25%  
**Research & Analytics** (user research, data analysis): ~15%  
**Admin & Learning**: ~5%

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- 3-5+ años de experiencia (puede ser Engineering, Design, Consulting, Analytics → transición a PM)
- Track record shipping products o features
- Strong analytical skills (data-driven decisions)
- Business acumen (understand revenue, costs, ROI)
- Technical fluency (can talk to engineers)

✅ **Puedes**:
- Write clear PRDs con user stories y acceptance criteria
- Priorizar features usando frameworks (RICE, value/effort)
- Analyze product metrics (funnels, cohorts, A/B tests)
- Influence stakeholders sin autoridad directa
- Facilitar trade-off discussions (scope, timeline, quality)

✅ **Te gusta**:
- Strategic thinking (vision, roadmap, long-term)
- Problem-solving (user needs + business goals)
- Cross-functional collaboration (Eng, Design, Sales, Marketing)
- Data & analytics (evidence-based decisions)
- Ownership (drive product success end-to-end)

---

## 🔗 Links Relacionados

- [Product Owner](product-owner.md) - Ejecución táctica, backlog
- [Business Analyst](business-analyst.md) - Análisis de requisitos
- [Data Analyst](data-analyst.md) - Métricas y análisis
- [Equipo de Producto](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: VP of Product / CPO