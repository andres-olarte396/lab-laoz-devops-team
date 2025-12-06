# Matrices RACI - Responsabilidades Detalladas

> **RACI Framework**:  
> - **R** (Responsible): Quien ejecuta la tarea  
> - **A** (Accountable): Quien tiene la responsabilidad final (solo 1 por actividad)  
> - **C** (Consulted): Quien debe ser consultado (comunicación bidireccional)  
> - **I** (Informed): Quien debe ser informado (comunicación unidireccional)

---

## 📋 Tabla de Contenidos

1. [Release Management](#1-release-management)
2. [Documentation](#2-documentation)
3. [Customer Support (Technical)](#3-customer-support-technical)
4. [Security & Compliance](#4-security--compliance)
5. [Incident Management](#5-incident-management)
6. [Performance & Quality](#6-performance--quality)
7. [Onboarding & Training](#7-onboarding--training)
8. [Data Privacy & GDPR](#8-data-privacy--gdpr)

---

## 1. Release Management

### 1.1 Release Planning & Scheduling

| Actividad | PM | PO | Tech Lead | Eng Manager | DevOps Lead | CI/CD Eng | SRE |
|-----------|----|----|-----------|-------------|-------------|-----------|-----|
| **Define release scope** | **A** | **R** | C | I | I | I | I |
| **Prioritize features** | **A** | **R** | C | I | I | I | I |
| **Create release roadmap** | **A** | **R** | C | I | I | I | I |
| **Set release dates** | **A** | C | C | C | C | I | I |
| **Capacity planning** | I | C | **R/A** | C | C | I | I |
| **Risk assessment** | C | C | **R** | **A** | C | C | **R** |

---

### 1.2 Release Preparation

| Actividad | PM | PO | Tech Lead | QA Eng | DevOps Lead | CI/CD Eng | SRE |
|-----------|----|----|-----------|--------|-------------|-----------|-----|
| **Feature completion validation** | I | **A** | **R** | C | I | I | I |
| **Code freeze decision** | I | C | **A** | I | **R** | I | I |
| **Release branch creation** | I | I | **R** | I | C | **A** | I |
| **Regression testing** | I | C | C | **R/A** | I | I | I |
| **Performance testing** | I | I | **R** | C | C | I | **A** |
| **Security scanning** | I | I | C | I | C | **R/A** (Security Eng) | I |
| **Feature flags config** | I | **R** | C | I | I | **A** | I |
| **Rollback plan** | I | C | C | I | C | **R** | **A** |

---

### 1.3 Release Execution (Day-of)

| Actividad | PM | PO | Tech Lead | Eng Manager | CI/CD Eng | SRE | Marketing |
|-----------|----|----|-----------|-------------|-----------|-----|-----------|
| **Go/No-Go decision** | **A** | C | C | **R** | C (readiness) | C (readiness) | I |
| **Deployment execution** | I | I | C | I | **R/A** | C (monitoring) | I |
| **Smoke tests** | I | C | C | I | **R** | **A** | I |
| **Production monitoring** | I | I | C | I | C | **R/A** | I |
| **Rollback decision** | I | C | C | **A** | C | **R** (execution) | I |
| **Status updates** (Slack) | I | I | I | **R** | C | C | I |
| **Customer communication** | **R/A** | C | I | C | I | I | C |

---

### 1.4 Post-Release

| Actividad | PM | PO | Tech Lead | QA Eng | Data Analyst | SRE | Customer Success |
|-----------|----|----|-----------|--------|--------------|-----|------------------|
| **Release notes (customer)** | **A** | **R** | C | I | I | I | C |
| **Release notes (internal)** | I | **R** | C | I | I | I | I |
| **Metrics tracking** | C | C | C | I | **R/A** | C | I |
| **Bug triage** | I | **A** | C | **R** | I | C | I |
| **Customer feedback** | **A** | C | I | I | **R** | I | **R** |
| **Release retrospective** | C | C | **R** | C | C | **A** (Eng Mgr) | I |
| **Hotfix coordination** | I | C | **R** | I | C | **A** | I |

---

## 2. Documentation

### 2.1 Technical Documentation

| Actividad | Tech Writer* | Backend Dev | Frontend Dev | Tech Lead | Data Architect |
|-----------|-------------|-------------|--------------|-----------|----------------|
| **API documentation** | **R/A** | **R*** (if no TW) | C | C | I |
| **SDK documentation** | **R/A** | **R*** | C | C | I |
| **Integration guides** | **R/A** | C | C | **A** (if no TW) | I |
| **Architecture docs (ADRs)** | I | C | C | **A** (Sol Architect) | **R** |
| **Database schema docs** | **R** (TW) | C | I | C | **A** |
| **Code comments** | I | **R/A** | **R/A** | C (review) | I |

*Si no hay Technical Writer, asignar R a Developers

---

### 2.2 User Documentation

| Actividad | Tech Writer* | PM | PO | UX Designer | Customer Success |
|-----------|-------------|----|----|-------------|------------------|
| **User guides** | **R/A** | **A*** (if no TW) | **R*** | C | C |
| **Getting started** | **R/A** | **A*** | **R*** | C | C |
| **FAQ** | **R** | C | C | I | **A** |
| **Video tutorials** | **R/A** | C | C | **R** (UX) | C |
| **Help center articles** | **R** | C | C | I | **A** |
| **Tooltips (in-app)** | C | C | **R** | **A** | I |

*Si no hay Technical Writer: PM = Accountable, PO = Responsible

---

### 2.3 Operational Documentation

| Actividad | SRE | Platform Eng | DevOps Lead | Security Eng | Tech Lead |
|-----------|-----|--------------|-------------|--------------|-----------|
| **Runbooks** | **R/A** | **R** | C | I | C |
| **On-call procedures** | **R/A** | C | C | I | C |
| **Incident response playbooks** | **R/A** | C | **A** | C | C |
| **Deployment docs** | C | **R** | **A** | I | C |
| **Disaster recovery** | **R** | **R** | **A** | C | C |
| **Security procedures** | C | C | C | **R/A** | I |

---

### 2.4 Process Documentation

| Actividad | BA | PM | Eng Manager | QA Eng | Tech Lead |
|-----------|----|----|-------------|--------|-----------|
| **Business process docs (BRD)** | **R/A** | C | I | I | I |
| **Requirements docs (FRD)** | **R/A** | C | I | C | C |
| **Development workflow** | I | I | **A** | C | **R** |
| **Testing procedures** | C | I | C | **R/A** | C |
| **Code review guidelines** | I | I | C | C | **R/A** |
| **Onboarding docs** | I | I | **R/A** | I | C |

---

## 3. Customer Support (Technical)

### 3.1 Support Tiers

| Actividad | Support Eng* | Developer | Tech Lead | QA Eng | Customer Success |
|-----------|-------------|-----------|-----------|--------|------------------|
| **L1: Basic troubleshooting** | I | I | I | I | **R/A** |
| **L2: Technical issues** | **R/A** | **R*** (if no SE) | C | C | C |
| **L3: Escalations** | C | **R** | **A** | I | C |
| **Bug reproduction** | **R/A** | C | C | C | C |
| **Integration support** | **R/A** | **R*** | C | I | C |
| **Customer onboarding (tech)** | **R/A** | C | I | I | **A** |

*Si no hay Support Engineer: Developer rotation (R), Tech Lead (A)

---

### 3.2 Support Processes

| Actividad | Support Eng* | PO | QA Eng | Data Analyst | Customer Success |
|-----------|-------------|----|----|--------------|------------------|
| **Ticket triage** | **R** | **A** | C | I | **R** |
| **Bug prioritization** | C | **R/A** | C | I | C |
| **Support ticket analysis** | **R** | I | I | **A** | **R** |
| **Customer feedback loop** | **R** | **A** (PM) | I | C | **R** |
| **Support documentation (FAQs)** | **R/A** | C | I | I | C |
| **Escalation to Engineering** | **R** | I | **A** (Tech Lead) | I | C |

---

## 4. Security & Compliance

### 4.1 Security Operations

| Actividad | Security Eng | Cloud Eng | Platform Eng | DevOps Lead | SRE |
|-----------|-------------|-----------|--------------|-------------|-----|
| **Security automation (SAST/DAST)** | **R/A** | C | C | C | I |
| **Vulnerability scanning** | **R/A** | C | C | C | I |
| **Infrastructure security** | **R/A** | **R** | **R** | C | C |
| **Security policies (OPA)** | **R/A** | C | **R** | C | I |
| **Secret management** | **R** | **R** | **R** | **A** | C |
| **Security monitoring** | **R** | I | C | C | **A** |
| **Incident response** | **R** | C | C | **A** | **R** |

---

### 4.2 Compliance & Governance

| Actividad | Security Eng | Enterprise Arch | Eng Manager | Legal/DPO | Auditor (ext) |
|-----------|-------------|-----------------|-------------|-----------|---------------|
| **SOC2 compliance** | **R** | C | **A** | C | **A** (audit) |
| **GDPR compliance (tech)** | **R** | C | **A** | **A** (legal) | I |
| **ISO27001** | **R** | C | **A** | C | **A** (audit) |
| **Compliance audits** | **R** | C | **A** | C | **R** (auditor) |
| **Security assessments** | **R/A** | C | C | I | I |
| **Policy documentation** | **R** | C | C | **A** | I |
| **Training delivery** | **R** | I | **A** | I | I |

---

### 4.3 Data Privacy

| Actividad | Security Eng | Data Architect | Backend Dev | Legal/DPO | PM |
|-----------|-------------|----------------|-------------|-----------|-----|
| **Data retention policies** | C | **R/A** | C | **A** (legal) | C |
| **Right to be forgotten (impl)** | C | **R** | **R** | **A** | C |
| **Data anonymization** | C | **R/A** | **R** | C | I |
| **Consent management (tech)** | C | I | **R/A** | C | **A** |
| **Privacy policy (legal)** | I | I | I | **R/A** | C |
| **GDPR compliance audits** | **R** | C | I | **A** | I |

---

## 5. Incident Management

### 5.1 Incident Response

| Actividad | SRE | Tech Lead | DevOps Lead | Eng Manager | PM |
|-----------|-----|-----------|-------------|-------------|-----|
| **On-call rotation** | **R/A** | **R** | **A** | C | I |
| **Incident detection** | **R/A** | I | C | I | I |
| **Incident commander** | **R** | C | **A** (escalation) | C | I |
| **Incident response** | **R** | **R** | C | **A** | I |
| **Rollback decision** | **R** | C | **A** | C | C |
| **Communication (internal)** | **R** | C | **A** | C | I |
| **Status page updates** | **R** | I | C | **A** | I |

---

### 5.2 Post-Incident

| Actividad | SRE | Tech Lead | Backend Dev | Eng Manager | PM | Customer Success |
|-----------|-----|-----------|-------------|-------------|-----|------------------|
| **Postmortem** | **R** | **R** | C | **A** | C | I |
| **Root cause analysis** | **R** | **R** | **R** (if code bug) | **A** | I | I |
| **Action items** | **R** | **R** | C | **A** | I | I |
| **Retrospective** | **R** | C | C | **A** | I | I |
| **Customer communication** | C | I | I | C | **R/A** | **R** |
| **Customer compensation** | I | I | I | C | **A** | **R** |

---

## 6. Performance & Quality

### 6.1 Performance Optimization

| Actividad | Backend Dev | Frontend Dev | SRE | Tech Lead | Data Architect |
|-----------|-------------|--------------|-----|-----------|----------------|
| **Application performance** | **R/A** | **R/A** | C | **A** | I |
| **Database optimization** | **R/A** | I | C | C | **R** (schema) |
| **Query optimization** | **R/A** | I | C | C | **A** |
| **Frontend performance** | I | **R/A** | C | C | I |
| **Load testing** | **R** | C | **A** | C | I |
| **Performance profiling** | **R/A** | **R/A** | C | **A** | I |
| **Performance budgets** | C | C | C | **R/A** | I |
| **CDN optimization** | C | **R** | **A** (Cloud Eng) | I | I |

---

### 6.2 Quality Assurance

| Actividad | QA Eng | Developers | Tech Lead | PO | Security Eng |
|-----------|--------|------------|-----------|----|--------------| 
| **Test strategy** | **R/A** | C | **A** | I | I |
| **Unit testing** | C | **R/A** | C (review) | I | I |
| **Integration testing** | **R** | **R** | **A** | I | I |
| **E2E testing** | **R/A** | C | C | C | I |
| **Manual testing** | **R/A** | I | C | C | I |
| **UAT** | **R** | I | C | **A** | I |
| **Performance testing** | **R** | **R** | **A** | I | I |
| **Security testing** | C | I | C | I | **R/A** |
| **Accessibility testing** | **R/A** | C | C | C (UX) | I |
| **Test automation** | **R/A** | C | **A** | I | I |

---

## 7. Onboarding & Training

### 7.1 New Hire Onboarding

| Actividad | Eng Manager | Tech Lead | Sr Developer | HR | PM |
|-----------|-------------|-----------|--------------|----|----|
| **Onboarding plan** | **R/A** | C | I | C | I |
| **Buddy assignment** | **R** | **A** | **R** (buddy) | I | I |
| **Access provisioning** | **R** | I | I | C | I |
| **Codebase tour** | C | **R/A** | **R** | I | I |
| **Team introductions** | **R** | **R** | C | C | **R** (PM intro) |
| **First task assignment** | C | **R/A** | C | I | I |
| **30/60/90 day check-ins** | **R/A** | C | I | C | I |

---

### 7.2 Training & Development

| Actividad | Eng Manager | Tech Lead | Sr Developer | L&D Specialist* | PM |
|-----------|-------------|-----------|--------------|-----------------|-----|
| **L&D budget ownership** | **R/A** | C | I | I | I |
| **Skills gap analysis** | **R/A** | C | I | **R*** | I |
| **Training programs** | **A** | C | C | **R/A*** | I |
| **Tech talks** (internal) | **R** (facilitate) | **R** (speak) | **R** | **A*** | C |
| **Lunch & learns** | **R** | **R** | **R** | **A*** | C |
| **External training** | **A** (approve) | C | I | **R*** (coordinate) | I |
| **Certifications** | **A** (budget) | C | **R** | I | I |
| **Mentorship program** | **A** | **R** | **R** | I | I |

*Si no hay L&D Specialist: Eng Manager = R/A

---

## 8. Data Privacy & GDPR

### 8.1 GDPR Implementation

| Actividad | Data Architect | Backend Dev | Security Eng | Legal/DPO | PM |
|-----------|----------------|-------------|--------------|-----------|-----|
| **Data mapping** | **R/A** | C | C | **A** | I |
| **Data retention** | **R/A** | C | C | **A** (legal) | C |
| **Right to access** (export) | **R** | **R** | C | **A** | C |
| **Right to be forgotten** | **R** | **R** | C | **A** | C |
| **Data anonymization** | **R/A** | **R** | C | C | I |
| **Consent management** | C | **R/A** | C | C | **A** |
| **Privacy policy** | I | I | I | **R/A** | C |
| **GDPR audits** | **R** | I | **R** | **A** | I |

---

## 📋 Cómo Usar Estas Matrices

### Paso 1: Adaptar a tu organización

- ✅ Añade/elimina roles según tu estructura
- ✅ Ajusta R/A/C/I según tus procesos
- ✅ Valida con team leads

---

### Paso 2: Resolver conflictos

Si hay múltiples "A" (Accountable):
- ❌ **Incorrecto**: 2 Accountables → ambigüedad
- ✅ **Correcto**: Solo 1 Accountable por actividad
- 🔧 **Solución**: Escalation hierarchy (e.g., Tech Lead → Eng Manager)

---

### Paso 3: Comunicar y documentar

- ✅ Share en Confluence/Notion
- ✅ Review en All-Hands
- ✅ Update cuando cambien responsabilidades

---

### Paso 4: Revisar trimestralmente

**Preguntas**:
- ¿Responsabilidades claras?
- ¿Bottlenecks por falta de ownership?
- ¿Nuevas actividades sin owner?

---

## 🔗 Links Relacionados

- [Análisis de Gaps](ANALISIS-RESPONSABILIDADES-GAPS.md) - Identificación de vacíos
- [Equipos Overview](equipos/README.md) - Estructura de equipos
- [Workflows](workflows/README.md) - Procesos de trabajo
- [Ceremonias](ceremonias/README.md) - Reuniones y rituales

---

**Mantenido por**: CTO / VP Engineering  
**Última actualización**: Diciembre 2025  
**Próxima revisión**: Marzo 2026