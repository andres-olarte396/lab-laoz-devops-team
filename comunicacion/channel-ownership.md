# Channel Ownership - Responsables de Canales de Comunicación

## 📋 Resumen Ejecutivo

**Problema**: Canales sin dueño → Se llenan de spam, información importante se pierde, nadie hace cleanup, nuevos miembros no saben qué postear dónde.

**Solución**: **Channel ownership model** con responsables claros, moderación activa, cleanup regular, y guías de uso.

**Beneficio**:
- Canales organizados y on-topic (fácil encontrar información)
- Moderación consistente (sin spam, trolling, off-topic)
- Cleanup regular (se archivan threads antiguos)
- Onboarding claro (cada canal tiene propósito definido)

---

## 🎯 Responsabilidades del Channel Owner

### Owner Responsibilities

**Daily** (5 min):
- Revisar mensajes nuevos
- Responder preguntas críticas o redirigir al experto
- Eliminar spam o contenido off-topic

**Weekly** (15 min):
- Pin mensajes importantes (decisiones, anuncios)
- Unpin mensajes antiguos (>2 semanas)
- Actualizar channel topic si hay cambios

**Monthly** (30 min):
- Revisar channel guidelines (¿siguen siendo claros?)
- Cleanup de threads resueltos (archive/delete)
- Feedback de miembros (¿el canal funciona bien?)

**Quarterly** (1 hora):
- Audit completo del canal
- Revisar members (¿alguien ya no debería estar?)
- Actualizar channel description
- Proponer mejoras

---

## 📢 Channel Ownership Matrix

### Canales Técnicos

#### #engineering

**Owner**: Engineering Manager  
**Backup**: Senior Tech Lead (rotation mensual)  
**Members**: Todos en Engineering (Development, DevOps, QA)  
**Size**: 50-200 personas (Enterprise)

**Purpose**:
- Anuncios importantes de Engineering (all-hands, cambios organizacionales)
- Discusiones de estrategia técnica (tech stack, arquitectura)
- Engineering metrics y KPIs (velocity, DORA metrics)
- Celebraciones de equipo (milestones, wins)

**NOT for**:
- ❌ Preguntas técnicas específicas (usar #development o #devops)
- ❌ Code reviews (usar #development)
- ❌ Incident response (usar #incidents)
- ❌ Day-to-day updates (usar daily standup)

**Guidelines**:
- Keep signal-to-noise ratio high (no memes, off-topic)
- Use threads for discussions (keep main channel clean)
- @channel solo para urgent announcements (SEV-1 incidents, all-hands)
- @here para time-sensitive pero no critical (deadline reminders)

**Moderator Actions**:
- Move off-topic discussions a #random
- Remind sobre uso de threads
- Pin decisiones importantes (ADRs, tech standards)

---

#### #development

**Owner**: Tech Lead (rotation mensual entre Tech Leads)  
**Backup**: Senior Developer  
**Members**: Developers (Frontend, Backend, Full-Stack, Mobile), QA  
**Size**: 30-150 personas

**Purpose**:
- Preguntas técnicas (code, debugging, best practices)
- Code review requests (PRs que necesitan atención)
- RFCs (Request for Comments) para decisiones técnicas
- Compartir aprendizajes (TIL - Today I Learned)
- Tech talks y recursos (artículos, videos, cursos)

**NOT for**:
- ❌ Deployments (usar #deployments)
- ❌ Incidents (usar #incidents)
- ❌ Product decisions (usar #product)
- ❌ Infraestructura (usar #devops)

**Guidelines**:
- Code snippets: Usar backticks ``` o pastebin para >10 líneas
- Code reviews: Link al PR, no copiar código completo
- Preguntas: Incluir contexto (qué intentas hacer, qué ya probaste)
- RFCs: Formato estándar (Problem, Proposed Solution, Alternatives, Decision)

**Moderator Actions**:
- Facilitar code reviews (si PR lleva >2 días sin review → ping reviewers)
- Mantener technical standards (enforce RFC format)
- Cleanup de threads resueltos (cada viernes)

**Template de RFC**:
```markdown
## RFC: [Título claro y descriptivo]

**Author**: @username
**Date**: YYYY-MM-DD
**Status**: Draft | Under Review | Accepted | Rejected

### Problem
[¿Qué problema estamos resolviendo?]

### Proposed Solution
[¿Cómo lo resolveremos?]

### Alternatives Considered
[¿Qué otras opciones evaluamos y por qué no las elegimos?]

### Decision
[¿Qué decidimos hacer? Owner + deadline]

### Discussion
[Thread para comentarios]
```

---

#### #devops

**Owner**: DevOps Lead / SRE Lead  
**Backup**: On-call DevOps Engineer (weekly rotation)  
**Members**: DevOps, SREs, Backend Developers, Tech Leads  
**Size**: 10-50 personas

**Purpose**:
- Infraestructura changes (Kubernetes upgrades, AWS changes)
- Deployment coordination (maintenance windows, rollbacks)
- Incident response (SEV-2/SEV-3, SEV-1 tiene su propio canal)
- Performance issues (latency, scaling)
- Monitoring y alerting (Datadog, Prometheus)
- Post-mortems de incidentes

**NOT for**:
- ❌ Application code bugs (usar #development)
- ❌ Product features (usar #product)
- ❌ SEV-1 incidents (crear canal dedicado #incident-YYYY-MM-DD)

**Guidelines**:
- Maintenance windows: Anunciar con 48 horas de anticipación
- Deployments: Usar thread para cada deploy (status updates)
- Incidents: Crear thread dedicado, postear updates cada 30 min (SEV-2)
- Runbooks: Link a runbook relevante cuando alguien pregunta cómo hacer algo

**Moderator Actions**:
- Coordinar incident response (asignar Incident Commander)
- Post-mortem follow-up (asegurar que se completan)
- Cleanup de threads de incidentes resueltos (archive after 1 week)
- Pin runbooks actualizados

**Incident Response Template** (thread):
```markdown
🚨 **Incident**: [Brief description]

**Severity**: SEV-2 (High)
**Started**: YYYY-MM-DD HH:MM UTC
**Impact**: [Affected users/services]
**Incident Commander**: @username

**Timeline**:
- HH:MM: Incident detected
- HH:MM: Investigation started
- HH:MM: Root cause identified
- HH:MM: Fix deployed
- HH:MM: Monitoring for stability

**Status**: Investigating | Mitigating | Resolved

**Next Update**: In 30 minutes
```

---

#### #qa

**Owner**: QA Lead  
**Backup**: Senior QA Engineer  
**Members**: QA Engineers, Developers  
**Size**: 5-20 personas

**Purpose**:
- Test plans y test cases
- Bug reports (antes de crear Jira ticket)
- Testing blockers (ambientes down, test data issues)
- Automation strategies (frameworks, CI/CD integration)
- Quality metrics (test coverage, bug trends)

**NOT for**:
- ❌ Product requirements (usar #product)
- ❌ Deployments (usar #deployments)
- ❌ Code reviews (usar #development)

**Guidelines**:
- Bug reports: Reproducible steps, screenshots, logs
- Test blockers: Tag developer/DevOps responsable
- Automation wins: Compartir cuando automatizas test manual

---

### Canales de Producto

#### #product

**Owner**: Head of Product o Product Manager Senior  
**Backup**: Product Owner  
**Members**: Product Managers, Product Owners, Developers, Designers, Stakeholders  
**Size**: 20-100 personas

**Purpose**:
- Roadmap discussions (próximos quarters)
- Feature prioritization (qué construir primero)
- User feedback (voz del cliente)
- Product analytics (métricas de uso, conversión)
- Go-to-market coordination (launches, releases)

**NOT for**:
- ❌ Technical implementation (usar #development)
- ❌ Design reviews (usar #design)
- ❌ Customer support issues (usar #customer-feedback)

**Guidelines**:
- Roadmap changes: Notificar con contexto (por qué cambiamos prioridad)
- User feedback: Incluir data (cuántos usuarios piden esto, impacto en revenue)
- Feature requests: Usar formato estándar (Problem, User Impact, Proposed Solution)

**Moderator Actions**:
- Facilitar roadmap discussions (evitar que se conviertan en debates infinitos)
- Priorización: Usar voting threads cuando hay desacuerdo
- Pin roadmap actualizado (quarterly)

---

#### #design

**Owner**: Design Lead (UX o Product Designer principal)  
**Backup**: Senior UX Researcher  
**Members**: Designers (UX, UI, Product), Developers (Frontend), Product Managers  
**Size**: 10-40 personas

**Purpose**:
- Design critiques (feedback en designs)
- Design system updates (nuevos componentes)
- User research shareouts (insights de usuarios)
- Design resources (Figma templates, design tools)

**NOT for**:
- ❌ Code implementation (usar #development)
- ❌ Product decisions (usar #product)

**Guidelines**:
- Design critiques: Constructive feedback only
- Figma links: Always include context (qué feedback necesitas)
- Design system: Major changes requieren RFC

---

### Canales de Procesos

#### #deployments

**Owner**: DevOps Lead  
**Backup**: On-call DevOps Engineer  
**Members**: DevOps, Developers, QA  
**Size**: 20-80 personas

**Purpose**:
- Deployment notifications (qué se deployó, cuándo)
- Deployment status (in-progress, completed, rolled back)
- Release notes (qué features/fixes incluye)

**NOT for**:
- ❌ Incidents (usar #incidents o #devops)
- ❌ Code reviews (usar #development)

**Guidelines**:
- Automated bot posts (CI/CD integración)
- Manual posts: Usar template estándar
- Read-only para developers (solo DevOps/release managers postean)

**Deployment Template**:
```markdown
🚀 **Deployment**: [Service Name] v[Version]

**Environment**: Production
**Started**: YYYY-MM-DD HH:MM UTC
**Completed**: YYYY-MM-DD HH:MM UTC
**Deployed by**: @username

**Changes**:
- Feature: User can reset password
- Fix: Bug in checkout flow
- Chore: Upgrade Node.js to 20.x

**Release Notes**: [Link to GitHub release or Confluence]

**Rollback Plan**: `kubectl rollout undo deployment/myapp`

**Status**: ✅ Deployed | ⚠️ Monitoring | ❌ Rolled Back
```

---

#### #incidents

**Owner**: DevOps Lead / SRE Lead  
**Backup**: On-call rotation  
**Members**: DevOps, SREs, Tech Leads, Engineering Manager  
**Size**: 15-50 personas

**Purpose**:
- Incident notifications (SEV-2, SEV-3)
- Incident updates (para SEV-1, crear canal dedicado)
- Post-mortem links

**NOT for**:
- ❌ SEV-1 incidents (crear #incident-YYYY-MM-DD-description)
- ❌ Development questions (usar #development)

**Guidelines**:
- SEV-1: Create dedicated channel immediately
- SEV-2/SEV-3: Post updates in thread
- Post-mortem: Link a doc cuando esté completo

**SEV-1 Channel Creation**:
```bash
# Nombre: #incident-2025-12-07-login-outage
# Members: IC, DevOps, Tech Leads, EM, PM, CTO (if needed)
# Purpose: War room para resolver incident
# Archive: 1 semana después de resolved
```

---

#### #on-call

**Owner**: DevOps Lead / SRE Lead  
**Backup**: Current on-call engineer  
**Members**: On-call rotation (DevOps, SREs, Senior Developers)  
**Size**: 10-30 personas

**Purpose**:
- On-call schedule (quién está on-call esta semana)
- On-call handoff (pasar contexto a próximo on-call)
- Runbook updates (mejorar documentación post-incident)
- On-call wins (incidentes resueltos rápido)

**NOT for**:
- ❌ Incidents (usar #incidents o crear canal dedicado)
- ❌ General DevOps questions (usar #devops)

**Guidelines**:
- Handoff template: Qué pasó esta semana, issues conocidos, follow-ups
- Runbook updates: Link al PR que actualiza runbook

**On-Call Handoff Template**:
```markdown
## On-Call Handoff - Week of YYYY-MM-DD

**Outgoing**: @alice
**Incoming**: @bob

### Incidents This Week
- SEV-2: Database slowdown (resolved, post-mortem pending)
- SEV-3: S3 bucket full (resolved, increased quota)

### Known Issues
- Staging environment is slower than usual (investigating)
- Monitoring alert for disk space (non-critical, monitoring)

### Follow-Ups
- [ ] Complete post-mortem for database incident (due Friday)
- [ ] Update runbook for S3 quota increase

### Questions?
Ping me @alice if you need context on anything.
```

---

### Canales de Seguridad (NUEVO)

#### #security-private

**Type**: 🔒 Private Channel  
**Owner**: CTO o Security Engineer  
**Backup**: DevOps Lead  
**Members**: CTO, VP Engineering, Security Engineer, DevOps Lead, Tech Leads (read-only)  
**Size**: 5-15 personas

**Purpose**:
- Reportar vulnerabilidades (CVEs, security scans)
- Discutir patches y remediations (sin exponer detalles públicamente)
- Compliance updates (GDPR, HIPAA, SOC2)
- Security audits y penetration tests
- Incident response para security breaches

**NOT for**:
- ❌ Security awareness general (usar #security público)
- ❌ Tool updates (1Password, SSO) (usar #security público)

**Guidelines**:
- Vulnerabilidades críticas: Report en <1 hora
- Vulnerabilidades altas: Report en <24 horas
- No compartir detalles en canales públicos hasta que estén patcheadas
- Post-mortem required para todos los security incidents

**Vulnerability Report Template**:
```markdown
🔐 **Vulnerability Report**

**Severity**: Critical | High | Medium | Low
**CVE**: CVE-YYYY-XXXXX (si aplica)
**Affected Systems**: [Lista de servicios/repos]
**Discovered**: YYYY-MM-DD
**Reported by**: @username o External researcher

**Description**:
[Qué vulnerabilidad, cómo puede ser explotada]

**Impact**:
[Qué data puede ser accedida, qué sistemas comprometidos]

**Remediation Plan**:
- [ ] Patch available? [Link to patch]
- [ ] Timeline: Deploy within X hours/days
- [ ] Owner: @username

**Status**: Investigating | Patching | Resolved
```

---

#### #security

**Type**: Public Channel  
**Owner**: Security Engineer (si existe) o DevOps Lead  
**Backup**: Senior Developer  
**Members**: Todos (Engineering, Product, Design)  
**Size**: 50-200 personas

**Purpose**:
- Security awareness (training, tips, best practices)
- Tool updates (1Password, SSO, VPN)
- Security best practices (password hygiene, phishing awareness)
- General security discussions (NO vulnerabilities específicas)

**NOT for**:
- ❌ Vulnerabilidades específicas (usar #security-private)
- ❌ Compliance confidencial (usar #security-private)

**Guidelines**:
- Educational content (compartir artículos, videos)
- Security tips (cómo usar 1Password, habilitar MFA)
- Phishing alerts (si alguien recibe phishing email, avisar a todos)

---

### Canales para Stakeholders Externos (NUEVO)

#### #product-updates

**Type**: Public, Read-Only para no-tech  
**Owner**: Product Manager  
**Backup**: Product Owner  
**Posting Rights**: PM, Engineering Manager  
**Subscribers**: Sales, Marketing, Customer Success, Executives  
**Size**: 30-150 personas

**Purpose**:
- Comunicar releases y roadmap a stakeholders no-técnicos
- Release notes en lenguaje de negocio (no técnico)
- Roadmap preview (próximas 2-4 semanas)
- Known issues y workarounds

**Frequency**: Semanal (viernes)

**Template**:
```markdown
## Product Updates - Week of YYYY-MM-DD

### 🚀 Shipped This Week
- **Feature**: User can reset password via email
  - **Impact**: Reduces support tickets by ~20%
  - **Available**: All users as of Friday 5pm

- **Fix**: Checkout flow bug on mobile
  - **Impact**: Fixes issue affecting 5% of mobile users

### 🔮 Coming Next (Next 2-4 Weeks)
- Multi-factor authentication (MFA)
- Dark mode for mobile app
- Export to CSV feature

### ⚠️ Known Issues
- Search is slower than usual (investigating, ETA: next week)

### ❓ Questions?
Contact @product-team or reply in thread
```

---

#### #customer-feedback

**Type**: Public  
**Owner**: Customer Success Lead  
**Backup**: Product Manager  
**Posting Rights**: Sales, CS, Support  
**Subscribers**: Product, Engineering, Design  
**Size**: 30-100 personas

**Purpose**:
- Centralizar feedback de clientes
- Feature requests (voz del cliente)
- Bug reports from customers
- Trends en customer pain points

**Process**:
- CS postea top 5 customer requests (mensual)
- Product Manager triages y responde (dentro de 1 semana)
- Critical bugs escalados a #development inmediatamente

**Template**:
```markdown
## Customer Feedback - [Customer Name or Segment]

**Source**: Sales call | Support ticket | User interview
**Customer**: [Name/Company] (Enterprise | SMB | Individual)
**Priority**: High | Medium | Low

**Feedback**:
[Qué dijo el cliente, copy-paste si posible]

**Impact**:
[Cuántos clientes afectados, revenue en riesgo, churn risk]

**Product Team**: Please triage 👇
```

---

#### #sales-engineering

**Type**: Private Channel  
**Owner**: Sales Engineering Lead  
**Backup**: Solution Architect  
**Members**: Sales Engineers, Solution Architects, Tech Leads  
**Size**: 10-30 personas

**Purpose**:
- Coordinar entre Sales y Engineering
- RFPs (Request for Proposals) técnicos
- Customer demos (technical feasibility)
- Custom integrations (scoping)

**NOT for**:
- ❌ Product roadmap (usar #product)
- ❌ General sales questions (usar #sales)

**Guidelines**:
- RFPs: Incluir deadline, customer name, deal size
- Custom integrations: Consultar con Tech Lead antes de prometer

---

## 🧹 Channel Cleanup Process

### Monthly Cleanup (30 min)

**Owner responsibilities**:

1. **Review pinned messages** (unpin antiguos >1 mes)
2. **Archive resolved threads** (issues/questions ya resueltos)
3. **Update channel topic** (si cambió propósito o guidelines)
4. **Check member list** (remover gente que ya no debería estar)

### Quarterly Cleanup (1 hora)

1. **Full audit**:
   - ¿El canal sigue siendo necesario?
   - ¿El propósito sigue siendo claro?
   - ¿Hay overlap con otros canales?

2. **Propose changes**:
   - Merge canales si hay overlap
   - Archive canales sin actividad (>3 meses sin posts)
   - Split canales si están muy llenos (>100 posts/día)

3. **Update documentation**:
   - Actualizar este doc si cambian owners o guidelines
   - Comunicar cambios a miembros

### Archive Criteria

**Archive un canal si**:
- ✅ No activity en >3 meses
- ✅ Propósito ya no es relevante (proyecto terminó)
- ✅ Merged con otro canal
- ✅ Todos los members se fueron (empty channel)

**Before archiving**:
1. Notificar en canal (1 semana antes)
2. Pin mensaje explicando por qué se archiva
3. Dar tiempo para objections (si alguien usa, no archivar)
4. Archive y post en #general (FYI)

---

## 📊 Channel Health Metrics

### Metrics to Track (Quarterly)

| Metric | Target | Red Flag |
|--------|--------|----------|
| **Channel noise** (off-topic %) | <20% | >40% |
| **Response time** (technical questions) | <4 horas | >1 día |
| **Pin messages** (actualizados) | <30 días | >60 días |
| **Member satisfaction** | >4/5 | <3/5 |
| **Channel topic updated** | <90 días | >180 días |

### Survey Questions (Quarterly)

Send to members:
1. ¿El canal tiene propósito claro? (1-5)
2. ¿Encuentras información útil fácilmente? (1-5)
3. ¿Hay demasiado ruido/spam? (1-5)
4. ¿El owner responde preguntas oportunamente? (1-5)
5. Sugerencias para mejorar:

---

## 🎯 Success Criteria

### Mes 1
- ✅ Owners asignados para todos los canales principales
- ✅ Channel topics actualizados (propósito claro)
- ✅ Guidelines comunicadas a todos los members

### Mes 2-3
- ✅ Monthly cleanup completado (cada mes)
- ✅ Channel noise <30% (medido via survey)
- ✅ Response time <6 horas (preguntas técnicas)

### Mes 4+
- ✅ Quarterly health metrics >4/5 satisfacción
- ✅ <5 complaints por quarter sobre channel noise
- ✅ New hires saben dónde postear (onboarding survey)

---

## 🔗 Links Relacionados

- [Estrategia de Comunicación General](./README.md) - Principios y canales
- [Incident Communication](./incident-communication.md) - Proceso para incidentes críticos
- [Onboarding Guide](./onboarding-guide.md) - Cómo comunicarse (nuevos hires)
- [Escalation Matrix](./escalation-matrix.md) - Cómo escalar issues

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (survey + audit)
