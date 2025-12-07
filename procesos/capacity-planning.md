# Capacity Planning - Planificación de Capacidad y Escalamiento

## 📋 Resumen Ejecutivo

**Problema**: Traffic crece 300% en Black Friday → Servers crash, revenue perdido. O peor: Pagamos por servidores que usamos 10%.

**Solución**: **Capacity planning process** con forecasting, scaling triggers, cost optimization.

**Beneficio**:
- No más outages por falta de capacidad
- Escala automática (traffic spike → auto-scale)
- Cost optimization (right-sizing, reserved instances)
- Predictable budgets (sabemos cuánto vamos a gastar)

---

## 🎯 Capacity Metrics

### Infrastructure Metrics

**CPU Utilization**:
- **Current**: Average 45%, Peak 85%
- **Target**: Average 60-70%, Peak <80% (headroom for spikes)
- **Alert**: >80% sustained for 10 min

**Memory Utilization**:
- **Current**: Average 60%, Peak 90%
- **Target**: Average 70-80%, Peak <85%
- **Alert**: >85% sustained for 10 min

**Disk Space**:
- **Current**: 70% used
- **Target**: <80% used (plan expansion at 75%)
- **Alert**: >90% used

**Network Bandwidth**:
- **Current**: 100 Mbps average, 500 Mbps peak
- **Target**: <70% of link capacity (1 Gbps link = 700 Mbps max)
- **Alert**: >80% sustained

---

### Application Metrics

**Request Rate (RPS - Requests Per Second)**:
- **Current**: 500 RPS average, 2,000 RPS peak
- **Capacity**: 3,000 RPS (before degradation)
- **Target**: Keep peak <80% capacity (2,400 RPS)

**Response Time (Latency)**:
- **Current**: P50 100ms, P95 300ms, P99 800ms
- **Target**: P95 <500ms, P99 <1000ms
- **Alert**: P95 >1000ms (degrading, need more capacity)

**Error Rate**:
- **Current**: 0.1%
- **Target**: <1%
- **Alert**: >1% (may indicate capacity issue)

**Database Connections**:
- **Current**: 50 connections average, 150 peak
- **Max**: 200 connections (PostgreSQL limit)
- **Target**: Peak <80% max (160 connections)
- **Alert**: >160 connections

---

### Business Metrics

**Active Users**:
- **Current**: 10,000 DAU (Daily Active Users)
- **Growth**: +20% QoQ (Quarter over Quarter)
- **Forecast**: 15,000 DAU in Q2, 20,000 DAU in Q3

**Revenue**:
- **Current**: $100K/month
- **Growth**: +25% QoQ
- **Forecast**: $125K Q2, $156K Q3

**Storage Growth**:
- **Current**: 500 GB database, 2 TB object storage
- **Growth**: +30 GB/month database, +200 GB/month storage
- **Forecast**: 600 GB database in 3 months, 3 TB storage in 6 months

---

## 📈 Growth Forecasting

### Linear Growth Model

**Use Case**: Steady, predictable growth

**Formula**: `Future Value = Current Value × (1 + Growth Rate)^Periods`

**Example** (Users):
- Current: 10,000 DAU
- Growth: +5% per month
- Forecast (6 months): 10,000 × (1.05)^6 = 13,401 DAU

**Example** (Storage):
- Current: 500 GB
- Growth: +30 GB/month
- Forecast (12 months): 500 + (30 × 12) = 860 GB

---

### Exponential Growth Model

**Use Case**: Viral growth, marketing campaigns

**Formula**: `Future Value = Current Value × e^(Growth Rate × Time)`

**Example** (Black Friday):
- Normal: 500 RPS
- Black Friday: 10x traffic = 5,000 RPS
- Plan capacity: 6,000 RPS (20% headroom)

---

### Seasonal Patterns

**Example** (E-commerce):

```
Traffic Pattern (RPS):
January:   500 RPS (post-holiday drop)
February:  600 RPS
March:     700 RPS
...
November:  1,000 RPS (Black Friday prep)
December:  5,000 RPS (Black Friday + Holidays)
```

**Capacity Plan**:
- Baseline: 1,000 RPS capacity (year-round)
- Seasonal scale: +4,000 RPS (November-December only)
- Method: Auto-scaling (scale up for holidays, scale down after)

---

### Historical Trend Analysis

**Steps**:

1. **Collect Data** (last 12 months)
   - CPU, memory, RPS, users, storage

2. **Calculate Growth Rate**
   ```
   Growth Rate = (Current - 12 Months Ago) / 12 Months Ago
   
   Example:
   Users 12 months ago: 5,000
   Users today: 10,000
   Growth Rate = (10,000 - 5,000) / 5,000 = 100% (doubled in 1 year)
   Monthly Growth Rate = (1 + 100%)^(1/12) - 1 = 5.95% per month
   ```

3. **Forecast Future**
   - 6 months: 10,000 × (1.0595)^6 = 13,540 users
   - 12 months: 10,000 × (1.0595)^12 = 20,000 users

4. **Plan Capacity**
   - Current: 1,000 RPS capacity
   - If users double → RPS doubles (assume linear)
   - Need: 2,000 RPS capacity in 12 months
   - When to upgrade: 9 months (plan 3 months ahead)

---

## ⚙️ Scaling Strategies

### Vertical Scaling (Scale Up)

**Definition**: Bigger servers (more CPU, RAM)

**When**:
- Single-threaded workloads (can't parallelize)
- Database (PostgreSQL, MySQL)
- Legacy applications (can't scale horizontally)

**Pros**:
- ✅ Simple (no code changes)
- ✅ Faster (more powerful CPU)

**Cons**:
- ❌ Expensive (2x CPU = 2x cost)
- ❌ Downtime (need to restart)
- ❌ Hard limit (can't scale infinitely)

**Example** (Azure):
```bash
# Upgrade VM from Standard_D2s_v3 (2 vCPU, 8GB RAM) to Standard_D4s_v3 (4 vCPU, 16GB RAM)
az vm resize \
  --resource-group myapp-rg \
  --name myapp-vm \
  --size Standard_D4s_v3
```

---

### Horizontal Scaling (Scale Out)

**Definition**: More servers (add replicas)

**When**:
- Stateless applications (API, web servers)
- High traffic (can distribute load)
- Fault tolerance (one server dies, others handle)

**Pros**:
- ✅ No hard limit (can scale infinitely)
- ✅ Fault tolerance (redundancy)
- ✅ Cost-effective (add cheap servers)

**Cons**:
- ❌ Complex (need load balancer, session management)
- ❌ Not all apps support (stateful apps)

**Example** (Kubernetes):
```bash
# Scale deployment from 3 replicas to 10 replicas
kubectl scale deployment myapp --replicas=10
```

---

### Auto-Scaling

**Definition**: Automatically add/remove servers based on load

**Trigger**: CPU >70% → Scale up, CPU <30% → Scale down

**Benefits**:
- Handle traffic spikes (Black Friday)
- Save money (scale down at night)

**Example** (Kubernetes HPA - Horizontal Pod Autoscaler):

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 3
  maxReplicas: 50
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70  # Scale up if CPU >70%
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80  # Scale up if Memory >80%
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 60  # Wait 60s before scaling up (avoid flapping)
      policies:
      - type: Percent
        value: 50  # Add 50% more pods per scale-up
        periodSeconds: 60
    scaleDown:
      stabilizationWindowSeconds: 300  # Wait 5 min before scaling down (avoid flapping)
      policies:
      - type: Pods
        value: 1  # Remove 1 pod at a time
        periodSeconds: 60
```

**Result**:
- Normal: 3 replicas
- Traffic spike (CPU >70%): Scales up to 10, 15, 20... (max 50)
- Traffic drops (CPU <30%): Scales down to 3 (min)

---

### Database Scaling

**Read Replicas** (for read-heavy workloads):

```bash
# Create read replica (Azure SQL)
az sql db replica create \
  --resource-group myapp-rg \
  --server myapp-sql-primary \
  --name myapp-db \
  --partner-server myapp-sql-replica
```

**Use Case**:
- 80% reads, 20% writes
- Route reads → Replica, writes → Primary
- Example: 1,000 RPS → 800 RPS to replica, 200 RPS to primary

**Sharding** (for write-heavy workloads):

- Split data across multiple databases (e.g., users A-M → DB1, users N-Z → DB2)
- Complex (application logic needs to route queries)

---

## 💰 Cost Optimization

### Right-Sizing

**Problem**: Over-provisioned servers (8 CPU, but using 2)

**Solution**: Downsize to match actual usage

**Steps**:

1. **Analyze Utilization** (last 30 days)
   ```bash
   # Azure Cost Management
   az consumption usage list --start-date 2025-01-01 --end-date 2025-01-31
   ```

2. **Identify Waste**
   - VM using 20% CPU → Downsize from 8 vCPU to 2 vCPU
   - Database connections <50 → Downsize from 200 max connections to 100

3. **Resize**
   ```bash
   # Downgrade VM
   az vm resize --resource-group myapp-rg --name myapp-vm --size Standard_B2s
   ```

**Savings**: 50-70% cost reduction

---

### Reserved Instances / Savings Plans

**Problem**: On-demand pricing (expensive)

**Solution**: Commit to 1-year or 3-year term → 40-60% discount

**Example** (Azure):
- On-demand: $0.10/hour × 730 hours/month = $73/month
- 1-year reserved: $0.06/hour × 730 hours/month = $44/month (40% savings)
- 3-year reserved: $0.04/hour × 730 hours/month = $29/month (60% savings)

**When to Use**:
- Baseline capacity (always running)
- NOT for auto-scaling (use spot instances)

---

### Spot Instances (Cheap but Evictable)

**Definition**: Unused cloud capacity (up to 90% discount, but can be terminated)

**When to Use**:
- Batch jobs (can be interrupted)
- Auto-scaling (if terminated, another instance starts)
- NOT for critical workloads (use reserved instances)

**Example** (Kubernetes):

```yaml
apiVersion: v1
kind: Node
metadata:
  labels:
    kubernetes.azure.com/scalesetpriority: spot  # Use Spot VMs
spec:
  taints:
  - key: kubernetes.azure.com/scalesetpriority
    value: spot
    effect: NoSchedule
```

**Pod Tolerations** (allow scheduling on Spot nodes):

```yaml
tolerations:
- key: "kubernetes.azure.com/scalesetpriority"
  operator: "Equal"
  value: "spot"
  effect: "NoSchedule"
```

---

### Storage Tiering

**Problem**: All data in hot storage (expensive)

**Solution**: Move old data to cold storage (cheap)

**Tiers**:
- **Hot** (frequent access): $0.02/GB/month
- **Cool** (infrequent access): $0.01/GB/month
- **Archive** (rare access): $0.002/GB/month

**Example** (Azure Blob Storage Lifecycle Policy):

```json
{
  "rules": [
    {
      "name": "moveToCool",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": ["blockBlob"]
        },
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            },
            "tierToArchive": {
              "daysAfterModificationGreaterThan": 90
            },
            "delete": {
              "daysAfterModificationGreaterThan": 365
            }
          }
        }
      }
    }
  ]
}
```

**Result**:
- Files <30 days old: Hot ($0.02/GB)
- Files 30-90 days old: Cool ($0.01/GB)
- Files >90 days old: Archive ($0.002/GB)
- Files >365 days old: Deleted

**Savings**: 50-90% on storage

---

### Shutdown Non-Production Environments

**Problem**: Dev/Test environments running 24/7

**Solution**: Shutdown nights/weekends (only run 8-10 hours/day)

**Savings**:
- Running 24/7: $73/month
- Running 10 hours/day (weekdays only): $73 × (10/24) × (5/7) = $22/month
- Savings: 70%

**Automation** (Azure):

```bash
# Auto-shutdown VM at 6 PM
az vm auto-shutdown \
  --resource-group myapp-rg \
  --name myapp-dev-vm \
  --time 1800  # 6 PM
```

---

## 🔄 Quarterly Capacity Review

**Frequency**: Every 3 months

**Participants**: DevOps Lead, Finance, Engineering Manager

**Agenda**:

1. **Review Current Utilization** (30 min)
   - CPU, memory, storage, network
   - Identify waste (under-utilized resources)

2. **Forecast Growth** (30 min)
   - User growth (+20% QoQ?)
   - Storage growth (+30 GB/month?)
   - Traffic growth (+15% QoQ?)

3. **Capacity Plan** (30 min)
   - When to scale (9 months from now?)
   - How much (double capacity?)
   - Budget ($10K/month → $15K/month?)

4. **Cost Optimization** (30 min)
   - Right-sizing opportunities
   - Reserved instances to purchase
   - Storage tiering

5. **Action Items** (15 min)
   - [ ] Downsize dev VMs (save $500/month)
   - [ ] Purchase 1-year reserved instances (save $2K/month)
   - [ ] Implement storage lifecycle policy (save $300/month)

---

**Capacity Review Report Template**:

```markdown
## Quarterly Capacity Review - Q1 2025

**Date**: 2025-01-15
**Participants**: @alice-devops, @bob-finance, @charlie-em

### 1. Current Utilization

| Metric         | Current  | Target   | Status |
| -------------- | -------- | -------- | ------ |
| CPU            | 45%      | 60-70%   | ✅ OK   |
| Memory         | 60%      | 70-80%   | ✅ OK   |
| Disk           | 70%      | <80%     | ✅ OK   |
| RPS            | 500      | <2,400   | ✅ OK   |

### 2. Growth Forecast (Next 12 Months)

- Users: 10K → 20K DAU (+100%)
- Traffic: 500 RPS → 1,000 RPS (+100%)
- Storage: 500 GB → 860 GB (+72%)

### 3. Capacity Plan

**When to Scale**: Q3 2025 (6 months from now)

**Action**: Double API capacity (3 replicas → 6 replicas)

**Budget Impact**: $10K/month → $15K/month

### 4. Cost Optimization

**Identified Savings**:
- Right-size dev VMs: -$500/month
- Purchase reserved instances: -$2,000/month
- Storage tiering: -$300/month
**Total Savings**: -$2,800/month (28% reduction)

### 5. Action Items

- [ ] @alice-devops: Downsize dev VMs (by Feb 1)
- [ ] @bob-finance: Purchase 1-year reserved instances (by Feb 15)
- [ ] @alice-devops: Implement storage lifecycle policy (by Mar 1)

**Next Review**: 2025-04-15 (Q2)
```

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | DevOps | Finance | EM  | CTO |
| --------------------------------- | ------ | ------- | --- | --- |
| Monitor capacity metrics          | A/R    | I       | I   | I   |
| Forecast growth                   | R      | R       | A   | C   |
| Quarterly capacity review         | R      | R       | A   | C   |
| Approve scaling (budget)          | C      | A       | C   | A   |
| Implement auto-scaling            | A/R    | I       | I   | I   |
| Cost optimization                 | R      | A       | C   | C   |

---

## 🚀 Implementation Roadmap

### Sprint 1: Metrics & Monitoring
- [ ] Define capacity metrics (CPU, memory, RPS, storage)
- [ ] Setup Grafana dashboards (capacity utilization)
- [ ] Alert on thresholds (>80% CPU)

### Sprint 2: Auto-Scaling
- [ ] Implement HPA (Horizontal Pod Autoscaler)
- [ ] Test auto-scaling (load test: 500 → 5,000 RPS)
- [ ] Tune thresholds (scale at 70% CPU, not 90%)

### Sprint 3: Forecasting
- [ ] Collect historical data (last 12 months)
- [ ] Calculate growth rates
- [ ] Build forecast model (linear/exponential)

### Sprint 4: Cost Optimization
- [ ] Analyze utilization (right-sizing opportunities)
- [ ] Purchase reserved instances (baseline capacity)
- [ ] Implement storage tiering

### Sprint 5: Quarterly Review
- [ ] Schedule Q1 capacity review
- [ ] Document capacity plan
- [ ] Track action items

---

## ✅ Success Criteria

### Mes 1
- ✅ Capacity metrics defined & monitored
- ✅ Grafana dashboards created
- ✅ Auto-scaling implemented (HPA)

### Mes 2-3
- ✅ Growth forecast completed (next 12 months)
- ✅ First quarterly capacity review done
- ✅ Cost optimization implemented (>20% savings)

### Mes 4+
- ✅ Zero outages due to capacity (auto-scaling works)
- ✅ Quarterly reviews happening (on schedule)
- ✅ Cost variance <10% (predictable budgets)

---

## 🔗 Links Relacionados

- [Monitoring & Alerting](./monitoring-alerting.md) - Capacity metrics
- [Deployment Procedures](./deployment-procedures.md) - Scaling strategies
- [Change Management](./change-management.md) - Capacity change approval

---

## 📚 Antipatterns

### ❌ Antipattern #1: "We'll Scale When We Need To"

**Problem**: Reactive scaling (wait for outage, then panic-scale)

**Example**:
- Black Friday: 10x traffic
- Servers crash (not enough capacity)
- Team: "Quick, add more servers!"
- Takes 2 hours → Revenue lost

**Solution**: ✅ Proactive planning (forecast, auto-scale, load test)

---

### ❌ Antipattern #2: "Over-Provision Everything"

**Problem**: Buy 10x capacity "just in case"

**Example**:
- Current: 500 RPS
- Provision: 10,000 RPS capacity (20x)
- Utilization: 5% (waste 95%)
- Cost: $50K/month (should be $5K/month)

**Solution**: ✅ Right-sizing + auto-scaling (pay for what you use)

---

### ❌ Antipattern #3: "Ignore Growth"

**Problem**: Never review capacity, assume "it's fine"

**Example**:
- Users: 10K → 50K (5x growth in 6 months)
- Capacity: Still sized for 10K
- Result: Constant outages ("Why is the site slow?")

**Solution**: ✅ Quarterly capacity reviews

---

### ❌ Antipattern #4: "No Auto-Scaling"

**Problem**: Manual scaling ("Add 3 servers, please")

**Example**:
- Traffic spike (3 AM)
- On-call: Asleep
- Servers crash (no one scaled up)

**Solution**: ✅ Auto-scaling (HPA)

---

### ❌ Antipattern #5: "No Cost Tracking"

**Problem**: Don't monitor cloud bill, get $100K surprise

**Example**:
- Dev leaves auto-scaling maxed (100 replicas)
- Runs for 1 month
- Bill: $100K (should be $10K)

**Solution**: ✅ Budget alerts (alert if >$15K/month)

---

**Versión**: 1.0  
**Última Actualización**: 2025-01-15  
**Owner**: DevOps Lead / Finance  
**Review Cycle**: Trimestral
