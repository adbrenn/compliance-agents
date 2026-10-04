# compliance-agents

A collection of AI agents and skills for compliance work: a two-stage framework gap analysis toolkit and a third-party risk assessment skill based on SOC reports.

Bring your own licensed (or public-domain) control catalogs. This repository ships the agent prompts, workflow docs, and folder layout — **not** copyrighted ISO or NIST control text.

## What's in this repo

- [`gap-analysis/`](gap-analysis/) — the two-stage framework gap analysis toolkit described below.
- [`tprm/`](tprm/) — a skill and checklist template for third-party risk assessments based on a provider's SOC 2 report. See [`tprm/README.md`](tprm/README.md).

## Gap analysis: what this is

Two Claude Code custom agents that run a framework gap analysis in stages:

| Stage | Agent | Role | Input | Output |
|---|---|---|---|---|
| 1 | `compliance-specialist` | Assessor — identifies evidence needed per control, reviews authorized evidence, issues determinations | Your controls markdown file | `gap-analysis/findings/<framework>_findings.md` |
| 2 | `compliance-report-writer` | Project manager — organizes findings into a stakeholder-ready deliverable | Findings file | `gap-analysis/reports/<framework>_gap_analysis.csv` or `.md` |

The specialist never guesses: a control without adequate evidence is marked **Insufficient Evidence** with a list of what to supply. The report writer never changes a determination; it only organizes.

## Layout

```
tprm/                       # SOC 2 third-party risk review skill + checklist template
gap-analysis/
  organization-profile.md   # Fill in before first run (applicability context)
  controls/                 # YOU supply licensed/public-domain control markdown here
  evidence/                 # Drop policies, records, exports, etc.
  findings/                 # Specialist writes structured findings here
  reports/                  # Report writer outputs CSV or markdown here
  gap-agents/               # Agent definitions + workflow docs
```

## Important: control catalogs are not included

ISO/IEC 27701, ISO/IEC 42001, NIST SP 800-53, and similar standards are copyrighted. **Do not** commit copyrighted control text to this (or any public) repository. Place your own licensed or public-domain control markdown under `gap-analysis/controls/` — see that folder's README for the expected format.

## Quick start

1. Fill in `gap-analysis/organization-profile.md`.
2. Add your controls file(s) under `gap-analysis/controls/` (e.g. `controls/<framework>_controls.md`).
3. Drop evidence into `gap-analysis/evidence/`.
4. Copy the agent markdown files from `gap-analysis/gap-agents/` into your Claude Code `.claude/agents/` directory (or work from this tree if your setup loads agents from here).
5. Follow the workflow in [`gap-analysis/gap-agents/README.md`](gap-analysis/gap-agents/README.md).

## Workflow (summary)

1. **Assess** — invoke `compliance-specialist` with your controls file path and authorized evidence sources → findings.
2. **Report** — invoke `compliance-report-writer` with the findings path and format (`csv` or `markdown`) → report.
3. Circulate evidence requests, add artifacts, re-assess insufficient controls, regenerate the report.

Details, example prompts, and tips: [`gap-analysis/gap-agents/README.md`](gap-analysis/gap-agents/README.md).

## License / usage notes

Agent prompts and tooling layout in this repo are provided as a portfolio/example toolkit. You are responsible for obtaining and using control catalogs under a license that permits your use. Do not contribute copyrighted ISO/NIST control text via pull request.
