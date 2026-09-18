# Evidence Folder

Drop evidence artifacts for the gap analysis here: policies, procedures, standards, contracts/DPAs, records, exports, screenshots, training materials, tickets, audit reports, etc. The compliance-specialist agent reads everything in this folder (recursively) when "local evidence" is an authorized source.

Tips for better assessments:

- **Prefer text formats** (md, txt, pdf, docx exports to pdf/text, csv) — the agent reads these directly. Screenshots work but carry less context.
- **Name files descriptively**, ideally with a date or version: `data-retention-policy-v3-2026-01.pdf` beats `policy_final2.pdf`. Evidence currency affects determinations.
- **Subfolders are fine** — organizing by domain (e.g., `privacy/`, `ai-governance/`, `hr/`, `vendor/`) or by control ID both work.
- **Optional but recommended:** create an `evidence-map.md` in this folder mapping control IDs to evidence locations. The agent checks it first before searching broadly, which makes assessments faster and more accurate. Example:

```markdown
| Control ID | Evidence | Location |
|---|---|---|
| A.7.2.1 | Records of Processing Activities | privacy/ropa-export-2026-06.csv |
| A.7.2.6 | Standard DPA template + signed examples | vendor/dpa-template-v2.pdf |
| 5.2 | AI Policy | ai-governance/ai-policy-v1-2026-03.md |
```
