# Deployment Procedures - Estrategias de Despliegue

## 📋 Resumen Ejecutivo

**Problema**: Deployments causan downtime, afectan usuarios, y generan estrés en el equipo ("¿funcionará?").

**Solución**: **Deployment strategies probadas** (Blue-Green, Canary, Rolling) con smoke tests automatizados y rollback en segundos.

**Beneficio**:

- Zero-downtime deployments (99.9% uptime mantenido)
- Risk reducido (gradual rollout, auto-rollback)
- Confidence (deploy any time, no "Friday deployment fear")
- Deployment frequency: De semanal → Diaria

---

## 🎯 Deployment Strategies Overview

### Comparación de Estrategias

| Strategy       | Downtime | Risk   | Complexity | Cost | Use Case                 |
| -------------- | -------- | ------ | ---------- | ---- | ------------------------ |
| **Blue-Green** | Zero     | Low    | Medium     | High | Major releases           |
| **Canary**     | Zero     | Low    | High       | Low  | High-risk changes        |
| **Rolling**    | Zero     | Medium | Low        | Low  | Standard deployments     |
| **Recreate**   | High     | High   | Low        | Low  | Dev/Test only (NOT PROD) |

---

## 🔵🟢 Strategy #1: Blue-Green Deployment

### Concept

**Two identical environments**:

- **Blue**: Current production (serving 100% traffic)
- **Green**: New version (idle, ready to swap)

**Process**:

1. Deploy new version to Green
2. Test Green thoroughly
3. Switch traffic: Blue → Green (instantaneous)
4. Monitor Green
5. If OK: Keep Green, decommission Blue
6. If FAIL: Switch back to Blue (instant rollback)

---

### Architecture

```
┌─────────────┐
│ Load Balancer│
└──────┬───────┘
       │
       │ (100% traffic)
       ↓
┌─────────────┐
│   BLUE      │ ← Current production (v1.2.0)
│ Environment │
└─────────────┘

┌─────────────┐
│   GREEN     │ ← New version (v1.3.0) - idle
│ Environment │
└─────────────┘

--- After Switch ---

┌─────────────┐
│ Load Balancer│
└──────┬───────┘
       │
       │ (100% traffic)
       ↓
┌─────────────┐
│   GREEN     │ ← Now production (v1.3.0)
│ Environment │
└─────────────┘

┌─────────────┐
│   BLUE      │ ← Standby (v1.2.0) - can rollback
│ Environment │
└─────────────┘
```

---

### Implementation (Kubernetes)

**1. Create Blue and Green Deployments**

```yaml
# blue-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      version: blue
  template:
    metadata:
      labels:
        app: myapp
        version: blue
    spec:
      containers:
        - name: myapp
          image: myapp:1.2.0 # Old version
```

```yaml
# green-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-green
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      version: green
  template:
    metadata:
      labels:
        app: myapp
        version: green
    spec:
      containers:
        - name: myapp
          image: myapp:1.3.0 # New version
```

---

**2. Service (routes traffic)**

```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
    version: blue # Initially points to BLUE
  ports:
    - port: 80
      targetPort: 8080
```

---

**3. Deploy Green**

```bash
# Deploy new version to Green
kubectl apply -f green-deployment.yaml

# Wait for Green to be ready
kubectl wait --for=condition=available deployment/myapp-green --timeout=300s
```

---

**4. Test Green**

```bash
# Port-forward to Green (internal testing)
kubectl port-forward deployment/myapp-green 8080:8080

# Run smoke tests against Green
curl http://localhost:8080/health
curl http://localhost:8080/api/users/1

# Or: Direct test via internal service
kubectl run -it --rm test-pod --image=curlimages/curl \
  --restart=Never -- curl http://myapp-green-service/health
```

---

**5. Switch Traffic: Blue → Green**

```bash
# Update Service selector to point to Green
kubectl patch service myapp-service -p '{"spec":{"selector":{"version":"green"}}}'

# Traffic now 100% on Green
```

**Switch time**: <1 second (instant)

---

**6. Monitor Green**

Monitor for 30-60 min:

- Error rate <0.5%
- Latency P95 <300ms
- No alerts triggered

---

**7. Rollback (if needed)**

```bash
# Switch back to Blue (instant)
kubectl patch service myapp-service -p '{"spec":{"selector":{"version":"blue"}}}'
```

**Rollback time**: <1 second

---

**8. Decommission Blue (if Green is stable)**

```bash
# After 24-48h of Green being stable, remove Blue
kubectl delete deployment myapp-blue
```

---

### Pros & Cons

**Pros** ✅:

- Zero downtime
- Instant rollback (<1 sec)
- Full testing of new version before traffic switch
- Clean separation (blue is intact until green proven)

**Cons** ❌:

- High cost (2x infrastructure)
- Database migration challenges (both versions must be compatible)
- Stateful applications complex (sessions, caches)

---

### Best For

- Major releases (big features, architecture changes)
- High-risk deployments
- Applications where instant rollback is critical
- When you have budget for 2x infra

---

## 🕊️ Strategy #2: Canary Deployment

### Concept

**Gradual rollout**: New version serves small % of traffic initially, increasing gradually

**Process**:

1. Deploy new version (Canary) to 10% of servers
2. Route 10% traffic to Canary
3. Monitor metrics (error rate, latency)
4. If OK: Increase to 25% → 50% → 100%
5. If FAIL: Rollback (90% of users unaffected)

---

### Architecture

```
┌─────────────┐
│ Load Balancer│
└──────┬───────┘
       │
       ├─── 90% traffic ───→ ┌─────────────┐
       │                      │   STABLE    │ v1.2.0 (9 pods)
       │                      └─────────────┘
       │
       └─── 10% traffic ───→ ┌─────────────┐
                              │   CANARY    │ v1.3.0 (1 pod)
                              └─────────────┘

--- If Canary OK, increase ---

       ├─── 50% traffic ───→ STABLE (5 pods)
       └─── 50% traffic ───→ CANARY (5 pods)

--- If Canary OK, full rollout ---

       ├─── 100% traffic ──→ CANARY (10 pods)
```

---

### Implementation (Kubernetes + Istio)

**1. Install Istio** (for traffic splitting)

```bash
istioctl install --set profile=default
kubectl label namespace default istio-injection=enabled
```

---

**2. Deploy Stable and Canary**

```yaml
# Stable deployment (v1.2.0)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-stable
spec:
  replicas: 9
  selector:
    matchLabels:
      app: myapp
      version: stable
  template:
    metadata:
      labels:
        app: myapp
        version: stable
    spec:
      containers:
        - name: myapp
          image: myapp:1.2.0
```

```yaml
# Canary deployment (v1.3.0)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-canary
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
      version: canary
  template:
    metadata:
      labels:
        app: myapp
        version: canary
    spec:
      containers:
        - name: myapp
          image: myapp:1.3.0
```

---

**3. VirtualService (traffic split)**

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: myapp-virtualservice
spec:
  hosts:
    - myapp
  http:
    - match:
        - headers:
            x-canary:
              exact: "true" # Canary users (optional: for targeted testing)
      route:
        - destination:
            host: myapp
            subset: canary
    - route:
        - destination:
            host: myapp
            subset: stable
          weight: 90 # 90% to stable
        - destination:
            host: myapp
            subset: canary
          weight: 10 # 10% to canary
```

---

**4. Monitor Canary**

**Metrics to Watch** (10% traffic for 30 min):

- Error rate: Canary vs Stable (should be similar)
- Latency P95: Canary vs Stable
- Custom metrics (conversion rate, API success rate)

**Auto-Rollback Trigger**:

- If Canary error rate >2x Stable → Rollback
- If Canary latency >1.5x Stable → Rollback

---

**5. Increase Traffic Gradually**

```yaml
# Update VirtualService: 50/50 split
- route:
    - destination:
        host: myapp
        subset: stable
      weight: 50
    - destination:
        host: myapp
        subset: canary
      weight: 50
```

Monitor for 30 min, then 100%:

```yaml
# 100% to Canary
- route:
    - destination:
        host: myapp
        subset: canary
      weight: 100
```

---

**6. Full Rollout**

```bash
# Replace stable with canary image
kubectl set image deployment/myapp-stable myapp=myapp:1.3.0

# Remove canary deployment
kubectl delete deployment myapp-canary
```

---

### Automated Canary with Flagger

**Flagger** automates canary analysis and promotion

```yaml
apiVersion: flagger.app/v1beta1
kind: Canary
metadata:
  name: myapp
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  service:
    port: 80
  analysis:
    interval: 1m
    threshold: 5 # Number of checks before promotion
    maxWeight: 50
    stepWeight: 10 # Increase by 10% each step
    metrics:
      - name: request-success-rate
        thresholdRange:
          min: 99 # Must be >99% success rate
      - name: request-duration
        thresholdRange:
          max: 500 # Max 500ms P99 latency
  canaryAnalysis:
    interval: 1m
    threshold: 5
    iterations: 10
```

**How Flagger Works**:

1. Deploy new version → Flagger detects
2. Flagger starts: 10% → 20% → 30% → ... → 50%
3. At each step, checks metrics (success rate, latency)
4. If metrics OK: Promote to next step
5. If metrics FAIL: Auto-rollback to stable
6. If all checks pass: Promote to 100%

---

### Pros & Cons

**Pros** ✅:

- Low risk (only 10% users affected if fails)
- Real production testing (actual users, actual load)
- Gradual rollout (can stop at any %)
- Low cost (only 10% extra capacity needed)

**Cons** ❌:

- Complex setup (Istio, Flagger)
- Slower than Blue-Green (takes 30-60 min)
- Requires good monitoring/metrics
- Debugging harder (which version caused issue?)

---

### Best For

- High-risk changes (major refactors, new algorithms)
- User-facing features (want real user feedback)
- Limited infrastructure budget
- When you want data-driven promotion

---

## 🔄 Strategy #3: Rolling Deployment

### Concept

**Update pods one-by-one** (or in small batches)

**Process**:

1. Update 1 pod to new version
2. Wait for pod to be healthy
3. Update next pod
4. Repeat until all pods updated

---

### Architecture

```
Initial State (all v1.2.0):
Pod 1: v1.2.0 ✅
Pod 2: v1.2.0 ✅
Pod 3: v1.2.0 ✅
Pod 4: v1.2.0 ✅

--- Rolling Update Starts ---

Pod 1: v1.3.0 ✅ (updated)
Pod 2: v1.2.0 ✅
Pod 3: v1.2.0 ✅
Pod 4: v1.2.0 ✅

Pod 1: v1.3.0 ✅
Pod 2: v1.3.0 ✅ (updated)
Pod 3: v1.2.0 ✅
Pod 4: v1.2.0 ✅

... continue ...

Final State (all v1.3.0):
Pod 1: v1.3.0 ✅
Pod 2: v1.3.0 ✅
Pod 3: v1.3.0 ✅
Pod 4: v1.3.0 ✅
```

---

### Implementation (Kubernetes Default)

**Deployment with Rolling Update Strategy**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1 # Max 1 extra pod during rollout (total: 5)
      maxUnavailable: 0 # Never reduce below 4 pods (zero downtime)
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: myapp:1.3.0 # New version
          readinessProbe: # Health check
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 5
```

---

**Trigger Rolling Update**

```bash
# Update image
kubectl set image deployment/myapp myapp=myapp:1.3.0

# Watch rollout
kubectl rollout status deployment/myapp

# Output:
# Waiting for deployment "myapp" rollout to finish: 1 out of 4 new replicas have been updated...
# Waiting for deployment "myapp" rollout to finish: 2 out of 4 new replicas have been updated...
# Waiting for deployment "myapp" rollout to finish: 3 out of 4 new replicas have been updated...
# deployment "myapp" successfully rolled out
```

---

**Rollback**

```bash
# Rollback to previous version
kubectl rollout undo deployment/myapp

# Or rollback to specific revision
kubectl rollout history deployment/myapp  # List revisions
kubectl rollout undo deployment/myapp --to-revision=3
```

---

### Configuration Options

**maxSurge**:

- `1`: One extra pod (conservative, slower)
- `25%`: 25% extra pods (faster rollout)
- `100%`: Double pods temporarily (Blue-Green-like)

**maxUnavailable**:

- `0`: Zero downtime (always 4 pods available)
- `1`: Allow 1 pod down (faster, but brief capacity reduction)
- `25%`: Allow 25% down

**Recommended**:

```yaml
maxSurge: 1 or 25%
maxUnavailable: 0 # Zero downtime
```

---

### Pros & Cons

**Pros** ✅:

- Built-in (no extra tools needed)
- Zero downtime
- Low cost (minimal extra capacity)
- Simple to understand

**Cons** ❌:

- Slower rollback (must roll back pod-by-pod)
- Both versions running simultaneously (can cause issues)
- No traffic control (can't route 10% to new version)
- If issue detected late, many users affected

---

### Best For

- Standard, low-risk deployments
- Simple applications (stateless)
- When you don't need traffic splitting
- Default choice for most teams

---

## 🧪 Smoke Tests (All Strategies)

### Pre-Deployment Smoke Tests

**Run in Staging** (before Production deployment):

```bash
#!/bin/bash
# smoke-tests.sh

echo "🧪 Running smoke tests against Staging..."

# Test 1: Health check
echo "Test 1: Health check"
curl -f https://staging.myapp.com/health || exit 1

# Test 2: API endpoints
echo "Test 2: API endpoints"
curl -f https://staging.myapp.com/api/users || exit 1

# Test 3: Database connectivity
echo "Test 3: Database connectivity"
curl -f https://staging.myapp.com/api/db-health || exit 1

# Test 4: Critical user flow (login)
echo "Test 4: Login flow"
TOKEN=$(curl -X POST https://staging.myapp.com/api/login \
  -d '{"email":"test@example.com","password":"test123"}' \
  -H "Content-Type: application/json" | jq -r '.token')

if [ -z "$TOKEN" ]; then
  echo "❌ Login failed"
  exit 1
fi

# Test 5: Performance check
echo "Test 5: Performance check (P95 latency)"
ab -n 100 -c 10 https://staging.myapp.com/ | grep "95%"

echo "✅ All smoke tests passed"
```

---

### Post-Deployment Smoke Tests

**Run after Production deployment** (auto or manual):

**Automated (in CI/CD)**:

```yaml
# GitHub Actions
- name: Post-Deployment Smoke Tests
  run: |
    sleep 30  # Wait for pods to stabilize

    # Health check
    curl -f https://myapp.com/health || exit 1

    # Check error rate (last 5 min should be <1%)
    ERROR_RATE=$(curl -s "https://api.datadog.com/api/v1/query?query=sum:myapp.errors{*}.as_rate()" \
      -H "DD-API-KEY: ${{ secrets.DATADOG_API_KEY }}" | jq '.series[0].pointlist[-1][1]')

    if (( $(echo "$ERROR_RATE > 0.01" | bc -l) )); then
      echo "❌ Error rate too high: $ERROR_RATE"
      exit 1
    fi

    echo "✅ Smoke tests passed"
```

---

### Synthetic Monitoring (Continuous Smoke Tests)

**Datadog Synthetic Tests** (run every 1-5 min):

```yaml
# Example: Synthetic test for critical flow
- name: "Login Flow"
  type: browser
  locations:
    - aws:us-east-1
    - aws:eu-west-1
  interval: 300 # Every 5 min
  steps:
    - type: navigate
      url: https://myapp.com/login
    - type: fillInput
      selector: "#email"
      value: "test@example.com"
    - type: fillInput
      selector: "#password"
      value: "test123"
    - type: click
      selector: "#login-button"
    - type: assertElementPresent
      selector: "#dashboard"
  assertions:
    - type: responseTime
      operator: lessThan
      value: 2000 # <2 sec
```

If synthetic test fails post-deployment → Alert → Consider rollback

---

## 📊 Deployment Metrics

### Metric #1: Deployment Frequency

**Target**: Diaria (>1 deploy/day)

**DORA Metric**: Elite performers deploy multiple times per day

---

### Metric #2: Lead Time for Changes

**Target**: <4 horas (commit → production)

---

### Metric #3: Deployment Success Rate

**Definition**: % of deployments that don't require rollback

**Target**: >95%

---

### Metric #4: Deployment Duration

**Definition**: Time from deployment start → all pods healthy

**Target**:

- Rolling: <10 min
- Canary: <1 hour (gradual)
- Blue-Green: <5 min (switch is instant)

---

### Metric #5: Rollback Frequency

**Definition**: % of deployments that rollback

**Target**: <5%

**If high**: Improve Staging testing, slow down deployment frequency

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                       | Developer | DevOps | Tech Lead | Manager |
| ------------------------------- | --------- | ------ | --------- | ------- |
| Choose deployment strategy      | C         | R/A    | C         | I       |
| Implement deployment automation | C         | R/A    | C         | I       |
| Run smoke tests (Staging)       | R         | C      | A         | I       |
| Approve production deployment   | I         | R/A    | C         | I       |
| Monitor deployment (first 2h)   | C         | R/A    | C         | I       |
| Rollback decision               | C         | R/A    | C         | I       |
| Post-deployment review          | C         | R      | A         | I       |

---

## 🚀 Implementation Roadmap

### Fase 1: Rolling Deployment (Sprint 1-2)

- [ ] Implement Kubernetes rolling update strategy
- [ ] Configure readiness probes
- [ ] Test rollback procedures
- [ ] Document runbook

---

### Fase 2: Blue-Green (Sprint 3-4)

- [ ] Setup Blue and Green environments
- [ ] Implement traffic switching mechanism
- [ ] Practice Blue-Green deployment (Staging)
- [ ] Cost analysis (2x infrastructure)

---

### Fase 3: Canary (Sprint 5-7)

- [ ] Install Istio/Flagger
- [ ] Configure traffic splitting
- [ ] Define canary metrics (success rate, latency)
- [ ] Setup auto-rollback triggers
- [ ] Practice canary deployment (Staging)

---

### Fase 4: Smoke Tests & Automation (Sprint 8+)

- [ ] Automated smoke tests (CI/CD)
- [ ] Synthetic monitoring (Datadog, Pingdom)
- [ ] Deployment dashboard (metrics)
- [ ] One-click rollback button

---

## ✅ Success Criteria

### Mes 1

- ✅ Rolling deployment working
- ✅ Rollback tested and works
- ✅ Deployment success rate >90%

### Mes 2-3

- ✅ Blue-Green OR Canary implemented
- ✅ Smoke tests automated
- ✅ Deployment frequency >3/week

### Mes 4+

- ✅ Deployment frequency daily
- ✅ Deployment success rate >95%
- ✅ Rollback time <5 min

---

## 🔗 Links Relacionados

- [CI/CD Pipeline](./cicd-pipeline.md) - Automated deployment
- [Monitoring & Alerting](./monitoring-alerting.md) - Deployment monitoring
- [Incident Management](./incident-management.md) - Rollback procedures

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-06  
**Owner**: DevOps Lead  
**Review Cycle**: Trimestral
