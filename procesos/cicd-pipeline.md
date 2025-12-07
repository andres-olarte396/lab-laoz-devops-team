# CI/CD Pipeline - Proceso Completo

## 📋 Resumen Ejecutivo

**Problema**: Deployments manuales son lentos, propensos a errores, y bloquean a desarrolladores esperando releases.

**Solución**: **Pipeline CI/CD automatizado** que lleva código desde commit hasta producción con validaciones automáticas en cada etapa.

**Beneficio**:

- Deployment Frequency: De semanal → Diaria o múltiple por día
- Lead Time for Changes: De días → Horas
- Change Failure Rate: De 30% → <15%
- Developer velocity: 3x más rápido

---

## 🎯 Pipeline Overview

### Full Pipeline Flow

```
┌─────────────┐
│   COMMIT    │ Developer pushes code
└──────┬──────┘
       ↓
┌─────────────┐
│   BUILD     │ Compile, package
└──────┬──────┘
       ↓
┌─────────────┐
│    TEST     │ Unit, Integration, Security
└──────┬──────┘
       ↓
┌─────────────┐
│  DEPLOY DEV │ Auto-deploy to Dev environment
└──────┬──────┘
       ↓
┌─────────────┐
│ DEPLOY STG  │ Auto-deploy to Staging
└──────┬──────┘
       ↓
┌─────────────┐
│ SMOKE TESTS │ Automated smoke tests on Staging
└──────┬──────┘
       ↓
┌─────────────┐
│  APPROVAL   │ Manual gate (for Production)
└──────┬──────┘
       ↓
┌─────────────┐
│ DEPLOY PROD │ Canary or Blue-Green deployment
└──────┬──────┘
       ↓
┌─────────────┐
│  MONITORING │ Post-deploy monitoring (2h)
└─────────────┘
```

**Duration**: Commit → Production en <2 horas (si aprobado)

---

## 🔀 Branching Strategy

### Git Flow Simplificado

```
main (production)
  ↑
  │ PR + Review
  │
develop (integration)
  ↑
  │ PR + Review
  │
feature/* (developer branches)
```

**Branch Types**:

1. **`main`** (o `master`)

   - Código en producción
   - Siempre deployable
   - Protected branch (no direct commits)
   - Requiere PR + approval + CI passing

2. **`develop`**

   - Integration branch
   - Auto-deploy a Dev environment
   - All features merge aquí primero

3. **`feature/*`**

   - Developer working branches
   - Naming: `feature/JIRA-123-short-description`
   - Short-lived (<3 días idealmente)

4. **`hotfix/*`**

   - Emergency fixes for production
   - Branch from `main`
   - Merge to `main` AND `develop`
   - Naming: `hotfix/JIRA-456-critical-bug`

5. **`release/*`**
   - Release preparation
   - Branch from `develop`
   - Bug fixes only (no new features)
   - Merge to `main` + tag version

---

### Branch Protection Rules

**`main` branch**:

- ✅ Require PR (no direct commits)
- ✅ Require 1+ approvals
- ✅ Require CI checks passing
- ✅ Require branch up-to-date
- ✅ Require signed commits (optional)
- ❌ No force push
- ❌ No delete

**`develop` branch**:

- ✅ Require PR
- ✅ Require CI checks passing
- ❌ No force push

---

## 🏗️ Build Stage

### Trigger

- **Push to any branch** → Build + Test
- **PR creation/update** → Build + Test + Preview environment (optional)

---

### Build Steps

**1. Checkout Code**

```yaml
- uses: actions/checkout@v3
```

**2. Setup Environment**

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v3
  with:
    node-version: "18"
    cache: "npm"
```

**3. Install Dependencies**

```yaml
- run: npm ci # Clean install (faster, reproducible)
```

**4. Compile/Build**

```yaml
- run: npm run build
```

**5. Version Tagging**

- Generate build number: `1.2.3-build-456`
- Commit SHA: First 7 chars `a1b2c3d`
- Tag Docker image: `myapp:1.2.3-a1b2c3d`

---

### Build Artifacts

**Outputs**:

- Docker image (pushed to Container Registry)
- Build artifacts (uploaded to artifact storage)
- Build manifest (version info, dependencies)

**Retention**:

- Dev builds: 7 días
- Staging builds: 30 días
- Production builds: 365 días

---

## 🧪 Test Stage

### Test Pyramid

```
        /\
       /  \  E2E Tests (5%)
      /────\
     /      \  Integration Tests (15%)
    /────────\
   /          \  Unit Tests (80%)
  /────────────\
```

**Test Distribution**:

- **80%**: Unit tests (fast, isolated)
- **15%**: Integration tests (API, DB, services)
- **5%**: E2E tests (UI automation, critical flows)

---

### Test Execution

**1. Linting & Code Quality**

```yaml
- run: npm run lint
- run: npm run prettier:check
```

**Tools**: ESLint, Prettier, SonarQube

**Gates**:

- ❌ Fail if linting errors
- ⚠️ Warn if code smells (SonarQube)

---

**2. Unit Tests**

```yaml
- run: npm run test:unit
```

**Tools**: Jest, Mocha, Pytest (Python), JUnit (Java)

**Coverage Target**: >80%

**Gates**:

- ❌ Fail if tests fail
- ❌ Fail if coverage <70%

---

**3. Integration Tests**

```yaml
- run: npm run test:integration
```

**What's tested**:

- API endpoints (CRUD operations)
- Database interactions
- Third-party service integrations (mocked)

**Duration**: <5 min

---

**4. Security Scans**

**A. Dependency Scanning**

```yaml
- run: npm audit --production
```

**Tools**: `npm audit`, Snyk, Dependabot

**Gates**:

- ❌ Fail if critical vulnerabilities (CVE score >9.0)
- ⚠️ Warn if high vulnerabilities (CVE score 7.0-9.0)

---

**B. Static Application Security Testing (SAST)**

```yaml
- uses: github/codeql-action/analyze@v2
```

**Tools**: CodeQL, SonarQube Security, Checkmarx

**Checks**:

- SQL Injection patterns
- XSS vulnerabilities
- Hardcoded secrets (API keys, passwords)
- Insecure crypto usage

**Gates**:

- ❌ Fail if high/critical security issues

---

**C. Container Image Scanning**

```yaml
- uses: aquasecurity/trivy-action@master
  with:
    image-ref: "myapp:1.2.3"
```

**Tools**: Trivy, Grype, Clair

**Checks**:

- OS-level vulnerabilities
- Outdated base images
- Exposed ports

---

**5. Performance Tests** (Staging only)

```yaml
- run: npm run test:performance
```

**Tools**: Artillery, K6, JMeter

**Metrics**:

- P95 response time <200ms
- Throughput >1000 req/sec
- Error rate <0.1%

**Duration**: 10 min load test

---

## 🚀 Deploy Stage

### Environment Progression

```
feature/* → Dev (auto)
develop → Dev (auto) + Staging (auto)
main → Staging (auto) + Production (manual approval)
```

---

### Deploy to Dev

**Trigger**: Push to `develop` branch (or any feature branch)

**Process**:

```yaml
- name: Deploy to Dev
  run: |
    kubectl set image deployment/myapp \
      myapp=myregistry.azurecr.io/myapp:${IMAGE_TAG} \
      --namespace=dev
```

**No approval needed** (auto-deploy)

**Rollback**: Auto-rollback si health checks fail

---

### Deploy to Staging

**Trigger**: Push to `develop` or `release/*` branch

**Process**:

1. Deploy to Staging environment (mirror de Prod)
2. Run smoke tests automáticamente
3. If smoke tests pass → Ready for Prod deployment
4. If smoke tests fail → Block Prod deployment

**Smoke Tests** (5 min):

- Health check endpoints: `/health`, `/ready`
- Critical user flows: Login, Checkout, Payment
- Database connectivity
- Third-party integrations

**No approval needed** (auto-deploy)

---

### Deploy to Production

**Trigger**: Manual approval (via GitHub Actions, Azure DevOps, etc.)

**Approval Required**:

- **Who**: DevOps Lead or Release Manager
- **When**: During business hours (9am-5pm) o maintenance window
- **Exceptions**: Hotfix (emergency) can deploy anytime

**Deployment Strategy**: Canary or Blue-Green (ver [Deployment Procedures](./deployment-procedures.md))

---

**Production Deployment Process**:

**1. Pre-Deployment Checks**

```yaml
- name: Pre-flight checks
  run: |
    # Check if Staging is healthy
    curl -f https://staging.myapp.com/health || exit 1

    # Check if on-call engineer is available
    # Check if no major incidents ongoing
```

**2. Deploy (Canary)**

```yaml
- name: Deploy Canary (10% traffic)
  run: |
    kubectl set image deployment/myapp-canary \
      myapp=myregistry.azurecr.io/myapp:${IMAGE_TAG}
```

**3. Monitor Canary (30 min)**

- Error rate <0.5%
- P95 latency <300ms
- No alerts triggered

**4. Promote to 100%**

```yaml
- name: Promote to 100%
  run: |
    kubectl set image deployment/myapp \
      myapp=myregistry.azurecr.io/myapp:${IMAGE_TAG}
```

**5. Post-Deployment Monitoring (2h)**

- Monitor dashboards
- Watch for alerts
- On-call engineer on standby

---

### Rollback Procedures

**Auto-Rollback Triggers**:

- Health checks fail >3 consecutive times
- Error rate >5% for >5 min
- P95 latency >1000ms for >5 min

**Manual Rollback**:

```bash
# Rollback to previous version
kubectl rollout undo deployment/myapp --namespace=production

# Or rollback to specific version
kubectl rollout undo deployment/myapp --to-revision=42
```

**Rollback Time Target**: <5 min

---

## 🔐 Automated Gates

### Quality Gates (Must Pass to Proceed)

| Gate                    | Threshold           | Action if Fail                    |
| ----------------------- | ------------------- | --------------------------------- |
| **Unit Tests**          | 100% passing        | ❌ Block merge                    |
| **Code Coverage**       | >70%                | ❌ Block merge                    |
| **Linting**             | 0 errors            | ❌ Block merge                    |
| **Security Scan**       | 0 critical CVEs     | ❌ Block merge                    |
| **Integration Tests**   | 100% passing        | ❌ Block deploy to Staging        |
| **Smoke Tests**         | 100% passing        | ❌ Block deploy to Production     |
| **Performance Tests**   | P95 <200ms          | ⚠️ Warn (manual decision)         |
| **Canary Health Check** | Error rate <0.5%    | ❌ Auto-rollback                  |
| **Approval**            | 1+ DevOps Lead      | ❌ Block deploy to Production     |
| **Deployment Window**   | Business hours / MW | ⚠️ Warn (override for emergencies |

---

## 📊 Pipeline Metrics

### DORA Metrics

**1. Deployment Frequency**

- **Target**: Diaria (>1 deploy/day)
- **Current**: Track via CI/CD logs

**2. Lead Time for Changes**

- **Target**: <4 horas (commit → production)
- **Current**: Measure time from first commit to deploy

**3. Mean Time to Recovery (MTTR)**

- **Target**: <1 hora
- **Current**: Time from incident detection to rollback/fix deployed

**4. Change Failure Rate**

- **Target**: <15%
- **Current**: % of deploys que requieren rollback o hotfix

---

### Pipeline Health Metrics

| Metric                       | Target  | How to Measure                       |
| ---------------------------- | ------- | ------------------------------------ |
| **Pipeline Success Rate**    | >90%    | (Successful runs / Total runs)       |
| **Average Pipeline Runtime** | <30 min | Time from commit to deploy to Dev    |
| **Flaky Test Rate**          | <5%     | Tests that fail/pass intermittently  |
| **Build Failure Root Cause** | Track   | Categorize: Code, Infra, Flaky Tests |
| **Rollback Rate**            | <10%    | % of Prod deploys that rollback      |

---

## 🛠️ Tools & Technologies

### CI/CD Platform

**Options**:

- GitHub Actions (Recommended for GitHub-hosted repos)
- Azure DevOps Pipelines
- GitLab CI/CD
- Jenkins (legacy, migrar a cloud-native)

---

### Infrastructure as Code (IaC)

**Tools**:

- Terraform (multi-cloud)
- Bicep / ARM Templates (Azure)
- Pulumi (code-first IaC)

**Pipeline Integration**:

- IaC changes go through same CI/CD pipeline
- `terraform plan` on PR
- `terraform apply` on merge to main

---

### Container Registry

**Options**:

- Azure Container Registry (ACR)
- Docker Hub
- Amazon ECR
- Google Container Registry (GCR)

**Image Tagging Strategy**:

```
myapp:latest                   # Latest successful build
myapp:1.2.3                    # Semantic version
myapp:1.2.3-a1b2c3d            # Version + Git SHA
myapp:1.2.3-build-456          # Version + Build number
myapp:dev-latest               # Dev environment latest
myapp:staging-20250115-1430    # Staging environment snapshot
```

---

### Orchestration

**Kubernetes** (Recommended):

- Azure Kubernetes Service (AKS)
- Amazon EKS
- Google GKE

**Deployment Tools**:

- `kubectl` (CLI)
- Helm (package manager)
- Flux / ArgoCD (GitOps)

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                       | Developer | DevOps | Tech Lead | Manager |
| ------------------------------- | --------- | ------ | --------- | ------- |
| Escribir código                 | R         | C      | A         | I       |
| Crear PR                        | R/A       | C      | C         | I       |
| Code review                     | C         | C      | R/A       | I       |
| Aprobar merge a develop         | R         | C      | A         | I       |
| Fix pipeline failures           | R         | C/A    | C         | I       |
| Deploy to Dev/Staging           | I         | R/A    | C         | I       |
| Aprobar deploy to Production    | I         | R/A    | C         | I       |
| Monitorear post-deploy          | C         | R/A    | C         | I       |
| Rollback si falla               | C         | R/A    | C         | I       |
| Mantener pipeline configuration | C         | R/A    | C         | I       |
| Optimizar pipeline performance  | C         | R/A    | C         | I       |

**Legend**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 🚀 Implementation Roadmap

### Fase 1: Basic CI (Sprint 0-1)

**Goal**: Automated build + test on every commit

- [ ] Setup GitHub Actions / Azure Pipelines
- [ ] Implement build stage (compile, package)
- [ ] Implement unit tests
- [ ] Configure branch protection rules
- [ ] Auto-deploy to Dev environment

**Success Criteria**:

- Every commit triggers CI
- Unit tests run automatically
- Build artifacts stored

---

### Fase 2: Automated Testing (Sprint 2-3)

**Goal**: Comprehensive test coverage

- [ ] Add integration tests
- [ ] Add security scans (SAST, dependency scan)
- [ ] Add code coverage reports
- [ ] Configure quality gates (>70% coverage, 0 critical CVEs)
- [ ] Flaky test detection

**Success Criteria**:

- Test coverage >70%
- 0 critical security vulnerabilities
- <5% flaky test rate

---

### Fase 3: Automated Deployment (Sprint 4-6)

**Goal**: Auto-deploy to Dev + Staging

- [ ] Auto-deploy to Dev on `develop` branch
- [ ] Auto-deploy to Staging on `main` branch
- [ ] Implement smoke tests for Staging
- [ ] Configure rollback automation
- [ ] Setup deployment notifications (Slack)

**Success Criteria**:

- Develop → Dev (auto, <10 min)
- Main → Staging (auto, <15 min)
- Smoke tests passing >95%

---

### Fase 4: Production Pipeline (Sprint 7-9)

**Goal**: Safe, repeatable Production deployments

- [ ] Implement approval gate for Production
- [ ] Configure Canary deployment strategy
- [ ] Setup post-deployment monitoring (2h)
- [ ] Implement auto-rollback on failure
- [ ] Document runbooks

**Success Criteria**:

- Production deploys diarios
- Rollback time <5 min
- Change failure rate <15%

---

### Fase 5: Optimization (Sprint 10+)

**Goal**: Fast, reliable pipeline

- [ ] Optimize test suite (parallel execution)
- [ ] Implement test result caching
- [ ] Configure incremental builds
- [ ] Add performance tests (load testing)
- [ ] Implement blue-green deployment (alternative to Canary)

**Success Criteria**:

- Pipeline runtime <20 min (commit → Dev)
- Flaky test rate <2%
- Deployment frequency >2/day

---

## ✅ Success Criteria

### Mes 1 (Post-Implementation)

- ✅ CI pipeline running on every commit
- ✅ Auto-deploy to Dev working
- ✅ Unit tests + linting automated
- ✅ Build success rate >85%

### Mes 2-3

- ✅ Auto-deploy to Staging working
- ✅ Smoke tests automated
- ✅ Security scans integrated
- ✅ Deployment frequency >3/week

### Mes 4+

- ✅ Production deployments diarios
- ✅ Lead time <4 horas
- ✅ MTTR <1 hora
- ✅ Change failure rate <15%
- ✅ Pipeline success rate >90%

---

## 🔗 Links Relacionados

- [Deployment Procedures](./deployment-procedures.md) - Canary, Blue-Green, Rolling deployments
- [Incident Management](./incident-management.md) - Rollback procedures
- [Monitoring & Alerting](./monitoring-alerting.md) - Post-deploy monitoring

---

## 📚 Antipatterns (Evitar)

### ❌ Antipattern #1: Manual Steps in Pipeline

**Problema**: Pipeline requiere intervención manual (ej: "Run script X manualmente antes de deploy")

**Por qué es malo**: Rompe automatización, introduces errores humanos, no es repetible

**Solución**: Automatizar TODO. Si no puede automatizarse, documentar como issue y crear workaround temporal.

---

### ❌ Antipattern #2: Long-Running Pipelines

**Problema**: Pipeline tarda >1 hora en completar

**Por qué es malo**: Developers esperan demasiado, pierden contexto, feedback loop lento

**Solución**:

- Paralelizar tests
- Cachear dependencies (`npm ci` con cache)
- Ejecutar tests E2E solo en Staging, no en cada commit
- Incremental builds

---

### ❌ Antipattern #3: Flaky Tests Ignored

**Problema**: "Test X falla a veces, pero lo ignoramos y re-corremos el pipeline"

**Por qué es malo**: Erosiona confianza en pipeline, developers ignoran fallos reales

**Solución**:

- Flaky test detection (track tests que fail/pass intermittently)
- Fix or quarantine flaky tests (skip temporalmente, pero fijar en <1 semana)
- Root cause analysis (network timeouts, race conditions, etc.)

---

### ❌ Antipattern #4: No Rollback Plan

**Problema**: Deploy falla en Prod, no hay rollback automatizado, team scrambles

**Por qué es malo**: MTTR alto (>1 hora), panic mode, potential data loss

**Solución**:

- Auto-rollback on health check failure
- One-click manual rollback button
- Practice rollback drills (quarterly)

---

### ❌ Antipattern #5: "Works on My Machine"

**Problema**: Código funciona localmente pero falla en CI

**Por qué es malo**: Pierdes tiempo debugging, otros developers bloqueados

**Solución**:

- Docker containers para environments consistentes
- Developers corren CI localmente antes de push: `act` (GitHub Actions locally)
- Lock dependency versions (`package-lock.json`, `requirements.txt`)

---

### ❌ Antipattern #6: Deploy Fridays 5pm

**Problema**: "Let's deploy this big feature Friday evening before weekend"

**Por qué es malo**: Si algo falla, arruinas weekend del team, limited support availability

**Solución**:

- Deployment freeze: No deploys Fridays después de 2pm (a menos que hotfix crítico)
- Deploy early week (Martes-Jueves) para tener tiempo de monitorear

---

### ❌ Antipattern #7: No Monitoring Post-Deploy

**Problema**: Deploy to Prod, everyone goes home, nadie monitorea

**Por qué es malo**: Incidents no detectados hasta que users reportan

**Solución**:

- Mandatory 2h post-deploy monitoring
- On-call engineer stays available
- Automated alerts for anomalies (error rate spike, latency spike)

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-06  
**Owner**: DevOps Lead  
**Review Cycle**: Trimestral
