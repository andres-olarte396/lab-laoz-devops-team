# Communication Cleanup Process - Proceso de Limpieza de Comunicación

## 📋 Resumen Ejecutivo

**Problema**: Slack con 200+ canales (mayoría inactivos). Threads de hace 6 meses pinnados. Mensajes de 2023 que nadie lee. Channel topics desactualizados ("Working on Q3 goals" en Q1). Información crítica enterrada en noise.

**Solución**: **Cleanup process sistemático** con review mensual/trimestral, automated archival, y ownership claro.

**Beneficio**:
- Channels relevantes (archivamos 50% de canales inactivos)
- Información findable (pins actualizados, threads archivados)
- Onboarding más fácil (nuevos hires solo ven canales activos)
- Mejor signal-to-noise ratio

---

## 🗓️ Cleanup Calendar

### Monthly Cleanup (Last Friday, 30 min)

**Who**: Channel Owners (see [Channel Ownership](./channel-ownership.md))

**What to clean**:
1. ✅ **Pinned Messages** (review all pins):
   - Unpin outdated messages (>30 days old)
   - Pin new important messages
   - Update pin descriptions

2. ✅ **Channel Topic** (update if needed):
   - Remove outdated info ("Q3 goals" → "Q1 goals")
   - Add current context ("Migrating to Kubernetes" if relevant)

3. ✅ **Old Threads** (archive threads >90 days):
   - Mark as resolved (if applicable)
   - Summarize key decisions in #engineering wiki

4. ✅ **Member Audit** (check who's in channel):
   - Remove people who left company
   - Add new team members

**Time**: 30 minutes per channel (allocate 30 min last Friday of month)

---

### Quarterly Cleanup (First Friday of Quarter, 1 hour)

**Who**: Engineering Manager + Channel Owners

**What to clean**:
1. ✅ **Channel Audit** (full review):
   - Archive inactive channels (no activity >3 months)
   - Merge duplicate channels (#frontend vs #front-end)
   - Rename confusing channels (#team-a → #payments-team)

2. ✅ **Documentation Sync** (update docs):
   - Update channel list in Confluence
   - Update onboarding guide (channels to join)
   - Update RACI matrix (channel ownership)

3. ✅ **Metrics Review** (analyze channel health):
   - Channels with <5 messages/month → Archive?
   - Channels with >100 messages/day → Split?
   - Member count (too many? too few?)

**Time**: 1 hour (quarterly planning)

---

### Yearly Cleanup (January, Half Day)

**Who**: Engineering Manager + Entire Team

**What to clean**:
1. ✅ **Full Audit** (review all 200+ channels):
   - Archive 50% of inactive channels
   - Consolidate similar channels
   - Create new channels (if needed)

2. ✅ **Workspace Settings** (global cleanup):
   - Update emoji packs (remove unused)
   - Update Slack apps/bots (remove unused integrations)
   - Review retention policy (keep messages how long?)

3. ✅ **Onboarding Refresh** (update onboarding materials):
   - Update channel list for new hires
   - Update templates (deployment notifications, RFCs)
   - Update buddy system guide

**Time**: Half day (company-wide initiative)

---

## 📝 Monthly Cleanup Checklist (Template)

**Channel**: #engineering  
**Owner**: @engineering-manager  
**Date**: 2025-12-27 (Last Friday of December)

### 1. Pinned Messages

**Current pins** (5 total):
- ✅ Keep: "Incident response protocol" (updated last week)
- ✅ Keep: "On-call schedule Q1 2026" (still relevant)
- ❌ Unpin: "Q3 goals thread" (outdated, Q3 ended)
- ❌ Unpin: "Kubernetes migration update" (migration done 2 months ago)
- ✅ Keep: "Dark mode launch announcement" (launched last week, still fresh)

**New pins**:
- 📌 Pin: "Q1 2026 goals" (just posted today)

**Total**: 3 pins (5 → 3, cleaned!)

---

### 2. Channel Topic

**Current topic**: 
> "Engineering team discussions. Q3 goals: Ship dark mode, Kubernetes migration."

**Updated topic**:
> "Engineering team discussions. Q1 2026: Slack integration, performance improvements. On-call: @current-oncall"

---

### 3. Old Threads (Archive)

**Threads >90 days** (5 threads):
- ❌ Archive: "Kubernetes migration plan" (migration done, no longer relevant)
- ❌ Archive: "Q2 retro thread" (Q2 ended, summarized in Confluence)
- ✅ Keep: "API v2 design discussion" (still ongoing, not resolved)

**Action**: Archived 2 threads, summarized in Confluence

---

### 4. Member Audit

**Current members**: 25 people

**Changes**:
- ➕ Add: @new-backend-engineer (joined last week)
- ➕ Add: @new-frontend-engineer (joined last week)
- ➖ Remove: @old-engineer (left company 2 months ago)

**New total**: 26 members (25 → 26)

---

### 5. Completion

**Time spent**: 25 minutes  
**Next cleanup**: Jan 31, 2026 (last Friday of January)  
**Status**: ✅ Complete

---

## 🤖 Automated Cleanup (Slack Bots)

### Bot 1: Stale Pin Detector

**Purpose**: Alert channel owners when pins are >30 days old

**How it works**:
1. Bot runs weekly (every Monday 9am)
2. Scans all channels for pins
3. Finds pins >30 days old
4. Posts reminder in channel:

**Slack message** (example):
```markdown
🧹 **Stale Pin Alert**

This channel has 3 pins older than 30 days:
- "Q3 goals thread" (pinned 120 days ago by @manager)
- "Kubernetes migration" (pinned 75 days ago by @devops-lead)

@channel-owner Please review and unpin outdated messages.

Cleanup guide: https://docs.company.com/cleanup
```

**Implementation** (Slack Workflow Builder or custom bot):
```javascript
// Pseudo-code
const pins = await slack.getPins(channelId);
const stalePins = pins.filter(pin => pin.age > 30);

if (stalePins.length > 0) {
  await slack.postMessage({
    channel: channelId,
    text: `🧹 Stale Pin Alert: ${stalePins.length} pins >30 days`,
    blocks: [...]
  });
}
```

---

### Bot 2: Inactive Channel Detector

**Purpose**: Flag channels with no activity >3 months (candidates for archival)

**How it works**:
1. Bot runs monthly (first Monday of month)
2. Scans all channels
3. Finds channels with <5 messages in last 90 days
4. Posts in #engineering:

**Slack message** (example):
```markdown
🗂️ **Inactive Channel Report** (December 2025)

These channels had <5 messages in the last 90 days:

1. #old-project (0 messages, last activity 150 days ago)
2. #archived-feature (2 messages, last activity 95 days ago)
3. #random-team (4 messages, mostly bot posts)

**Recommendation**: Archive these channels (no one uses them)

@engineering-manager Review and archive if appropriate.
```

**Implementation**:
```javascript
// Pseudo-code
const channels = await slack.getChannels();
const inactiveChannels = [];

for (const channel of channels) {
  const messages = await slack.getMessages(channel.id, last90Days);
  if (messages.length < 5) {
    inactiveChannels.push(channel);
  }
}

await slack.postMessage({
  channel: '#engineering',
  text: `🗂️ Inactive channels: ${inactiveChannels.length}`,
  blocks: [...]
});
```

---

### Bot 3: Thread Archiver

**Purpose**: Auto-archive threads >90 days (move to "Resolved Threads" channel or Confluence)

**How it works**:
1. Bot runs weekly (every Friday 5pm)
2. Scans channels for threads
3. Finds threads >90 days with no recent activity
4. Posts reminder:

**Slack message** (example):
```markdown
📦 **Old Thread Alert**

This thread is 120 days old with no activity in 60 days:

**Thread**: "Kubernetes migration plan"
**Last activity**: 60 days ago

Should we archive this? 
- ✅ Yes, migration is done
- ⏸️ No, still relevant

React with ✅ to archive.

@channel-owner
```

**Auto-archive** (if no response in 7 days):
- Move thread to #resolved-threads (or Confluence)
- Post link in original channel: "Thread archived → [link]"

---

## 🗑️ Channel Archival Process

### When to Archive a Channel

**Archive if**:
- ❌ No activity >3 months (dead channel)
- ❌ Project finished (e.g., #kubernetes-migration after migration done)
- ❌ Duplicate of another channel (e.g., #frontend vs #front-end)
- ❌ Team disbanded (e.g., #project-x-team if project cancelled)

**Don't archive if**:
- ✅ Seasonal activity (e.g., #tax-season active only in March-April)
- ✅ Long-term reference (e.g., #incident-2024-12-07 for post-mortem)
- ✅ Still has members actively checking (even if low message volume)

---

### How to Archive a Channel

**Process** (Engineering Manager or Channel Owner):

1. ✅ **Post archive notice** (7 days warning):
   ```markdown
   📢 **Channel Archival Notice**
   
   This channel will be archived on Jan 15 (7 days from now).
   
   **Reason**: No activity in 4 months (project finished)
   
   **Action needed**:
   - Save any important messages (copy to Confluence)
   - React with ⚠️ if you think we should keep this channel
   
   Questions? DM @engineering-manager
   ```

2. ✅ **Wait 7 days** (allow time for objections)

3. ✅ **Archive channel** (if no objections):
   - Slack → Click channel name → Settings → Archive channel
   - Archived channels are read-only (searchable but can't post)

4. ✅ **Update documentation**:
   - Remove from onboarding guide (channels to join)
   - Remove from Confluence (channel list)
   - Update RACI matrix (if channel had ownership)

5. ✅ **Post in #engineering**:
   ```markdown
   🗂️ Archived #old-project channel
   
   **Reason**: Project completed 6 months ago
   **Messages preserved**: Yes (searchable in Slack)
   
   If you need access, search Slack for "#old-project"
   ```

---

### How to Unarchive a Channel (If Needed)

**Scenario**: Team realizes they need archived channel back

**Process**:
1. ✅ DM @engineering-manager or @workspace-admin
2. ✅ Manager unarchives channel (Slack → Settings → Unarchive)
3. ✅ Post in channel:
   ```markdown
   🔓 This channel was unarchived
   
   **Reason**: [Why it was needed again]
   **Going forward**: [New purpose or ownership]
   
   @new-owner
   ```

---

## 📊 Cleanup Metrics

### Metrics to Track

| Metric | Target | Red Flag | How to Measure |
|--------|--------|----------|----------------|
| **Active channels** | <50 (manageable) | >100 (too many) | Slack analytics |
| **Inactive channels (>3mo)** | <10% | >30% | Monthly bot report |
| **Stale pins (>30 days)** | <5 per channel | >10 per channel | Weekly bot report |
| **Monthly cleanup completion** | 100% (all owners) | <80% | Checklist completion rate |
| **Onboarding time (find info)** | <10 min to find channel | >30 min | New hire survey |

---

### Dashboard (Example - Slack Analytics)

**Metrics to visualize**:
- Total channels (trend: decreasing = good cleanup)
- Inactive channels count (trend: should stay low)
- Messages/channel/month (identify dead channels)
- Pins per channel (flag channels with >10 pins)

---

## ✅ Monthly Cleanup Workflow

**Last Friday of every month** (30 min):

### Step 1: Bot Sends Reminder (9am)

**Slack message** in #engineering:
```markdown
🧹 **Monthly Cleanup Day!** (Last Friday of month)

Channel owners: Please clean your channels today (30 min)

**Checklist**:
- [ ] Review pinned messages (unpin old, pin new)
- [ ] Update channel topic (remove outdated info)
- [ ] Archive old threads (>90 days)
- [ ] Audit members (add new, remove left)

**Template**: https://docs.company.com/monthly-cleanup

Post ✅ in thread when done!

@channel-owners
```

---

### Step 2: Owners Complete Cleanup (9am-5pm)

**Owners**:
- Tech Lead cleans #engineering
- DevOps Lead cleans #devops, #deployments, #incidents
- Product Manager cleans #product
- Design Lead cleans #design

**Each owner posts completion**:
```markdown
✅ #engineering cleanup done (25 min)

**Changes**:
- Unpinned 2 old messages
- Updated topic (Q3 → Q1 goals)
- Archived 3 threads
- Added 2 new team members

Next cleanup: Jan 31
```

---

### Step 3: Engineering Manager Reviews (5pm)

**Manager checks completion**:
- ✅ All channel owners posted completion? (if not, ping stragglers)
- ✅ Any channels need archival? (flag for quarterly review)

**Manager posts summary**:
```markdown
✅ **December Cleanup Complete!**

**Channels cleaned**: 12/12 (100%)
**Pins unpinned**: 15 (across all channels)
**Threads archived**: 8
**Members updated**: +5 new, -2 left

**Inactive channels flagged**: 3 (#old-project, #archived-feature, #random-team)
→ Will archive in Q1 cleanup (January)

Great job team! 🎉

Next cleanup: Jan 31 (last Friday of January)
```

---

## 🔧 Tools for Cleanup

### Slack Built-In Features

1. **Channel Analytics** (Slack workspace admin):
   - View message volume per channel
   - See member activity
   - Export channel list

2. **Search** (find old messages):
   - `in:#engineering after:2025-01-01 before:2025-01-31` (messages in Jan)
   - `has:pin` (find all pinned messages)
   - `from:@user` (find messages from specific person)

3. **Workflow Builder** (automate reminders):
   - Create workflow: "Monthly cleanup reminder"
   - Trigger: Last Friday of month, 9am
   - Action: Post message in #engineering

---

### Third-Party Tools

1. **Slack Archivist** (bot):
   - Auto-archive inactive channels
   - Generate reports on channel health
   - [https://slackarchivist.com](https://slackarchivist.com)

2. **Standuply** (bot):
   - Auto-detect stale pins
   - Remind channel owners to clean
   - [https://standuply.com](https://standuply.com)

3. **Statsbot** (analytics):
   - Dashboard for channel metrics
   - Alert on inactive channels
   - [https://statsbot.co](https://statsbot.co)

---

## 📝 Quarterly Cleanup Checklist (Template)

**Quarter**: Q1 2026 (Jan 1 - Mar 31)  
**Cleanup Date**: First Friday of January (Jan 3)  
**Owner**: @engineering-manager  
**Time**: 1 hour

### 1. Channel Audit

**Total channels**: 120 (before cleanup)

**Inactive channels** (no activity >3 months):
- #old-project (0 messages, 150 days)
- #archived-feature (2 messages, 95 days)
- #random-team (4 messages, 120 days)
- #kubernetes-migration (10 messages, 90 days - migration done)

**Action**: Archive 4 channels → New total: 116 channels

---

### 2. Duplicate Channels (Merge)

**Duplicates found**:
- #frontend + #front-end → Merge into #frontend (archive #front-end)
- #deployments + #deploys → Merge into #deployments (archive #deploys)

**Action**: Merge 2 pairs → Archive 2 channels → New total: 114 channels

---

### 3. Rename Confusing Channels

**Confusing names**:
- #team-a → #payments-team (clearer purpose)
- #project-x → #slack-integration (project name is vague)

**Action**: Rename 2 channels (post announcement in each)

---

### 4. Documentation Sync

**Update docs**:
- ✅ Update Confluence (channel list)
- ✅ Update onboarding guide (remove archived channels)
- ✅ Update RACI matrix (update ownership)

---

### 5. Metrics Review

**Channel health**:
- Active channels (<50): ✅ 40 channels (good!)
- Inactive channels (>3mo): ✅ 6% (7/114, target <10%, good!)
- Channels with >10 pins: ⚠️ 3 channels (#engineering, #devops, #product)
  - Action: Owners clean pins

**Member satisfaction** (survey):
- "Easy to find channels": 4.2/5 (up from 3.8 last quarter ✅)
- "Channels are organized": 4.0/5 (up from 3.5 ✅)

---

### 6. New Channels (Create if needed)

**Requests**:
- ✅ Create #security-private (for vulnerability discussions)
- ✅ Create #customer-feedback (centralize feedback from CS)

**Action**: Created 2 channels → New total: 116 channels

---

### 7. Summary

**Before cleanup**: 120 channels (30% inactive)  
**After cleanup**: 116 channels (6% inactive)  
**Time spent**: 1 hour  
**Next cleanup**: April 4, 2026 (first Friday of Q2)

---

## ✅ Success Criteria

### Mes 1
- ✅ Cleanup calendar documented (monthly/quarterly/yearly)
- ✅ Bots deployed (stale pin detector, inactive channel detector)
- ✅ First monthly cleanup completed (100% channel owners participated)

### Mes 2-3
- ✅ Inactive channels <15% (target <10% by Q2)
- ✅ Monthly cleanup completion >90%
- ✅ Team satisfaction >3.5/5 ("Channels are organized")

### Mes 4+
- ✅ Inactive channels <10%
- ✅ Monthly cleanup completion 100%
- ✅ Team satisfaction >4/5
- ✅ Onboarding time <10 min (to find right channel)

---

## 🔗 Links Relacionados

- [Channel Ownership](./channel-ownership.md) - Quién es responsable de limpiar qué canal
- [Onboarding Guide](./onboarding-guide.md) - Canales que nuevos hires deben unirse
- [Documentation Ownership](./documentation-ownership.md) - Cleanup de docs (similar workflow)
- [External Stakeholders](./external-stakeholders.md) - Stakeholder channels a mantener

---

**Versión**: 1.0  
**Última Actualización**: 2025-12-07  
**Owner**: Engineering Manager  
**Review Cycle**: Trimestral (ajustar proceso según feedback)
