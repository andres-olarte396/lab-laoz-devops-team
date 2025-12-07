# Onboarding Communication Guide - Guía de Comunicación para Nuevos Integrantes

## 📋 Resumen Ejecutivo

**Problema**: Nuevo developer empieza → No sabe dónde preguntar → Espera 2 días para respuesta simple. Nuevo PM llega → Se pierde en 50+ canales de Slack → Información crítica missed.

**Solución**: **Onboarding communication guide** con canales esenciales, buddy system, templates para preguntas, y expectations claras de respuesta.

**Beneficio**:
- Time to first contribution: 1 semana (vs 3+ semanas)
- Menos frustración (saben dónde preguntar)
- Mejor integración (conectados con equipo desde día 1)
- Knowledge retention (documentación accesible)

---

## 🗓️ Communication Timeline (First 30 Days)

### Day 1: Essentials

**Morning (First 2 hours)**:
1. ✅ **IT Setup** (before 10am):
   - Slack account created (HR sends invite)
   - Email configured (company.com)
   - Calendar access (Google Workspace)
   - GitHub organization added

2. ✅ **Slack Essentials** (10am-11am):
   Join these channels (total: 8):
   - **#general** - Company-wide announcements
   - **#engineering** - All engineering updates
   - **#your-team** (e.g., #frontend-team)
   - **#watercooler** - Social/casual chat
   - **#help** - Ask anything
   - **#deployments** - Deployment notifications (read-only)
   - **#incidents** - Incident alerts (read-only)
   - **#on-call** - On-call schedule (read-only)

   **DO NOT join all 50+ channels on day 1** (overwhelming)

3. ✅ **Meet Your Buddy** (11am-12pm):
   - Manager assigns buddy (experienced team member)
   - 30 min intro call:
     - Buddy explains team structure
     - Shows key documentation
     - Answers initial questions
   - Buddy adds you to team-specific channels

**Afternoon (2pm-5pm)**:
4. ✅ **Documentation Scavenger Hunt** (2pm-3:30pm):
   Buddy sends checklist:
   ```markdown
   Welcome! Find these docs to understand our workflow:
   
   - [ ] Team README (who we are, what we do)
   - [ ] Dev setup guide (how to run project locally)
   - [ ] Git workflow (branching strategy, PR process)
   - [ ] Deployment guide (how code gets to production)
   - [ ] On-call runbook (what to do if paged)
   
   Post ✅ in #your-team when you've read them.
   ```

5. ✅ **First Commit** (3:30pm-5pm):
   - Fix a typo in README (trivial PR to learn process)
   - Buddy reviews (teaches PR feedback culture)
   - Merge → First contribution! 🎉

**Evening**:
6. ✅ **Reflection** (5pm):
   Buddy sends end-of-day check-in:
   ```markdown
   How was day 1? 
   
   - What went well?
   - What was confusing?
   - Questions for tomorrow?
   
   No rush to reply, whenever you're ready.
   ```

---

### Week 1: Integration

**Monday-Tuesday** (already done day 1)

**Wednesday** (Day 3):
1. ✅ **Join Sprint Ceremonies**:
   - Standup (9am daily)
   - Buddy explains standup format (what to say)
   - You say: "I'm [name], new this week, working on [task] with [buddy]"

2. ✅ **Shadow Buddy** (all day):
   - Buddy shares screen during coding
   - Explains decisions ("why we use this library", "why this pattern")
   - You ask questions in real-time

**Thursday** (Day 4):
1. ✅ **First Real Task**:
   - Manager assigns small bug fix (1-2 days)
   - Buddy is available for questions
   - Post updates in #your-team:
     ```markdown
     Working on #1234 (fix login button alignment)
     
     Progress: ✅ Reproduced bug, 🚧 Working on fix
     ETA: Tomorrow
     
     Questions: None yet (will ping @buddy if stuck)
     ```

**Friday** (Day 5):
1. ✅ **End of Week Retro** (with buddy):
   - 30 min call
   - Discuss:
     - What did you learn?
     - What's still confusing?
     - What do you need for week 2?

2. ✅ **Team Intro** (optional):
   Post in #your-team:
   ```markdown
   Hi team! 👋
   
   I'm [name], joined this week as [role].
   
   Background: [Brief - 2 sentences]
   Excited about: [What excites you about this team]
   
   This week I:
   - ✅ Fixed my first bug (#1234)
   - ✅ Learned our Git workflow
   - ✅ Met awesome buddy @buddy
   
   Looking forward to working with y'all!
   ```

---

### Week 2-3: Autonomy

**Week 2**:
1. ✅ **Independent Work** (Monday-Wednesday):
   - Take on task without buddy shadowing
   - Post updates proactively in #your-team (daily)
   - Ask questions in #help or #your-team (not DM)

2. ✅ **Join Planning** (Wednesday):
   - Attend sprint planning
   - Observe (don't estimate yet, just learn)
   - Buddy explains estimation process

3. ✅ **First On-Call Shadow** (optional, if applicable):
   - Shadow on-call engineer for 1 shift
   - Learn runbooks, incident response
   - Not responsible for fixes (just observe)

**Week 3**:
1. ✅ **Contribute to Planning**:
   - Estimate your own tasks (with buddy guidance)
   - Ask clarifying questions during planning

2. ✅ **Write First Doc**:
   - Found something undocumented? Write it down
   - Add to team wiki (even small things help)
   - Example: "How to run database migrations locally"

---

### Week 4: Full Integration

1. ✅ **Independent Contributor**:
   - Work autonomously (buddy available but not shadowing)
   - Participate in all ceremonies (standup, planning, retro)
   - Post updates in #your-team

2. ✅ **30-Day Check-In** (with manager):
   - 1 hour meeting
   - Discuss:
     - How's onboarding going?
     - What's working well?
     - What could be improved?
     - Goals for next 60 days

3. ✅ **Give Feedback on Onboarding**:
   - Fill out onboarding survey
   - Suggest improvements (for next new hire)

---

## 📱 Slack Channels (By Priority)

### Must-Join (Day 1)

| Channel | Purpose | When to Post | When to Mute |
|---------|---------|--------------|--------------|
| **#general** | Company announcements | Never (read-only) | Never (critical info) |
| **#engineering** | All engineering updates | Rarely (big news only) | Never |
| **#your-team** | Daily work, questions | Daily (updates/questions) | Never |
| **#help** | Ask any question | Anytime (no dumb questions) | Optional (can get noisy) |
| **#watercooler** | Social, casual chat | Optional (fun stuff) | Optional |

### Join Week 1

| Channel | Purpose | When to Join |
|---------|---------|--------------|
| **#deployments** | Deployment notifications | Day 3 (after first commit) |
| **#incidents** | Incident alerts | Day 3 (understand incident process) |
| **#product** | Product updates | Week 1 (context on roadmap) |
| **#design** | Design reviews | Week 1 (if working with designers) |

### Join Week 2-4 (Role-Specific)

**For Developers**:
- **#development** - Development best practices
- **#devops** - Infrastructure questions
- **#qa** - Testing discussions
- **#security** - Security awareness

**For Product Managers**:
- **#customer-feedback** - Customer requests
- **#sales-engineering** - Customer calls
- **#product-updates** - Release notes

**For Designers**:
- **#design-critique** - Design feedback
- **#design-resources** - Tools/resources

### Optional (Join as Needed)

| Channel | Purpose | When Relevant |
|---------|---------|---------------|
| **#tech-debt** | Tech debt prioritization | If working on refactors |
| **#architecture** | Architecture discussions | If designing new systems |
| **#performance** | Performance optimization | If working on perf issues |
| **#random** | Memes, fun | Whenever 😄 |

---

## 🤝 Buddy System

### Buddy Selection

**Who is a buddy?**:
- Experienced team member (6+ months on team)
- NOT manager (buddy is peer)
- Good communicator (patient, explains well)
- Volunteers (not forced)

**Manager assigns buddy on Day 0** (before new hire starts)

---

### Buddy Responsibilities

**Week 1** (High touch - ~5 hours total):
- ✅ **Day 1**: 2 hours (intro call, doc scavenger hunt, first commit)
- ✅ **Day 2-3**: 2 hours (shadow buddy, answer questions)
- ✅ **Day 4-5**: 1 hour (review first PR, end-of-week retro)

**Week 2-3** (Medium touch - ~2 hours total):
- ✅ **Check-in calls**: 30 min/week (how's it going?)
- ✅ **Ad-hoc questions**: Available on Slack (respond <2 hours)

**Week 4** (Low touch - ~30 min):
- ✅ **Final retro**: 30 min (how was onboarding? what to improve?)

**After Week 4**:
- Buddy "graduates" (new hire is autonomous)
- Buddy remains available but not actively checking in

---

### Buddy Communication Guide

**How to ask buddy questions**:

❌ **Bad** (DM):
```
hey can you help me?
```
(Vague, no context)

✅ **Good** (DM or #your-team):
```markdown
@buddy Quick question about testing:

Context: I'm writing tests for login API
Issue: Tests pass locally but fail in CI
What I tried: Checked env vars, same as CI

Can you help me debug? No rush (today/tomorrow ok)
```
(Context, what you tried, timeline)

---

**Buddy response guidelines**:
- ✅ **Respond within 2 hours** (even if "I'll look later")
- ✅ **Explain the "why"** (not just "do this")
- ✅ **Encourage questions** ("This is confusing, ask anytime!")
- ✅ **Pair if needed** (screen share for 15 min)

---

## ❓ How to Ask Questions

### Question Framework

**Use this template** (in #help or #your-team):
```markdown
**Need help with**: [Brief description]

**Context**: [What are you trying to do?]

**What I tried**:
1. [Attempt 1]
2. [Attempt 2]

**Error/Issue**: [Error message or unexpected behavior]

**Question**: [Specific question]

**Urgency**: [Blocking me / Can wait]
```

**Example**:
```markdown
**Need help with**: Database migration failing

**Context**: Running `npm run migrate` to apply new user table

**What I tried**:
1. Checked database connection (works)
2. Ran migration on fresh DB (works)
3. Checked production DB permissions (seem ok)

**Error**: 
```
Error: permission denied for table users
```

**Question**: Do I need special permissions to alter tables in prod DB?

**Urgency**: Blocking me (need to deploy today)
```

---

### Question Etiquette

✅ **Do**:
- Ask in public channels (#help, #your-team) **not DMs**
  - Why: Others can learn from answer
- Search Slack history first (maybe already answered)
- Tag specific person if needed (`@buddy can you help?`)
- Say "thanks" when answered
- Post solution if you figured it out ("Solved! Issue was X")

❌ **Don't**:
- Ask "can I ask a question?" (just ask!)
- DM random people (use #help instead)
- Ask same question in 5 channels (pick one)
- Expect instant response (people are busy, <4 hours is ok)

---

### Response Time Expectations

| Channel | Expected Response | Red Flag |
|---------|-------------------|----------|
| **#help** | <4 hours (during work hours) | >1 day |
| **#your-team** | <2 hours (teammates prioritize) | >4 hours |
| **@buddy (DM)** | <2 hours | >4 hours |
| **@manager (DM)** | <1 day | >2 days |
| **#incidents** | <5 min (urgent!) | >15 min |

**If no response**: 
- Tag again after time window (polite ping)
- Escalate if blocking (`@tech-lead need help, been stuck 4 hours`)

---

## 📝 Documentation Expectations

### Where to Find Docs

| Doc Type | Location | Example |
|----------|----------|---------|
| **Team README** | `/docs/teams/your-team/README.md` | Team mission, members, processes |
| **Dev setup** | `/README.md` (root) | How to run project locally |
| **Runbooks** | `/docs/runbooks/` | Incident response procedures |
| **ADRs** | `/docs/adr/` | Architecture decisions |
| **API docs** | `/docs/api/` | API reference |
| **Confluence** | [company.atlassian.net](https://company.atlassian.net) | Product specs, design docs |

---

### Your Responsibility: Document as You Learn

**If you find something undocumented → Document it!**

**Example**:
- You: "How do I run database migrations?"
- Buddy: "Oh, run `npm run migrate:dev`"
- You: "Cool, is this in docs?"
- Buddy: "Hmm, don't think so"
- **You**: Add to `/docs/dev-setup.md`:
  ```markdown
  ## Running Database Migrations
  
  ```bash
  npm run migrate:dev
  ```
  
  This applies all pending migrations to local database.
  ```

**Why document small things?**:
- Next new hire won't ask same question
- You'll forget in 2 weeks (future you will thank you)
- Shows initiative (manager loves this)

---

### Documentation Updates

**When you update docs**:
1. ✅ Create PR (even for small doc changes)
2. ✅ Tag buddy or tech lead for review
3. ✅ Post in #your-team:
   ```markdown
   📝 Updated dev setup docs (added migration instructions)
   
   PR: #1234
   
   This was missing, added it for next new hire.
   ```

4. ✅ Merge → Docs are now better!

---

## 🎤 Communication Style Expectations

### Async-First Culture

**Default to async** (Slack, email, docs) **not meetings**.

✅ **Good**:
- Post question in #help (others answer when available)
- Document decision in ADR (everyone can read later)
- Comment on PR (async review)

❌ **Bad**:
- "Can we jump on a call?" (for every question)
- Undocumented verbal decisions (lost knowledge)
- Waiting for someone to be online (timezone differences)

**When to go sync** (call/meeting):
- Complex discussion (easier to talk than type)
- Pair programming (screen share to debug)
- 1:1 with manager (relationship building)

---

### Written Communication Best Practices

1. ✅ **Be concise** (respect people's time):
   - ❌ Bad: "Hey, so I was wondering if maybe you could possibly help me with this thing I'm working on..."
   - ✅ Good: "Need help with X. Context: Y. Question: Z."

2. ✅ **Provide context** (don't assume knowledge):
   - ❌ Bad: "The thing is broken"
   - ✅ Good: "Login API returns 500. Error: [paste]. Tried: [X, Y]."

3. ✅ **Use formatting** (easier to scan):
   - Use **bold** for key points
   - Use `code blocks` for code/commands
   - Use bullet lists (not paragraphs)

4. ✅ **Emoji for tone** (avoid misunderstandings):
   - "Can you review my PR? 🙏" (polite request)
   - "Thanks for the help! 🎉" (gratitude)
   - "Oops, my bad 😅" (acknowledge mistake)

---

### Meeting Etiquette (For Ceremonies)

**Standup** (9am daily, 15 min):
- ✅ Be on time (9am sharp)
- ✅ Turn on camera (builds rapport)
- ✅ Be brief (Yesterday/Today/Blockers in <2 min)
- ❌ Don't deep-dive (move to #your-team after standup)

**Planning** (Wednesday, 1 hour):
- ✅ Come prepared (read user stories beforehand)
- ✅ Ask questions (clarify ambiguity)
- ✅ Estimate honestly (don't sandbag or underestimate)

**Retro** (Friday, 45 min):
- ✅ Be honest (what went well, what didn't)
- ✅ Be constructive (solutions, not just complaints)
- ✅ Be respectful (no blaming individuals)

---

## 📊 Onboarding Communication Metrics

### Week 1 Success Criteria

- ✅ Joined 8 essential Slack channels
- ✅ Had 3+ interactions with buddy
- ✅ Asked 1+ question in #help or #your-team (overcame hesitation!)
- ✅ Made first commit (even if trivial)
- ✅ Read 5 core docs

### Week 2-3 Success Criteria

- ✅ Posted daily updates in #your-team
- ✅ Asked 5+ questions (learning actively)
- ✅ Answered 1+ question from teammate (contributing back!)
- ✅ Participated in all ceremonies (standup, planning)

### Week 4 Success Criteria

- ✅ Working autonomously (buddy not shadowing)
- ✅ Updated 1+ doc (contributing to knowledge base)
- ✅ Buddy confirms "ready to graduate"
- ✅ Manager confirms "onboarding complete"

---

## 🚨 Red Flags (Escalate to Manager)

**If you experience these**, tell your manager immediately:

❌ **Buddy unresponsive** (>4 hours to reply):
- Tell manager: "My buddy hasn't responded in 6 hours, I'm stuck"
- Manager will assign backup buddy

❌ **No one answers questions** (posted in #help, no reply in 1 day):
- Tell manager: "I asked in #help, no one responded"
- Manager will ping team or answer directly

❌ **Feeling overwhelmed** (too much too fast):
- Tell manager: "I'm drowning in info, need to slow down"
- Manager will adjust pace

❌ **Docs are missing/outdated** (can't complete scavenger hunt):
- Tell manager: "Dev setup docs are broken"
- Manager will fix or assign someone

❌ **Not included in ceremonies** (forgot to invite you):
- Tell manager: "Wasn't invited to standup"
- Manager will add you

---

## ✅ Success Stories (Examples)

### Example 1: Sarah (Frontend Developer)

**Week 1**:
- Joined 8 channels
- Fixed typo in README (first commit)
- Shadow buddy for 2 days
- Asked 10 questions in #help (overcame hesitation!)

**Week 2**:
- Fixed first bug (#1234 - login button alignment)
- Participated in planning (observed, didn't estimate)
- Posted daily updates in #frontend-team

**Week 3**:
- Took on medium-sized task (build new dashboard component)
- Estimated task in planning (8 points, buddy confirmed)
- Wrote doc: "How to test components locally"

**Week 4**:
- Working autonomously (shipped 3 features)
- Buddy graduated her ("You're ready!")
- Manager 30-day check-in: "Exceeded expectations"

**Outcome**: Sarah now mentors new hires 🎉

---

### Example 2: Mike (Backend Engineer)

**Week 1**:
- Joined Slack
- BUT: Too shy to ask questions (struggled alone for 3 days)
- Buddy noticed: "Mike, you seem stuck, what's up?"
- Mike: "I didn't want to bother anyone"
- Buddy: "No such thing as a dumb question, ask in #help!"

**Week 2**:
- Started asking questions (3-5/day in #backend-team)
- Team was supportive ("Great question!")
- Confidence increased

**Week 3-4**:
- Active participant (asking + answering questions)
- Buddy: "You're ready!"

**Lesson**: **Ask questions early** (don't suffer in silence)

---

## 🔗 Links Relacionados

- [Channel Ownership](./channel-ownership.md) - Quién modera cada canal
- [Escalation Matrix](./escalation-matrix.md) - Cómo escalar blockers
- [Documentation Ownership](./documentation-ownership.md) - Cómo mantener docs actualizados
- [Onboarding Process](../procesos/onboarding.md) - Full onboarding (no solo comunicación)

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (con feedback de nuevos hires)
