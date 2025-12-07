# Translation Framework - Framework de Traducción Tech ↔ Business

## 📋 Resumen Ejecutivo

**Problema**: Developer dice "High latency in P95" → Sales no entiende. Product Manager pregunta "Are we scalable?" → Engineer responde "Depends on traffic patterns and database sharding strategy" → PM confundido. Executive pregunta "What's our velocity?" → Engineer dice "40 story points" → Executive pregunta "¿Es bueno o malo?"

**Solución**: **Translation framework** para convertir tech jargon → business language (y viceversa), con diccionario de términos, templates, y ejemplos.

**Beneficio**:
- Stakeholders entienden status (sin confusión)
- Engineers entienden business context (por qué importa)
- Decisiones más rápidas (no bloqueado por miscommunication)
- Menos meetings (comunicación escrita es clara)

---

## 🗣️ Translation Principles

### Principle 1: Speak Their Language

❌ **Bad** (tech jargon para non-tech):
> "We're experiencing high P95 latency (>500ms) due to database connection pool exhaustion. We need to implement connection pooling with HikariCP and add read replicas."

✅ **Good** (business language):
> "The app is slower than usual (2-3 seconds to load instead of <1 second). This affects ~10% of users. We're fixing it today by upgrading our database. No user action needed."

**Rule**: Use **impact language** (what users experience) not **technical implementation** (how we fix it)

---

### Principle 2: Quantify Impact

❌ **Bad** (vague):
> "This bug is bad."

✅ **Good** (quantified):
> "This bug affects 500 users (5% of total). They can't checkout. Estimated revenue loss: $2K/day."

**Rule**: Always include **numbers** (users affected, revenue impact, time saved)

---

### Principle 3: Translate Metrics

❌ **Bad** (tech metrics):
> "Our P95 latency is 200ms, P99 is 400ms, and we have 99.95% uptime."

✅ **Good** (business metrics):
> "95% of users see page load in <1 second. The app was available 99.95% of the time (43 minutes downtime this month). Industry standard is 99.9%, so we're exceeding."

**Rule**: Provide **context** (is this good? how does it compare?)

---

## 📖 Tech → Business Dictionary

### Infrastructure & Performance

| Tech Term | Business Translation | Example |
|-----------|----------------------|---------|
| **P95 latency** | "95% of users see page load in X seconds" | "P95 latency is 200ms" → "95% of users see page load in <1 second" |
| **Uptime** | "App was available X% of time" | "99.95% uptime" → "App was down 22 minutes this month" |
| **Throughput** | "We can handle X requests per second" | "1000 req/sec throughput" → "We can handle 86 million requests/day (current usage is 10M/day)" |
| **Load balancer** | "Traffic director (spreads users across servers)" | "We added a load balancer" → "We now spread traffic across 3 servers for better performance" |
| **Database sharding** | "Split database into pieces for speed" | "We sharded the database" → "We split the database to handle 10x more users" |
| **Cache** | "Temporary storage for speed" | "We added Redis cache" → "We store frequently-used data for 10x faster loading" |
| **CDN** | "Fast file delivery network" | "Using Cloudflare CDN" → "Images load instantly (served from nearby servers)" |

---

### Code Quality & Testing

| Tech Term | Business Translation | Example |
|-----------|----------------------|---------|
| **Test coverage** | "% of code tested automatically" | "80% test coverage" → "We automatically test 80% of features (target is 80%+)" |
| **Tech debt** | "Code shortcuts that slow us down later" | "High tech debt" → "We took shortcuts to ship fast, now we need 2 weeks to clean up" |
| **Refactoring** | "Cleaning up code (no new features)" | "Refactoring the API" → "Cleaning up code to make future changes 50% faster" |
| **CI/CD** | "Automated testing + deployment" | "We have CI/CD" → "Every code change is auto-tested and deployed in 10 minutes" |
| **Code review** | "Peer review before merging code" | "All code goes through review" → "Every change is checked by 2 engineers for quality" |

---

### Architecture & Scalability

| Tech Term | Business Translation | Example |
|-----------|----------------------|---------|
| **Microservices** | "App split into independent pieces" | "Migrating to microservices" → "Splitting app so teams can work independently (faster shipping)" |
| **Monolith** | "Single large codebase" | "We have a monolith" → "All code is in one place (easier to start, harder to scale)" |
| **API** | "Way for systems to talk to each other" | "We built an API" → "Other apps can now integrate with us (e.g., Zapier)" |
| **Kubernetes** | "Tool to run apps at scale" | "We use Kubernetes" → "Our app auto-scales (handles 10x traffic spikes automatically)" |
| **Database migration** | "Moving data to new database" | "Migrating to PostgreSQL" → "Upgrading database for 3x faster queries" |

---

### Security & Compliance

| Tech Term | Business Translation | Example |
|-----------|----------------------|---------|
| **Encryption** | "Scrambling data so hackers can't read it" | "Data is encrypted at rest" → "Customer data is scrambled (unreadable even if stolen)" |
| **2FA** | "Two-step login (password + phone)" | "We added 2FA" → "Users need password + phone code to login (hackers can't login with just password)" |
| **SOC 2** | "Security audit (proves we're secure)" | "We're SOC 2 compliant" → "We passed independent security audit (customers can trust us)" |
| **Penetration testing** | "Hiring hackers to find vulnerabilities" | "We did a pentest" → "We hired ethical hackers to test security (found 3 issues, fixed them)" |
| **Zero-day vulnerability** | "Security bug attackers found before us" | "Zero-day in Log4j" → "Hackers found bug before vendor, we patched in 4 hours" |

---

### Metrics & KPIs

| Tech Term | Business Translation | Example |
|-----------|----------------------|---------|
| **Velocity** | "Team output (features shipped per sprint)" | "40 story points/sprint" → "We ship 5-7 features every 2 weeks (on track)" |
| **Story points** | "Complexity score (not hours)" | "This is 8 points" → "This is complex (1-2 weeks of work)" |
| **Sprint** | "2-week work cycle" | "Next sprint" → "Next 2 weeks" |
| **Deploy frequency** | "How often we ship code" | "8 deploys/week" → "We ship new code daily (fast iteration)" |
| **MTTR** | "Time to fix incidents" | "MTTR is 30 min" → "When something breaks, we fix it in 30 minutes (target <1 hour)" |
| **Change failure rate** | "% of deploys that break things" | "5% failure rate" → "1 in 20 deploys breaks something (target <5%)" |

---

## 📝 Translation Templates

### Template 1: Feature Status Update (for Sales/Marketing)

**Use case**: Sales asks "When will X feature be ready?"

**Tech version** (internal):
> Feature X is in development. We're at 60% completion. Backend API is done, frontend is in progress. ETA: 2 weeks (1 sprint), barring any blockers. Test coverage is 80%. Will deploy to staging next week for QA.

**Business version** (for Sales):
```markdown
**Feature**: X
**Status**: In development (60% complete)
**ETA**: Dec 20 (2 weeks)
**Confidence**: High (no blockers currently)

**What's done**:
- ✅ Backend (data handling)
- 🚧 Frontend (user interface) - in progress

**What's next**:
- Finish UI (1 week)
- Test with real users (1 week)
- Launch!

**Demo**: Available Dec 15 (you can show to customers after this date)

Questions? Let me know!
```

---

### Template 2: Incident Explanation (for CS → Customers)

**Use case**: App went down, CS needs to explain to customers

**Tech version** (internal post-mortem):
> Incident: Database connection pool exhausted (max 100 connections). Root cause: N+1 query in /users endpoint caused connection leak. Fix: Added connection pooling with HikariCP, increased max connections to 200, fixed N+1 query. Prevention: Added monitoring for connection pool usage.

**Business version** (for customers):
```markdown
**What happened**: Our app was slow/unavailable for 45 minutes (2:15pm - 3:00pm PST)

**Impact**: You may have experienced slow loading or errors during this time

**Root cause**: Our database got overloaded (too many requests)

**How we fixed it**: 
- Upgraded database capacity (2x more powerful)
- Optimized code to use database more efficiently

**Prevention**: 
- We now monitor database closely (alerts before it gets overloaded)
- We're upgrading servers next week for extra capacity

**Apologies**: We know this was frustrating. We've improved our systems to prevent this in the future.

Questions? Email support@company.com
```

---

### Template 3: Roadmap Explanation (for Executives)

**Use case**: Executive asks "What's the plan for Q1?"

**Tech version** (internal):
> Q1 goals: (1) Migrate to microservices (reduce deploy time from 30 min to 5 min), (2) Implement dark mode (top customer request, 15 requests), (3) Slack integration (API-based, 2 weeks effort), (4) Reduce P95 latency to <200ms (currently 300ms), (5) Increase test coverage to 90% (currently 80%).

**Business version** (for executives):
```markdown
**Q1 2026 Engineering Goals**

## 1. Speed Up Deployments (Internal Efficiency)
**What**: Upgrade our deployment process
**Why**: Ship features 6x faster (30 min → 5 min per deploy)
**Impact**: More features shipped, faster iteration

## 2. Dark Mode (Customer Request)
**What**: Add dark theme to app
**Why**: Top request (15 customers asked this quarter)
**Impact**: Better UX, potential 10% upgrade rate to Enterprise

## 3. Slack Integration (New Feature)
**What**: Send app notifications to Slack
**Why**: Customers want notifications in Slack (not just email)
**Impact**: Unlock $500K deal (Acme Corp waiting for this)

## 4. Performance Improvements (Speed)
**What**: Make app 30% faster
**Why**: Users complain about slow loading
**Impact**: Better UX, lower churn

## 5. Quality Improvements (Fewer Bugs)
**What**: Increase automated testing
**Why**: Catch bugs before customers find them
**Impact**: Fewer customer complaints, higher satisfaction

**Success Metrics**:
- Ship 20 features (current pace: 15/quarter)
- <3 bugs/month (current: 5/month)
- Customer satisfaction >4.5/5 (current: 4.2/5)
```

---

### Template 4: Technical Decision Explanation (for Product)

**Use case**: Product asks "Why did we choose PostgreSQL over MySQL?"

**Tech version** (internal ADR):
> Decision: Migrate from MySQL 5.7 to PostgreSQL 14. Rationale: PostgreSQL has better JSON support (`jsonb` type with indexing), advanced SQL features (CTEs, window functions), and better replication (logical replication, <1s lag vs 5s in MySQL). Tradeoffs: 2 weeks migration cost, team training needed, some queries need rewriting.

**Business version** (for Product):
```markdown
**Decision**: Upgrade from MySQL to PostgreSQL

**Why this matters to Product**:
- ✅ **Faster analytics**: Complex customer reports run 3x faster (users happier)
- ✅ **Better search**: Full-text search works better (find anything feature)
- ✅ **Easier integrations**: JSON support makes API integrations easier (faster partnerships)

**Cost**:
- 2 weeks of engineering time (delays 1 feature)
- $500/month extra hosting cost (negligible)

**Timeline**:
- Start: Jan 1
- Done: Jan 15
- Rollout: Jan 20 (monitored, can rollback)

**Risk**: Low (we've tested extensively, can rollback in 5 minutes if issues)

**Recommendation**: Do it (long-term benefits outweigh short-term cost)
```

---

## 🎯 Common Translation Scenarios

### Scenario 1: Executive Asks "Are We Scalable?"

❌ **Bad** (tech jargon):
> "Depends on traffic patterns and database sharding strategy. Current architecture supports ~10K concurrent users with horizontal scaling via Kubernetes. We'd need to implement caching and read replicas for 100K+ users."

✅ **Good** (business language):
```markdown
**Short answer**: Yes, we can handle 10x our current usage (5K → 50K users).

**Current capacity**: 5K users (current), 50K users (max)

**If we grow beyond 50K**:
- We need 2 weeks to upgrade (costs $2K/month extra)
- We'll know 3 months in advance (we monitor growth)

**Bottom line**: We're good for next 12 months. No immediate action needed.
```

---

### Scenario 2: Sales Asks "Is This Feature Enterprise-Ready?"

❌ **Bad** (vague):
> "Yeah, it's pretty solid. We did some testing."

✅ **Good** (specific):
```markdown
**Feature**: User Analytics Dashboard

**Enterprise-readiness checklist**:
- ✅ Scalability: Tested with 100K users (works great)
- ✅ Security: Data encrypted, SOC 2 compliant
- ✅ Performance: Loads in <1 second (even with 10M data points)
- ✅ Reliability: 99.95% uptime (monitored 24/7)
- ✅ Support: We have runbooks for on-call (fixes in <1 hour)

**Limitations** (be honest):
- ⚠️ No SSO yet (coming Q2 2026)
- ⚠️ No audit logs (coming Q1 2026)

**Recommendation**: Yes, ready to sell to Enterprise customers (with caveats above)
```

---

### Scenario 3: CS Asks "Why Is This Taking So Long?"

❌ **Bad** (defensive):
> "It's complex! We have to refactor the entire API layer, update database schemas, write tests, and ensure backwards compatibility."

✅ **Good** (empathetic + clear):
```markdown
**What customer asked for**: Dark mode

**Why it's taking 3 weeks** (not 1 day):
1. **Design**: 5 days (redesign every screen for dark theme)
2. **Development**: 10 days (update 50+ UI components)
3. **Testing**: 5 days (test on all browsers/devices)

**Can we go faster?**:
- We could ship in 1 week with bugs (not recommended)
- We could skip testing (risky, customer complaints)

**Recommendation**: Stick with 3 weeks (quality > speed)

**Workaround for customer**: 
- They can use browser extension for now (not perfect, but helps)
- We'll notify them when ready (priority beta access)

Make sense?
```

---

## 🎭 RACI: Translation Responsibilities

| Actividad | Engineering | Product | Sales | CS | Executives |
|-----------|-------------|---------|-------|-----|-----------|
| **Tech → Business (feature status)** | R | A | I | I | I |
| **Business → Tech (customer requests)** | C | R | A | A | I |
| **Incident translation (customer comms)** | R | C | I | A | I |
| **Roadmap translation (exec updates)** | R | A | I | I | I |
| **Metrics translation (QBR)** | R | C | I | I | A |

**Leyenda**: R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## 📚 Translation Examples (Real Scenarios)

### Example 1: "Kubernetes Migration"

**Tech version**:
> "We're migrating from EC2 to Kubernetes for container orchestration. This will enable horizontal pod autoscaling, declarative infrastructure, and blue-green deployments. ETA: 4 weeks (2 sprints)."

**Business version**:
```markdown
**What we're doing**: Upgrading our server infrastructure

**Why**:
- ✅ Auto-scaling: App handles traffic spikes automatically (no manual intervention)
- ✅ Faster deployments: Ship features in 5 minutes (vs 30 minutes now)
- ✅ Zero-downtime deploys: Users never see "app is down" messages

**Timeline**: 4 weeks (done by Jan 15)

**Risk**: Low (we're testing extensively, can rollback)

**Customer impact**: Zero (invisible upgrade, just makes app better)
```

---

### Example 2: "High P99 Latency"

**Tech version**:
> "P99 latency spiked to 2 seconds (target <500ms). Root cause: Database query missing index. Fix: Added composite index on `user_id, created_at`. Latency now back to 300ms."

**Business version**:
```markdown
**What happened**: App was slow for ~1% of users (99% were fine)

**Impact**: 
- Affected: 50 users (out of 5,000)
- Duration: 2 hours
- Symptoms: Pages took 2-3 seconds to load (normally <1 second)

**Root cause**: Database query was slow (missing optimization)

**How we fixed**: Optimized database (2-minute fix)

**Prevention**: We now monitor this closely (alerts if slow)

**Status**: Resolved ✅
```

---

### Example 3: "Tech Debt Refactor"

**Tech version**:
> "We need 3 weeks to refactor the authentication module. Current code is spaghetti (high coupling, low cohesion). Refactor will reduce complexity from 200 lines/function to 20 lines/function, making future features 50% faster to ship."

**Business version**:
```markdown
**What we're doing**: Cleaning up code (no new features this sprint)

**Why**:
- Current code is messy (built 2 years ago when we were moving fast)
- Adding new features takes 2x longer than it should
- Bugs are harder to find (risky)

**Benefit**:
- Future features ship 50% faster (2 weeks → 1 week)
- Fewer bugs (cleaner code = less mistakes)
- Easier onboarding (new engineers ramp up faster)

**Timeline**: 3 weeks (Jan 1 - Jan 20)

**Tradeoff**: We'll ship 2 fewer features this month, but 10 more features next quarter (net positive)

**Recommendation**: Do it now (tech debt gets worse over time)
```

---

## ✅ Success Criteria

### Mes 1
- ✅ Translation framework documented (this doc)
- ✅ Team trained (1-hour workshop on translation)
- ✅ 5 examples of good translations (shared in #engineering)

### Mes 2-3
- ✅ Stakeholder satisfaction >3.5/5 ("I understand engineering updates")
- ✅ Zero "I don't understand what engineering is saying" complaints
- ✅ 80% of updates use business language (not tech jargon)

### Mes 4+
- ✅ Stakeholder satisfaction >4/5
- ✅ Engineers proactively translate (don't need reminders)
- ✅ Sales can explain features to customers (no engineering involvement needed)

---

## 🔗 Links Relacionados

- [External Stakeholders](./external-stakeholders.md) - Quién necesita qué información
- [Channel Ownership](./channel-ownership.md) - Dónde postear updates traducidos
- [Incident Communication](./incident-communication.md) - Cómo traducir incidentes para customers
- [Documentation Ownership](./documentation-ownership.md) - Cómo documentar decisiones técnicas

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (con feedback de stakeholders)
