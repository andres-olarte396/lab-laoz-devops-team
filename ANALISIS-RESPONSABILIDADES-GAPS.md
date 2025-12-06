# Análisis de Responsabilidades y Gaps Organizacionales

> **Análisis realizado**: 6 de diciembre de 2025  
> **Equipos analizados**: Desarrollo (7 roles), DevOps (6 roles), Arquitectura (3 roles), Diseño (4 roles), Producto (4 roles)  
> **Total roles documentados**: 24 roles

---

## 📊 Resumen Ejecutivo

### ✅ Fortalezas Identificadas

1. **Cobertura técnica sólida**: Development + DevOps + Arquitectura bien definidos
2. **Product discovery robusto**: PM + PO + BA + Data Analyst (coverage completo)
3. **Security**: Security Engineer con responsabilidades claras (DevSecOps)
4. **Design thinking**: UX + UI + Research + Product Designer (roles especializados)
5. **Observability**: SRE con ownership claro de monitoring y alerting

### ⚠️ Gaps Críticos Identificados

| Gap | Severidad | Impacto | Rol Faltante Sugerido |
|-----|-----------|---------|------------------------|
| **Technical Writing** | 🔴 CRITICAL | Documentación API/user docs inconsistente | Technical Writer |
| **Customer Support Eng** | 🔴 CRITICAL | No hay ownership de soporte técnico L2/L3 | Support Engineer / DevRel |
| **Release Management** | 🟡 HIGH | Ambigüedad entre PO, DevOps, y Tech Lead | Release Manager (o clarificar) |
| **Training & Onboarding** | 🟡 HIGH | No hay ownership de internal training | Training Specialist (o asignar) |
| **Localization (i18n/l10n)** | 🟡 HIGH | No hay ownership de internacionalización | i18n Specialist (o asignar a Frontend) |
| **Performance Engineering** | 🟠 MEDIUM | Disperso entre Backend, SRE, Data Architect | Performance Engineer (opcional) |
| **Developer Experience** | 🟠 MEDIUM | Platform Engineer cubre parcialmente | DevEx Engineer (opcional) |
| **Marketing/Growth** | 🟠 MEDIUM | PM tiene GTM, pero falta growth hacking | Growth PM / Marketing (fuera de tech) |

---

## 🗺️ Mapa de Responsabilidades por Área Funcional

### 1. **Security & Compliance**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Security automation** (SAST/DAST) | Security Engineer | CI/CD Engineer | ✅ |
| **Infrastructure security** | Security Engineer | Cloud Engineer, Platform Eng | ✅ |
| **Compliance** (SOC2, GDPR, ISO27001) | Security Engineer | Enterprise Architect, BA | ✅ |
| **Vulnerability mgmt** | Security Engineer | DevOps Lead | ✅ |
| **Security incidents** | Security Engineer | SRE (detection), DevOps Lead | ✅ |
| **Penetration testing** | ❌ NINGUNO | Security Engineer (limited) | 🔴 **GAP: External pentest needed** |
| **Security audits** | Security Engineer | Compliance team (external?) | 🟡 **Audit support unclear** |
| **Security training** | Security Engineer | Engineering Manager? | 🟡 **GAP: Who delivers training?** |

**Recomendaciones**:
- ✅ Security Engineer tiene buen coverage
- 🔴 **Agregar**: Pentest policy (internal vs external vendors)
- 🟡 **Clarificar**: Who owns security awareness training delivery?
- 🟡 **Considerar**: Compliance Specialist para empresas reguladas (finance, health)

---

### 2. **Observability & Monitoring**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Monitoring setup** | SRE | Platform Engineer (infrastructure) | ✅ |
| **Alerting & on-call** | SRE | DevOps Lead (escalation) | ✅ |
| **Incident response** | SRE | Tech Lead, Engineering Manager | ✅ |
| **Postmortems** | SRE | Tech Lead | ✅ |
| **SLO/SLI definition** | SRE | Product Manager (business metrics) | ✅ |
| **APM** (Application Performance Monitoring) | SRE | Backend/Frontend Developers | ✅ |
| **Log aggregation** | SRE | Platform Engineer | ✅ |
| **Distributed tracing** | SRE | Backend Developers | ✅ |
| **Business metrics dashboards** | Data Analyst | PM, SRE (uptime metrics) | ✅ |
| **Cost monitoring** (cloud spend) | ❌ AMBIGUO | Platform Eng? DevOps Lead? | 🟡 **GAP: FinOps ownership unclear** |

**Recomendaciones**:
- ✅ SRE tiene excelente coverage
- 🟡 **Clarificar**: Who owns FinOps (cloud cost optimization)?
  - **Opción A**: Assign to Platform Engineer + DevOps Lead
  - **Opción B**: Hire FinOps Engineer (large orgs, >$500k/year cloud spend)

---

### 3. **Quality Assurance & Testing**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Unit testing** | Developers (all) | Tech Lead (code review) | ✅ |
| **Integration testing** | Developers | QA Engineer | ✅ |
| **E2E testing** | QA Engineer | Developers | ✅ |
| **Manual testing** (exploratory) | QA Engineer | PO (UAT) | ✅ |
| **UAT** (User Acceptance Testing) | Product Owner | Business Analyst, QA | ✅ |
| **Performance testing** | ❌ AMBIGUO | Backend Dev? SRE? | 🟡 **GAP: No clear owner** |
| **Load testing** | ❌ AMBIGUO | SRE? Backend Dev? | 🟡 **GAP: No clear owner** |
| **Security testing** (pentest) | Security Engineer | QA (limited) | 🟡 **External pentest needed** |
| **Accessibility testing** (WCAG) | UX Designer, UI Designer | QA Engineer? | 🟡 **GAP: QA lacks WCAG expertise?** |
| **Mobile testing** (devices) | Mobile Developer, QA | - | ✅ |
| **Test automation strategy** | QA Engineer | Tech Lead | ✅ |
| **Test data management** | ❌ AMBIGUO | QA? Backend Dev? | 🟡 **GAP: No clear owner** |

**Recomendaciones**:
- 🟡 **Asignar**: Performance/Load testing
  - **Opción A**: Backend Developer (for application code)
  - **Opción B**: SRE (for infrastructure limits)
  - **Mejor**: Shared responsibility con clear RACI
- 🟡 **Considerar**: QA Engineer training on WCAG accessibility testing
- 🟡 **Asignar**: Test data management
  - **Opción A**: QA Engineer owns test data scripts
  - **Opción B**: Data Architect provides production-like anonymized data

---

### 4. **Documentation**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **API documentation** | ❌ NINGUNO | Backend Dev (ad-hoc) | 🔴 **GAP CRÍTICO** |
| **User documentation** | ❌ NINGUNO | PM? PO? | 🔴 **GAP CRÍTICO** |
| **Technical guides** | ❌ NINGUNO | Developers (inconsistent) | 🔴 **GAP** |
| **Architecture docs** (ADRs) | Solution Architect | Enterprise Architect | ✅ |
| **Design system docs** | UI Designer | UX Designer | ✅ |
| **Runbooks** (operations) | SRE | Platform Engineer | ✅ |
| **Onboarding docs** | ❌ AMBIGUO | Engineering Manager? | 🟡 **GAP** |
| **Process documentation** | Business Analyst | PM, PO | ✅ (for business processes) |
| **Requirements docs** (BRD/FRD) | Business Analyst | PM | ✅ |
| **Release notes** | ❌ AMBIGUO | PO? PM? | 🟡 **GAP** |
| **Knowledge base** | ❌ NINGUNO | Everyone (Confluence chaos) | 🟡 **No ownership** |
| **Video tutorials** | ❌ NINGUNO | - | 🟠 **Nice to have** |

**Recomendaciones**:
- 🔴 **CRÍTICO: Contratar Technical Writer** (o 0.5 FTE)
  - **Responsabilidades**:
    - API documentation (OpenAPI/Swagger, Postman collections)
    - User guides (help center, getting started)
    - Developer documentation (SDK docs, integration guides)
    - Release notes (customer-facing)
    - Video tutorials (optional)
  - **Reports to**: Product Manager o Engineering Manager
  - **Ratio**: 1 Technical Writer per 15-25 engineers
  - **Cuándo contratar**: Si tienes API pública o >20 engineers

- 🟡 **Alternativa (si no puedes contratar)**:
  - **Assign to Backend Developers**: API docs (parte de Definition of Done)
  - **Assign to Product Owner**: Release notes, user-facing docs
  - **Assign to Engineering Manager**: Onboarding docs, knowledge base curation

---

### 5. **Customer Support (Technical)**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **L1 Support** (basic troubleshooting) | ❌ FUERA DE TECH | Customer Support team | N/A (no tech) |
| **L2 Support** (technical issues) | ❌ NINGUNO | Developers (ad-hoc) | 🔴 **GAP CRÍTICO** |
| **L3 Support** (escalations) | Tech Lead | SRE (production issues) | 🟡 **Reactive, no proactive** |
| **Customer success** (tech integrations) | ❌ NINGUNO | PM (limited) | 🔴 **GAP** |
| **Bug triage** (customer-reported) | Product Owner | QA Engineer | ✅ |
| **Support ticket analysis** | ❌ NINGUNO | UX Researcher (limited) | 🟡 **GAP: Not systematic** |
| **Customer onboarding** (technical) | ❌ NINGUNO | - | 🔴 **GAP** |
| **Integration support** (API help) | ❌ NINGUNO | Backend Dev (ad-hoc) | 🔴 **GAP** |

**Recomendaciones**:
- 🔴 **CRÍTICO: Definir L2/L3 Support ownership**

**Opción A: Hire Support Engineer / DevRel**:
```yaml
Rol: Support Engineer (Solutions Engineer)
Responsabilidades:
  - L2/L3 technical support (tickets)
  - Customer onboarding (technical setup)
  - Integration support (API troubleshooting)
  - Reproduce customer bugs
  - Customer feedback → Product/Engineering
  - Support documentation (FAQs, troubleshooting guides)
  
Skills:
  - Technical: Backend/API knowledge, SQL, debugging
  - Soft: Customer empathy, communication
  
Team: Reports to Engineering Manager or Customer Success
Ratio: 1 Support Engineer per 200-500 customers (B2B) or per 5-10 engineers
Cuándo: API-first products, B2B SaaS, technical products
```

**Opción B: Developer Rotation** (sin contratar):
- Assign 1 developer per week to "Support Duty"
- Responsibilities: L2 tickets, customer bugs, escalations
- Pro: No hiring, developers learn customer pain
- Con: Context switching, lower velocity

**Opción C: DevRel (Developer Relations)**:
- Si tienes API pública o developer-facing product
- Responsibilities: Developer onboarding, integration support, content (blog, tutorials), community management

---

### 6. **Release Management**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Release planning** | Product Owner | PM (roadmap alignment) | ✅ |
| **Release coordination** | ❌ AMBIGUO | PO? DevOps? Tech Lead? | 🟡 **GAP: Unclear** |
| **Feature flags** | CI/CD Engineer | Developers | ✅ |
| **Deployment execution** | CI/CD Engineer | SRE (rollback) | ✅ |
| **Release notes** | ❌ AMBIGUO | PO? PM? | 🟡 **GAP** |
| **Rollback decisions** | SRE | Tech Lead, DevOps Lead | ✅ |
| **Release communication** | ❌ AMBIGUO | PM? PO? | 🟡 **GAP** |
| **Go/No-Go decision** | ❌ AMBIGUO | PM? Engineering Manager? | 🟡 **GAP** |
| **Release validation** | QA Engineer | SRE (smoke tests) | ✅ |

**Recomendaciones**:
- 🟡 **Opción A: Clarificar ownership en RACI matrix** (no contratar):

```yaml
Release Process RACI:
  Release Planning:
    Responsible: Product Owner
    Accountable: Product Manager
    Consulted: Tech Lead, Engineering Manager
    Informed: Stakeholders
    
  Release Coordination (day-of):
    Responsible: CI/CD Engineer + SRE
    Accountable: Tech Lead
    Consulted: PO (rollback impact)
    Informed: PM, Engineering Manager
    
  Release Notes (customer-facing):
    Responsible: Product Owner
    Accountable: Product Manager
    Consulted: Technical Writer (if exists)
    Informed: Marketing, Sales, Customer Success
    
  Go/No-Go Decision:
    Responsible: Engineering Manager
    Accountable: Product Manager
    Consulted: Tech Lead, SRE (production readiness), PO (feature completeness)
    Informed: Stakeholders
```

- 🟡 **Opción B: Hire Release Manager** (large orgs, >50 engineers):
  - Coordinates releases across multiple teams
  - Maintains release calendar
  - Go/No-Go facilitator (not decider)
  - Release retrospectives
  - Best for: Enterprise, highly regulated industries

---

### 7. **Training & Onboarding**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **New hire onboarding** | ❌ AMBIGUO | Engineering Manager? | 🟡 **GAP** |
| **Technical onboarding** | ❌ AMBIGUO | Tech Lead (buddy system) | 🟡 **Ad-hoc, no process** |
| **Codebase tours** | Tech Lead | Senior Developers | ✅ (informal) |
| **Internal tech talks** | ❌ NINGUNO | Developers (voluntary) | 🟡 **Not systematic** |
| **Skill development** | ❌ AMBIGUO | Engineering Manager? | 🟡 **GAP: No L&D budget owner?** |
| **Certification support** | ❌ AMBIGUO | Engineering Manager? | 🟡 **GAP** |
| **Lunch & learns** | ❌ NINGUNO | Voluntary | 🟡 **No ownership** |
| **External training** | ❌ AMBIGUO | Engineering Manager? | 🟡 **GAP** |

**Recomendaciones**:
- 🟡 **Assign to Engineering Manager**:
  - Owner of onboarding process (documentation + buddy assignments)
  - Owner of L&D budget (training, certifications, conferences)
  - Facilitate tech talks (schedule, encourage speakers)
  
- 🟡 **Opción: Hire Learning & Development Specialist** (large orgs, >100 people):
  - Internal training programs
  - Onboarding curriculum
  - Lunch & learns coordination
  - Skills gap analysis
  - Best for: >100 employees, high growth

---

### 8. **Performance Optimization**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Application performance** | Backend Developer | Frontend Dev (client-side) | ✅ |
| **Database optimization** | Backend Developer | Data Architect (schema design) | ✅ |
| **Query optimization** | Backend Developer | Data Analyst (query patterns) | ✅ |
| **Frontend performance** | Frontend Developer | UI Designer (asset size) | ✅ |
| **Load testing** | ❌ AMBIGUO | Backend Dev? SRE? | 🟡 **GAP** |
| **Performance profiling** | ❌ AMBIGUO | Backend Dev? | 🟡 **GAP: Ad-hoc** |
| **CDN optimization** | Cloud Engineer | Frontend Developer | ✅ |
| **Infrastructure performance** | SRE | Platform Engineer | ✅ |
| **Performance budgets** | ❌ NINGUNO | Tech Lead? | 🟡 **GAP** |

**Recomendaciones**:
- 🟡 **Clarificar ownership**:
  - **Backend Developer**: Application code performance (profiling, optimization)
  - **SRE**: Load testing (infrastructure capacity planning)
  - **Tech Lead**: Define performance budgets (e.g., "API response <200ms p95")
  
- 🟠 **Opcional: Performance Engineer** (large scale, >10M users):
  - Dedicated to performance optimization
  - Load testing, profiling, bottleneck analysis
  - Best for: High-traffic products (gaming, fintech, social media)

---

### 9. **Accessibility (WCAG Compliance)**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **Design accessibility** | UX Designer, UI Designer | Product Designer | ✅ |
| **Frontend implementation** | Frontend Developer | UI Designer (specs) | ✅ |
| **Accessibility testing** | ❌ AMBIGUO | QA? UX Designer? | 🟡 **GAP** |
| **Screen reader testing** | ❌ NINGUNO | UX Designer (limited) | 🟡 **GAP** |
| **Accessibility audit** | ❌ NINGUNO | UX Designer (tools) | 🟡 **Manual testing gap** |
| **WCAG compliance** | ❌ AMBIGUO | Legal? Design? | 🟡 **GAP** |

**Recomendaciones**:
- 🟡 **Asignar**: Accessibility testing
  - **Opción A**: QA Engineer (train on WCAG, aXe, WAVE, NVDA)
  - **Opción B**: UX Designer (owns audits, QA executes tests)
  
- 🟡 **Opción: Hire Accessibility Specialist** (if legally required):
  - Industries: Government, education, finance (ADA compliance)
  - Responsibilities: WCAG audits, remediation, training
  - Best for: Public-facing products, regulated industries

---

### 10. **Internationalization (i18n) & Localization (l10n)**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **i18n architecture** | ❌ NINGUNO | Frontend Dev (ad-hoc) | 🟡 **GAP** |
| **Translation keys** | ❌ NINGUNO | Frontend Dev | 🟡 **GAP** |
| **Translation management** | ❌ NINGUNO | PM? Product Designer? | 🔴 **GAP** |
| **Locale support** | ❌ NINGUNO | Frontend Dev | 🟡 **GAP** |
| **RTL support** (Arabic, Hebrew) | ❌ NINGUNO | UI Designer? Frontend Dev? | 🟡 **GAP** |
| **Date/time/currency formatting** | ❌ NINGUNO | Frontend Dev | 🟡 **GAP** |

**Recomendaciones**:
- 🟡 **Assign to Frontend Developer**:
  - i18n architecture (i18next, react-intl)
  - Translation key management
  - Locale support implementation
  
- 🟡 **Assign to Product Manager**:
  - Translation content (coordinate with translators/agencies)
  - Prioritize locales (which languages?)
  
- 🟡 **Assign to UI Designer**:
  - RTL layout design
  - Text expansion considerations (German +30%, Arabic RTL)

---

### 11. **Data Privacy & GDPR**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **GDPR compliance** (technical) | Security Engineer | Data Architect | ✅ |
| **Data retention policies** | Data Architect | Security Engineer | ✅ |
| **Right to be forgotten** (implementation) | Backend Developer | Data Architect (schema design) | ✅ |
| **Data anonymization** | Data Architect | Backend Dev (implementation) | ✅ |
| **Consent management** | ❌ AMBIGUO | Frontend Dev? Legal? | 🟡 **GAP** |
| **Privacy policy** (legal) | ❌ FUERA DE TECH | Legal team | N/A |
| **DPO** (Data Protection Officer) | ❌ FUERA DE TECH | Legal/Compliance (external?) | 🟡 **Required for GDPR (EU)** |

**Recomendaciones**:
- ✅ Good coverage en tech side
- 🟡 **Clarificar**: Consent management (cookie banners, opt-ins)
  - **Opción A**: Frontend Developer (technical implementation)
  - **Opción B**: Product Manager (business logic, what to track)
  
- 🟡 **GDPR (EU companies)**: Require DPO (Data Protection Officer)
  - Can be external consultant or internal (Legal/Compliance)
  - Not a tech role, but tech teams must collaborate

---

### 12. **Incident Management**

| Responsabilidad | Owner Principal | Contribuidores | Gap? |
|-----------------|-----------------|----------------|------|
| **On-call rotation** | SRE | Backend/Frontend Developers | ✅ |
| **Incident detection** | SRE | Monitoring systems | ✅ |
| **Incident response** | SRE | Tech Lead, Developers | ✅ |
| **Incident commander** | SRE | DevOps Lead (escalation) | ✅ |
| **Communication** (status page) | ❌ AMBIGUO | SRE? PM? | 🟡 **GAP** |
| **Postmortems** | SRE | Tech Lead | ✅ |
| **RCA** (Root Cause Analysis) | SRE | Backend Dev (code bugs) | ✅ |
| **Incident retrospectives** | SRE | Engineering Manager | ✅ |
| **Customer communication** | ❌ AMBIGUO | PM? Customer Success? | 🟡 **GAP** |

**Recomendaciones**:
- ✅ Good coverage
- 🟡 **Clarificar RACI**:

```yaml
Incident Communication:
  Status Page Updates (statuspage.io):
    Responsible: SRE (technical updates)
    Accountable: Engineering Manager
    
  Customer Communication (email, in-app):
    Responsible: Product Manager
    Accountable: Customer Success
    Consulted: SRE (technical details)
```

---

## 🔴 Gaps Críticos - Priorización

### Prioridad 1: CRÍTICO (Contratar o asignar AHORA)

#### 1. **Technical Writer** 🔴

**Por qué es crítico**:
- API documentation inconsistente → developer frustration
- User docs ausentes → support tickets ↑
- Onboarding lento (new hires spend weeks sin docs)

**Cuándo contratar**:
- ✅ Si tienes API pública
- ✅ Si tienes >20 engineers
- ✅ Si >30% de support tickets son "How do I...?"

**Alternativa (si no puedes contratar)**:
- Assign to Developers: API docs = Definition of Done
- Assign to PO: User-facing docs, release notes
- Tools: Swagger/OpenAPI (auto-generate API docs)

---

#### 2. **Support Engineer / DevRel** 🔴

**Por qué es crítico**:
- Developers doing L2 support → low velocity
- Customer bugs no reproducidos → frustration
- No customer feedback loop → product misses needs

**Cuándo contratar**:
- ✅ Si tienes API-first product o B2B SaaS
- ✅ Si >100 support tickets/month técnicos
- ✅ Si developers spend >20% time on support

**Alternativa (si no puedes contratar)**:
- Developer rotation: 1 dev/week on "Support Duty"
- Clear escalation: L1 (Support) → L2 (Support Dev) → L3 (Tech Lead)

---

#### 3. **Translation/Localization Ownership** 🟡→🔴 (si vas a mercados internacionales)

**Por qué es crítico**:
- Expanding to new markets sin i18n = rewrite costs
- Poor translations = bad UX = churn

**Cuándo es crítico**:
- ✅ Si tienes >20% users fuera de tu país de origen
- ✅ Si planeas expansion internacional

**Solución**:
- **Assign to Frontend Developer**: i18n architecture
- **Assign to PM**: Translation content, locale prioritization
- **Hire translator agency**: Content translation (not in-house)

---

### Prioridad 2: HIGH (Resolver en 3-6 meses)

#### 4. **Release Management Clarity** 🟡

**Solución**: Crear RACI matrix (no contratar)
- Ver sección "Release Management" arriba

---

#### 5. **Performance Testing Ownership** 🟡

**Solución**: Asignar a Backend Dev + SRE (RACI)
- **Backend Dev**: Application performance (code profiling)
- **SRE**: Load testing (infrastructure capacity)

---

#### 6. **Accessibility Testing** 🟡

**Solución**: Train QA Engineer en WCAG
- Tools: aXe, WAVE, Lighthouse, NVDA screen reader
- Owner: QA (execution), UX Designer (audits, specs)

---

### Prioridad 3: MEDIUM (Nice to have, evaluar en 6-12 meses)

#### 7. **FinOps Engineer** 🟠

**Cuándo considerar**:
- ✅ Cloud spend >$500k/year
- ✅ Multi-cloud (AWS + Azure + GCP)
- ✅ Cost optimization is strategic priority

**Alternativa**: Assign to Platform Engineer + DevOps Lead

---

#### 8. **Developer Experience (DevEx) Engineer** 🟠

**Cuándo considerar**:
- ✅ >50 engineers
- ✅ Developer productivity is bottleneck
- ✅ Tooling fragmentation

**Alternativa**: Platform Engineer ya cubre parcialmente

---

#### 9. **Growth PM / Marketing** 🟠

**Fuera de tech team** (Product-led growth)
- Cuándo: B2C products, viral loops, acquisition focus
- Alternativa: PM tiene GTM responsibilities

---

## 📋 RACI Matrix Recomendada - Áreas Críticas

### Security

| Activity | Security Eng | Cloud Eng | DevOps Lead | Eng Manager |
|----------|-------------|-----------|-------------|-------------|
| Security automation | **R/A** | C | I | I |
| Pentest coordination | **R/A** | I | C | I |
| Compliance audits | **R/A** | C | C | **A** |
| Security incidents | **R** | C | **A** | I |
| Security training | **R** | I | C | **A** |

---

### Documentation

| Activity | Tech Writer* | Developers | PO | PM |
|----------|-------------|------------|----|----|
| API docs | **R/A** | C | I | I |
| User guides | **R/A** | I | C | **A** |
| Release notes | **R** | I | C | **A** |
| Technical guides | **R/A** | C | I | I |
| Onboarding docs | **R** | C | I | **A** (Eng Manager) |

*Si no existe Tech Writer: Assign R to Developers (API), PO (user docs)

---

### Customer Support (Technical)

| Activity | Support Eng* | Developers | Tech Lead | PM |
|----------|-------------|-----------|-----------|-----|
| L2 tickets | **R/A** | C | I | I |
| L3 escalations | C | **R** | **A** | I |
| Bug reproduction | **R** | C | **A** (Tech Lead) | I |
| Customer feedback | **R** | I | I | **A** |
| Integration support | **R/A** | C | I | C |

*Si no existe Support Eng: Assign R to Developer rotation

---

### Release Management

| Activity | CI/CD Eng | SRE | PO | PM | Eng Manager |
|----------|----------|-----|----|----|-------------|
| Release planning | I | I | **R** | **A** | C |
| Release coordination | **R** | **R** (deployment) | C | I | **A** |
| Go/No-Go decision | C | C (readiness) | C | **A** | **R** |
| Release notes | I | I | **R** | **A** | I |
| Deployment | **R/A** | C (rollback) | I | I | I |

---

## ✅ Recomendaciones Accionables

### Corto Plazo (0-3 meses)

1. ✅ **Crear RACI matrix detallada** para:
   - Release management
   - Incident communication
   - Performance testing
   - Accessibility testing

2. ✅ **Asignar ownership claro** de:
   - API documentation → Backend Developers (DoD)
   - User documentation → Product Owner
   - Onboarding docs → Engineering Manager
   - Release notes → Product Owner
   - Performance testing → Backend Dev (app) + SRE (infra)
   - Accessibility testing → QA Engineer (train WCAG)

3. ✅ **Evaluar contratación de**:
   - **Technical Writer** (si API pública o >20 engineers)
   - **Support Engineer** (si >100 tickets técnicos/mes)

---

### Mediano Plazo (3-6 meses)

4. ✅ **Implementar procesos**:
   - Developer rotation para L2 support (si no contratas Support Eng)
   - Accessibility testing en CI/CD (automated aXe scans)
   - Performance budgets (define metrics, enforce in CI)

5. ✅ **Training & upskilling**:
   - QA Engineer → WCAG accessibility testing
   - Developers → Technical writing basics
   - Security Engineer → Security awareness training delivery

6. ✅ **Documentación**:
   - Crear templates: API docs, user guides, runbooks, ADRs
   - Knowledge base curation (Confluence cleanup)

---

### Largo Plazo (6-12 meses)

7. ✅ **Evaluar roles adicionales** (según crecimiento):
   - **FinOps Engineer** (si cloud spend >$500k/year)
   - **Release Manager** (si >50 engineers, multiple teams)
   - **Learning & Development Specialist** (si >100 employees)
   - **Accessibility Specialist** (si regulated industry: govt, finance, edu)

8. ✅ **Optimizaciones organizacionales**:
   - Split QA team si >10 QA engineers (Automation QA vs Manual QA)
   - Consider Staff+ engineering roles (Staff Engineer, Principal Engineer) para technical leadership sin management

---

## 📊 Matriz de Decisión: ¿Contratar o Asignar?

| Gap | Contratar si... | Asignar si... |
|-----|-----------------|---------------|
| **Technical Writer** | API pública O >20 engineers | <20 engineers, internal tools only |
| **Support Engineer** | >100 tickets técnicos/mes O B2B SaaS | <50 tickets/mes, B2C simple |
| **Release Manager** | >50 engineers, regulated industry | <30 engineers, clear RACI suficiente |
| **FinOps Engineer** | Cloud >$500k/year, multi-cloud | Cloud <$200k/year |
| **Accessibility Specialist** | Government/Finance (ADA required) | Best-effort accessibility |
| **Performance Engineer** | >10M users, gaming/fintech | <1M users, normal load |
| **DevEx Engineer** | >100 engineers, tooling chaos | <50 engineers, Platform Eng OK |

---

## 🎯 Próximos Pasos Sugeridos

### Paso 1: Priorizar Gaps (Workshop con Leadership)

**Participantes**: CTO, Engineering Manager, Product Manager, DevOps Lead

**Agenda**:
1. Revisar este documento (30 min)
2. Priorizar top 3 gaps críticos para tu organización (30 min)
3. Decidir: ¿Contratar o asignar? (30 min)
4. Definir timeline y owners (30 min)

---

### Paso 2: Crear RACI Matrices Detalladas

**Para cada área con ambigüedad**:
- Release Management
- Documentation
- Customer Support (Technical)
- Performance Testing
- Accessibility Testing
- Incident Communication

**Template**: Ver ejemplos en secciones arriba

---

### Paso 3: Documentar y Comunicar

**Crear**:
- `RACI-RELEASE-MANAGEMENT.md`
- `RACI-DOCUMENTATION.md`
- `RACI-CUSTOMER-SUPPORT.md`
- `ROLES-DECISION-LOG.md` (por qué asignamos X responsabilidad a Y rol)

**Comunicar**:
- All-hands: "Clarificación de responsabilidades"
- Team-specific: "Tus nuevas responsabilidades son..."

---

### Paso 4: Contratar (si aplica)

**Job descriptions recomendadas**:
- [Technical Writer JD](https://www.notion.so/Technical-Writer-JD) (crear)
- [Support Engineer JD](https://www.notion.so/Support-Engineer-JD) (crear)

---

### Paso 5: Revisión Trimestral

**Cada 3 meses**:
- ¿Nuevos gaps identificados?
- ¿Overlaps resueltos?
- ¿Ownership claro funcionando?
- ¿Necesitamos ajustar RACI?

---

## 📎 Apéndices

### A. Roles NO cubiertos en este análisis (fuera de Tech)

- **Marketing**: Growth, Content, SEO, Ads
- **Sales**: Account Executives, SDRs
- **Customer Success**: CSMs, Onboarding Specialists
- **Legal**: Contracts, IP, Privacy policy
- **Finance**: Accounting, FP&A
- **HR**: Recruiting, People Ops
- **Operations**: Office management, Procurement

---

### B. Roles comunes en otras organizaciones (evaluar necesidad)

- **Data Scientist** (vs Data Analyst): Machine learning, predictive models
- **ML Engineer** (vs Backend Dev): ML ops, model deployment
- **iOS/Android Developers** (vs Mobile Developer): Native specialists
- **DevOps Platform Lead** (vs DevOps Lead): Larger teams (>10 DevOps engineers)
- **Scrum Master**: Si equipos son 100% Scrum (puede ser Engineering Manager)
- **Agile Coach**: Enterprise transformations (consultants, no full-time)

---

## 🔗 Links Relacionados

- [Team Topologies](../README.md) - Modelo organizacional
- [Equipos Overview](../equipos/README.md) - Estructura de equipos
- [Workflows](../workflows/README.md) - Procesos de trabajo
- [Ceremonias](../ceremonias/README.md) - Reuniones y rituales
- [Comunicación](../comunicacion/README.md) - Patrones de comunicación

---

**Mantenido por**: CTO / VP Engineering  
**Última actualización**: Diciembre 2025  
**Próxima revisión**: Marzo 2026