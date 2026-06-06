# Incident Response Playbooks

SOC runbook templates based on real incident response 
workflows at NationsBenefits India (Nov 2022 – Aug 2023).

---

## Playbook 1 — Failed Authentication / Brute Force

**Severity level:** SEV-C (review) — escalate to SEV-B 
if attack confirmed  
**Detection sources:** SentinelOne, Microsoft 365 Defender, 
Azure AD sign-in logs

---

### Step 1 — Identify

- Note the username, source IP, timestamp, and alert source
- Check if the account is active and belongs to a real user
- Determine if the source IP is internal or external
- Check whether any login succeeded after the failures
- Review sign-in history for the past 7 days in Azure AD

Key questions:
- Is this a known user or a service account?
- Did MFA trigger or was it bypassed?
- Is the IP flagged in threat intelligence?

---

### Step 2 — Analyse

- Cross-reference source IP against VirusTotal and AbuseIPDB
- Check if multiple accounts were targeted from the same IP 
  (password spray pattern)
- If a login succeeded — review what the account accessed 
  immediately after
- Check for any inbox rule creation or forwarding rules 
  added (common post-compromise action)

---

### Step 3 — Contain

**If confirmed malicious:**
- Disable the compromised account immediately
- Block the source IP at the firewall or email gateway
- Revoke active sessions in Azure AD
- Force MFA re-registration
- Notify account owner and IT team
- Escalate to Tier-2 with full evidence package including 
  log exports, IP details, and timeline

**If likely false positive:**
- Document findings in the ticket
- Note the pattern for future alert tuning
- Close with false positive classification

---

### Step 4 — Document

Every incident ticket must contain:
- Alert source and alert ID
- Complete timeline of events
- Source IP and geolocation
- Actions taken at each step
- Escalation decision and justification
- Final resolution and classification

---

## Playbook 2 — BitLocker Recovery Request

**Trigger:** User reports device locked, BitLocker 
recovery key required  
**Severity:** Low — administrative, not security incident  
**Detection source:** Helpdesk ticket or direct user request

---

### Steps

1. Verify user identity through HR records or IT asset 
   management system
2. Confirm the device asset tag belongs to the requesting 
   user — do not issue keys for unverified devices
3. Retrieve the BitLocker recovery key from Azure AD 
   device management portal
4. Deliver the key via a secure, audited channel only — 
   never via email or chat
5. Log the recovery event: user name, device ID, date, 
   time, and approving analyst name
6. Follow up after 24 hours to confirm device access 
   restored successfully

**Security note:** BitLocker recovery requests are a 
common social engineering vector. Always verify identity 
independently before issuing keys.

---

## Playbook 3 — SEV-C Alert Response

**Severity:** SEV-C = review required, not yet confirmed 
as an incident  
**Target response time:** Within defined SLA window

---

### Steps

1. Open alert in the SIEM/EDR console
2. Read the full alert context — do not action without 
   understanding what triggered it
3. Check asset details — who owns the device, what team 
   are they on, is it a critical system?
4. Pull relevant logs for the time window around the alert
5. Apply the appropriate specific playbook (failed login, 
   malware detection, DLP breach, etc.)
6. Make a classification decision:
   - False positive → document and close
   - True positive, low risk → remediate and document
   - True positive, elevated risk → escalate to Tier-2 
     with full evidence

---

*Based on SOC runbooks authored at NationsBenefits India 
(2022–2023).*
