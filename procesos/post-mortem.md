# Post-Mortem - Análisis Post-Incidente (Blameless)

## 📋 Resumen Ejecutivo

**Problema**: Incident ocurre → Culpamos a alguien → No aprendemos → Mismo incident se repite.

**Solución**: **Blameless post-mortem process** con 5 Whys root cause analysis, action items tracking, learning sharing.

**Beneficio**:
- Aprendemos de errores (root cause, no síntomas)
- Cultura de transparencia (no blame → report honestly)
- Prevención (action items → no más este incident)
- Knowledge sharing (todo el equipo aprende)

---

## 🎯 Blameless Culture

### Prime Directive

> **"Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand."**
> 
> — Norm Kerth, "Project Retrospectives"

**Translation**: No culpar personas, buscar system failures.

---

### Why Blameless?

**Blame Culture** (❌ Bad):
- Alice deploys bug → Production down
- Manager: "Alice, you're fired!"
- Result: Team hides mistakes, no one reports issues, incidents go unreported

**Blameless Culture** (✅ Good):
- Alice deploys bug → Production down
- Manager: "Alice, thank you for reporting. Let's figure out why our testing didn't catch this."
- Result: Team reports issues early, we fix root cause (tests), no more bugs

---

**Key Principle**: Blame people → They hide mistakes. Blame systems → We fix processes.

---

## 📝 Post-Mortem Template

### 1. Incident Summary

**Date**: 2025-01-15  
**Duration**: 14:30 - 16:45 UTC (2 hours 15 min)  
**Severity**: SEV-1 (Critical)  
**Impact**: 100% of users unable to login  
**Estimated Revenue Loss**: $50,000  

---

### 2. Timeline (Chronological)

**All times UTC**

| Time  | Event                                                                 | Who          |
| ----- | --------------------------------------------------------------------- | ------------ |
| 14:20 | Deploy v2.5.0 to production (canary 10%)                              | @alice       |
| 14:25 | Canary promotion to 25% (automated)                                   | Flagger      |
| 14:30 | **🔴 INCIDENT START**: Error rate spikes to 100% (login endpoint)     | Datadog      |
| 14:31 | PagerDuty alert sent to @bob (on-call SRE)                            | PagerDuty    |
| 14:35 | @bob investigates, sees 500 errors on /login                          | @bob         |
| 14:40 | @bob declares SEV-1, creates #incident-20250115 Slack channel         | @bob         |
| 14:45 | @alice joins war room, identifies bug in auth service                 | @alice       |
| 14:50 | Decision: Rollback to v2.4.0                                          | @bob         |
| 14:55 | Rollback initiated (kubectl rollout undo)                             | @alice       |
| 15:00 | Rollback complete, error rate drops to 0%                             | Datadog      |
| 15:05 | Monitoring for stability                                              | Team         |
| 15:30 | Customer Support notified (send status page update)                   | @charlie     |
| 16:45 | **✅ INCIDENT RESOLVED**: Confirmed stable, post-mortem scheduled     | @bob         |

---

### 3. Root Cause Analysis (5 Whys)

**Problem Statement**: 100% of users unable to login for 2 hours 15 min

**5 Whys**:

1. **Why did users get 500 errors?**
   - Auth service crashed (NullPointerException in login handler)

2. **Why did auth service crash?**
   - New code assumed `user.profile` always exists (but can be null for new users)

3. **Why didn't our tests catch this?**
   - Integration tests only covered existing users (with profiles), not new users

4. **Why didn't canary catch this?**
   - Canary traffic was only 10% → Only 10% of users affected initially
   - Auto-promotion happened too fast (5 min) → Didn't give us time to notice

5. **Why didn't code review catch this?**
   - Reviewer didn't think to ask "What if user.profile is null?"
   - No checklist for null safety

**Root Cause**: Missing null check + incomplete test coverage + fast canary promotion

---

### 4. What Went Well

**Positives** (celebrate these!):

- ✅ **Fast detection**: Alert triggered within 1 min (MTTD = 1 min)
- ✅ **Fast response**: On-call responded in 5 min (MTTA = 5 min)
- ✅ **Clear communication**: War room created immediately, stakeholders notified
- ✅ **Effective rollback**: Rollback completed in 5 min (no fumbling)
- ✅ **Monitoring worked**: Datadog caught error rate spike immediately

---

### 5. What Went Wrong

**Negatives** (fix these):

- ❌ **Incomplete tests**: Integration tests only covered happy path, not edge cases
- ❌ **Fast canary**: Auto-promotion at 5 min too fast (should be 15-30 min)
- ❌ **No null checks**: Code didn't handle null `user.profile`
- ❌ **Code review missed**: Reviewer didn't catch missing null check
- ❌ **Long MTTR**: 2h 15min to resolve (target: <1h for SEV-1)

---

### 6. Action Items

**Prevent Recurrence**:

| #   | Action Item                                      | Owner    | Priority | Due Date   | Status      |
| --- | ------------------------------------------------ | -------- | -------- | ---------- | ----------- |
| 1   | Add null check to auth service login handler     | @alice   | P0       | 2025-01-16 | ✅ DONE     |
| 2   | Add test for new users (without profile)         | @alice   | P0       | 2025-01-16 | ✅ DONE     |
| 3   | Slow canary promotion (5 min → 15 min)           | @bob     | P1       | 2025-01-20 | 🔄 IN PROGRESS |
| 4   | Create code review checklist (null safety)       | @david   | P1       | 2025-01-25 | ⏳ TODO     |
| 5   | Add linter rule (warn on unchecked nulls)        | @alice   | P2       | 2025-02-01 | ⏳ TODO     |

**Priorities**:
- **P0** (Critical): Fix immediately (today)
- **P1** (High): Fix this sprint
- **P2** (Medium): Fix next sprint

---

### 7. Lessons Learned

**Key Takeaway**: Always test edge cases (null values, empty arrays, etc.)

**Broader Lessons**:
- Canary rollout is not a substitute for thorough testing
- Code review checklists help catch common mistakes
- Fast rollback is critical (we recovered in 5 min)

---

### 8. Supporting Data

**Graphs** (attach screenshots):
- Error rate spike (0% → 100% at 14:30, back to 0% at 15:00)
- Latency spike (P95 200ms → 5000ms)
- Traffic drop (500 RPS → 0 RPS during outage)

**Logs** (attach snippets):
```
[ERROR] 2025-01-15 14:30:15 - NullPointerException in AuthService.login()
  at com.company.auth.AuthService.login(AuthService.java:42)
  Caused by: user.profile is null
```

---

## 🔍 5 Whys Analysis (Technique)

### What is 5 Whys?

**Technique**: Ask "Why?" 5 times to get to root cause

**Example**:

**Problem**: Car won't start

1. Why? → Battery is dead
2. Why? → Alternator not charging
3. Why? → Alternator belt broken
4. Why? → Belt was old and worn
5. Why? → We didn't replace belt during maintenance

**Root Cause**: Skipped maintenance → **Action Item**: Add belt replacement to maintenance checklist

---

### 5 Whys Tips

**Do**:
- ✅ Ask "Why" multiple times (don't stop at first answer)
- ✅ Focus on process/system (not people)
- ✅ Use evidence (logs, metrics)

**Don't**:
- ❌ Stop at symptoms ("Why? → Bug in code" is too shallow)
- ❌ Blame people ("Why? → Alice wrote bad code" → Not helpful)
- ❌ Make up answers (use data)

---

## 📊 Action Items Tracking

### Action Item Ownership

**Every action item MUST have**:
- **Owner**: Who is responsible?
- **Priority**: P0/P1/P2
- **Due Date**: When is it due?
- **Status**: Todo / In Progress / Done

---

### Action Item Review

**Weekly Review** (every Monday):
- Review all open action items
- Update status (any blockers?)
- Escalate overdue items (past due date → Manager notified)

**Target**: >70% completion rate within 30 days

---

### Action Item Tracking (Jira Integration)

**Create Jira Tickets** (for accountability):

```markdown
## Jira Ticket: PM-123

**Title**: Add null check to auth service login handler

**Description**:
Post-mortem action item from incident #20250115.

Root cause: Missing null check in `AuthService.login()` caused 2h15min outage.

**Acceptance Criteria**:
- [ ] Add null check for `user.profile`
- [ ] Add test for new users (without profile)
- [ ] Deploy to production
- [ ] Verify in production (no errors)

**Priority**: P0 (Critical)
**Due Date**: 2025-01-16
**Owner**: @alice
```

---

## 🎓 Learning Sharing

### Post-Mortem Meeting

**Attendees**: Entire engineering team (not just incident responders)

**Agenda** (1 hour):

1. **Incident Summary** (10 min)
   - What happened? (timeline)
   - Impact? (users affected, revenue lost)

2. **Root Cause** (15 min)
   - 5 Whys analysis
   - Why didn't our defenses catch this?

3. **What Went Well** (10 min)
   - Celebrate wins (fast detection, rollback)

4. **What Went Wrong** (10 min)
   - Honest discussion (no blame)

5. **Action Items** (10 min)
   - Review action items
   - Assign owners

6. **Q&A** (5 min)

**Goal**: Everyone learns (even if not involved in incident)

---

### Post-Mortem Document (Public)

**Share post-mortem doc** with:
- ✅ Engineering team (internal wiki)
- ✅ Customer Support (so they know what happened)
- ✅ Customers (if major outage, external blog post)

**Example** (External Blog Post):

```markdown
# Incident Report: Login Outage on January 15, 2025

On January 15, 2025, from 14:30 to 16:45 UTC (2 hours 15 min), our users were unable to log in due to a bug in our authentication service. We sincerely apologize for the disruption.

## What Happened
During a deployment, a code change introduced a bug that caused our login service to crash for new users. We detected the issue within 1 minute and rolled back the deployment within 30 minutes, fully resolving the issue at 16:45 UTC.

## Root Cause
The bug was caused by a missing null check in our code. Our testing did not cover this edge case, allowing the bug to reach production.

## What We're Doing to Prevent This
- Added comprehensive tests for edge cases
- Slowed our canary rollout (more time to catch issues)
- Added code review checklists (null safety)
- Deployed a linter to catch unchecked nulls

## Conclusion
We take reliability seriously and are committed to learning from this incident. Thank you for your patience and understanding.

— The Engineering Team
```

---

### Monthly Incident Review

**Frequency**: Last Friday of every month

**Attendees**: Engineering team

**Agenda** (1 hour):

1. **Review all incidents** (last month)
   - How many SEV-1, SEV-2, SEV-3?
   - Common patterns? (e.g., 3 incidents caused by missing tests)

2. **Metrics**:
   - MTTR: Average time to resolve
   - MTTD: Average time to detect
   - Incident frequency: Increasing or decreasing?

3. **Systemic Issues**:
   - Are we seeing the same root causes? (e.g., missing tests)
   - What process changes needed?

4. **Celebrate Wins**:
   - Zero SEV-1 incidents this month? 🎉
   - Improved MTTR from 2h to 1h? 🎉

---

## 📊 Post-Mortem Metrics

### Metric #1: Post-Mortem Completion Rate

**Target**: 100% (every SEV-1 and SEV-2 gets post-mortem)

**Alert**: If post-mortem not completed within 48 hours → Escalate to Manager

---

### Metric #2: Action Item Completion Rate

**Target**: >70% completed within 30 days

**Track**: Jira tickets (overdue → Red)

---

### Metric #3: Incident Recurrence

**Target**: 0 repeat incidents (same root cause)

**Example**:
- Incident #1: Null pointer exception in auth service
- Incident #2 (3 months later): Null pointer exception in payment service
- **Problem**: We didn't fix the systemic issue (missing null checks)
- **Solution**: Add linter (enforce null checks everywhere)

---

### Metric #4: Time to Post-Mortem

**Target**: Post-mortem meeting within 48 hours of incident resolution

**Why**: While incident is fresh in memory

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | Incident Commander | Participants | Manager | Team |
| --------------------------------- | ------------------ | ------------ | ------- | ---- |
| Write post-mortem doc             | A/R                | C            | I       | I    |
| 5 Whys analysis                   | A                  | R            | C       | I    |
| Identify action items             | A                  | R            | C       | I    |
| Schedule post-mortem meeting      | A/R                | I            | I       | I    |
| Facilitate post-mortem meeting    | A/R                | C            | C       | C    |
| Track action item completion      | R                  | I            | A       | I    |
| Share post-mortem externally      | C                  | C            | A       | I    |

---

## 🚀 Implementation Roadmap

### Sprint 1: Post-Mortem Template
- [ ] Document post-mortem template (this doc)
- [ ] Create post-mortem doc template (Google Docs)
- [ ] Train team on 5 Whys analysis

### Sprint 2: First Post-Mortem
- [ ] Conduct first blameless post-mortem (next incident)
- [ ] Gather feedback (was it useful?)
- [ ] Iterate on template

### Sprint 3: Action Item Tracking
- [ ] Create Jira workflow (action items)
- [ ] Weekly action item review (calendar)
- [ ] Track completion rate

### Sprint 4: Learning Sharing
- [ ] Schedule monthly incident review (last Friday)
- [ ] Create internal wiki (post-mortem archive)
- [ ] Share externally (blog post template)

---

## ✅ Success Criteria

### Mes 1
- ✅ Post-mortem template documented
- ✅ Team trained on blameless culture + 5 Whys
- ✅ First post-mortem completed (48h after incident)

### Mes 2-3
- ✅ 100% post-mortem completion (every SEV-1/SEV-2)
- ✅ Action item completion >50% (within 30 days)
- ✅ Monthly incident review happening

### Mes 4+
- ✅ Action item completion >70%
- ✅ Zero repeat incidents (same root cause)
- ✅ External post-mortems published (major incidents)

---

## 🔗 Links Relacionados

- [Incident Management](./incident-management.md) - Incident response process
- [Security Response](./security-response.md) - Security incident post-mortems

---

## 📚 Antipatterns

### ❌ Antipattern #1: "Blame the Person"

**Problem**: Post-mortem blames individual, not system

**Example**:
- Post-mortem: "Alice deployed bad code. Alice should be more careful."
- Action item: "Alice will double-check code"
- Result: Alice feels bad, hides future mistakes, team doesn't learn

**Solution**: ✅ Blame system ("Why didn't tests catch this? Why didn't code review catch this?")

**Better Post-Mortem**:
- Root cause: "Tests didn't cover edge case"
- Action item: "Add test for edge case, create code review checklist"

---

### ❌ Antipattern #2: "No Action Items"

**Problem**: Post-mortem has no follow-up

**Example**:
- Post-mortem: "We had an outage. It was bad. Let's be more careful."
- Action items: None
- Result: Same incident happens again

**Solution**: ✅ Actionable items with owners and due dates

---

### ❌ Antipattern #3: "Action Items Never Completed"

**Problem**: Create action items, then forget them

**Example**:
- Action item: "Add monitoring for X" (due: Feb 1)
- Feb 1: No one did it
- Feb 15: Still not done
- March: Forgot about it

**Solution**: ✅ Weekly action item review, escalate overdue items

---

### ❌ Antipattern #4: "Secret Post-Mortems"

**Problem**: Only incident responders attend post-mortem

**Example**:
- Incident: Auth service down
- Post-mortem: Only @alice and @bob attend
- Team: "What happened?" (no one knows)

**Solution**: ✅ Invite entire engineering team (everyone learns)

---

### ❌ Antipattern #5: "Stop at Symptoms"

**Problem**: 5 Whys only 1 level deep

**Example**:
- Problem: Outage
- Why? → Bug in code
- Action item: "Fix bug"
- Result: Doesn't address root cause (why didn't tests catch it?)

**Solution**: ✅ Ask "Why" 5 times (get to systemic issues)

**Better 5 Whys**:
1. Why? → Bug in code
2. Why? → Missing null check
3. Why? → Tests didn't cover edge case
4. Why? → No test coverage requirements
5. Why? → No CI gate for coverage
**Action Item**: Add CI gate (require >80% coverage)

---

### ❌ Antipattern #6: "No External Communication"

**Problem**: Major outage, customers in the dark

**Example**:
- 2-hour outage (100% users affected)
- No status page update
- No email to customers
- Customers: "What happened? Can I trust this service?"

**Solution**: ✅ Transparent communication (status page, blog post, email)

---

**Versión**: 1.0  
**Última Actualización**: 2025-01-15  
**Owner**: Incident Commander / Engineering Manager  
**Review Cycle**: Después de cada incidente
