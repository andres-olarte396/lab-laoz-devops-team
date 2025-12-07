# Security Response - Respuesta a Incidentes de Seguridad

## 📋 Resumen Ejecutivo

**Problema**: Data breach, unauthorized access, malware → Si no respondemos rápido: data robada, multas (GDPR €20M), reputación destruida.

**Solución**: **Security incident response process** con clasificación de severidad, containment procedures, forensics, disclosure plan.

**Beneficio**:
- Contención rápida (breach detected → contained en <1 hora)
- Minimizar data loss
- Cumplir regulaciones (GDPR, SOC 2, ISO 27001)
- Preservar evidencia (forensics para investigación)
- Transparencia con clientes (disclosure honesto)

---

## 🎯 Security Incident Types

### Type 1: Data Breach

**Definition**: Acceso no autorizado a datos sensibles (PII, PHI, financial data)

**Examples**:
- Database dump leaked
- S3 bucket público con customer data
- SQL injection expone user passwords

**Severity**: 🔴 CRITICAL (SEV-1)

**Regulatory Impact**: GDPR breach notification (72 hours), fines hasta €20M

---

### Type 2: Unauthorized Access

**Definition**: Alguien accede a sistemas sin permiso

**Examples**:
- Compromised credentials (password reuse)
- Privilege escalation (user → admin)
- API key leaked en GitHub

**Severity**: 🟠 HIGH (SEV-2)

**Impact**: Can lead to data breach

---

### Type 3: Malware / Ransomware

**Definition**: Malicious software infecta sistemas

**Examples**:
- Ransomware encrypts files (pide Bitcoin)
- Cryptominer en production servers
- Trojan steals credentials

**Severity**: 🔴 CRITICAL (SEV-1)

**Impact**: Downtime, data loss, ransom payment

---

### Type 4: Denial of Service (DoS/DDoS)

**Definition**: Atacantes saturan sistema con tráfico → servicio cae

**Examples**:
- DDoS attack (1M requests/sec)
- Resource exhaustion (CPU/memory maxed)
- DNS amplification attack

**Severity**: 🟠 HIGH (SEV-2)

**Impact**: Downtime, revenue loss

---

### Type 5: Phishing / Social Engineering

**Definition**: Atacantes engañan a empleados para obtener acceso

**Examples**:
- Phishing email ("Click here to reset password")
- CEO fraud ("Wire $50K to this account")
- Fake support call ("I need your credentials to fix issue")

**Severity**: 🟡 MEDIUM (SEV-3)

**Impact**: Can lead to unauthorized access

---

### Type 6: Insider Threat

**Definition**: Empleado (actual o ex) con acceso malicioso

**Examples**:
- Disgruntled employee deletes production database
- Ex-employee still has access (offboarding failed)
- Employee leaks customer data

**Severity**: 🔴 CRITICAL (SEV-1)

**Impact**: Data breach, sabotage

---

## 🚨 Security Incident Severity

### SEV-1 (Critical Security Incident)

**Definition**: Active data breach, widespread impact, regulatory notification required

**Examples**:
- Customer PII exposed (>1,000 records)
- Production database compromised
- Ransomware encrypting files
- Attacker has admin access

**Response Time**: <15 min (immediate war room)

**Notification**: CEO, Legal, PR, Customers (if PII affected)

---

### SEV-2 (High Security Incident)

**Definition**: Security vulnerability exploited, limited impact

**Examples**:
- Single user account compromised
- API key leaked (revoked quickly)
- DDoS attack (mitigated)

**Response Time**: <1 hour

**Notification**: Security team, Engineering Manager

---

### SEV-3 (Medium Security Incident)

**Definition**: Potential security issue, no confirmed breach

**Examples**:
- Phishing email reported (no one clicked)
- Suspicious login attempt (blocked by MFA)
- Vulnerability scan found issue (not exploited)

**Response Time**: <4 hours

**Notification**: Security team

---

### SEV-4 (Low Security Incident)

**Definition**: Security policy violation, no immediate risk

**Examples**:
- Employee shared password (changed)
- Laptop left unlocked
- Unsanctioned software installed

**Response Time**: <24 hours

**Notification**: Security team, Manager

---

## 🛡️ Incident Response Process (NIST Framework)

### Phase 1: Preparation (Before Incident)

**Goal**: Be ready before attack happens

**Actions**:

- [ ] **Security Training** (all employees)
  - Phishing awareness (quarterly training)
  - Password hygiene (password manager, no reuse)
  - Reporting suspicious activity

- [ ] **Security Tools Deployed**
  - SIEM (Security Information and Event Management): Splunk, Datadog Security
  - EDR (Endpoint Detection and Response): CrowdStrike, Microsoft Defender
  - IDS/IPS (Intrusion Detection/Prevention): Snort, Suricata
  - WAF (Web Application Firewall): Cloudflare, Azure WAF

- [ ] **Incident Response Plan Documented** (this doc)

- [ ] **Contact List Updated**
  - Security team (24/7 on-call)
  - Legal counsel
  - PR/Communications
  - External forensics firm (retainer)

- [ ] **Backups Tested** (can restore in <4 hours)

---

### Phase 2: Detection & Analysis (<15 min)

**Goal**: Detect attack, assess severity, activate war room

**Detection Sources**:

1. **Automated Alerts** (SIEM, EDR)
   - Example: "Unusual login from China" (user is in USA)
   - Example: "10,000 failed login attempts in 1 min"

2. **User Reports**
   - Employee: "I got a weird email asking for my password"
   - Customer: "I see someone else's data in my account"

3. **External Notification**
   - Security researcher: "Your database is exposed on Shodan"
   - GitHub: "You committed an API key"

---

**Analysis Checklist** (15 min):

- [ ] **Confirm Incident is Real** (not false positive)
  - Check logs
  - Verify with affected user
  
- [ ] **Assess Scope**
  - How many users affected?
  - What data accessed?
  - Is attacker still active?

- [ ] **Classify Severity** (SEV-1, 2, 3, 4)

- [ ] **Activate War Room** (if SEV-1 or SEV-2)
  - Create #security-incident-YYYYMMDD Slack channel
  - Page on-call security engineer (PagerDuty)
  - Notify Security Lead, CTO, Legal (if SEV-1)

---

### Phase 3: Containment (<1 hour)

**Goal**: Stop attack from spreading, preserve evidence

**Short-term Containment** (immediate, <15 min):

- [ ] **Isolate Affected Systems**
  ```bash
  # Disconnect compromised server from network
  kubectl cordon node-compromised-01  # Stop new pods
  kubectl drain node-compromised-01   # Evict existing pods
  
  # Block attacker IP at firewall
  az network nsg rule create \
    --resource-group myapp-rg \
    --nsg-name myapp-nsg \
    --name block-attacker \
    --priority 100 \
    --source-address-prefixes 1.2.3.4 \
    --access Deny
  ```

- [ ] **Revoke Compromised Credentials**
  ```bash
  # Rotate API keys immediately
  az keyvault secret set --vault-name myapp-kv --name api-key --value NEW_KEY
  
  # Force password reset for affected users
  az ad user update --id alice@company.com --force-change-password-next-login true
  
  # Revoke OAuth tokens
  curl -X POST https://oauth.company.com/revoke -d "token=COMPROMISED_TOKEN"
  ```

- [ ] **Enable Extra Logging** (for forensics)
  ```bash
  # Increase logging verbosity
  kubectl set env deployment/myapp LOG_LEVEL=debug
  ```

---

**Long-term Containment** (within 1 hour):

- [ ] **Patch Vulnerability** (if exploited)
  - Apply security patch
  - Deploy fixed version
  
- [ ] **Rebuild Compromised Systems** (from clean backup)
  - Do NOT just "clean" infected system (rootkits hide)
  - Nuke & rebuild from trusted image

- [ ] **Reset All Credentials** (if widespread breach)
  - Force password reset for all users
  - Rotate all API keys, database passwords, certificates

---

### Phase 4: Eradication (1-4 hours)

**Goal**: Remove attacker completely, close vulnerability

**Actions**:

- [ ] **Remove Malware** (if present)
  - Scan with antivirus (ClamAV, Windows Defender)
  - Manual inspection (check cron jobs, startup scripts)

- [ ] **Close Security Holes**
  - Patch vulnerable software (CVE-2025-XXXX)
  - Fix misconfiguration (S3 bucket no longer public)
  - Update firewall rules (block unnecessary ports)

- [ ] **Verify Attacker is Gone**
  - Monitor for suspicious activity (next 24 hours)
  - Check for backdoors (webshells, SSH keys)

---

### Phase 5: Recovery (4-24 hours)

**Goal**: Restore service to normal

**Actions**:

- [ ] **Restore from Backup** (if data corrupted)
  ```bash
  # Restore database from last clean backup
  pg_restore -h localhost -U postgres -d myapp_db /backups/myapp_db_20250114.dump
  ```

- [ ] **Bring Systems Back Online**
  ```bash
  # Uncordon Kubernetes node
  kubectl uncordon node-repaired-01
  
  # Resume traffic
  az network traffic-manager endpoint update \
    --resource-group myapp-rg \
    --profile-name myapp-tm \
    --name primary-endpoint \
    --endpoint-status Enabled
  ```

- [ ] **Monitor Closely** (next 48 hours)
  - Watch for anomalies (unexpected traffic, failed logins)
  - Verify backups working (in case of reinfection)

---

### Phase 6: Post-Incident Activity (48 hours - 1 week)

**Goal**: Learn from incident, prevent recurrence

**Actions**:

- [ ] **Forensics Report** (what happened, how, why)
  - Timeline of events
  - Root cause analysis (5 Whys)
  - Indicators of Compromise (IOCs)

- [ ] **Blameless Post-Mortem** (see [Post-Mortem Process](./post-mortem.md))
  - What went well
  - What went wrong
  - Action items to prevent recurrence

- [ ] **Regulatory Notification** (if required)
  - GDPR: 72 hours to notify DPA (Data Protection Authority)
  - CCPA: "Without unreasonable delay"
  - HIPAA: 60 days for breach >500 records

- [ ] **Customer Communication** (if PII affected)
  - Email to affected customers (within 72 hours)
  - Offer credit monitoring (if SSN/financial data leaked)

- [ ] **Implement Fixes** (from post-mortem action items)
  - Deploy patch
  - Update security policies
  - Add detection rules (so we catch this next time)

---

## 🔍 Forensics & Evidence Preservation

### Why Forensics?

**Goals**:
- Understand attack (how did they get in?)
- Identify attacker (IP, methods, tools)
- Legal evidence (if prosecuting)
- Improve defenses (prevent recurrence)

---

### Evidence Collection Checklist

**Preserve Evidence BEFORE cleaning up**:

- [ ] **Disk Images** (full copy of compromised system)
  ```bash
  # Create forensic image (bit-for-bit copy)
  dd if=/dev/sda of=/mnt/forensics/disk.img bs=4M status=progress
  
  # Calculate hash (verify integrity)
  sha256sum /mnt/forensics/disk.img > disk.img.sha256
  ```

- [ ] **Memory Dump** (RAM contents, can contain passwords)
  ```bash
  # Capture memory (Linux)
  sudo dd if=/dev/mem of=/mnt/forensics/memory.dump bs=1M
  ```

- [ ] **Logs** (all logs from last 30 days)
  ```bash
  # Export logs
  kubectl logs --all-containers --since=720h > /mnt/forensics/k8s-logs.txt
  
  # Export SIEM logs (Datadog, Splunk)
  # Via UI: Export to CSV/JSON
  ```

- [ ] **Network Traffic Capture** (if ongoing)
  ```bash
  # Capture packets (tcpdump)
  sudo tcpdump -i eth0 -w /mnt/forensics/traffic.pcap
  ```

- [ ] **Database Audit Logs** (who accessed what, when)
  ```sql
  -- PostgreSQL audit log
  SELECT * FROM pg_stat_activity WHERE query NOT LIKE '%pg_stat_activity%';
  ```

---

**Chain of Custody** (for legal admissibility):

- Document who collected evidence (name, timestamp)
- Document who has access (locked storage)
- Hash evidence (SHA-256 checksum to prove tampering didn't occur)

---

### Indicators of Compromise (IOCs)

**What to look for**:

- **Unusual Network Traffic**
  - Connections to known malicious IPs (check threat intel: VirusTotal, AbuseIPDB)
  - Data exfiltration (large uploads to unknown servers)

- **Suspicious Processes**
  ```bash
  # Check running processes (Linux)
  ps aux | grep -E 'nc|ncat|socat'  # Netcat (reverse shell)
  
  # Check cron jobs (persistence)
  crontab -l
  cat /etc/cron.d/*
  ```

- **File Modifications**
  ```bash
  # Check recently modified files
  find / -type f -mtime -1  # Modified in last 24 hours
  
  # Check for webshells
  grep -r "eval(" /var/www/html/
  ```

- **Authentication Anomalies**
  - Failed login attempts (brute force)
  - Logins from unusual locations (China, Russia when user is in USA)
  - Logins at unusual times (3 AM when user normally works 9-5)

---

## 📢 Disclosure & Communication

### Internal Communication

**War Room** (#security-incident-YYYYMMDD):

- **Incident Commander**: Security Lead
- **Participants**: Security team, DevOps, Legal, PR, CTO
- **Updates**: Every 30 min (SEV-1), every 2 hours (SEV-2)

**Status Update Template**:

```markdown
## Security Incident Update - 14:30 UTC

**Status**: CONTAINMENT IN PROGRESS

**Summary**:
- Detected unauthorized access to production database at 13:45 UTC
- ~5,000 customer records potentially accessed (names, emails, no passwords)
- Attacker IP blocked, credentials rotated

**Actions Taken**:
- [x] Blocked attacker IP (1.2.3.4)
- [x] Revoked compromised API key
- [x] Isolated affected database
- [ ] Forensics in progress (ETA: 16:00 UTC)

**Next Steps**:
- Complete forensics analysis
- Verify no other systems compromised
- Draft customer notification (if required)

**ETA to Resolution**: 18:00 UTC
```

---

### External Communication (Customers)

**When to Notify Customers**:

- ✅ PII data accessed (names, emails, addresses)
- ✅ Financial data accessed (credit cards, bank accounts)
- ✅ Passwords compromised (even if hashed)
- ❌ No customer data affected (internal system only)

---

**Customer Notification Email Template**:

```
Subject: Security Incident Notification

Dear [Customer Name],

We are writing to inform you of a security incident that may have affected your account.

**What Happened**:
On January 15, 2025, we detected unauthorized access to our production database. We immediately blocked the attacker and began an investigation.

**What Information Was Affected**:
The following information may have been accessed:
- Name
- Email address
- Phone number
- Account creation date

The following information was NOT affected:
- Passwords (stored encrypted, not compromised)
- Credit card numbers (not stored in affected database)
- Social Security Numbers (we don't collect this)

**What We're Doing**:
- We have secured the vulnerability and blocked the attacker
- We are conducting a full forensics investigation
- We have engaged external security experts
- We are implementing additional security measures

**What You Should Do**:
- Change your password immediately (out of abundance of caution)
- Enable two-factor authentication (if not already enabled)
- Monitor your account for suspicious activity
- Be cautious of phishing emails (we will never ask for your password)

**Questions?**:
Contact our security team at security@company.com or call 1-800-XXX-XXXX.

We sincerely apologize for this incident and are committed to protecting your data.

Sincerely,
[CEO Name]
CEO, Company Name
```

**Timing**: Within 72 hours of discovering breach (GDPR requirement)

---

### Regulatory Notification (GDPR)

**GDPR Requirements** (EU):

- **72-hour notification** to Data Protection Authority (DPA)
  - Submit via DPA portal (e.g., ICO in UK, CNIL in France)
  - Include: Nature of breach, data affected, mitigation steps

- **Fine for non-compliance**: Up to €20M or 4% of global revenue

---

**GDPR Notification Template** (to DPA):

```
PERSONAL DATA BREACH NOTIFICATION
(Article 33 GDPR)

**1. Identity of Data Controller**:
Company Name, Address, DPO Contact: dpo@company.com

**2. Nature of Breach**:
Unauthorized access to production database containing customer PII

**3. Date & Time of Breach**:
January 15, 2025, 13:45 UTC (detected)
Estimated breach occurred: January 15, 2025, 10:00 UTC

**4. Categories of Data Affected**:
- Names (5,000 records)
- Email addresses (5,000 records)
- Phone numbers (2,000 records)

**5. Likely Consequences**:
Low risk: No financial data or passwords compromised.
Risk of phishing emails (attacker has emails).

**6. Measures Taken**:
- Blocked attacker IP immediately
- Revoked compromised credentials
- Notified affected individuals (January 16, 2025)
- Implemented additional access controls

**7. Contact Point**:
dpo@company.com, +44-XXX-XXX-XXXX
```

---

### Public Statement (Media)

**When to Issue**:
- Major breach (>10,000 records)
- Media coverage (reporters asking questions)
- Regulatory action (DPA issued statement)

**PR Statement Template**:

```
FOR IMMEDIATE RELEASE

Company Name Announces Security Incident

[CITY, DATE] - Company Name today announced that it detected and contained a security incident affecting customer data.

On January 15, 2025, we identified unauthorized access to one of our databases. We immediately blocked the attacker, secured the vulnerability, and began an investigation. Approximately 5,000 customer records (names and email addresses) may have been accessed. No passwords, financial data, or Social Security Numbers were affected.

We have notified all affected customers and offered free credit monitoring services. We are cooperating with law enforcement and have engaged external cybersecurity experts.

"The security and privacy of our customers' data is our top priority," said [CEO Name], CEO. "We deeply regret this incident and are taking additional steps to prevent future occurrences."

For more information, visit [company.com/security-incident].

Contact:
PR Team, pr@company.com
```

---

## 📊 Security Metrics

### Metric #1: Mean Time to Detect (MTTD)

**Definition**: Time from breach occurring to detection

**Target**: <5 min

**How to Improve**:
- Deploy SIEM (automated alerts)
- Enable audit logging
- Threat intelligence feeds

---

### Metric #2: Mean Time to Contain (MTTC)

**Definition**: Time from detection to containment (attacker blocked)

**Target**: <15 min

**How to Improve**:
- Automated response (block IP via script)
- Runbooks (step-by-step containment)

---

### Metric #3: Security Incidents per Quarter

**Track**: Number of SEV-1, SEV-2, SEV-3, SEV-4 incidents

**Target**: Decreasing trend (better defenses)

---

### Metric #4: Phishing Test Success Rate

**Test**: Send fake phishing emails (quarterly)

**Target**: <5% click rate (employees don't fall for phishing)

---

## 🎭 Roles & Responsibilities (RACI)

| Actividad                         | Security Lead | DevOps | Legal | PR  | CEO |
| --------------------------------- | ------------- | ------ | ----- | --- | --- |
| Detect incident                   | A/R           | R      | I     | I   | I   |
| Classify severity                 | A/R           | C      | I     | I   | I   |
| Contain attack                    | A             | R      | I     | I   | I   |
| Forensics investigation           | A/R           | C      | C     | I   | I   |
| Customer notification (SEV-1)     | C             | I      | A     | R   | A   |
| Regulatory notification (GDPR)    | C             | I      | A/R   | I   | C   |
| Public statement (media)          | C             | I      | C     | A/R | A   |
| Post-mortem                       | A/R           | C      | I     | I   | I   |

---

## 🚀 Implementation Roadmap

### Sprint 1: Incident Response Plan
- [ ] Document security incident response process (this doc)
- [ ] Create war room runbook
- [ ] Test incident response (tabletop exercise)

### Sprint 2: Detection Tools
- [ ] Deploy SIEM (Splunk, Datadog Security)
- [ ] Configure alerts (unauthorized access, data exfiltration)
- [ ] Integrate threat intelligence

### Sprint 3: Training
- [ ] Security awareness training (all employees)
- [ ] Phishing simulation (quarterly)
- [ ] Incident response drill (simulate breach)

### Sprint 4: Compliance
- [ ] GDPR compliance review
- [ ] Breach notification templates ready
- [ ] Legal review of disclosure process

---

## ✅ Success Criteria

### Mes 1
- ✅ Incident response plan documented
- ✅ War room runbook ready
- ✅ Tabletop exercise completed

### Mes 2-3
- ✅ SIEM deployed (alerts working)
- ✅ Security training completed (all employees)
- ✅ Phishing test <10% click rate

### Mes 4+
- ✅ MTTD <5 min, MTTC <15 min
- ✅ Zero SEV-1 incidents (or rapid containment)
- ✅ Compliance audits passed (GDPR, SOC 2)

---

## 🔗 Links Relacionados

- [Incident Management](./incident-management.md) - General incident response
- [Post-Mortem](./post-mortem.md) - Post-incident analysis
- [Backup & Recovery](./backup-recovery.md) - Disaster recovery

---

## 📚 Antipatterns

### ❌ Antipattern #1: "Hope It Goes Away"

**Problem**: Ignore security alert, hope it's false positive

**Example**:
- Alert: "Unusual login from China"
- Team: "Probably a false alarm, ignore it"
- Reality: Account compromised, data breached

**Solution**: ✅ Investigate every alert (even if likely false positive)

---

### ❌ Antipattern #2: "Hide the Breach"

**Problem**: Don't notify customers, hope no one finds out

**Example**:
- Breach discovered, 10,000 records leaked
- Team: "If we don't tell anyone, maybe they won't notice?"
- Reality: Researcher finds data on dark web, reports to media → Huge scandal

**Solution**: ✅ Transparency (notify customers, regulators, earn trust)

---

### ❌ Antipattern #3: "Wipe Evidence"

**Problem**: Immediately delete compromised system (destroys forensics)

**Example**:
- Server compromised → "Delete it!"
- Forensics: "How did they get in? We don't know, you deleted evidence"

**Solution**: ✅ Preserve evidence (disk image, logs) BEFORE cleanup

---

### ❌ Antipattern #4: "Blame the Victim"

**Problem**: Blame employee who fell for phishing

**Example**:
- Employee: "I clicked a phishing link, sorry"
- Manager: "You're fired!"
- Result: Other employees hide mistakes, breaches go unreported

**Solution**: ✅ Blameless culture (thank employee for reporting)

---

### ❌ Antipattern #5: "No Post-Mortem"

**Problem**: Breach contained, back to normal, no lessons learned

**Example**:
- Breach: SQL injection
- Team: "We patched it, done!"
- 3 months later: Same vulnerability in different endpoint

**Solution**: ✅ Post-mortem (why did this happen? how to prevent?)

---

**Versión**: 1.0  
**Última Actualización**: 2025-01-15  
**Owner**: Security Lead / CISO  
**Review Cycle**: Semestral (cada incident = review)
