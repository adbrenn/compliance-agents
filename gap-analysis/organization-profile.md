# Organization Profile — Gap Analysis Context

The compliance-specialist agent reads this file before every assessment. It drives applicability judgements (e.g., whether ISO 27701 Annex A controller controls or Annex B processor controls apply, and which ISO 42001 requirements are in scope for your AI roles). Replace every `[FILL IN]` — unanswered sections cause controls to be marked "Undetermined — organization profile incomplete" rather than assessed.

## 1. Organization Overview

- **Organization name:** [FILL IN]
- **Industry / sector:** [FILL IN]
- **Approximate size (headcount):** [FILL IN]
- **Brief description of what the organization does:** [FILL IN]

## 2. Products and Services in Scope

List the products, services, and business units covered by this gap analysis. Anything not listed is treated as out of scope.

- [FILL IN]

## 3. Existing Certifications and Frameworks

- **ISO/IEC 27001 certified?** [Yes / No / In progress — the ISO 27701 controls file assumes clauses 5–6 are inherited from an existing 27001 ISMS]
- **Other certifications or attestations (SOC 2, HIPAA, etc.):** [FILL IN]

## 4. Privacy Roles (drives ISO 27701 Annex A vs. Annex B applicability)

- **Does the organization act as a PII controller?** (decides why and how personal data is processed — e.g., for its own employees, marketing contacts, direct customers) [Yes / No — if yes, briefly describe for which data]
- **Does the organization act as a PII processor?** (processes personal data on behalf of customers under their instructions) [Yes / No — if yes, briefly describe]
- **Categories of PII handled:** [e.g., employee HR data, customer contact data, end-user content, health data]
- **Categories of PII principals:** [e.g., employees, job applicants, customers' end users]
- **Does the organization use third-party PII processors / subprocessors?** [Yes / No — if yes, name the main ones]
- **Any joint controller arrangements?** [Yes / No / Unknown]

## 5. AI Roles (drives ISO 42001 applicability — see clause 4.1)

Check every role that applies and describe the relevant systems:

- **AI provider** (offers AI products/services to others): [Yes / No — details]
- **AI producer/developer** (designs, trains, or builds AI systems or models): [Yes / No — details]
- **AI user/customer** (uses AI systems, including third-party tools, in operations): [Yes / No — details]
- **AI partner** (integrates AI systems or supplies data for others' AI): [Yes / No — details]
- **AI systems in scope** (internal and product-facing): [FILL IN — name and one-line purpose each]
- **Third-party AI services used** (e.g., model APIs, embedded AI features): [FILL IN]

## 6. Jurisdictions and Data Transfers

- **Countries where the organization operates:** [FILL IN]
- **Countries where PII is stored or processed:** [FILL IN]
- **Cross-border PII transfers?** [Yes / No — if yes, between which jurisdictions]
- **Key applicable regulations:** [e.g., GDPR, CCPA, EU AI Act — as understood by the organization]

## 7. Management System Scope Statement

One paragraph describing the intended boundaries of the PIMS (privacy) and/or AIMS (AI) — which entities, locations, systems, and processes are inside the boundary.

[FILL IN]

## 8. Stakeholders and Control Owners

Used to populate "Suggested Owner" in findings. Map functions to teams/roles as they exist in your organization.

| Function | Team / role in this organization |
|---|---|
| Privacy / Legal | [FILL IN] |
| Information Security | [FILL IN] |
| Engineering | [FILL IN] |
| IT / Infrastructure | [FILL IN] |
| Human Resources | [FILL IN] |
| Procurement / Vendor Management | [FILL IN] |
| AI / ML Governance | [FILL IN] |

## 9. Standing Evidence-Source Authorizations (optional)

The specialist agent only searches sources authorized in its invocation. If you want a standing default, record it here (e.g., "local evidence/ folder plus the Compliance space in Confluence; never Slack"). Per-run instructions override this section.

[FILL IN or leave blank]

## 10. Assumptions and Notes

Anything the assessor should know that doesn't fit above (recent reorgs, systems being decommissioned, known gaps already accepted by leadership, etc.).

[FILL IN or leave blank]
