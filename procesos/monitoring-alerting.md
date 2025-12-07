# Monitoring & Alerting - Observabilidad y Alertas

## 📋 Resumen Ejecutivo

**Problema**: Producción falla pero nadie se entera hasta que usuarios se quejan en Twitter. "We didn't know it was down!"

**Solución**: **Monitoring stack completo** con métricas, logs, traces, alertas inteligentes, y on-call automation.

**Beneficio**:
- MTTD (Mean Time to Detect): De 30 min → <5 min
- Proactive alerting (sabemos antes que usuarios)
- Root cause analysis rápido (logs + traces + metrics)
- SLO-based alerting (solo alertas que importan)

---

## 🎯 Observability Pillars

### The Three Pillars

```
┌─────────────┐
│   METRICS   │ What's happening? (CPU, memory, requests/sec)
└─────────────┘

┌─────────────┐
│    LOGS     │ Why did it happen? (Error messages, stack traces)
└─────────────┘

┌─────────────┐
│   TRACES    │ Where is the bottleneck? (Request flow across services)
└─────────────┘
```

**Together** → Full observability

---

## 📊 Pillar #1: Metrics

### Infrastructure Metrics

**What to Monitor**:

| Metric            | Threshold       | Alert Priority | Action                    |
| ----------------- | --------------- | -------------- | ------------------------- |
| **CPU Usage**     | >80% for >5 min | 🟡 Medium      | Scale up or optimize      |
| **Memory Usage**  | >85%            | 🟠 High        | Check for memory leaks    |
| **Disk Usage**    | >90%            | 🔴 Critical    | Clean up or scale storage |
| **Network I/O**   | >80% capacity   | 🟡 Medium      | Check for DDoS or spike   |
| **Pod Restarts**  | >3 in 10 min    | 🟠 High        | Check crash loops         |

---

### Application Metrics (Golden Signals)

**1. Latency** (Response Time)

```
P50: 50th percentile (median)
P95: 95th percentile (most users)
P99: 99th percentile (worst case)
```

**Targets**:
- API endpoints: P95 <200ms, P99 <500ms
- Database queries: P95 <50ms, P99 <200ms
- External API calls: P95 <1s, P99 <3s

**Alert**:
- 🟡 Warning: P95 >300ms for >5 min
- 🔴 Critical: P95 >1000ms for >2 min

---

**2. Traffic** (Requests per Second)

**What to Monitor**:
- Requests/sec (RPS)
- Active connections
- Throughput (bytes/sec)

**Alert**:
- 🟡 Traffic spike: >2x normal (could be attack or viral feature)
- 🔴 Traffic drop: <50% normal (service down or routing issue)

---

**3. Errors** (Error Rate)

**Error Types**:
- 4xx errors (client errors): User mistakes, validation failures
- 5xx errors (server errors): Our bugs, outages

**Targets**:
- Error rate <0.5% (99.5% success rate)
- 5xx error rate <0.1% (99.9% success rate)

**Alert**:
- 🟡 Warning: Error rate >1% for >5 min
- 🔴 Critical: Error rate >5% for >2 min

---

**4. Saturation** (Resource Utilization)

**What to Monitor**:
- Queue depth (message queues, job queues)
- Connection pool utilization
- Thread pool utilization

**Alert**:
- 🟡 Queue depth >1000 for >10 min
- 🔴 Connection pool >90% for >5 min

---

### Business Metrics (KPIs)

**Examples**:
- Sign-ups per hour
- Purchases per hour
- Revenue per hour
- Active users (DAU, MAU)

**Alert**:
- 🟡 Revenue drop >20% from yesterday
- 🔴 Zero purchases for >30 min (payment system down?)

---

### Monitoring Stack

**Metrics Collection & Storage**:

**Option A: Prometheus + Grafana** (Open Source)
```yaml
# Prometheus scrapes metrics from applications
# Grafana visualizes metrics

Advantages:
- Free and open source
- Powerful query language (PromQL)
- Large community

Disadvantages:
- Self-hosted (you manage it)
- Scaling can be complex
```

**Option B: Datadog** (SaaS, Recommended)
```yaml
Advantages:
- Fully managed (no ops overhead)
- Metrics + Logs + Traces in one platform
- Great UI, easy to use
- Powerful alerting

Disadvantages:
- $$$$ Cost (can be expensive at scale)
```

**Option C: Azure Monitor / Application Insights** (Azure)
```yaml
Advantages:
- Native Azure integration
- Good if already on Azure

Disadvantages:
- Lock-in to Azure
- UI not as good as Datadog
```

---

### Metrics Implementation

**Expose Metrics from Application** (Prometheus format):

```javascript
// Node.js + Express + prom-client
const promClient = require('prom-client');
const express = require('express');
const app = express();

// Create metrics
const httpRequestDuration = new promClient.Histogram({
  name: 'http_request_duration_ms',
  help: 'Duration of HTTP requests in ms',
  labelNames: ['method', 'route', 'status_code'],
  buckets: [10, 50, 100, 200, 500, 1000, 2000, 5000]
});

const httpRequestTotal = new promClient.Counter({
  name: 'http_requests_total',
  help: 'Total number of HTTP requests',
  labelNames: ['method', 'route', 'status_code']
});

// Middleware to track metrics
app.use((req, res, next) => {
  const start = Date.now();
  
  res.on('finish', () => {
    const duration = Date.now() - start;
    httpRequestDuration.labels(req.method, req.route?.path || req.path, res.statusCode).observe(duration);
    httpRequestTotal.labels(req.method, req.route?.path || req.path, res.statusCode).inc();
  });
  
  next();
});

// Expose /metrics endpoint
app.get('/metrics', async (req, res) => {
  res.set('Content-Type', promClient.register.contentType);
  res.end(await promClient.register.metrics());
});
```

---

**Prometheus Scrape Config**:

```yaml
# prometheus.yml
scrape_configs:
  - job_name: 'myapp'
    scrape_interval: 15s  # Scrape every 15 seconds
    static_configs:
      - targets: ['myapp:3000']  # Application exposes /metrics
```

---

**Grafana Dashboard** (visualize metrics):

```json
{
  "dashboard": {
    "title": "MyApp - Overview",
    "panels": [
      {
        "title": "Request Rate (RPS)",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])"
          }
        ]
      },
      {
        "title": "Error Rate (%)",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total{status_code=~\"5..\"}[5m]) / rate(http_requests_total[5m]) * 100"
          }
        ]
      },
      {
        "title": "P95 Latency (ms)",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_ms_bucket[5m]))"
          }
        ]
      }
    ]
  }
}
```

---

## 📝 Pillar #2: Logs

### Log Levels

| Level     | Use Case                                    | Example                                   |
| --------- | ------------------------------------------- | ----------------------------------------- |
| **DEBUG** | Development debugging (not in production)   | "SQL query: SELECT * FROM users WHERE..." |
| **INFO**  | Normal operations, state changes            | "User 123 logged in"                      |
| **WARN**  | Unexpected but recoverable                  | "API rate limit approaching"              |
| **ERROR** | Errors that need attention                  | "Payment processing failed for order 456" |
| **FATAL** | Critical errors, application crash          | "Database connection lost"                |

---

### Structured Logging (JSON)

**Bad** ❌ (plain text, hard to parse):
```
2025-01-15 14:32:15 ERROR User login failed for alice@example.com
```

**Good** ✅ (JSON, easy to parse and search):
```json
{
  "timestamp": "2025-01-15T14:32:15Z",
  "level": "ERROR",
  "message": "User login failed",
  "user_email": "alice@example.com",
  "user_id": null,
  "error_code": "INVALID_PASSWORD",
  "ip_address": "192.168.1.100",
  "trace_id": "a1b2c3d4-e5f6-7890",
  "service": "auth-service"
}
```

**Benefits**:
- Searchable (find all logs for `user_id=123`)
- Parseable (aggregate error counts by `error_code`)
- Traceable (follow request with `trace_id`)

---

### Log Aggregation

**Stack**: ELK (Elasticsearch, Logstash, Kibana) or Datadog Logs

**Flow**:
```
Application → Logs (JSON) → Log Shipper (Filebeat, Fluentd) → 
Log Aggregator (Logstash, Datadog) → Storage (Elasticsearch) → 
Search/Visualize (Kibana, Datadog)
```

---

**Example: Search Logs in Kibana**

```
# Find all ERROR logs for user 123 in last 1 hour
level:ERROR AND user_id:123 AND @timestamp:[now-1h TO now]

# Find all 5xx errors
status_code:5* AND @timestamp:[now-1h TO now]

# Find slow queries (>1 second)
query_duration_ms:>1000 AND @timestamp:[now-1h TO now]
```

---

### Log Retention

| Log Type        | Retention | Storage         | Cost      |
| --------------- | --------- | --------------- | --------- |
| **Production**  | 90 days   | Hot (searchable)| High      |
| **Production (old)** | 1 year | Cold (archive) | Low  |
| **Staging**     | 30 days   | Hot             | Medium    |
| **Development** | 7 days    | Hot             | Low       |

**Cost Optimization**:
- Only log ERROR/WARN in production (not DEBUG/INFO)
- Sample high-volume logs (log 10% of requests)
- Archive old logs to S3/Azure Blob (cheap)

---

## 🔍 Pillar #3: Distributed Tracing

### Concept

**Trace** = Full journey of a request across multiple services

**Example**: User clicks "Buy" button

```
Frontend (Browser)
  ↓ HTTP Request (trace_id: abc123)
API Gateway (50ms)
  ↓ gRPC Call (trace_id: abc123)
Auth Service (30ms)
  ↓ SQL Query (trace_id: abc123)
Database (20ms)
  ↓ Returns
Auth Service
  ↓ gRPC Call (trace_id: abc123)
Payment Service (200ms)
  ↓ HTTP Call to Stripe (trace_id: abc123)
Stripe API (150ms)
  ↓ Returns
Payment Service
  ↓ Returns
API Gateway
  ↓ HTTP Response (trace_id: abc123)
Frontend (Browser)

Total: 450ms
```

**Trace shows**:
- Which service is slowest (Payment Service: 200ms)
- Where the bottleneck is (Stripe API: 150ms)

---

### Tracing Tools

**Options**:
- **Jaeger** (Open Source, CNCF project)
- **Datadog APM** (SaaS, Recommended)
- **Azure Application Insights** (Azure)
- **OpenTelemetry** (Standard for instrumentation)

---

### Tracing Implementation (OpenTelemetry)

```javascript
// Node.js + OpenTelemetry
const { NodeTracerProvider } = require('@opentelemetry/sdk-trace-node');
const { registerInstrumentations } = require('@opentelemetry/instrumentation');
const { HttpInstrumentation } = require('@opentelemetry/instrumentation-http');
const { ExpressInstrumentation } = require('@opentelemetry/instrumentation-express');

// Setup tracer
const provider = new NodeTracerProvider();
provider.register();

// Auto-instrument HTTP and Express
registerInstrumentations({
  instrumentations: [
    new HttpInstrumentation(),
    new ExpressInstrumentation(),
  ],
});

// Each request automatically gets a trace_id and span_id
```

**Trace appears in Jaeger/Datadog**:
- Service: myapp-api
- Operation: GET /api/orders/123
- Duration: 245ms
- Child spans: DB query (50ms), External API call (150ms)

---

## 🚨 Alerting Strategy

### SLI / SLO / SLA

**SLI (Service Level Indicator)**: Metric we measure
- Example: "Request success rate", "P95 latency"

**SLO (Service Level Objective)**: Target we aim for
- Example: "99.9% success rate", "P95 latency <200ms"

**SLA (Service Level Agreement)**: Promise to customers (contractual)
- Example: "99.5% uptime or money back"

**Relationship**: `SLA < SLO < SLI`
- SLI: What we measure (99.95% uptime)
- SLO: Internal target (99.9% uptime)
- SLA: Customer promise (99.5% uptime)

**Buffer**: SLO > SLA (so we have margin before breaking SLA)

---

### Error Budget

**Error Budget** = 100% - SLO

**Example**:
- SLO: 99.9% uptime
- Error Budget: 0.1% downtime = 43 minutes/month

**If we exceed error budget**:
- Stop feature work
- Focus on reliability (fix bugs, improve monitoring, etc.)
- Resume features when error budget recovers

---

### Alert Rules (Prometheus)

**Rule #1: High Error Rate**

```yaml
# prometheus-alerts.yml
groups:
  - name: application_alerts
    rules:
      - alert: HighErrorRate
        expr: |
          rate(http_requests_total{status_code=~"5.."}[5m]) 
          / 
          rate(http_requests_total[5m]) > 0.05
        for: 2m  # Alert if condition true for 2 min
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value | humanizePercentage }} (threshold: 5%)"
```

---

**Rule #2: High Latency**

```yaml
- alert: HighLatency
  expr: |
    histogram_quantile(0.95, 
      rate(http_request_duration_ms_bucket[5m])
    ) > 1000
  for: 5m
  labels:
    severity: warning
  annotations:
    summary: "API latency is high"
    description: "P95 latency is {{ $value }}ms (threshold: 1000ms)"
```

---

**Rule #3: Pod Restart Loop**

```yaml
- alert: PodCrashLooping
  expr: |
    rate(kube_pod_container_status_restarts_total[15m]) > 0.2
  for: 5m
  labels:
    severity: critical
  annotations:
    summary: "Pod {{ $labels.pod }} is crash looping"
    description: "Pod has restarted {{ $value }} times in 15 min"
```

---

### Alert Routing (Alertmanager)

```yaml
# alertmanager.yml
route:
  receiver: 'default-receiver'
  routes:
    # Critical alerts -> Page on-call engineer (PagerDuty)
    - match:
        severity: critical
      receiver: 'pagerduty'
      continue: true  # Also send to Slack
    
    # Warning alerts -> Slack only
    - match:
        severity: warning
      receiver: 'slack'

receivers:
  - name: 'pagerduty'
    pagerduty_configs:
      - service_key: 'PAGERDUTY_SERVICE_KEY'
  
  - name: 'slack'
    slack_configs:
      - api_url: 'https://hooks.slack.com/services/XXX'
        channel: '#alerts'
        title: '{{ .GroupLabels.alertname }}'
        text: '{{ .Annotations.description }}'
```

---

### Alert Fatigue Prevention

**Problem**: Too many alerts → Engineers ignore them

**Solutions**:

1. **Alert on Symptoms, Not Causes**
   - ❌ Bad: "CPU >80%" (could be normal during traffic spike)
   - ✅ Good: "Error rate >5%" (actual user impact)

2. **Use Error Budgets**
   - Only alert if SLO is at risk
   - Ignore small blips (transient issues)

3. **Group Related Alerts**
   - If 10 pods fail, send 1 alert (not 10)

4. **Silence Known Issues**
   - Maintenance window → Silence alerts
   - Known issue with workaround → Silence until fixed

5. **Alert Thresholds**
   - Tune thresholds (not too sensitive, not too lazy)
   - Review alerts monthly (are they actionable?)

---

## 📚 Runbooks

### Runbook = Playbook for on-call engineer

**What to Include**:
1. **Alert description**: What this alert means
2. **Impact**: User-facing impact (can users still use the app?)
3. **Diagnosis steps**: How to investigate (check logs, metrics, traces)
4. **Mitigation**: Quick fix to restore service
5. **Resolution**: Permanent fix (may need code change)

---

### Example Runbook: High Error Rate

```markdown
# Runbook: High Error Rate Alert

## Alert Description
Error rate >5% for 2 minutes.

## Impact
- **User Impact**: Users seeing 5xx errors, degraded experience
- **Business Impact**: Revenue loss (if payment/checkout affected)

## Diagnosis Steps

### 1. Check Error Rate Dashboard
- Go to: https://grafana.company.com/d/errors
- Identify: Which endpoint has high errors?

### 2. Check Recent Deployments
```bash
kubectl rollout history deployment/myapp
```
- Was there a recent deployment? (could be bad release)

### 3. Check Logs
```bash
kubectl logs -l app=myapp --tail=100 | grep ERROR
```
- Look for error messages, stack traces

### 4. Check Dependencies
- Database healthy? `curl https://myapp.com/health/db`
- External APIs healthy? (Stripe, Auth0, etc.)

## Mitigation (Stop the Bleeding)

### Option 1: Rollback (if recent deployment)
```bash
kubectl rollout undo deployment/myapp
```
- ETA: <5 min

### Option 2: Scale Up (if capacity issue)
```bash
kubectl scale deployment/myapp --replicas=10
```
- ETA: <2 min

### Option 3: Restart Pods (if memory leak)
```bash
kubectl rollout restart deployment/myapp
```
- ETA: <5 min

## Resolution (Permanent Fix)
- Fix bug in code
- Deploy to Staging, test
- Deploy to Production (gradual canary)

## Escalation
- If not resolved in 30 min → Page Tech Lead
- If not resolved in 1 hour → Page Engineering Manager
```

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                          | DevOps | SRE | Developer | Manager |
| ---------------------------------- | ------ | --- | --------- | ------- |
| Setup monitoring stack             | R/A    | C   | C         | I       |
| Define SLIs/SLOs                   | C      | R/A | C         | C       |
| Configure alerts                   | R/A    | C   | C         | I       |
| Write runbooks                     | R      | R   | C         | I       |
| Respond to alerts (on-call)        | C      | R/A | C         | I       |
| Tune alert thresholds              | R/A    | C   | C         | I       |
| Review dashboards monthly          | R      | C   | C         | A       |

---

## 🚀 Implementation Roadmap

### Sprint 1-2: Metrics
- [ ] Setup Prometheus/Datadog
- [ ] Instrument applications (expose /metrics)
- [ ] Create Grafana dashboards (Golden Signals)

### Sprint 3-4: Logs
- [ ] Implement structured logging (JSON)
- [ ] Setup log aggregation (ELK/Datadog)
- [ ] Create log search queries

### Sprint 5-6: Tracing
- [ ] Setup Jaeger/Datadog APM
- [ ] Instrument with OpenTelemetry
- [ ] Trace critical flows (login, checkout, payment)

### Sprint 7-8: Alerting
- [ ] Define SLIs/SLOs
- [ ] Configure alert rules
- [ ] Setup PagerDuty integration
- [ ] Write runbooks (top 5 alerts)

### Sprint 9+: Optimization
- [ ] Tune alert thresholds
- [ ] Reduce alert fatigue
- [ ] Synthetic monitoring

---

## ✅ Success Criteria

### Mes 1
- ✅ Metrics dashboard functional
- ✅ Basic alerts configured (error rate, latency)
- ✅ On-call rotation setup

### Mes 2-3
- ✅ Logs aggregated and searchable
- ✅ Distributed tracing working
- ✅ MTTD <10 min

### Mes 4+
- ✅ SLOs defined and tracked
- ✅ MTTD <5 min
- ✅ Alert fatigue <10 alerts/week/person
- ✅ 100% of critical alerts have runbooks

---

## 🔗 Links Relacionados

- [Incident Management](./incident-management.md) - Alert response procedures
- [CI/CD Pipeline](./cicd-pipeline.md) - Deployment monitoring

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-06  
**Owner**: DevOps Lead / SRE Lead  
**Review Cycle**: Trimestral
