# Documentation Ownership - Ownership de Documentación Técnica

## 📋 Resumen Ejecutivo

**Problema**: READMEs desactualizados (instrucciones de 2 años no funcionan). Runbooks obsoletos (nuevo on-call no puede resolver incidentes). ADRs sin owner (nadie sabe quién decidió qué). Docs huérfanas (nadie sabe quién mantiene qué).

**Solución**: **Documentation ownership model** claro con RACI matrix, review cycles, automated staleness detection, y ownership assignment.

**Beneficio**:
- Docs actualizados (>90% frescos <90 días)
- Onboarding más rápido (nuevos developers pueden self-serve)
- Menos incidentes (runbooks funcionan cuando los necesitas)
- Knowledge retention (decisiones documentadas permanecen)

---

## 📁 Documentation Types & Ownership

### 1. READMEs (Project Documentation)

**Purpose**: Cómo setup/run/deploy proyecto

**Locations**:
- `/README.md` (root - main project)
- `/services/api/README.md` (service-specific)
- `/docs/teams/frontend/README.md` (team-specific)

**Owner**: **Tech Lead del proyecto/servicio**
**Backup**: **Senior Developer en el equipo**

**Content Requirements**:
```markdown
# Project Name

## What is this?
[1-2 sentences - what does this service do?]

## Quick Start
```bash
npm install
npm run dev
```

## Prerequisites
- Node 18+
- PostgreSQL 14+
- Redis 6+

## Environment Variables
```bash
DATABASE_URL=postgresql://localhost:5432/mydb
REDIS_URL=redis://localhost:6379
API_KEY=your-key-here
```

## Running Locally
[Step-by-step instructions]

## Running Tests
```bash
npm test
```

## Deploying
[How to deploy to staging/production]

## Troubleshooting
[Common issues + solutions]

## Architecture
[High-level diagram + explanation]

## Links
- [API Docs](./docs/api.md)
- [Runbook](./docs/runbook.md)
- [ADRs](./docs/adr/)

## Owner
**Owner**: @tech-lead  
**Last Updated**: 2025-12-07  
**Review Cycle**: Monthly
```

**Review Cycle**: **Monthly** (last Friday of month)
**Staleness Threshold**: 90 days (if not updated in 90 days → flagged as stale)

---

### 2. Runbooks (Operational Documentation)

**Purpose**: Cómo responder a incidentes/alerts

**Location**: `/docs/runbooks/`

**Owner**: **DevOps Lead / On-Call Rotation**
**Backup**: **SRE Team**

**Content Requirements**:
```markdown
# Runbook: [Service] - [Alert Name]

## Alert Details
**Alert Name**: `HighAPILatency`  
**Severity**: SEV-2  
**Threshold**: P95 latency >500ms for 5 minutes  
**PagerDuty**: Alerts #on-call

## Symptoms
- API responses slow (>500ms)
- Users complain about "slow app"
- Datadog dashboard shows red

## Impact
- **User Impact**: Slow UX, some users may timeout
- **Business Impact**: Potential revenue loss if checkout slow

## Triage Steps (First 5 Minutes)

1. **Check service health**:
   ```bash
   kubectl get pods -n production
   ```
   Look for: CrashLoopBackOff, OOMKilled

2. **Check database**:
   ```bash
   psql -c "SELECT COUNT(*) FROM pg_stat_activity;"
   ```
   Look for: >100 connections (max is 100)

3. **Check external dependencies**:
   - Stripe API status: https://status.stripe.com
   - AWS status: https://health.aws.amazon.com

## Common Causes

### Cause 1: Database Connection Pool Exhausted
**Symptoms**: `FATAL: sorry, too many clients already`
**Solution**:
```bash
# Restart app (clears connections)
kubectl rollout restart deployment api -n production
```
**Prevention**: Increase connection pool limit (currently 20 → 50)

### Cause 2: Memory Leak
**Symptoms**: Pods restarting frequently (OOMKilled)
**Solution**:
```bash
# Increase memory limit temporarily
kubectl set resources deployment api --limits=memory=2Gi -n production
```
**Follow-up**: Profile app for memory leak (create Jira ticket)

### Cause 3: External API Down (Stripe)
**Symptoms**: Stripe status page shows outage
**Solution**:
- No fix on our end (wait for Stripe)
- Post in #incidents: "Stripe is down, checkout affected"
- Enable degraded mode (allow checkout without payment processing)

## Escalation

**If not resolved in 15 minutes**:
- Escalate to @devops-lead (Slack + phone)
- Create #incident-YYYY-MM-DD-api-latency channel
- Follow incident communication protocol

## Post-Incident

- [ ] Write post-mortem (within 48 hours)
- [ ] Update runbook if new info learned
- [ ] Create Jira tickets for prevention measures

## Owner
**Owner**: @devops-lead  
**Last Updated**: 2025-12-07  
**Review Cycle**: After every incident + Monthly
```

**Review Cycle**: 
- **Monthly** (proactive review)
- **After every incident** (update with lessons learned)

**Staleness Threshold**: 60 days (runbooks go stale fast)

---

### 3. ADRs (Architecture Decision Records)

**Purpose**: Documentar decisiones técnicas (why we chose X over Y)

**Location**: `/docs/adr/`

**Owner**: **Architect / Person who made decision**
**Backup**: **Tech Lead**

**Naming Convention**: `ADR-XXX-brief-title.md` (e.g., `ADR-001-migrate-to-postgres.md`)

**Content Requirements** (use template):
```markdown
# ADR-001: Migrate from MySQL to PostgreSQL

**Date**: 2025-12-07  
**Status**: Accepted  
**Deciders**: @architect, @cto  
**Consulted**: @devops-lead, @backend-team

## Context

We currently use MySQL 5.7 for our database. We're hitting scaling issues:
- Complex queries slow (no window functions)
- JSON support limited (need better JSON querying)
- Replication lag high (>5 seconds)

We need to migrate to a database with better:
- JSON support
- Advanced SQL features (CTEs, window functions)
- Replication performance

## Decision

**We will migrate from MySQL 5.7 to PostgreSQL 14.**

## Rationale

**Why PostgreSQL**:
- ✅ Best-in-class JSON support (`jsonb` type, fast queries)
- ✅ Advanced SQL (CTEs, window functions, full-text search)
- ✅ Better replication (logical replication, <1s lag)
- ✅ Open source (no licensing issues)

**Why NOT other options**:
- ❌ **MongoDB**: Schemaless not good for transactional data
- ❌ **Oracle**: Too expensive ($10K+/month)
- ❌ **Stay on MySQL**: Doesn't solve scaling issues

## Consequences

**Positive**:
- ✅ Faster complex queries (3-5x faster with window functions)
- ✅ Better JSON querying (can index `jsonb` columns)
- ✅ Lower replication lag (<1s vs 5s)

**Negative**:
- ❌ Migration cost (2 weeks engineering time)
- ❌ Team training (devs need to learn PostgreSQL nuances)
- ❌ Some MySQL queries need rewriting (minor syntax differences)

## Implementation Plan

**Phase 1** (Week 1-2): Setup
- [ ] Provision PostgreSQL 14 on AWS RDS
- [ ] Configure replication from MySQL → PostgreSQL
- [ ] Test data sync

**Phase 2** (Week 3-4): Migration
- [ ] Rewrite incompatible queries
- [ ] Run dual-write (write to both MySQL + PostgreSQL)
- [ ] Validate data consistency

**Phase 3** (Week 5-6): Cutover
- [ ] Switch reads to PostgreSQL (monitored rollout)
- [ ] Monitor performance (7 days)
- [ ] Decommission MySQL

**Owner**: @devops-lead  
**Deadline**: 2026-01-31  
**Success Criteria**: 
- Zero data loss
- <100ms P95 latency (same as MySQL)
- Zero downtime

## Follow-Up

- [ ] Update runbooks (new database connection strings)
- [ ] Update READMEs (PostgreSQL setup instructions)
- [ ] Train team (PostgreSQL best practices workshop)

## References

- [PostgreSQL vs MySQL Benchmark](https://example.com/benchmark)
- [AWS RDS PostgreSQL Pricing](https://aws.amazon.com/rds/postgresql/pricing/)
- [Team Discussion Thread](https://company.slack.com/archives/C123/p1234567890)

## Owner
**Owner**: @architect  
**Last Updated**: 2025-12-07  
**Review Cycle**: Yearly (or when decision revisited)
```

**Review Cycle**: **Yearly** (ADRs rarely change, but revisit if context changes)

**Staleness Threshold**: 365 days (ADRs are timeless, but review yearly)

---

### 4. API Documentation

**Purpose**: Cómo usar APIs (endpoints, request/response formats)

**Location**: 
- `/docs/api/` (generated from OpenAPI/Swagger)
- Hosted on docs site (e.g., `https://docs.company.com/api`)

**Owner**: **Backend Team Lead**
**Backup**: **API Developer (who built the endpoint)**

**Content Requirements**:
- Auto-generated from code (OpenAPI spec)
- Examples for every endpoint
- Authentication guide
- Error codes reference

**Example** (OpenAPI snippet):
```yaml
paths:
  /users/{id}:
    get:
      summary: Get user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
              example:
                id: 123
                name: "John Doe"
                email: "john@example.com"
        '404':
          description: User not found
```

**Review Cycle**: **Every deployment** (auto-generated docs update on deploy)

**Staleness Threshold**: N/A (auto-generated, always fresh)

---

### 5. Team Wikis (Confluence/Notion)

**Purpose**: Product specs, design docs, meeting notes

**Location**: Confluence (e.g., `company.atlassian.net`)

**Owner**: **Product Manager (product docs) or Engineering Manager (engineering docs)**

**Content Examples**:
- Product specs (PRDs)
- Design docs (system design)
- Meeting notes (sprint planning, retros)
- Onboarding guides

**Review Cycle**: **Quarterly** (too many docs to review monthly)

**Staleness Threshold**: 180 days (Confluence docs can be long-lived)

---

## 🎭 RACI: Documentation Responsibilities

| Doc Type | Create | Update | Review | Archive |
|----------|--------|--------|--------|---------|
| **READMEs** | R: Developer<br>A: Tech Lead | R: Tech Lead<br>A: Tech Lead | R: Team<br>A: Tech Lead | R: Tech Lead<br>A: EM |
| **Runbooks** | R: On-Call<br>A: DevOps Lead | R: On-Call<br>A: DevOps Lead | R: SRE Team<br>A: DevOps Lead | R: DevOps Lead<br>A: EM |
| **ADRs** | R: Architect<br>A: Architect | R: Architect<br>A: Architect | R: Tech Leads<br>A: CTO | R: Architect<br>A: CTO |
| **API Docs** | R: Auto-generated<br>A: Backend Lead | R: Auto-generated<br>A: Backend Lead | R: Backend Team<br>A: Backend Lead | N/A (auto-updated) |
| **Wikis** | R: PM/EM<br>A: PM/EM | R: PM/EM<br>A: PM/EM | R: Team<br>A: PM/EM | R: PM/EM<br>A: Director |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## ⏰ Review Cycles (Summary)

| Doc Type | Review Frequency | Staleness Threshold | Owner |
|----------|------------------|---------------------|-------|
| **READMEs** | Monthly (last Friday) | 90 days | Tech Lead |
| **Runbooks** | Monthly + After incidents | 60 days | DevOps Lead |
| **ADRs** | Yearly | 365 days | Architect |
| **API Docs** | Every deployment (auto) | N/A (auto-updated) | Backend Lead |
| **Wikis** | Quarterly | 180 days | PM/EM |

---

## 🤖 Automated Staleness Detection

### GitHub Action (For Docs in Git)

**File**: `.github/workflows/stale-docs.yml`

```yaml
name: Stale Docs Detection

on:
  schedule:
    - cron: '0 9 * * 1' # Every Monday 9am

jobs:
  check-staleness:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Find stale READMEs
        run: |
          # Find READMEs not updated in 90 days
          find . -name "README.md" -mtime +90 > stale-readmes.txt
          
      - name: Find stale runbooks
        run: |
          # Find runbooks not updated in 60 days
          find ./docs/runbooks -name "*.md" -mtime +60 > stale-runbooks.txt
          
      - name: Post to Slack
        if: ${{ hashFiles('stale-readmes.txt') != '' || hashFiles('stale-runbooks.txt') != '' }}
        run: |
          curl -X POST ${{ secrets.SLACK_WEBHOOK_URL }} \
            -H 'Content-Type: application/json' \
            -d '{
              "text": "⚠️ Stale docs detected!",
              "blocks": [
                {
                  "type": "section",
                  "text": {
                    "type": "mrkdwn",
                    "text": "*Stale READMEs*:\n```$(cat stale-readmes.txt)```"
                  }
                },
                {
                  "type": "section",
                  "text": {
                    "type": "mrkdwn",
                    "text": "*Stale Runbooks*:\n```$(cat stale-runbooks.txt)```"
                  }
                }
              ]
            }'
```

**Slack Message** (example):
```
⚠️ Stale docs detected!

Stale READMEs (not updated in 90 days):
- /services/api/README.md (last updated 120 days ago)
- /services/worker/README.md (last updated 150 days ago)

Stale Runbooks (not updated in 60 days):
- /docs/runbooks/high-cpu.md (last updated 75 days ago)

@tech-lead Please review and update.
```

---

### Confluence Staleness Bot

**Tool**: Use Confluence API to detect stale pages

**Script**: `scripts/check-confluence-staleness.js`

```javascript
// Pseudo-code
const confluenceAPI = require('confluence-api');

// Find pages not updated in 180 days
const stalePages = await confluenceAPI.search({
  cql: 'lastModified < now("-180d") AND space = "ENG"'
});

// Post to Slack
await slack.postMessage({
  channel: '#engineering',
  text: `⚠️ ${stalePages.length} stale Confluence pages detected`,
  attachments: stalePages.map(page => ({
    title: page.title,
    title_link: page.url,
    text: `Last updated: ${page.lastModified} (${page.owner})`
  }))
});
```

**Run**: Weekly (cron job on Jenkins)

---

## 📝 Doc Update Process

### Monthly Review (For READMEs/Runbooks)

**Last Friday of every month** (30 min):

1. ✅ **Staleness bot posts report** (automated):
   ```markdown
   ⚠️ Monthly Doc Review (December 2025)
   
   Stale READMEs (3):
   - /services/api/README.md (@tech-lead-api)
   - /services/worker/README.md (@tech-lead-worker)
   - /docs/teams/frontend/README.md (@tech-lead-frontend)
   
   Stale Runbooks (2):
   - /docs/runbooks/high-cpu.md (@devops-lead)
   - /docs/runbooks/disk-full.md (@devops-lead)
   
   Please review and update by EOD Friday.
   ```

2. ✅ **Owners review their docs** (15 min each):
   - Read through doc
   - Test instructions (do they still work?)
   - Update if needed
   - If no changes needed → Update "Last Updated" date (proves it was reviewed)

3. ✅ **Owners confirm completion** (post in #engineering):
   ```markdown
   ✅ December doc review complete:
   
   - /services/api/README.md - Updated (fixed env vars)
   - /services/worker/README.md - No changes (still accurate)
   
   @engineering-manager
   ```

---

### Incident-Driven Update (For Runbooks)

**After every incident** (within 48 hours):

1. ✅ **Incident Commander updates runbook** (during post-mortem):
   - What was missing from runbook?
   - What new information did we learn?
   - What steps should we add?

2. ✅ **Create PR** (runbook update):
   ```markdown
   Title: Update high-cpu runbook (from incident 2025-12-07)
   
   Changes:
   - Added step to check Redis memory (was missing)
   - Updated threshold (500ms → 300ms based on incident)
   - Added new common cause: Redis memory leak
   
   Incident: #incident-2025-12-07-api-latency
   ```

3. ✅ **DevOps Lead reviews + merges**

---

## 🗂️ Doc Archival Process

**When to archive docs**:
- ❌ Service decommissioned (README no longer needed)
- ❌ Decision superseded (ADR replaced by new ADR)
- ❌ Process changed (runbook no longer relevant)

**How to archive**:

1. ✅ **Move to `/docs/archive/`**:
   ```bash
   git mv docs/runbooks/old-service.md docs/archive/runbooks/old-service.md
   git commit -m "Archive old-service runbook (service decommissioned)"
   ```

2. ✅ **Add archive notice**:
   ```markdown
   # [ARCHIVED] Runbook: Old Service
   
   > ⚠️ **This doc is archived** (2025-12-07)
   > 
   > **Reason**: Service decommissioned
   > **Replacement**: See [new-service runbook](../runbooks/new-service.md)
   
   [Original content below...]
   ```

3. ✅ **Update links**:
   - Find all docs linking to archived doc
   - Update links to point to replacement (or remove if no replacement)

---

## 📊 Documentation Health Metrics

### Metrics to Track

| Metric | Target | Red Flag | How to Measure |
|--------|--------|----------|----------------|
| **Doc Freshness** | >90% docs updated <90 days | <70% | GitHub Action report |
| **Runbook Accuracy** | 100% runbooks tested in last incident | <80% | Post-mortem feedback |
| **Onboarding Time** | New hire can setup locally <2 hours | >4 hours | Onboarding survey |
| **Stale Docs Count** | <5 stale docs | >20 | Weekly bot report |
| **Doc Coverage** | Every service has README | <90% coverage | Manual audit (quarterly) |

---

### Dashboard (Example - Datadog/Grafana)

**Metrics to visualize**:
- Stale docs count (last 30 days)
- Docs updated (last 7 days)
- Average time to update doc (after incident)
- New hire onboarding time (self-reported)

---

## ✅ Success Criteria

### Mes 1
- ✅ Documentation ownership assigned (RACI matrix)
- ✅ Staleness bot deployed (weekly reports)
- ✅ First monthly review completed

### Mes 2-3
- ✅ Doc freshness >80% (<90 days)
- ✅ Zero stale runbooks (<60 days)
- ✅ New hire onboarding time <3 hours (can setup locally)

### Mes 4+
- ✅ Doc freshness >90%
- ✅ 100% runbooks tested in incidents
- ✅ New hire onboarding time <2 hours
- ✅ Team satisfaction >4/5 (docs are helpful)

---

## 🔗 Links Relacionados

- [Onboarding Guide](./onboarding-guide.md) - Docs nuevos hires necesitan
- [Channel Ownership](./channel-ownership.md) - Dónde postear doc updates
- [Incident Communication](./incident-communication.md) - Cómo comunicar runbook updates
- [Post-Mortem Process](../procesos/post-mortem.md) - Actualizar runbooks después de incidentes

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (team feedback)
