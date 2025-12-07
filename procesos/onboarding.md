# Onboarding - Incorporación de Nuevos Miembros al Equipo

## 📋 Resumen Ejecutivo

**Problema**: Nuevo engineer llega → No sabe qué hacer, pide accesos por semanas, no es productivo por 3 meses.

**Solución**: **Onboarding plan estructurado** con Day 1/Week 1/Month 1 checklist, accesos automatizados, buddy system.

**Beneficio**:
- Time to first PR: 3 días (vs 3 semanas)
- Time to productivity: 1 mes (vs 3 meses)
- Retention: +20% (buenos primeros días = se queda)
- Consistency: Todos reciben el mismo onboarding

---

## 🎯 Onboarding Timeline

### Day 1 (First Day)

**Goal**: ¡Bienvenido! Laptop configurado, cuentas activas, primer commit.

**Schedule**:

```
09:00 - 09:30  Welcome meeting (Manager)
09:30 - 10:00  Laptop setup (IT)
10:00 - 11:00  Accounts & access provisioning
11:00 - 12:00  Code tour (Buddy)
12:00 - 13:00  Lunch con equipo
13:00 - 14:30  Dev environment setup
14:30 - 16:00  First task (typo fix, small bug)
16:00 - 17:00  Daily standup + team introductions
17:00 - 17:30  Day 1 retro (Manager check-in)
```

**Checklist**:

- [ ] **Welcome Meeting** (Manager)
  - [ ] Team overview (quiénes somos, qué hacemos)
  - [ ] Project roadmap (qué estamos construyendo)
  - [ ] Expectations (horarios, comunicación, cultura)
  - [ ] Questions answered

- [ ] **Laptop Setup** (IT / Self-service)
  - [ ] Laptop received (Mac/Windows)
  - [ ] OS updates installed
  - [ ] Corporate VPN installed
  - [ ] Slack installed + logged in
  - [ ] Email configured
  - [ ] Password manager installed (1Password, Bitwarden)

- [ ] **Accounts Created** (Auto-provisioning via script)
  - [ ] GitHub account added to `company` org
  - [ ] Azure subscription access granted
  - [ ] Datadog account created
  - [ ] PagerDuty account created (for on-call)
  - [ ] Jira/ADO account created
  - [ ] Slack channels joined:
    - [ ] #team-devops (main channel)
    - [ ] #incidents
    - [ ] #deployments
    - [ ] #random

- [ ] **Code Access** (Git clone)
  - [ ] SSH key generated + added to GitHub
  - [ ] Repositories cloned:
    ```bash
    git clone git@github.com:company/myapp-api.git
    git clone git@github.com:company/myapp-frontend.git
    git clone git@github.com:company/infrastructure.git
    ```
  - [ ] Dev environment setup (follow README.md)
  - [ ] Application running locally (http://localhost:3000)

- [ ] **First Commit** (Day 1 win!)
  - [ ] Pick "good first issue" (typo fix, update docs)
  - [ ] Create branch, make change, submit PR
  - [ ] PR reviewed by buddy
  - [ ] PR merged → FIRST COMMIT! 🎉

- [ ] **Team Introductions** (Standup)
  - [ ] Introduce yourself (30 sec: background, fun fact)
  - [ ] Meet the team (names, roles)

- [ ] **Day 1 Retro** (Manager check-in)
  - [ ] How did today go?
  - [ ] Anything blocking?
  - [ ] Questions?

**Expected Outcome**: Engineer feels welcome, has working laptop, made first commit.

---

### Week 1 (First 5 Days)

**Goal**: Understand codebase, submit real PR, shadow on-call.

**Checklist**:

- [ ] **Codebase Orientation** (Buddy-led)
  - [ ] Architecture overview (diagram)
    - API (Node.js/Express)
    - Frontend (React)
    - Database (PostgreSQL)
    - Infrastructure (Kubernetes)
  - [ ] Code walkthrough:
    - [ ] How authentication works
    - [ ] How API requests flow
    - [ ] Where data is stored
    - [ ] How deployments happen
  - [ ] Key files/directories:
    - [ ] `src/` - Application code
    - [ ] `tests/` - Unit/integration tests
    - [ ] `k8s/` - Kubernetes manifests
    - [ ] `docs/` - Architecture docs

- [ ] **Development Workflow** (Pair programming)
  - [ ] Git workflow (branching, commit messages)
  - [ ] PR process (how to submit, review, merge)
  - [ ] Testing (run tests locally, write new test)
  - [ ] Debugging (use debugger, check logs)

- [ ] **Real Work** (First feature)
  - [ ] Pick task from backlog (small feature, ~2-3 days)
  - [ ] Implement feature (pair with buddy)
  - [ ] Write tests
  - [ ] Submit PR
  - [ ] Address review comments
  - [ ] PR merged → Second commit! 🎉

- [ ] **Operations Basics** (DevOps)
  - [ ] How to deploy (CI/CD pipeline)
  - [ ] How to check logs (kubectl logs, Datadog)
  - [ ] How to check metrics (Grafana dashboards)
  - [ ] How to rollback (kubectl rollout undo)

- [ ] **Shadow On-Call** (Friday afternoon)
  - [ ] Join on-call engineer for 2 hours
  - [ ] See how alerts work
  - [ ] Watch incident response
  - [ ] Ask questions

- [ ] **Week 1 Retro** (Manager check-in)
  - [ ] How was your week?
  - [ ] Feeling productive?
  - [ ] What's confusing?
  - [ ] Action items for Week 2

**Expected Outcome**: Engineer understands codebase, submitted real PR, shadowed on-call.

---

### Month 1 (First 30 Days)

**Goal**: Fully productive, first on-call shift, leading small feature.

**Checklist**:

- [ ] **Productivity Milestones**
  - [ ] 5+ PRs merged
  - [ ] Led 1 feature end-to-end (design → code → deploy)
  - [ ] Fixed 1 bug independently
  - [ ] Reviewed 3+ PRs from teammates

- [ ] **On-Call Readiness**
  - [ ] PagerDuty account configured
  - [ ] Runbooks reviewed (incident response)
  - [ ] Shadowed on-call 3+ times
  - [ ] First on-call shift (with backup support)

- [ ] **Technical Depth**
  - [ ] Attended architecture review
  - [ ] Deployed to production (with supervision)
  - [ ] Participated in post-mortem
  - [ ] Wrote documentation (update README, runbook)

- [ ] **Team Integration**
  - [ ] 1:1 with all team members
  - [ ] Presented in team meeting (demo your work)
  - [ ] Participated in retrospective
  - [ ] Joined team lunch/social event

- [ ] **Month 1 Review** (Manager)
  - [ ] Performance check-in
  - [ ] Feedback (what's going well, what to improve)
  - [ ] Goals for Month 2-3
  - [ ] Career development discussion

**Expected Outcome**: Engineer is fully productive, comfortable on-call, integrated into team.

---

## 🔐 Access Provisioning

### Automated Access Script

**Goal**: Provision all accounts in <1 hour (vs manual 2-3 days)

**Script** (`onboard-user.sh`):

```bash
#!/bin/bash
# onboard-user.sh - Automate new hire access provisioning

set -e

NEW_HIRE_EMAIL=$1
NEW_HIRE_NAME=$2

if [ -z "$NEW_HIRE_EMAIL" ] || [ -z "$NEW_HIRE_NAME" ]; then
  echo "Usage: ./onboard-user.sh <email> <name>"
  echo "Example: ./onboard-user.sh alice@company.com 'Alice Smith'"
  exit 1
fi

echo "🚀 Onboarding $NEW_HIRE_NAME ($NEW_HIRE_EMAIL)..."

# 1. GitHub
echo "Adding to GitHub..."
gh api \
  --method PUT \
  -H "Accept: application/vnd.github+json" \
  /orgs/company/memberships/$NEW_HIRE_EMAIL

gh api \
  --method PUT \
  -H "Accept: application/vnd.github+json" \
  /orgs/company/teams/developers/memberships/$NEW_HIRE_EMAIL

# 2. Azure (assign Contributor role)
echo "Granting Azure access..."
az role assignment create \
  --assignee $NEW_HIRE_EMAIL \
  --role "Contributor" \
  --scope "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/myapp-rg"

# 3. Datadog
echo "Creating Datadog user..."
curl -X POST "https://api.datadoghq.com/api/v1/user" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -H "Content-Type: application/json" \
  -d "{
    \"handle\": \"$NEW_HIRE_EMAIL\",
    \"name\": \"$NEW_HIRE_NAME\",
    \"access_role\": \"st\"
  }"

# 4. PagerDuty
echo "Creating PagerDuty user..."
curl -X POST "https://api.pagerduty.com/users" \
  -H "Authorization: Token token=${PD_API_TOKEN}" \
  -H "Content-Type: application/json" \
  -d "{
    \"user\": {
      \"name\": \"$NEW_HIRE_NAME\",
      \"email\": \"$NEW_HIRE_EMAIL\",
      \"role\": \"user\"
    }
  }"

# 5. Slack (send welcome message)
echo "Sending Slack welcome..."
curl -X POST https://slack.com/api/chat.postMessage \
  -H "Authorization: Bearer $SLACK_BOT_TOKEN" \
  -H "Content-Type: application/json" \
  -d "{
    \"channel\": \"#team-devops\",
    \"text\": \"Welcome to the team, $NEW_HIRE_NAME! 🎉\"
  }"

echo "✅ Onboarding complete!"
echo "📧 Send welcome email with credentials to: $NEW_HIRE_EMAIL"
```

**Usage**:

```bash
./onboard-user.sh alice@company.com "Alice Smith"
```

**ETA**: <5 min (vs manual 2-3 days)

---

### Access Checklist (Manual Review)

**Before Day 1**:

- [ ] HR adds to HRIS (BambooHR, Workday)
- [ ] IT orders laptop (ships to home)
- [ ] Manager runs onboarding script
- [ ] Manager assigns buddy
- [ ] Manager schedules Day 1 meetings

**Day 1**:

- [ ] Verify all accounts active:
  - [ ] Email works
  - [ ] GitHub access granted
  - [ ] Azure access granted
  - [ ] Datadog login works
  - [ ] PagerDuty login works
  - [ ] Slack channels joined

**Week 1**:

- [ ] VPN access granted (if remote)
- [ ] Office badge activated (if on-site)
- [ ] Calendar shared (see team events)

---

## 👥 Buddy System

### What is a Buddy?

**Buddy**: Experienced engineer assigned to new hire for first 3 months

**NOT a manager** (manager = performance reviews, promotions)

**IS a peer** (buddy = technical questions, culture guide, friend)

---

### Buddy Responsibilities

**Week 1**:
- [ ] Code walkthrough (2 hours)
- [ ] Pair programming (4 hours)
- [ ] Daily check-ins (15 min standup)
- [ ] Help with first PR

**Week 2-4**:
- [ ] Weekly 1:1 (30 min)
- [ ] Review PRs promptly (<4 hours)
- [ ] Answer technical questions (Slack)
- [ ] Introduce to team members

**Month 2-3**:
- [ ] Biweekly check-ins (30 min)
- [ ] Share tribal knowledge (why we do X, not Y)
- [ ] Invite to relevant meetings
- [ ] Career advice (how to grow here)

---

### Buddy Selection Criteria

**Good Buddy**:
- ✅ 1+ year tenure (knows company culture)
- ✅ Strong technical skills (can answer questions)
- ✅ Patient & communicative
- ✅ Available (not on PTO, not crunching)

**Avoid**:
- ❌ Too junior (themselves still learning)
- ❌ Too busy (no time for new hire)
- ❌ Negative attitude (will influence new hire)

---

### Buddy Compensation

**Incentive**: Being a buddy counts toward performance review

**Recognition**:
- Mentioned in 360 reviews
- "Mentorship" competency
- Eligible for "Buddy of the Quarter" award

---

## 📚 Training Resources

### Self-Paced Learning (Week 1)

**Architecture Docs** (2 hours):
- [ ] Read [Architecture Overview](../arquitectura/README.md)
- [ ] Watch [System Design Video](link) (30 min)

**Development Workflow** (1 hour):
- [ ] Read [Git Workflow](../procesos/cicd-pipeline.md)
- [ ] Read [Code Review Guide](link)

**DevOps Basics** (2 hours):
- [ ] Read [Kubernetes Basics](link)
- [ ] Read [Monitoring Guide](../procesos/monitoring-alerting.md)

**Security** (1 hour):
- [ ] Complete Security Training (mandatory)
- [ ] Read [Security Best Practices](link)

---

### Live Training Sessions (Weeks 2-4)

**Week 2: Architecture Deep Dive** (2 hours, led by Tech Lead)
- System design decisions
- Database schema walkthrough
- API design patterns

**Week 3: DevOps Workshop** (2 hours, led by DevOps Lead)
- How CI/CD works
- How to deploy safely
- How to debug production issues

**Week 4: On-Call Training** (2 hours, led by SRE)
- How to respond to incidents
- Runbook walkthrough
- Practice in test environment

---

### Certifications (Optional, Month 2+)

**Encouraged**:
- Kubernetes (CKAD)
- Azure (AZ-104, AZ-204)
- AWS (AWS Solutions Architect)

**Company pays** for exam + study materials

---

## 🎯 Buddy Check-In Template

**Weekly Buddy 1:1** (30 min):

```markdown
## Buddy Check-In - Week 3

**Date**: 2025-01-20
**Buddy**: @bob-senior-dev
**New Hire**: @alice-new-engineer

### How are you feeling? (1-5)
- **Productivity**: 4/5 (submitted 2 PRs this week!)
- **Clarity**: 3/5 (still confused about deployment process)
- **Team fit**: 5/5 (everyone is friendly)

### Wins this week
- Implemented user profile feature
- Fixed bug in API response
- Attended first architecture review

### Challenges
- Deployment process confusing (too many steps)
- Unsure when to ask for help (don't want to bother people)

### Questions
- Q: Why do we use Kubernetes instead of serverless?
- A: We need fine-grained control over resources, auto-scaling policies

### Action Items
- [ ] Bob: Schedule deployment walkthrough (1 hour)
- [ ] Bob: Share "When to ask for help" guide
- [ ] Alice: Shadow next deployment (Friday)

### Next Check-In
- **Date**: 2025-01-27
- **Focus**: Deployment process, on-call readiness
```

---

## 📊 Onboarding Metrics

### Metric #1: Time to First PR

**Target**: <3 days

**Current**: Track for each new hire

**Example**:
- Alice: Day 1 (typo fix) ✅
- Bob: Day 5 (delayed by laptop issue) ⚠️

---

### Metric #2: Time to Productivity

**Definition**: Time until engineer is fully productive (5+ PRs/week, on-call ready)

**Target**: <30 days

**Track**: Manager assessment

---

### Metric #3: Onboarding Satisfaction

**Survey** (after 30 days):

```markdown
## Onboarding Survey (1-5 scale)

1. How clear were expectations on Day 1?
2. How helpful was your buddy?
3. How well did the checklist guide you?
4. How prepared do you feel for your role?
5. How welcomed did you feel by the team?
6. What could we improve?
```

**Target**: Average >4/5

---

### Metric #4: Retention (6-month)

**Target**: >90% retention after 6 months

**Track**: Did engineer stay past probation period?

**Why it matters**: Bad onboarding → High turnover

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | Manager | Buddy | New Hire | HR  | IT  |
| --------------------------------- | ------- | ----- | -------- | --- | --- |
| Assign buddy                      | A/R     | I     | I        | I   | I   |
| Provision accounts (script)       | A       | I     | I        | I   | R   |
| Day 1 welcome meeting             | A/R     | C     | C        | I   | I   |
| Code walkthrough                  | I       | A/R   | C        | I   | I   |
| First PR review                   | I       | A/R   | R        | I   | I   |
| On-call training                  | A       | C     | R        | I   | I   |
| Month 1 performance review        | A/R     | C     | C        | I   | I   |
| Update onboarding checklist       | A       | C     | C        | I   | I   |

---

## 🚀 Implementation Roadmap

### Sprint 0: Preparation
- [ ] Write onboarding checklist (this doc)
- [ ] Create access provisioning script
- [ ] Prepare "good first issues" backlog

### Sprint 1: Pilot Onboarding
- [ ] Test onboarding process with next hire
- [ ] Gather feedback (from new hire + buddy)
- [ ] Iterate on checklist

### Sprint 2: Scale
- [ ] Train all managers on onboarding process
- [ ] Automate access provisioning (script)
- [ ] Create onboarding dashboard (track metrics)

### Sprint 3: Continuous Improvement
- [ ] Monthly onboarding retro (what worked, what didn't)
- [ ] Update checklist based on feedback
- [ ] Share best practices across teams

---

## ✅ Success Criteria

### Mes 1
- ✅ Onboarding checklist documented
- ✅ Access provisioning automated (<1 hour)
- ✅ First hire onboarded successfully (survey >4/5)

### Mes 2-3
- ✅ 3+ hires onboarded
- ✅ Time to first PR <3 days (average)
- ✅ Buddy system working (weekly check-ins)

### Mes 4+
- ✅ Time to productivity <30 days (average)
- ✅ Onboarding satisfaction >4/5 (average)
- ✅ 6-month retention >90%

---

## 🔗 Links Relacionados

- [CI/CD Pipeline](./cicd-pipeline.md) - Deployment workflow
- [Incident Management](./incident-management.md) - On-call procedures
- [Monitoring & Alerting](./monitoring-alerting.md) - How to check production

---

## 📚 Antipatterns

### ❌ Antipattern #1: "Figure It Out Yourself"

**Problem**: No checklist, no buddy, new hire struggles for weeks

**Example**:
- New hire: "Where do I find the docs?"
- Team: "Uh, check the wiki? Maybe someone wrote something?"
- Result: 3 weeks to make first PR

**Solution**: ✅ Structured onboarding checklist + buddy

---

### ❌ Antipattern #2: "Drinking from the Fire Hose"

**Problem**: Too much information on Day 1 (8-hour lecture)

**Example**:
- Day 1: 8 hours of presentations on architecture, security, DevOps, culture
- New hire: Overwhelmed, remembers nothing

**Solution**: ✅ Spread learning over 30 days (Day 1, Week 1, Month 1)

---

### ❌ Antipattern #3: "Ghost Buddy"

**Problem**: Buddy assigned but too busy to help

**Example**:
- Buddy: "I'm on PTO next week, then crunching on a deadline, ping me in a month?"
- New hire: Struggles alone

**Solution**: ✅ Buddy availability check (not on PTO, not crunching)

---

### ❌ Antipattern #4: "No First Day Win"

**Problem**: Day 1 spent on paperwork, no code

**Example**:
- Day 1: 8 hours of HR forms, laptop setup, account creation
- No code touched
- New hire: "Am I even an engineer?"

**Solution**: ✅ First commit on Day 1 (even a typo fix)

---

### ❌ Antipattern #5: "Sink or Swim" On-Call

**Problem**: On-call on Day 30 with no training

**Example**:
- Day 30: "You're on-call this week, good luck!"
- SEV-1 incident → New hire panics
- Result: Burnout, quit

**Solution**: ✅ Shadow on-call 3+ times before first shift

---

**Versión**: 1.0  
**Última Actualización**: 2025-01-15  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (cada nuevo hire = feedback)
