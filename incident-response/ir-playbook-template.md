# Incident Response Playbooks

SOC Tier-1 runbooks based on real incident response 
workflows at NB Healthcare Technologies (NationsBenefits 
India), Nov 2022 – Aug 2023.

Approximately 10 incidents were escalated to Tier-2 
analysts and Information Security Engineers over the 
course of the role. The playbooks below reflect the 
actual investigation and response steps followed.

---

## Playbook 1 — Failed Login Attempts / Brute Force

**Trigger:** Multiple failed authentication attempts  
**Detection sources:** SentinelOne, Arctic Wolf, 
Microsoft 365 Defender, Azure AD sign-in logs  
**Initial severity:** SEV-C (review) — escalate to 
SEV-B if attack pattern confirmed

### Investigation Steps

1. Pull the alert from Zoho Service Desk or the 
   detection platform
2. Note the username, source IP, timestamp, and 
   number of failed attempts
3. Determine if the account is active and belongs 
   to a real user
4. Check whether the source IP is internal or external
5. Verify if any login succeeded after the failures
6. Review Azure AD sign-in logs for the past 7 days
7. Cross-reference source IP against VirusTotal 
   and AbuseIPDB
8. Check whether multiple accounts were targeted 
   from the same IP (password spray indicator)

### Response Actions

**If confirmed malicious:**
- Disable the affected account immediately
- Block the source IP at the email gateway or firewall
- Revoke active sessions in Azure AD
- Force password reset and MFA re-registration
- Notify the account owner's team lead
- Escalate to Tier-2 with full evidence package:
  log exports, IP details, timeline, account details

**If likely false positive:**
- Document findings in Zoho Service Desk
- Note the pattern for future alert tuning
- Close with false positive classification

### Escalation Criteria
Escalate immediately if:
- Login succeeded and suspicious post-login 
  activity is detected
- Multiple accounts targeted from the same source
- Administrative or privileged account involved
- Activity detected outside business hours from 
  an unrecognized location

---

## Playbook 2 — BitLocker Recovery Request

**Trigger:** User locked out of device, BitLocker 
recovery key required  
**Severity:** Low — administrative workflow  
**Detection source:** Zoho Service Desk helpdesk ticket

### Investigation Steps

1. Verify the request came through the official 
   Zoho Service Desk channel
2. Confirm the user's identity via HR records or 
   IT asset management
3. Verify the device asset tag belongs to the 
   requesting user
4. Check if the device is listed as active and 
   compliant in Absolute

### Response Actions

1. Retrieve the BitLocker recovery key from 
   Azure AD device management portal
2. Deliver the key via a secure, audited channel 
   only — never via email or chat
3. Log the recovery in Zoho Service Desk:
   - User name
   - Device ID and asset tag
   - Date and time
   - Approving analyst name
4. Follow up after 24 hours to confirm device 
   access was restored

**Security note:** BitLocker recovery requests are 
a social engineering vector. Always independently 
verify identity before issuing any recovery key.

---

## Playbook 3 — Email Quarantine Investigation

**Trigger:** Email flagged and quarantined by 
Microsoft 365 Defender  
**Detection source:** Microsoft 365 Security portal, 
Zoho Service Desk user report

### Investigation Steps

1. Access the quarantine queue in Microsoft 365 
   Security portal
2. Review the sender address and domain reputation
3. Analyze email headers — check for spoofing, 
   mismatched reply-to addresses
4. Review the email subject and body for phishing 
   indicators
5. Check if the sender is a known vendor or 
   internal contact
6. Verify whether other users received the 
   same email

### Response Actions

**If legitimate business email:**
- Release from quarantine
- Whitelist the sender if appropriate
- Document the false positive

**If confirmed malicious:**
- Keep in quarantine — do not release
- Block the sender domain at the email gateway
- Check if any users clicked links before 
  quarantine was applied
- Escalate if link clicks or attachments 
  were opened

### Escalation Criteria
Escalate to Tier-2 if:
- Attachment was opened by any user
- Link was clicked before quarantine
- Multiple users received the same phishing email
- Email impersonates internal leadership

---

## General Escalation Criteria

Escalate any incident to Tier-2 / Information 
Security Engineers when:

- Malware is detected or suspected on any endpoint
- Account compromise is confirmed or suspected
- Multiple users or systems are affected
- Critical business systems are impacted
- Administrative or privileged accounts are involved
- Lateral movement indicators are present
- The incident exceeds Tier-1 investigation capability

---

## Documentation Requirements

Every incident ticket in Zoho Service Desk must contain:

- Incident summary and alert source
- Complete timeline of events
- Source details (IP, user, device)
- Actions taken at each step
- Escalation decision and justification
- Final resolution and classification
- Lessons learned (for escalated incidents)

---

*Based on SOC incident response experience at NB 
Healthcare Technologies (NationsBenefits India), 
2022–2023.*
