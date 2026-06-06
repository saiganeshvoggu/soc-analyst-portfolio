# DLP Policy Notes — Microsoft Purview

Practical notes based on DLP policy review and maintenance 
at NationsBenefits India (Nov 2022 – Aug 2023).

---

## What is DLP and Why It Matters

Data Loss Prevention policies detect and prevent unauthorised 
sharing or exposure of sensitive data. In a regulated 
environment like healthcare benefits administration, DLP 
is critical because the data includes SSNs, payment card 
numbers, and government IDs — all of which carry legal 
liability if exposed.

---

## Sensitive Data Types Managed

| Data Type | Sensitivity | Regulatory Context |
|---|---|---|
| Social Security Number (SSN) | Critical | HIPAA, PII regulations |
| Universal Account Number (UAN) | High | Indian labour regulations |
| Credit / Debit Card Numbers | Critical | PCI-DSS |
| Financial account information | High | Internal compliance policy |

---

## Microsoft Purview — Key Concepts

### Policy Components

**Conditions** — what triggers the policy:
- Specific sensitive info type detected (e.g. credit card number)
- Volume threshold (e.g. 10+ instances in one message)
- Recipient type (internal vs external)

**Actions** — what happens when triggered:
- Block external sharing entirely
- Block with override (user must justify)
- Audit only — log without blocking
- Send policy tip to the user
- Alert the security team

**Scope** — where the policy applies:
- Exchange Online (email)
- SharePoint and OneDrive
- Microsoft Teams messages
- Windows endpoints (via Defender)

---

## Policy Review Process

Steps followed during policy reviews at NationsBenefits:

1. Pull recent DLP match reports from Microsoft Purview 
   compliance portal
2. Identify high false-positive rules causing unnecessary 
   business disruption
3. Review threshold settings — adjust confidence levels 
   or instance counts if needed
4. Check scope — ensure policies cover all required 
   workloads (Exchange, SharePoint, endpoints)
5. Test any changes in audit mode before enforcing
6. Document all changes with business justification
7. Monitor match reports for 2 weeks post-change to 
   confirm expected behaviour

---

## Common False Positive Scenarios Encountered

**HR bulk file transfers** — large employee data files 
containing UAN numbers flagged during legitimate payroll 
processing. Resolution: created scoped exception for 
the HR shared mailbox.

**Test environments** — developers using dummy SSN-format 
data in non-production systems triggering real DLP alerts. 
Resolution: excluded specific SharePoint test sites from 
the policy scope.

**Finance team card processing** — internal finance 
workflows involving payment card references blocked by 
overly broad PCI rules. Resolution: adjusted instance 
count threshold and added trusted group exception.

---

## Lessons Learned

- DLP policy management is iterative — set once is never 
  the right approach
- False positive reduction requires close collaboration 
  between security and business teams
- Audit mode before enforcement prevents business disruption
- Documentation of every policy change is essential for 
  audit trails

---

*Based on hands-on experience with Microsoft Purview at 
NationsBenefits India (2022–2023).*
