# DLP Policy Operations Notes — Microsoft Purview

Practical notes based on DLP operations at NB Healthcare 
Technologies (NationsBenefits India), Nov 2022 – Aug 2023.

---

## Context

NationsBenefits operates in the healthcare benefits space, 
handling sensitive member data including SSNs, payment card 
information, and employee records across a 2,000+ user 
environment in India and the United States. DLP policy 
management was a core daily responsibility within SOC 
operations.

---

## Sensitive Data Types Protected

| Data Type | Sensitivity | Regulatory Context |
|---|---|---|
| Social Security Number (SSN) | Critical | HIPAA, PII regulations |
| Credit / Debit Card Numbers | Critical | PCI-DSS |
| Employee personal information | High | Internal policy, GDPR alignment |
| Financial records | High | Internal compliance |
| Internal business data | Medium | Confidentiality policy |

---

## Microsoft Purview — Core Components

### Policy Conditions
What triggers a DLP alert:
- Sensitive information type detected (e.g. SSN pattern match)
- Volume threshold exceeded (e.g. 5+ credit card numbers)
- External recipient detected on internal sensitive content
- Unauthorized cloud storage destination

### Policy Actions
What happens when a condition is met:
- **Block** — prevent the action completely
- **Block with override** — user must provide justification
- **Audit only** — log the activity without blocking
- **Policy tip** — notify the user in real time
- **Alert security team** — trigger SOC investigation queue

### Policy Scope
Where policies apply:
- Exchange Online (email)
- SharePoint and OneDrive
- Microsoft Teams messages
- Windows endpoints via Defender

---

## DLP Investigation Workflow

Used during daily SOC operations at NationsBenefits:

### Step 1 — Alert Review
Pull the alert from Microsoft Purview compliance portal:
- Which user triggered the alert?
- Which file or message was involved?
- Which policy and sensitive data type was matched?
- What was the intended destination (internal/external)?
- What time did the activity occur?

### Step 2 — Validation
Determine whether the activity was legitimate:
- Was this a known business workflow (e.g. HR payroll file)?
- Did the user have authorization for this transfer?
- Is this a pattern or a one-time occurrence?
- Cross-reference with the user's recent activity history

### Step 3 — Communication
If context is needed:
- Contact the user's team lead first — not the user directly
- Ask whether a business justification exists
- Document the response received

### Step 4 — Resolution

| Outcome | Action Required |
|---|---|
| False positive | Document, tune policy threshold, close ticket |
| Business justification approved | Document justification, close ticket, consider exception rule |
| Policy violation confirmed | Escalate to senior analyst, initiate formal process |
| Escalation required | Package evidence, escalate to Tier-2 with full context |

---

## Common False Positive Scenarios

**HR bulk file operations** — Payroll files containing employee 
data triggering PII rules during legitimate monthly processing.

**Finance team card references** — Internal finance workflows 
involving payment references blocked by PCI rules.

**Developer test data** — Non-production environments using 
dummy data in SSN format triggering real DLP alerts.

**Resolution approach:** Adjust confidence thresholds, add 
scoped exceptions for specific groups or locations, or 
implement allow-list rules after approval.

---

## Key Lessons from Operations

- DLP is not a set-and-forget system — policies require 
  regular review and tuning
- High false positive rates erode user trust and cause 
  alert fatigue in the SOC
- Every policy change must be tested in audit mode before 
  enforcement
- Business context is essential — security and operations 
  teams must communicate closely
- All DLP incidents must be documented regardless of outcome 
  for audit trail purposes

---

*Based on DLP operations experience at NB Healthcare 
Technologies (NationsBenefits India), 2022–2023.*
