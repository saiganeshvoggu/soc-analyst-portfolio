# MITRE ATT&CK Detection Notes

Reference notes for SOC Tier-1 analysts covering key 
ATT&CK tactics, detection sources, and investigation 
steps. Based on alert patterns encountered using 
SentinelOne and Microsoft 365 Defender.

---

## Why MITRE ATT&CK Matters in SOC Work

MITRE ATT&CK gives analysts a common language to describe 
attacker behaviour. When you receive a SentinelOne alert, 
mapping it to an ATT&CK technique tells you:
- What the attacker is trying to do
- What they likely did before this step
- What they will likely do next

This context is what separates reactive alert-closers 
from analysts who understand attacker intent.

---

## TA0001 — Initial Access

The attacker's first attempt to get inside the environment.

**Most common techniques:**

**T1566 — Phishing**  
Malicious email with attachment or link. Most common 
initial access vector in enterprise environments.  
Detection: Email gateway alerts, user-reported phishing, 
Microsoft Defender for Office 365 alerts

**T1078 — Valid Accounts**  
Using stolen or guessed credentials to log in legitimately.  
Detection: Azure AD unusual sign-in alerts, login from 
new location/device, failed logins followed by success

**T1190 — Exploit Public-Facing Application**  
Attacking internet-exposed services.  
Detection: WAF alerts, IDS signatures, unusual traffic 
patterns on perimeter systems

---

## TA0003 — Persistence

Attacker ensures they maintain access even after 
password resets or reboots.

**T1098 — Account Manipulation**  
Adding attacker-controlled credentials to an existing 
account or creating new accounts.  
Detection: Azure AD new account creation alerts, 
unexpected admin privilege grants, SentinelOne 
process activity around net user commands

**T1053 — Scheduled Task / Job**  
Creating scheduled tasks to run malicious code 
automatically.  
Detection: Windows Event ID 4698 (task created), 
SentinelOne behavioral detection on unusual 
schtasks.exe activity

---

## TA0006 — Credential Access

Attacker attempts to steal credentials to move further.

**T1110 — Brute Force**  
Repeated login attempts against one or many accounts.  
Detection: Multiple failed logins in Azure AD, 
SentinelOne network detection, Microsoft 365 
identity protection alerts  
Investigation: Check for password spray pattern 
(many accounts, few attempts each) vs credential 
stuffing (one account, many attempts)

**T1003 — OS Credential Dumping**  
Tools like Mimikatz used to extract credentials from 
memory.  
Detection: SentinelOne behavioral engine (high 
confidence), LSASS access alerts, unusual 
process injection activity

---

## TA0008 — Lateral Movement

Attacker moves from the initial compromised system 
to reach higher-value targets.

**T1021 — Remote Services**  
Using RDP, SMB, or WinRM to access other systems.  
Detection: SentinelOne network activity, unusual 
RDP connections between workstations (workstation 
to workstation RDP is almost always suspicious), 
Azure AD sign-ins from unexpected devices

**T1550 — Use Alternate Authentication Material**  
Pass-the-Hash or Pass-the-Ticket attacks.  
Detection: SentinelOne behavioral, event log 
anomalies, unexpected NTLM authentication patterns

---

## SentinelOne Alert Investigation Workflow

Used during alert triage at NationsBenefits:

1. Open alert in SentinelOne console
2. Read the full alert name and classification 
   (Malicious / Suspicious / Informational)
3. Check the process tree — what spawned what?
4. Identify the affected endpoint and owner
5. Check the timeline — what happened before 
   and after the alert?
6. Map the activity to a MITRE ATT&CK technique
7. Determine scope — is this isolated to one 
   endpoint or is there lateral movement?
8. Make escalation decision based on severity 
   and scope

---

*Notes based on threat detection experience using 
SentinelOne and Microsoft 365 Defender at 
NationsBenefits India (2022–2023).*
