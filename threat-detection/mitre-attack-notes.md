# MITRE ATT&CK — SOC Detection Notes

Reference notes on key MITRE ATT&CK tactics relevant 
to Tier-1 SOC alert triage and incident response.

---  

## TA0001 — Initial Access

**What it is:** Attacker attempts to get into the network.

**Common techniques:**
- T1566 Phishing — malicious email attachments or links
- T1190 Exploit Public-Facing Application
- T1078 Valid Accounts — using stolen credentials

**What to look for in alerts:**
- Unusual login locations or times
- Email gateway alerts for suspicious attachments
- Multiple failed logins followed by a success

---

## TA0003 — Persistence

**What it is:** Attacker maintains their foothold after 
initial compromise.

**Common techniques:**
- T1053 Scheduled Tasks — malicious tasks created
- T1547 Registry Run Keys — auto-start on boot
- T1136 Create Account — new unauthorized accounts

**What to look for:**
- New local accounts created outside IT workflows
- Unusual scheduled tasks in Windows Event Logs
- Registry modifications on endpoints

---

## TA0008 — Lateral Movement

**What it is:** Attacker moves through the network to 
reach target systems.

**Common techniques:**
- T1021 Remote Services — RDP, SMB abuse
- T1550 Pass the Hash — credential reuse
- T1563 Remote Service Session Hijacking

**What to look for:**
- Unusual RDP connections between workstations
- Authentication attempts using same credentials 
  across multiple systems
- SentinelOne alerts for credential dumping tools

---

## TA0040 — Impact

**What it is:** Attacker disrupts, destroys, or 
manipulates data/systems.

**Common techniques:**
- T1486 Data Encrypted for Impact (ransomware)
- T1490 Inhibit System Recovery — deletes backups
- T1485 Data Destruction

**What to look for:**
- Mass file rename/encryption activity on endpoints
- Deletion of Volume Shadow Copies
- Unusual process spawning from Office applications

---

*These notes are based on MITRE ATT&CK v14 and 
practical SOC experience.*
