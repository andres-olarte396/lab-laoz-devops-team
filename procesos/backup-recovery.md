# Backup & Recovery - Respaldo y Recuperación ante Desastres

## 📋 Resumen Ejecutivo

**Problema**: Base de datos se corrompe, servidor se quema, datacenter se cae → Perdemos todo si no hay backups.

**Solución**: **Backup strategy automatizada** con RTO/RPO targets, restoration testing, y disaster recovery plan.

**Beneficio**:
- Data loss minimizado (RPO <1 hora)
- Recovery rápido (RTO <4 horas)
- Compliance (regulaciones requieren backups)
- Peace of mind ("Tenemos backups, podemos recuperar")

---

## 🎯 RTO vs RPO

### Recovery Time Objective (RTO)

**Definition**: Tiempo máximo aceptable para restaurar servicio después de desastre

**Example**:
- RTO = 4 horas → Servicio debe estar UP en máximo 4 horas post-desastre

**Targets por Criticidad**:

| System Criticality | RTO Target    | Explanation                               |
| ------------------ | ------------- | ----------------------------------------- |
| **Tier 1 (Critical)** | <1 hour    | Production database, core API             |
| **Tier 2 (Important)** | <4 hours  | Analytics, reporting, admin dashboards    |
| **Tier 3 (Non-critical)** | <24 hours | Dev/test environments, internal tools |

---

### Recovery Point Objective (RPO)

**Definition**: Cantidad máxima de data que podemos perder (tiempo entre backups)

**Example**:
- RPO = 1 hora → Podemos perder máximo 1 hora de data

**Targets por Criticidad**:

| System Criticality | RPO Target  | Backup Frequency  |
| ------------------ | ----------- | ----------------- |
| **Tier 1 (Critical)** | <1 hour  | Continuous (replication) o hourly |
| **Tier 2 (Important)** | <4 hours | Every 4 hours     |
| **Tier 3 (Non-critical)** | <24 hours | Daily          |

---

### RTO vs RPO Trade-off

**Lower RTO/RPO = Higher Cost**

```
┌─────────────────────────────────┐
│  RPO <5 min, RTO <15 min        │ $$$$$ (Hot standby, real-time replication)
│  RPO <1 hour, RTO <1 hour       │ $$$   (Frequent backups, automated restore)
│  RPO <24 hours, RTO <24 hours   │ $$    (Daily backups, manual restore)
│  RPO <1 week, RTO <1 week       │ $     (Weekly backups, best effort)
└─────────────────────────────────┘
```

**Choose based on**:
- Business impact (¿cuánto cuesta 1 hora de downtime?)
- Compliance requirements
- Budget

---

## 💾 Backup Strategy

### Backup Types

**1. Full Backup**
- **What**: Complete copy of all data
- **When**: Weekly (Sundays)
- **Duration**: Longest (hours)
- **Storage**: Highest

**2. Incremental Backup**
- **What**: Only data changed since last backup (full or incremental)
- **When**: Daily
- **Duration**: Fast (minutes)
- **Storage**: Low
- **Restore**: Slower (need full + all incrementals)

**3. Differential Backup**
- **What**: Only data changed since last full backup
- **When**: Daily
- **Duration**: Medium
- **Storage**: Medium
- **Restore**: Faster (need full + latest differential)

---

### Recommended Schedule

**Tier 1 (Critical Systems)**:

```
Sunday:    Full Backup (complete snapshot)
Monday:    Incremental Backup (changes since Sunday)
Tuesday:   Incremental Backup (changes since Monday)
Wednesday: Incremental Backup (changes since Tuesday)
Thursday:  Incremental Backup (changes since Wednesday)
Friday:    Incremental Backup (changes since Thursday)
Saturday:  Incremental Backup (changes since Friday)

+ Continuous replication to secondary region (real-time)
```

**Tier 2 (Important Systems)**:

```
Sunday:    Full Backup
Mon-Sat:   Differential Backup (changes since Sunday)
```

**Tier 3 (Non-critical)**:

```
Sunday:    Full Backup (only)
```

---

### Backup Retention (3-2-1 Rule)

**3-2-1 Backup Rule**:
- **3** copies of data (1 primary + 2 backups)
- **2** different media types (disk + cloud)
- **1** copy offsite (different geographic location)

**Retention Schedule**:

| Backup Type    | Retention Period | Storage Tier       |
| -------------- | ---------------- | ------------------ |
| **Daily**      | 30 days          | Hot (fast restore) |
| **Weekly**     | 12 weeks (3 meses) | Warm            |
| **Monthly**    | 12 months        | Cold (archival)    |
| **Yearly**     | 7 years          | Glacier (compliance) |

**Example**:
- Daily backups: Keep last 30 days
- Weekly backups: Keep last 12 weeks
- Monthly backups: Keep last 12 months
- Yearly backups: Keep 7 years (for compliance: GDPR, SOX, HIPAA)

---

## 🗄️ What to Backup

### 1. Databases

**PostgreSQL / MySQL**:

```bash
# Full backup (pg_dump)
pg_dump -h localhost -U postgres -d myapp_db -F c -f backup_$(date +%Y%m%d_%H%M%S).dump

# Automated daily backup (cron)
0 2 * * * /usr/local/bin/pg_dump -h localhost -U postgres -d myapp_db -F c -f /backups/myapp_db_$(date +\%Y\%m\%d).dump
```

**Azure SQL / Managed Database**:
- Automated backups enabled (built-in, no scripting needed)
- Point-in-time restore (can restore to any time in last 7-35 days)

---

### 2. File Storage / Object Storage

**Azure Blob Storage**:
- Enable versioning (keeps old versions of files)
- Enable soft delete (can recover deleted files for 30 days)
- Cross-region replication (geo-redundant storage)

**Code/Configuration**:
```bash
# Git repository backups
git clone --mirror https://github.com/company/myapp.git
tar -czf myapp_git_backup_$(date +%Y%m%d).tar.gz myapp.git
```

---

### 3. Configuration Files

**Kubernetes Config** (Infrastructure as Code):

```bash
# Backup all Kubernetes resources
kubectl get all --all-namespaces -o yaml > k8s_backup_$(date +%Y%m%d).yaml

# Backup secrets (encrypted)
kubectl get secrets --all-namespaces -o yaml > k8s_secrets_$(date +%Y%m%d).yaml
```

**Store in Git** (GitOps approach):
- All infrastructure as code (Terraform, Helm charts)
- Git is the backup (version controlled)

---

### 4. Application State

**Persistent Volumes** (Kubernetes):

```bash
# Snapshot PersistentVolume (Azure Disk)
az snapshot create \
  --resource-group myapp-rg \
  --name myapp-pv-snapshot-$(date +%Y%m%d) \
  --source /subscriptions/XXX/resourceGroups/myapp-rg/providers/Microsoft.Compute/disks/myapp-pv
```

---

## 🔄 Backup Automation

### Automated Backup Script (PostgreSQL)

```bash
#!/bin/bash
# /usr/local/bin/backup-postgres.sh

set -e  # Exit on error

# Config
DB_NAME="myapp_db"
DB_USER="postgres"
BACKUP_DIR="/backups/postgres"
RETENTION_DAYS=30
S3_BUCKET="s3://myapp-backups"

# Create backup directory
mkdir -p $BACKUP_DIR

# Generate backup filename
BACKUP_FILE="$BACKUP_DIR/${DB_NAME}_$(date +%Y%m%d_%H%M%S).dump"

# Perform backup
echo "Starting backup of $DB_NAME..."
pg_dump -h localhost -U $DB_USER -d $DB_NAME -F c -f $BACKUP_FILE

# Compress backup
gzip $BACKUP_FILE

# Upload to S3 (offsite)
echo "Uploading to S3..."
aws s3 cp ${BACKUP_FILE}.gz $S3_BUCKET/postgres/

# Verify backup integrity
echo "Verifying backup..."
gunzip -t ${BACKUP_FILE}.gz

# Delete old backups (local)
find $BACKUP_DIR -type f -name "*.dump.gz" -mtime +$RETENTION_DAYS -delete

echo "Backup completed: ${BACKUP_FILE}.gz"
```

---

**Cron Schedule**:

```bash
# Daily backup at 2 AM
0 2 * * * /usr/local/bin/backup-postgres.sh >> /var/log/backup.log 2>&1

# Weekly full backup at 1 AM Sunday
0 1 * * 0 /usr/local/bin/backup-postgres.sh --full >> /var/log/backup.log 2>&1
```

---

### Backup Monitoring

**Alert if backup fails**:

```yaml
# Prometheus alert
- alert: BackupFailed
  expr: time() - backup_last_success_timestamp_seconds > 86400
  for: 1h
  labels:
    severity: critical
  annotations:
    summary: "Backup has not succeeded in 24 hours"
    description: "Last successful backup was {{ $value | humanizeDuration }} ago"
```

**Daily backup report** (Slack notification):

```bash
# Send Slack notification on backup completion
curl -X POST https://hooks.slack.com/services/XXX \
  -H 'Content-Type: application/json' \
  -d "{
    \"text\": \"✅ Backup completed successfully\",
    \"attachments\": [{
      \"fields\": [
        {\"title\": \"Database\", \"value\": \"$DB_NAME\", \"short\": true},
        {\"title\": \"Size\", \"value\": \"$(du -h $BACKUP_FILE | cut -f1)\", \"short\": true},
        {\"title\": \"Timestamp\", \"value\": \"$(date)\", \"short\": false}
      ]
    }]
  }"
```

---

## 🛠️ Restoration Procedures

### Database Restoration (PostgreSQL)

**1. Restore from Latest Backup**

```bash
# Download backup from S3
aws s3 cp s3://myapp-backups/postgres/myapp_db_20250115.dump.gz /tmp/

# Decompress
gunzip /tmp/myapp_db_20250115.dump.gz

# Drop existing database (CAREFUL!)
psql -h localhost -U postgres -c "DROP DATABASE IF EXISTS myapp_db;"

# Create new database
psql -h localhost -U postgres -c "CREATE DATABASE myapp_db;"

# Restore backup
pg_restore -h localhost -U postgres -d myapp_db /tmp/myapp_db_20250115.dump

# Verify data
psql -h localhost -U postgres -d myapp_db -c "SELECT COUNT(*) FROM users;"
```

**ETA**: 30 min - 2 hours (depending on database size)

---

**2. Point-in-Time Recovery (Azure SQL)**

```bash
# Restore to specific point in time
az sql db restore \
  --resource-group myapp-rg \
  --server myapp-sql-server \
  --name myapp-db-restored \
  --source-database myapp-db \
  --time "2025-01-15T14:32:00Z"  # Restore to this timestamp

# Switch application to restored database
# Update connection string in application config
```

**ETA**: 15-60 min

---

### File Restoration

**Restore deleted file** (Azure Blob soft delete):

```bash
# List deleted blobs
az storage blob list \
  --account-name myappstorageacct \
  --container-name backups \
  --include d \
  --output table

# Undelete blob
az storage blob undelete \
  --account-name myappstorageacct \
  --container-name backups \
  --name myfile.txt
```

**ETA**: <5 min

---

### Full Infrastructure Restoration (Disaster Recovery)

**Scenario**: Primary region (East US) completely down → Failover to secondary region (West US)

**Steps**:

1. **Activate Secondary Database** (geo-replication)
   ```bash
   az sql db failover-group failover \
     --resource-group myapp-rg \
     --server myapp-sql-server-secondary
   ```

2. **Route Traffic to Secondary Region** (DNS/Traffic Manager)
   ```bash
   az network traffic-manager endpoint update \
     --resource-group myapp-rg \
     --profile-name myapp-tm \
     --name secondary-endpoint \
     --type azureEndpoints \
     --priority 1  # Make secondary primary
   ```

3. **Deploy Application to Secondary Region** (if not already running)
   ```bash
   # Deploy from backup or Git
   kubectl apply -f k8s-manifests/ --namespace=production-west
   ```

4. **Verify Functionality**
   - Smoke tests
   - Check dashboards (error rates, latency)

**ETA**: 2-4 hours (RTO)

---

## 🧪 Backup Testing

### Monthly Restoration Test

**Why**: Untested backups = No backups

**Process** (every month):

1. **Select random backup** from last month
2. **Restore to test environment**
3. **Verify data integrity**:
   - Row counts match
   - Critical records exist
   - No corruption
4. **Document results** (success/failure, time taken)
5. **Update runbook** if issues found

---

**Test Checklist**:

```markdown
## Backup Restoration Test - January 2025

- [ ] Backup selected: myapp_db_20250115.dump
- [ ] Restoration started: 2025-01-20 10:00
- [ ] Restoration completed: 2025-01-20 10:45 (45 min)
- [ ] Data integrity check:
  - [ ] Users table: 10,245 rows (expected: 10,245) ✅
  - [ ] Orders table: 52,301 rows (expected: 52,300) ⚠️ (1 missing?)
  - [ ] Products table: 1,532 rows (expected: 1,532) ✅
- [ ] Application smoke tests: PASSED ✅
- [ ] Issues found: 1 order missing (investigate)
- [ ] Action items:
  - [ ] Investigate missing order (check backup logs)
  - [ ] Update backup verification script

**Result**: ✅ PASSED (with minor issue)
**Tested by**: @alice-devops
```

---

## 🏗️ Disaster Recovery (DR) Plan

### DR Scenarios

**Scenario 1: Database Corruption**
- **Impact**: All data inaccessible
- **Recovery**: Restore from latest backup
- **RTO**: <1 hour
- **RPO**: <1 hour

**Scenario 2: Ransomware Attack**
- **Impact**: Files encrypted
- **Recovery**: Restore from offline backup (attacker can't delete)
- **RTO**: <4 hours
- **RPO**: <4 hours

**Scenario 3: Regional Outage (Azure East US down)**
- **Impact**: Primary region unavailable
- **Recovery**: Failover to West US
- **RTO**: <2 hours
- **RPO**: <5 min (geo-replication)

**Scenario 4: Accidental Data Deletion**
- **Impact**: Critical table dropped
- **Recovery**: Point-in-time restore
- **RTO**: <1 hour
- **RPO**: 0 (can restore to exact moment before deletion)

---

### DR Runbook

```markdown
# Disaster Recovery Runbook

## When to Activate DR

- Primary region down >30 min
- Data corruption detected
- Ransomware attack confirmed
- Catastrophic failure (fire, flood, etc.)

## DR Activation Steps

### 1. Assess Situation (5 min)
- [ ] Confirm disaster (not just transient issue)
- [ ] Identify scope (database only? full region?)
- [ ] Notify stakeholders (#incidents channel)

### 2. Activate War Room (5 min)
- [ ] Create #dr-YYYYMMDD Slack channel
- [ ] Assemble team:
  - Incident Commander: DevOps Lead
  - Database Admin
  - Application Engineer
  - Customer Support Lead

### 3. Execute Recovery (varies by scenario)

**Option A: Database Restore**
- [ ] Download latest backup from S3
- [ ] Restore to new database instance
- [ ] Update application connection string
- [ ] Verify data integrity
- ETA: 1 hour

**Option B: Regional Failover**
- [ ] Failover database to secondary region
- [ ] Route traffic to secondary region (DNS)
- [ ] Deploy application to secondary region
- [ ] Verify functionality
- ETA: 2-4 hours

### 4. Verify Recovery (30 min)
- [ ] Smoke tests passed
- [ ] Error rate <1%
- [ ] Latency normal
- [ ] Critical user flows working

### 5. Communicate (ongoing)
- [ ] Update status page: "Service restored"
- [ ] Notify Customer Support
- [ ] Post-mortem scheduled (48h)

### 6. Post-Recovery (next 24h)
- [ ] Monitor for issues
- [ ] Investigate root cause
- [ ] Update DR plan based on learnings
```

---

## 📊 Backup Metrics

### Metric #1: Backup Success Rate

**Target**: >99% (backups succeed)

**Alert**: <95% → Investigate backup failures

---

### Metric #2: Backup Duration

**Target**: <1 hour for daily backups

**Track**: Is backup getting slower? (database growing)

---

### Metric #3: Restoration Test Success Rate

**Target**: 100% (all monthly tests pass)

**Alert**: Test fails → Fix backup process immediately

---

### Metric #4: RTO/RPO Achievement

**Target**: Achieve RTO/RPO targets in tests

**Track**: Actual restoration time vs target

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | DevOps | DBA | Developer | Manager |
| --------------------------------- | ------ | --- | --------- | ------- |
| Configure backup automation       | R/A    | C   | I         | I       |
| Monitor backup success            | R/A    | C   | I         | I       |
| Perform restoration tests         | R      | A   | C         | I       |
| Execute disaster recovery         | R      | A   | C         | I       |
| Update DR plan                    | R/A    | C   | C         | C       |
| Approve backup retention policy   | C      | C   | I         | A       |

---

## 🚀 Implementation Roadmap

### Sprint 1: Automated Backups
- [ ] Configure automated database backups
- [ ] Setup S3/Azure Blob for backup storage
- [ ] Test backup script

### Sprint 2: Monitoring & Alerts
- [ ] Alert on backup failures
- [ ] Daily backup report (Slack)
- [ ] Backup size tracking

### Sprint 3: Restoration Testing
- [ ] Write restoration runbook
- [ ] Perform first restoration test
- [ ] Schedule monthly tests (calendar)

### Sprint 4: Disaster Recovery
- [ ] Write DR plan
- [ ] Setup secondary region (geo-replication)
- [ ] DR drill (simulate regional outage)

---

## ✅ Success Criteria

### Mes 1
- ✅ Automated backups running daily
- ✅ Backups monitored (alerts on failure)
- ✅ First restoration test completed

### Mes 2-3
- ✅ Monthly restoration tests passing
- ✅ DR plan documented
- ✅ RTO/RPO targets met in tests

### Mes 4+
- ✅ Zero backup failures
- ✅ 100% restoration test success rate
- ✅ DR drill completed (full regional failover)

---

## 🔗 Links Relacionados

- [Incident Management](./incident-management.md) - Disaster response procedures
- [Monitoring & Alerting](./monitoring-alerting.md) - Backup monitoring

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-06  
**Owner**: DevOps Lead / DBA  
**Review Cycle**: Trimestral
