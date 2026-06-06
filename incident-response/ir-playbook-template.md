# Incident Response Playbook Template

Standard IR workflow template based on SOC operations 
experience. Follows a Prepare → Identify → Contain → 
Eradicate → Recover → Lessons Learned structure.
 
---

## Playbook: Failed Authentication / Brute Force Alert

**Severity:** SEV-C (review) → escalate to SEV-B if 
confirmed attack

**Trigger:** Multiple failed login attempts from 
single source within defined time window

---

### Step 1 — Identify

- [ ] Note the username, source IP, and timestamp 
  from the alert
- [ ] Check if the account is active and legitimate
- [ ] Determine if the IP is internal or external
- [ ] Check for successful login after failed attempts
- [ ] Review login history for the past 7 days

**Questions to answer:**
- Is this a known user or service account?
- Is the source IP recognized?
- Did any login succeed after the failures?

---

### Step 2 — Analyse

- [ ] Cross-reference IP against threat intel 
  (VirusTotal, AbuseIPDB)
- [ ] Check if other accounts were targeted from 
  the same IP
- [ ] Review endpoint activity if a login succeeded
- [ ] Check for MFA bypass attempts

---

### Step 3 — Contain

If confirmed malicious:
- [ ] Disable the affected account immediately
- [ ] Block the source IP at the firewall/gateway
- [ ] Notify the account owner and IT team
- [ ] Escalate to Tier-2 with full evidence package

If likely false positive:
- [ ] Document findings and close ticket
- [ ] Note the pattern for future tuning

---

### Step 4 — Document

Record in ticket:
- Alert source and ID
- Timeline of events
- Actions taken
- Escalation decision and reason
- Resolution

---

## Playbook: BitLocker Recovery Request

**Trigger:** User locked out, recovery key needed

**Steps:**
- [ ] Verify user identity through IT helpdesk process
- [ ] Confirm device belongs to the requesting user 
  via asset management
- [ ] Retrieve BitLocker recovery key from Azure AD 
  or MBAM
- [ ] Provide key via secure channel only
- [ ] Log the recovery event with user, device, 
  date, and approving analyst

---

*Template based on real SOC runbook experience at 
NationsBenefits India (2022–2023).*
