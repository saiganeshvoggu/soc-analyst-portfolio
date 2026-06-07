# Threat Detection Notes — SOC Operations

Detection reference based on alert triage experience 
at NB Healthcare Technologies (NationsBenefits India).
Primary detection platforms: SentinelOne, Arctic Wolf, 
Microsoft 365 Defender, Zoho Service Desk.

Daily alert volume: 25–55 alerts across platforms.

---

## Detection Platforms Used

| Platform | Primary Use |
|---|---|
| SentinelOne | Endpoint threat detection, behavioral analysis, device investigations |
| Arctic Wolf | Managed detection, network monitoring, threat correlation |
| Microsoft 365 Defender | Email security, identity alerts, cloud app monitoring |
| Zoho Service Desk | Alert ticketing, investigation tracking, operational reporting |

---

## Common Alert Categories Encountered

### Failed Login Attempts
**Volume:** High — most frequent daily alert type  
**MITRE Technique:** T1110 — Brute Force  
**Detection sources:** Azure AD, SentinelOne, Arctic Wolf

Investigation approach:
1. Check number of attempts and time window
2. Identify if single account or multiple accounts 
   targeted (spray vs stuffing)
3. Verify source IP — internal or external
4. Check if any attempt succeeded
5. Review post-login activity if login succeeded

---

### Suspicious Authentication Activity
**MITRE Technique:** T1078 — Valid Accounts  
**Detection sources:** Azure AD sign-in logs, 
Microsoft 365 Defender

Indicators to check:
- Login from new country or region
- Login from new device not previously seen
- Login at unusual time for the user
- MFA bypass attempt

---

### Endpoint Security Events
**MITRE Techniques:** T1059 (Command Execution), 
T1055 (Process Injection), T1003 (Credential Dumping)  
**Detection source:** SentinelOne behavioral engine

Investigation approach:
1. Open alert in SentinelOne console
2. Review the full process tree — what spawned what?
3. Identify the affected endpoint and device owner
4. Check timeline — what happened before and after?
5. Determine if isolated to one endpoint or spreading
6. Make containment or escalation decision

---

### Phishing and Email Threats
**MITRE Technique:** T1566 — Phishing  
**Detection source:** Microsoft 365 Defender, 
user-reported via Zoho Service Desk

Investigation approach:
1. Review quarantined email headers
2. Check sender domain reputation
3. Analyze links and attachments
4. Determine if any user interacted with content
5. Block sender and escalate if interaction confirmed

---

### DLP Incidents
**MITRE Technique:** T1048 — Exfiltration Over 
Alternative Protocol  
**Detection source:** Microsoft Purview

Investigation approach:
1. Identify user, file, and destination
2. Determine if transfer was authorized
3. Contact team lead for business justification
4. Resolve as false positive, approved, or violation

---

### BitLocker and Device Compliance
**Detection source:** Absolute Software, Zoho Service Desk  

Monitoring activities:
- Device compliance status checks
- BitLocker encryption status validation
- Recovery key request processing
- Device location and activity tracking

---

## MITRE ATT&CK Quick Reference

| Technique ID | Name | Relevance to NB Environment |
|---|---|---|
| T1110 | Brute Force | Most common daily alert — login attempts |
| T1078 | Valid Accounts | Post-compromise credential use |
| T1566 | Phishing | Email gateway quarantine alerts |
| T1048 | Exfiltration | DLP policy triggers in Purview |
| T1059 | Command Execution | SentinelOne behavioral detections |
| T1098 | Account Manipulation | Azure AD unauthorized changes |

---

## Alert Triage Workflow

Standard process followed for every alert:

1. Open ticket in Zoho Service Desk
2. Identify alert source and classification
3. Pull relevant logs and context
4. Apply the appropriate investigation playbook
5. Determine: false positive, true positive, or escalation
6. Document findings in the ticket
7. Close or escalate with full evidence package

---

*Based on threat detection operations at NB Healthcare 
Technologies (NationsBenefits India), 2022–2023.*
