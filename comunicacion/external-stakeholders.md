# External Stakeholders Communication - Comunicación con Stakeholders Externos

## 📋 Resumen Ejecutivo

**Problema**: Engineering y Sales hablan idiomas diferentes → "Está en staging" no significa nada para Sales. Marketing pregunta "cuándo sale X feature" → Developer responde con tecnicismos. CS necesita explicar issue a customer → No saben cómo explicar problema técnico.

**Solución**: **Stakeholder communication protocols** con canales dedicados, translation framework (tech → business), y templates para updates.

**Beneficio**:
- Stakeholders informados (saben estado de features sin preguntar)
- Menos frustr ación (Engineering no es bombardeado con preguntas)
- Mejor alineación (todos entienden prioridades y timelines)
- Customer satisfaction (CS puede comunicar issues claramente)

---

## 🎯 Stakeholder Segments

### 1. Sales Team

**Qué necesitan de Engineering**:
- **Feature status**: "Cuándo estará lista X feature?" (para cerrar deals)
- **Demo support**: "Necesito demo para cliente" (environment stability)
- **Custom requests**: "Cliente quiere integración con X" (feasibility)
- **Bug reports**: "Cliente reportó Y no funciona" (urgency)

**Communication Channels**:
- **#sales-engineering** (Slack private) - Technical questions, demo requests
- **#product-updates** (Slack read-only) - Weekly release notes
- **Bi-weekly sync** (30 min meeting) - Roadmap alignment

---

### 2. Marketing Team

**Qué necesitan de Engineering**:
- **Launch dates**: "Cuándo podemos anunciar X feature?" (for campaigns)
- **Feature descriptions**: "Cómo funciona Y?" (for blog posts/landing pages)
- **Screenshots/demos**: "Necesito video de feature" (for marketing assets)
- **Technical accuracy**: "Review our blog post" (avoid mistakes)

**Communication Channels**:
- **#marketing** (Slack) - Questions, content review requests
- **#product-updates** (Slack read-only) - Weekly release notes
- **Monthly sync** (1 hour meeting) - Upcoming launches

---

### 3. Customer Success (CS)

**Qué necesitan de Engineering**:
- **Incident updates**: "Why is app slow?" (to communicate to customers)
- **Bug status**: "Customer reported issue #1234, qué está pasando?" (ETA)
- **Feature explanations**: "Cómo usar X?" (to train customers)
- **Escalations**: "Customer is angry, need help" (urgent support)

**Communication Channels**:
- **#customer-feedback** (Slack) - Bug reports, feature requests from customers
- **#incidents** (Slack read-only) - Incident alerts (auto-posted)
- **#product-updates** (Slack read-only) - Weekly release notes
- **On-demand escalation** - For urgent customer issues (ping @engineering-manager)

---

### 4. Executive Team (CEO, CTO, VP Eng, CPO)

**Qué necesitan de Engineering**:
- **High-level status**: "Are we on track for Q1 goals?" (not details)
- **Risks**: "What could derail us?" (blockers, dependencies)
- **Incidents**: "Why was app down?" (impact, resolution)
- **Metrics**: "How's velocity, quality, uptime?" (KPIs)

**Communication Channels**:
- **Email** - Weekly status updates (Fridays 5pm)
- **#exec-updates** (Slack private) - Critical incidents, major launches
- **Quarterly Business Review (QBR)** - Deep dive on metrics, roadmap

---

## 📱 Communication Channels (Stakeholder-Specific)

### #sales-engineering (Private)

**Purpose**: Sales asks technical questions, Engineering answers

**Members**:
- Sales team (10 people)
- Engineering Manager
- Tech Lead (rotation)
- Solution Architect

**Posting Guidelines**:

**For Sales** (how to ask questions):
```markdown
Need help for customer call:

**Customer**: Acme Corp
**Use case**: [What customer wants to do]
**Question**: [Technical question]
**Urgency**: [Call is tomorrow / Next week / No rush]

Example:
**Customer**: Acme Corp
**Use case**: They want to integrate our API with Salesforce
**Question**: Do we support Salesforce integration?
**Urgency**: Call is tomorrow 10am

@engineering-manager
```

**For Engineering** (how to respond):
```markdown
✅ Yes, we support Salesforce integration via REST API.

**Documentation**: https://docs.company.com/integrations/salesforce
**Limitations**: Only works with Salesforce Enterprise (not Professional)
**ETA for demo environment**: Can setup today

Happy to join call if helpful. Let me know!
```

**Response Time SLA**: <4 hours (during work hours)

---

### #product-updates (Read-Only)

**Purpose**: Weekly release notes (what shipped this week)

**Owner**: Product Manager
**Posting Frequency**: Every Friday 3pm

**Template**:
```markdown
📦 **Release Notes - Week of Dec 2-6, 2025**

## 🚀 New Features
- **User Analytics Dashboard** - Customers can now see usage stats
  - Benefit: Helps customers optimize usage
  - Availability: All plans
  - Docs: https://docs.company.com/analytics

## 🐛 Bug Fixes
- Fixed login button alignment on mobile
- Fixed slow API response for large datasets

## 🔧 Improvements
- Reduced API latency by 30% (P95: 200ms → 140ms)
- Improved error messages (more actionable)

## 📅 Coming Next Week
- **Dark Mode** (in beta testing)
- **Slack Integration** (development in progress)

## 🔗 Links
- Full changelog: https://changelog.company.com
- Demo video: https://youtube.com/watch?v=abc123

Questions? Ask in #product or #sales-engineering.
```

**Who should read**:
- Sales (know what to sell)
- Marketing (know what to announce)
- CS (know what to support)
- Executives (know what shipped)

---

### #customer-feedback (Bi-Directional)

**Purpose**: CS reports customer feedback/bugs, Engineering responds

**Members**:
- Customer Success team
- Engineering Manager
- Product Manager

**Posting Guidelines**:

**For CS** (bug report):
```markdown
🐛 **Customer Bug Report**

**Customer**: Acme Corp (Enterprise plan)
**Issue**: Can't export CSV (button doesn't work)
**Frequency**: Happened 3 times this week
**Workaround**: Manual export works
**Impact**: HIGH (blocking customer workflow)

**Steps to reproduce**:
1. Go to Analytics page
2. Click "Export CSV"
3. Nothing happens (no download)

**Browser**: Chrome 120 on Windows

Can we prioritize this? @product-manager
```

**For Engineering** (response):
```markdown
✅ Triaged - this is a known issue (#1234)

**Status**: Fix in progress
**ETA**: Deploy tomorrow (Fri Dec 8)
**Workaround**: Use manual export for now

I'll post here when fixed. Thanks for reporting!
```

**For CS** (feature request):
```markdown
💡 **Customer Feature Request**

**Customer**: Acme Corp (5 similar requests this month)
**Request**: Dark mode
**Business value**: "Easier on eyes, we work late nights"
**Willingness to pay**: They'd upgrade to Enterprise for this

@product-manager FYI
```

**For Product** (response):
```markdown
Thanks! Dark mode is on roadmap for Q1 2026.

We're hearing this a lot (15 requests this quarter).
I'll bump priority.

ETA: Beta in Feb 2026
```

---

### #exec-updates (Private - Critical Only)

**Purpose**: Critical incidents + major launches (Executive awareness)

**Members**: CEO, CTO, VP Eng, CPO, CFO

**Posting Guidelines**:

**Incident Alert** (SEV-1 only):
```markdown
🚨 **INCIDENT ALERT** (SEV-1)

**What**: API completely down
**Impact**: All customers affected (100% outage)
**Started**: 2:15pm PST
**ETA**: Investigating (update in 15 min)

War room: #incident-2025-12-07-api-down

@cto
```

**Incident Resolved**:
```markdown
✅ **INCIDENT RESOLVED**

**What**: API down
**Duration**: 45 minutes (2:15pm - 3:00pm PST)
**Root cause**: Database connection pool exhausted
**Customers affected**: ~500 (all)
**Revenue impact**: ~$2K lost (estimated)

**Next steps**:
- Post-mortem tomorrow 10am
- Customer email going out now (from CS)
- Prevention: Increase connection pool (deploy Fri)

Full post-mortem: [link]

@cto @ceo
```

**Major Launch**:
```markdown
🚀 **MAJOR LAUNCH** - User Analytics Dashboard

**What**: New analytics dashboard (top customer request)
**Availability**: Live in production (all customers)
**Business impact**: Expect 10% upgrade rate (Enterprise plan)

**Marketing**: Blog post going live tomorrow
**Sales**: Demo environment ready

Announcement email: [draft link]

@ceo @cpo
```

---

## 🗣️ Communication Templates

### Template: Weekly Engineering Update (to Executives)

**Sent by**: Engineering Manager  
**Frequency**: Every Friday 5pm  
**Recipients**: CEO, CTO, VP Eng, CPO

**Email Subject**: `Engineering Weekly Update - Week of Dec 2-6`

**Email Body**:
```markdown
Hi team,

Weekly engineering update below.

## 🎯 Goals This Week
- ✅ Ship User Analytics Dashboard (DONE - launched Fri)
- ✅ Fix 5 critical bugs (DONE - 5/5 fixed)
- 🚧 Dark Mode (IN PROGRESS - 60% complete, on track for next week)

## 🚀 Shipped This Week
- User Analytics Dashboard (500 lines of code, 3 weeks effort)
- Performance improvements (API latency -30%)

## 📊 Metrics
- **Velocity**: 40 story points (on track, avg is 38)
- **Quality**: 2 bugs escaped to prod (target <3, ✅ on track)
- **Uptime**: 99.95% (target 99.9%, ✅ exceeding)
- **Deploy frequency**: 8 deploys (daily avg, healthy)

## 🚨 Risks / Blockers
- None this week (smooth sailing ✅)

## 📅 Next Week
- Launch Dark Mode (beta)
- Start Slack Integration (2-week project)
- Hire 1 backend engineer (offer sent, awaiting acceptance)

Full release notes: #product-updates

Let me know if you have questions!

Cheers,
[Engineering Manager]
```

---

### Template: Feature Status (for Sales)

**Posted in**: #sales-engineering  
**Use case**: Sales asks "Is X ready?"

**Response**:
```markdown
**Feature**: [Feature name]
**Status**: [In Development / Beta / GA / Not Planned]
**ETA**: [Date or "TBD"]
**Availability**: [All plans / Enterprise only / Custom]

**What it does**: [1-2 sentences, non-technical]

**Demo**: [Link to demo video or "available upon request"]

**Docs**: [Link to documentation or "coming soon"]

**Limitations** (if any): [List any caveats]

Happy to jump on a call to demo if helpful!
```

**Example**:
```markdown
**Feature**: Slack Integration
**Status**: In Development
**ETA**: Feb 2026 (beta), Mar 2026 (GA)
**Availability**: Enterprise plan only

**What it does**: Send notifications from our app to your Slack channels (e.g., "New user signed up" → post to #sales)

**Demo**: Not yet available (will post when beta ready)

**Docs**: Coming in Jan 2026

**Limitations**: Only works with Slack (not Teams), max 10 channels per customer

Happy to discuss on a call! Let me know.
```

---

### Template: Incident Update (for CS to share with customers)

**Use case**: CS needs to tell customers "app is down"

**For CS to copy-paste into customer email**:

**Email Subject**: `[Company] Service Update - [Brief Description]`

**Email Body**:
```markdown
Hi [Customer],

We're currently experiencing [brief issue description].

**Impact**: [What's affected - be specific]
**Started**: [Time]
**ETA**: [Estimated resolution time or "investigating"]

**What we're doing**:
- [Action 1]
- [Action 2]

**What you should do**:
- [Recommendation - e.g., "Wait 30 min and try again" or "No action needed"]

We'll send an update in [X minutes/hours] or when resolved.

For real-time updates: https://status.company.com

Apologies for the inconvenience.

[CS Rep]
```

**Example**:
```markdown
Hi Acme Corp,

We're currently experiencing slow API response times.

**Impact**: API calls taking 2-3 seconds (normally <500ms)
**Started**: 2:15pm PST
**ETA**: Resolving within 30 minutes

**What we're doing**:
- Identified root cause (database connection pool full)
- Deploying fix now (5 minutes)

**What you should do**:
- No action needed (your app will automatically speed up once fixed)

We'll send an update in 15 minutes or when resolved.

For real-time updates: https://status.company.com

Apologies for the inconvenience.

Sarah (Customer Success)
```

---

### Template: Feature Request Response (Engineering to CS)

**Use case**: CS forwards customer feature request to Engineering

**Response** (in #customer-feedback):
```markdown
**Feature Request**: [Feature name]
**Status**: [We're building it / On roadmap / Not planned / Need more info]

**Timeline**: [ETA or "TBD"]

**Why** [we're building it / not building it / need more info]:
[1-2 sentences explaining reasoning]

**What customer can do now**: [Workaround or "no current solution"]

Feel free to share with customer!
```

**Example 1** (We're building it):
```markdown
**Feature Request**: Dark Mode
**Status**: We're building it! ✅

**Timeline**: Beta in Feb 2026, GA in Mar 2026

**Why**: We've heard this from 15 customers this quarter (high demand)

**What customer can do now**: No current workaround (only light mode available)

Feel free to share with customer! We'll notify you when beta is ready.
```

**Example 2** (Not planned):
```markdown
**Feature Request**: Integration with Oracle Database
**Status**: Not planned ❌

**Timeline**: N/A

**Why**: Oracle integration is complex (3+ months), and we've only had 1 request (low demand). We're focusing on higher-priority features (Dark Mode, Slack Integration).

**What customer can do now**: Use our REST API to build custom integration (docs: https://docs.company.com/api)

Feel free to share with customer. We'll reconsider if demand increases.
```

---

## 🎭 RACI: Stakeholder Communication

| Actividad | Engineering | Product | Sales | Marketing | CS |
|-----------|-------------|---------|-------|-----------|-----|
| **Weekly Release Notes** | C | A/R | I | I | I |
| **Sales Demo Support** | R | C | A | I | I |
| **Feature Status Updates** | C | A/R | I | I | I |
| **Incident Communication** | R | C | I | I | A |
| **Customer Bug Triage** | R | C | I | I | A |
| **Executive Updates** | A/R | C | I | I | I |
| **Marketing Content Review** | C | I | I | A/R | I |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## ⏱️ Response Time SLAs

| Stakeholder | Channel | Question Type | Response Time | Red Flag |
|-------------|---------|---------------|---------------|----------|
| **Sales** | #sales-engineering | Feature status | <4 hours | >1 day |
| **Sales** | #sales-engineering | Demo request | <1 day | >3 days |
| **Marketing** | #marketing | Content review | <2 days | >1 week |
| **CS** | #customer-feedback | Bug report | <2 hours | >4 hours |
| **CS** | #customer-feedback | Feature request | <1 day | >3 days |
| **Executives** | Email | Weekly update | Every Friday 5pm | Late (>6pm) |
| **Executives** | #exec-updates | SEV-1 incident | <5 min | >15 min |

---

## 📊 Stakeholder Communication Metrics

### Metrics to Track

| Metric | Target | Red Flag | How to Measure |
|--------|--------|----------|----------------|
| **Sales response time (avg)** | <4 hours | >1 day | Slack analytics |
| **CS bug triage time (avg)** | <2 hours | >4 hours | Jira time-to-first-response |
| **Release notes sent on time** | 100% (every Fri) | Missed 2+ weeks | Calendar |
| **Exec update sent on time** | 100% (every Fri 5pm) | Late >2 weeks | Email logs |
| **Stakeholder satisfaction** | >4/5 | <3/5 | Quarterly survey |

---

### Quarterly Stakeholder Survey

**Sent to**: Sales, Marketing, CS (every quarter)

**Questions**:
1. How satisfied are you with Engineering's responsiveness? (1-5)
2. Do you feel informed about feature status? (Yes/No)
3. What could Engineering improve? (Free text)
4. Example of great communication from Engineering? (Free text)

**Results**: Shared with Engineering team, used to improve processes

---

## 🛠️ Escalation (When Stakeholder Needs Urgent Help)

### Sales Escalation (Urgent Demo/Deal)

**Scenario**: Sales has customer call tomorrow, needs urgent demo

**Process**:
1. ✅ **Post in #sales-engineering**:
   ```markdown
   🚨 URGENT: Need demo for Acme Corp call (tomorrow 10am)
   
   **Customer**: Acme Corp (potential $500K deal)
   **Use case**: [What they want to see]
   **Question**: Can we show [X feature]?
   
   @engineering-manager
   ```

2. ✅ **Engineering Manager responds** (<1 hour):
   - Can we support? (Yes/No)
   - If yes: Assign engineer to join call
   - If no: Suggest alternative (recorded demo, docs)

3. ✅ **Engineer joins call** (if needed):
   - Screen share demo
   - Answer technical questions
   - Follow-up email with docs/next steps

---

### CS Escalation (Angry Customer)

**Scenario**: Customer is furious, CS needs help NOW

**Process**:
1. ✅ **CS pings Engineering Manager** (DM or phone):
   ```markdown
   🚨 URGENT: Angry customer (Acme Corp)
   
   **Issue**: [What's wrong]
   **Customer impact**: [How it affects them]
   **Timeline**: Need resolution today
   
   Can you help?
   ```

2. ✅ **Engineering Manager triages** (<15 min):
   - Assign engineer to investigate
   - Provide ETA to CS (for customer communication)

3. ✅ **Engineer investigates + fixes** (or provides workaround)

4. ✅ **CS updates customer**:
   ```markdown
   Hi [Customer],
   
   Our engineering team investigated and [resolution].
   
   You should be unblocked now. Please try again and let us know if issues persist.
   
   Apologies for the trouble!
   ```

---

## ✅ Success Criteria

### Mes 1
- ✅ Stakeholder channels created (#sales-engineering, #customer-feedback, #product-updates)
- ✅ Templates documented (feature status, incident updates, weekly exec update)
- ✅ First weekly release notes sent

### Mes 2-3
- ✅ Sales response time <6 hours (avg)
- ✅ CS bug triage time <4 hours (avg)
- ✅ Release notes sent on time (100%)
- ✅ Stakeholder satisfaction >3.5/5

### Mes 4+
- ✅ Sales response time <4 hours (avg)
- ✅ CS bug triage time <2 hours (avg)
- ✅ Stakeholder satisfaction >4/5
- ✅ Zero "Engineering doesn't communicate" complaints

---

## 🔗 Links Relacionados

- [Translation Framework](./translation-framework.md) - Cómo traducir tech → business language
- [Channel Ownership](./channel-ownership.md) - Quién modera #sales-engineering, #customer-feedback
- [Incident Communication](./incident-communication.md) - Cómo comunicar SEV-1 incidents a stakeholders
- [Escalation Matrix](./escalation-matrix.md) - Cómo escalar urgencies

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (stakeholder feedback)
