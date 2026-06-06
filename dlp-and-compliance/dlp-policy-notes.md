# DLP Policy Notes — Microsoft Purview

Reference notes on Data Loss Prevention policy 
management based on hands-on experience with 
Microsoft Purview at NationsBenefits India.

---

## What is DLP?

Data Loss Prevention (DLP) policies detect and 
prevent the unauthorized sharing, transfer, or 
exposure of sensitive information.

In Microsoft Purview, DLP policies can monitor 
and protect data across:
- Microsoft 365 services (Exchange, SharePoint, Teams)
- Endpoints (Windows devices)
- Cloud apps connected via Defender

---

## Sensitive Information Types Worked With

| Data Type | Description | Regulatory Context |
|---|---|---|
| SSN | US Social Security Numbers | HIPAA, PII regulations |
| UAN | Universal Account Number (India) | Indian labour law |
| Payment Card Data | Credit/debit card numbers | PCI-DSS |

---

## DLP Policy Components

### 1. Conditions
What triggers the policy — e.g., email containing 
10+ credit card numbers being sent externally.

### 2. Actions
What happens when conditions are met:
- **Block** — prevent the action entirely
- **Block with override** — user can justify and proceed
- **Audit only** — log without blocking
- **Notify user** — show policy tip

### 3. Scope
Where the policy applies:
- Exchange Online (email)
- SharePoint / OneDrive
- Teams messages
- Windows endpoints

---

## Policy Review Process (NationsBenefits)

1. Review existing policy rules against current 
   data protection requirements
2. Identify gaps or overly broad rules causing 
   false positives
3. Update conditions and thresholds as needed
4. Test policy in audit mode before enforcing
5. Document changes with justification
6. Monitor policy match reports post-update

---

## Common False Positive Scenarios

- Test data containing dummy SSNs triggering 
  real alerts
- Internal finance teams sharing card data 
  through approved channels being blocked
- Bulk HR files with UAN numbers flagged 
  during legitimate transfers

**Resolution approach:** Adjust confidence thresholds, 
add trusted location exceptions, or create allow-list 
rules for specific user groups.

---

*Notes based on DLP policy review and maintenance 
experience at NationsBenefits India (2022–2023) 
using Microsoft Purview.*
