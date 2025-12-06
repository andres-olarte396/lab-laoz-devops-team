# Business Analyst

## 📋 Visión General

El Business Analyst (BA) es responsable de **analizar procesos de negocio, identificar necesidades, y traducirlas en requisitos técnicos** que Engineering puede implementar. Actúa como puente entre stakeholders de negocio y equipos técnicos, asegurando que las soluciones tecnológicas resuelvan problemas de negocio reales.

**Cuándo existe este rol**: Empresas grandes, entornos enterprise, industrias reguladas (finanzas, salud, gobierno) donde los requisitos son complejos y críticos.

## 🎯 Responsabilidades

### Requirements Gathering & Analysis

**Principales tareas**:
- Conduct stakeholder interviews (entender necesidades)
- Facilitar workshops (JAD - Joint Application Design)
- Analizar procesos actuales (as-is analysis)
- Documentar procesos futuros (to-be analysis)
- Gap analysis (brecha entre actual y deseado)

**Entregables**:
- Business Requirements Document (BRD)
- Functional Requirements Document (FRD)
- Use Cases
- User Stories (para Agile teams)
- Process Flow Diagrams (BPMN)

**Técnicas de elicitation**:
- **Interviews**: One-on-one con stakeholders
- **Workshops**: Grupo de stakeholders (brainstorming)
- **Observation**: Shadowing usuarios en su trabajo
- **Document analysis**: Revisar documentos existentes
- **Surveys**: Cuestionarios a múltiples stakeholders
- **Prototyping**: Mock-ups para validar requirements

---

### Business Process Modeling

**Principales tareas**:
- Mapear procesos de negocio (current state)
- Identificar ineficiencias y cuellos de botella
- Diseñar procesos optimizados (future state)
- Create process documentation (BPMN, flowcharts)
- Calculate process improvements (time savings, cost reduction)

**Notaciones**:
- **BPMN** (Business Process Model and Notation): Estándar ISO
- **Flowcharts**: Más simple, fácil de entender
- **Swimlane diagrams**: Muestra responsabilidades por rol
- **Value Stream Mapping**: Lean methodology (identify waste)

**Process analysis**:
```
Current State (As-Is):
  - Document existing process
  - Identify pain points
  - Measure baseline metrics (time, cost, errors)

Future State (To-Be):
  - Design optimized process
  - Propose technology solutions
  - Estimate improvements (ROI)

Gap Analysis:
  - What needs to change?
  - What technology/training needed?
  - Implementation roadmap
```

---

### Requirements Documentation

**Principales tareas**:
- Escribir BRD (Business Requirements Document)
- Escribir FRD (Functional Requirements Document)
- Create use cases y user stories
- Maintain requirements traceability matrix
- Version control de requirements

**BRD structure** (Business Requirements Document):
```markdown
# Business Requirements Document (BRD)

## Executive Summary
- Project overview, business objectives, expected benefits

## Business Objectives
- What are we trying to achieve?
- Success criteria (measurable)

## Stakeholders
- Who is impacted?
- Roles and responsibilities

## Current State (As-Is)
- How do things work today?
- Pain points and challenges

## Future State (To-Be)
- How should things work?
- Proposed solution (high-level)

## Business Requirements
- BR-001: System must support 10,000 concurrent users
- BR-002: Reports must be generated within 5 seconds
- BR-003: System must comply with GDPR

## Assumptions & Constraints
- Budget: $500k
- Timeline: 6 months
- Regulatory compliance required

## Risks
- Integration with legacy system (high complexity)
- User adoption (training needed)

## Success Metrics
- Process time reduced by 30%
- Error rate reduced by 50%
- User satisfaction >80%
```

**FRD structure** (Functional Requirements Document):
```markdown
# Functional Requirements Document (FRD)

## Functional Requirements

### FR-001: User Authentication
- Description: Users must log in with email and password
- Input: Email (valid format), Password (8+ chars)
- Output: Access granted or error message
- Business Rule: Max 3 login attempts before lockout
- Priority: Must Have

### FR-002: Generate Sales Report
- Description: Users can generate monthly sales reports
- Input: Date range (start, end), filters (region, product)
- Output: PDF report with charts and tables
- Business Rule: Report must include all sales within date range
- Priority: Must Have

### FR-003: Export Data
- Description: Users can export data to CSV or Excel
- Input: Dataset selection, format (CSV/Excel)
- Output: Downloaded file
- Business Rule: Max 100,000 rows per export
- Priority: Should Have
```

---

### Use Case Development

**Principales tareas**:
- Escribir use cases (formal UML style)
- Identificar actors (usuarios, sistemas)
- Describe main flow y alternate flows
- Edge cases y exception handling

**Use Case template**:
```markdown
# Use Case: Reset Password

**Use Case ID**: UC-001
**Actor**: Registered User
**Precondition**: User has a registered account
**Trigger**: User clicks "Forgot Password?" link

## Main Flow (Happy Path):
1. User navigates to login page
2. User clicks "Forgot Password?" link
3. System displays password reset page
4. User enters email address
5. User clicks "Send Reset Link"
6. System validates email exists
7. System sends reset email
8. System displays "Email sent" confirmation
9. User receives email within 2 minutes
10. User clicks reset link in email
11. System validates link (not expired, not used)
12. System displays new password form
13. User enters new password (8+ chars, 1 uppercase, 1 number)
14. User clicks "Reset Password"
15. System updates password
16. System logs user in automatically
17. System displays success message

## Alternate Flows:
- **A1: Email doesn't exist** (Step 6)
  - System displays generic message "If email exists, reset link sent" (security)
  - Use case ends

- **A2: Reset link expired** (Step 11)
  - System displays "Link expired, request new one"
  - Use case returns to Step 3

- **A3: Invalid password format** (Step 13)
  - System displays validation error
  - Use case returns to Step 13

## Exception Flows:
- **E1: Email service down** (Step 7)
  - System logs error
  - System displays "Service temporarily unavailable"
  - Use case ends

**Postcondition**: User's password is updated and user is logged in
**Business Rules**: 
- Reset link expires after 24 hours
- Reset link can only be used once
- Password must meet complexity requirements
```

---

### Data Analysis & Reporting

**Principales tareas**:
- Analizar data para inform requirements
- Create reports y dashboards (para stakeholders)
- Identify trends y patterns
- ROI calculations (project justification)
- Metrics definition (KPIs de negocio)

**Analysis types**:
- **Descriptive**: What happened? (historical data)
- **Diagnostic**: Why did it happen? (root cause)
- **Predictive**: What will happen? (forecasting)
- **Prescriptive**: What should we do? (recommendations)

**Tools**:
- Excel (pivot tables, charts, formulas)
- Power BI / Tableau (dashboards)
- SQL (query databases)
- Python (pandas, data analysis)

---

### Stakeholder Management

**Principales tareas**:
- Elicit requirements de stakeholders
- Manage conflicting priorities
- Communicate progress y changes
- Facilitate decision-making
- Ensure stakeholder buy-in

**Stakeholders típicos**:
- **Business Users**: End users del sistema
- **Executive Sponsors**: Budget, strategic direction
- **IT/Engineering**: Technical feasibility
- **Compliance**: Regulatory requirements
- **Operations**: Support, maintenance
- **Vendors**: Third-party integrations

---

### Testing & Validation

**Principales tareas**:
- Create test cases (basados en requirements)
- User Acceptance Testing (UAT) coordination
- Validate que solución cumple requirements
- Bug triage y prioritization
- Sign-off de deliverables

**UAT process**:
1. Create UAT test plan (scenarios, test cases)
2. Recruit UAT testers (business users)
3. Conduct UAT sessions (supervised testing)
4. Document findings (bugs, usability issues)
5. Work with Engineering para fix issues
6. Re-test hasta approval
7. Sign-off (business stakeholders approve)

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Junior to Senior (1-10 años de experiencia)

**Progresión típica**:
```
Junior Business Analyst (0-2 años)
    - Tareas: Requirements gathering, documentation, testing support
    ↓
Business Analyst (2-5 años)
    - Tareas: Full requirements lifecycle, process modeling, UAT
    ↓
Senior Business Analyst (5-8 años)
    - Tareas: Complex projects, stakeholder management, mentoring
    ↓
Lead Business Analyst (8-10 años)
    - Manage: 2-3 BAs, enterprise initiatives
    ↓
Business Analysis Manager (10+ años)
    - Manage: 5-10 BAs, BA practice
```

---

### Skills Requeridas

#### Business Analysis (Critical)

**Must have**:
- ✅ **Requirements elicitation**: Interviews, workshops, observation
- ✅ **Requirements documentation**: BRD, FRD, use cases, user stories
- ✅ **Process modeling**: BPMN, flowcharts, swimlanes
- ✅ **Gap analysis**: As-is vs to-be
- ✅ **Stakeholder management**: Communication, facilitation
- ✅ **UAT**: Test planning, execution, sign-off

**Nice to have**:
- 🔶 **Business process reengineering**: Lean, Six Sigma
- 🔶 **Change management**: Organizational change
- 🔶 **Project management**: PM basics (if no dedicated PM)

---

#### Technical Skills (Medium)

**Must have**:
- ✅ **SQL**: Query databases (basic to intermediate)
- ✅ **Excel**: Pivot tables, VLOOKUP, charts (advanced)
- ✅ **Visio / Lucidchart**: Process diagrams
- ✅ **JIRA / Azure DevOps**: Agile tools (if Agile environment)

**Nice to have**:
- 🔶 **Power BI / Tableau**: Data visualization
- 🔶 **Python**: Data analysis (pandas, automation)
- 🔶 **UML**: Unified Modeling Language (formal modeling)
- 🔶 **API basics**: REST, integrations

---

#### Domain Knowledge (depends on industry)

**Common domains**:
- **Finance**: Banking, payments, accounting
- **Healthcare**: HIPAA, EHR, patient workflows
- **Retail**: E-commerce, inventory, supply chain
- **Insurance**: Claims, underwriting, policy management
- **Government**: Regulatory compliance, procurement

**Value**: Deep domain knowledge → better requirements (understand business context)

---

#### Certifications (nice to have)

- **CBAP** (Certified Business Analysis Professional) - IIBA
- **CCBA** (Certification of Capability in Business Analysis) - IIBA
- **PMI-PBA** (Professional in Business Analysis) - PMI
- **Agile Analysis Certification** (IIBA-AAC)
- **Six Sigma** (Green Belt, Black Belt) - Process improvement

---

#### Soft Skills (Critical)

**Must have**:
- ✅ **Communication**: Written (documentation) + Oral (presentations)
- ✅ **Analytical thinking**: Problem-solving, critical thinking
- ✅ **Attention to detail**: Accurate requirements, no ambiguity
- ✅ **Facilitation**: Workshops, meetings
- ✅ **Negotiation**: Balance conflicting stakeholder needs
- ✅ **Adaptability**: Changing requirements, priorities

---

### Stack Tecnológico

El BA usa principalmente **documentation tools** y **modeling tools**:

#### Requirements Management
```yaml
Documentation: Confluence, SharePoint, Google Docs, MS Word
Requirements Tools: Jama, Helix RM, IBM DOORS (enterprise)
Agile Tools: Jira, Azure DevOps (user stories, backlog)
```

#### Process Modeling
```yaml
BPMN: Bizagi Modeler, Camunda Modeler (free)
Diagramming: Visio, Lucidchart, Draw.io, Miro
Wireframing: Balsamiq, Figma (basic mockups)
```

#### Data Analysis
```yaml
Spreadsheets: Excel (advanced), Google Sheets
Databases: SQL (MySQL, PostgreSQL, SQL Server)
BI Tools: Power BI, Tableau, Looker
```

#### Collaboration
```yaml
Communication: Slack, Microsoft Teams, Email
Meetings: Zoom, Google Meet
Presentations: PowerPoint, Google Slides
```

---

## 📊 Métricas de Éxito

### Requirements Quality

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Requirements Defect Rate** | <5% defects post-delivery | Por proyecto |
| **Requirements Stability** | <10% changes después de sign-off | Por proyecto |
| **UAT Pass Rate** | >90% first pass | Por proyecto |
| **Stakeholder Sign-off Time** | <2 semanas | Por proyecto |

### Project Impact

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Project Success Rate** | >80% on-time, on-budget | Anual |
| **Business Value Delivered** | ROI >150% | Por proyecto |
| **Process Improvement** | 20-30% efficiency gain | Por proyecto |
| **User Satisfaction** | >80% (UAT feedback) | Por proyecto |

### Stakeholder Satisfaction

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Business Stakeholder Satisfaction** | >4/5 | Trimestral |
| **Engineering Team Satisfaction** | >4/5 (requirements clarity) | Trimestral |
| **Documentation Quality** | >4/5 (peer review) | Por entregable |

---

## 🔄 Interacciones con Otros Equipos

### Con Business Stakeholders

**Frecuencia**: Weekly  
**Modo**: **Collaboration** + **Service Provider**

**Actividades**:
- Requirements elicitation (interviews, workshops)
- Process analysis (as-is, to-be)
- Demos y validaciones (prototypes, UAT)
- Status updates (progress, timeline)
- Change management (comunicar impactos)

**Tools**: Email, Zoom, Confluence, PowerPoint

---

### Con Engineering Team

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Requirements clarification (Q&A durante development)
- Feasibility discussions (technical constraints)
- Design reviews (architecture alignment)
- Testing collaboration (UAT, bug fixes)
- Sprint planning (if Agile)

**Tools**: Jira, Slack, Confluence

---

### Con Product Manager / Product Owner

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Translate business needs → user stories (Agile)
- Prioritization input (business value)
- Requirements validation (ensure completeness)
- Backlog refinement (detalle de historias)

**División** (si hay overlap):
- **BA**: Requirements detail, process analysis, UAT
- **PM/PO**: Strategy, roadmap, prioritization

---

### Con QA / Test Team

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Create test cases (basados en requirements)
- UAT coordination (recruit users, facilitate testing)
- Bug triage (prioritize based on business impact)
- Test data creation (realistic scenarios)

**Tools**: Jira, TestRail, Excel

---

### Con Project Manager

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Project planning (timeline, milestones)
- Risk management (identify risks)
- Status reporting (requirements progress)
- Scope management (change requests)

---

### Con Data Analysts

**Frecuencia**: Monthly  
**Modo**: **Collaboration**

**Actividades**:
- Data analysis para inform requirements
- Reporting requirements (dashboards, KPIs)
- Data validation (ensure data accuracy)

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: BA Specialization

```
Business Analyst (2-5 años)
    ↓
Senior Business Analyst (5-8 años)
    - Complex projects, enterprise initiatives
    ↓
Lead Business Analyst (8-10 años)
    - Manage 2-3 BAs, BA practice
    ↓
Business Analysis Manager (10+ años)
    - Manage BA team (5-10 BAs)
```

#### Opción 2: Product Management

```
Business Analyst (2-5 años)
    ↓
Product Owner (lateral move)
    - Agile execution focus
    ↓
Product Manager
    - Strategy, roadmap, vision
```

#### Opción 3: Project Management

```
Senior Business Analyst (5-8 años)
    ↓
Project Manager
    - Full project lifecycle ownership
    ↓
Program Manager
    - Multiple projects, strategic initiatives
```

#### Opción 4: Data Analytics

```
Business Analyst (2-5 años)
    ↓
Data Analyst (if strong SQL, BI skills)
    ↓
Business Intelligence Analyst
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Dominar requirements documentation (BRD, FRD, use cases)
- [ ] Aprender BPMN (process modeling)
- [ ] Get CBAP o CCBA certification (IIBA)
- [ ] Advanced Excel (pivot tables, macros)
- [ ] SQL basics (query databases)

**Próximos 1-2 años**:
- [ ] Lead full project (requirements → UAT → sign-off)
- [ ] Domain expertise (deep knowledge en industria)
- [ ] Power BI o Tableau (data visualization)
- [ ] Agile/Scrum practices (if transitioning to Agile BA)
- [ ] Stakeholder management at executive level

**Próximos 3-5 años** (hacia Senior/Lead):
- [ ] Business process reengineering (Lean, Six Sigma)
- [ ] Change management (organizational change)
- [ ] Enterprise architecture understanding
- [ ] Mentoring junior BAs
- [ ] Team management (if management track)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"Business Analysis Body of Knowledge (BABOK)"** - IIBA (industry standard)
- 📚 **"The Business Analyst's Handbook"** - Howard Podeswa
- 📚 **"Software Requirements"** - Karl Wiegers
- 📚 **"Mastering the Requirements Process"** - Suzanne & James Robertson
- 📚 **"User Stories Applied"** - Mike Cohn (Agile BA)

#### Certifications

- **CBAP** (Certified Business Analysis Professional) - IIBA
- **CCBA** (Certification of Capability in Business Analysis) - IIBA
- **PMI-PBA** (Professional in Business Analysis) - PMI
- **IIBA-AAC** (Agile Analysis Certification)
- **Six Sigma Green Belt** (process improvement)

#### Comunidades

- **IIBA** (International Institute of Business Analysis): Chapters, events
- **Modern Analyst**: Resources, templates
- **BA Times**: Newsletter, articles
- **LinkedIn Groups**: Business Analysis Professional, IIBA Community

---

## 📝 Herramientas del Día a Día

### Requirements Management

| Tool | Uso | Nivel |
|------|-----|-------|
| **Confluence** | Requirements docs, knowledge base | Advanced |
| **Jira** | Agile user stories, backlog (if Agile) | Intermediate |
| **Excel** | Requirements traceability matrix, analysis | Advanced |
| **IBM DOORS** | Enterprise requirements management (large orgs) | Intermediate |

### Process Modeling

| Tool | Uso |
|------|-----|
| **Visio** | BPMN diagrams, flowcharts |
| **Lucidchart** | Collaborative diagramming |
| **Bizagi Modeler** | BPMN (free, powerful) |
| **Draw.io** | Free diagramming |

### Data Analysis

| Tool | Uso |
|------|-----|
| **Excel** | Data analysis, pivot tables, charts |
| **SQL** (MySQL, PostgreSQL) | Query databases |
| **Power BI / Tableau** | Dashboards, data visualization |

### Collaboration

| Tool | Uso |
|------|-----|
| **Slack / Teams** | Communication |
| **Zoom / Google Meet** | Meetings, workshops |
| **PowerPoint** | Presentations a stakeholders |

---

## 🚀 Ejemplo de Semana Típica

### Lunes
- **9:00-10:00**: Stakeholder interview (elicit requirements para nuevo proyecto)
- **10:00-12:00**: Deep work: Escribir BRD (business requirements document)
- **14:00-15:00**: Workshop facilitation (JAD session con 5 stakeholders)
- **15:00-17:00**: Synthesis: Document workshop findings, update requirements

### Martes
- **9:00-10:00**: Requirements review meeting con Engineering (clarify technical questions)
- **10:00-12:00**: Process modeling: Create BPMN diagram (as-is process)
- **14:00-15:00**: SQL query data para analysis (support requirements)
- **15:00-17:00**: Data analysis: Excel pivot tables, identify trends

### Miércoles
- **9:00-12:00**: Deep work: Write FRD (functional requirements document)
- **14:00-15:00**: Design review con Engineering (validate architecture)
- **15:00-16:30**: Create use cases (3-4 use cases)
- **16:30-17:00**: 1:1 con PM (alignment on priorities)

### Jueves
- **9:00-10:00**: UAT planning meeting (define test scenarios)
- **10:00-12:00**: Create UAT test cases (based on requirements)
- **14:00-16:00**: Facilitate UAT session (3 business users testing)
- **16:00-17:00**: Document UAT findings (bugs, usability issues)

### Viernes
- **9:00-10:00**: Bug triage meeting con Engineering (prioritize fixes)
- **10:00-12:00**: Stakeholder presentation (demo solution, get feedback)
- **14:00-15:00**: Update requirements traceability matrix
- **15:00-16:00**: Team BA sync (share best practices, learnings)
- **16:00-17:00**: Week wrap-up, admin tasks

**Requirements elicitation & documentation**: ~35%  
**Process modeling & analysis**: ~20%  
**Stakeholder meetings**: ~20%  
**UAT & testing**: ~15%  
**Data analysis**: ~10%

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- 2-3+ años de experiencia (puede ser operations, consulting, project coordination → BA)
- Strong analytical skills (problem-solving, critical thinking)
- Excellent communication (written + oral)
- Domain knowledge (ideally en industria específica)
- Experience con requirements gathering (interviews, workshops)

✅ **Puedes**:
- Escribir requirements documents claros (BRD, FRD)
- Facilitate stakeholder workshops
- Create process diagrams (BPMN, flowcharts)
- Analyze data (Excel, SQL básico)
- Conduct UAT (test planning, execution)

✅ **Te gusta**:
- Problem-solving (understand root causes)
- Process optimization (make things better)
- Stakeholder interaction (interviews, presentations)
- Documentation (detailed, accurate writing)
- Bridge business + technology (translator role)

---

## 🔗 Links Relacionados

- [Product Manager](product-manager.md) - Estrategia de producto
- [Product Owner](product-owner.md) - Ejecución Agile
- [Data Analyst](data-analyst.md) - Análisis de datos
- [Equipo de Producto](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: Lead Business Analyst