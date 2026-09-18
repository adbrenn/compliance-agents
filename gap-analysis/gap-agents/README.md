# Compliance Gap Analysis Agents

Two Claude Code agents that run a framework gap analysis in two stages:

| Agent | Role | Input | Output |
|---|---|---|---|
| `compliance-specialist` | Compliance assessor — identifies evidence needed per control, reviews authorized evidence, issues determinations | Controls reference file (markdown) | `findings/<framework>_findings.md` |
| `compliance-report-writer` | Compliance project manager — organizes findings into a stakeholder-ready deliverable | Findings file | `reports/<framework>_gap_analysis.csv` or `.md` |

The specialist never guesses: a control without adequate evidence is marked **Insufficient Evidence** with a list of what to supply — it is never assumed to be in place or absent. The report writer never changes a determination; it only organizes.

## Installation in a new repo

1. Copy `compliance-specialist.md` and `compliance-report-writer.md` into the repo's `.claude/agents/` directory.
2. Copy `organization-profile.md` into the repo root (or keep it beside `evidence/` / `controls/` as in this layout) and fill it in (see Prerequisites).
3. Create an `evidence/` folder for artifacts and a `controls/` folder for your licensed/public-domain control markdown (see `../controls/README.md`).
4. Restart your Claude Code session so the agents load, then confirm they appear under `/agents`.

## Prerequisites — do these before the first run

**1. Fill in `organization-profile.md`.** The specialist reads it before every assessment to judge applicability (PII controller vs. processor, AI provider vs. user, jurisdictions, scope). Unfilled sections cause controls to come back "Undetermined — organization profile incomplete" instead of assessed.

**2. Supply your controls markdown.** Place licensed or public-domain control catalogs under `controls/` (e.g. `controls/<framework>_controls.md`). Copyrighted ISO/NIST control text is not included in this repository — see `../controls/README.md`.

**3. Add evidence to `evidence/`.** Policies, procedures, records, contracts, exports, screenshots. Descriptive filenames with dates/versions produce better determinations (`data-retention-policy-v3-2026-01.pdf`, not `policy_final2.pdf`). Optionally add an `evidence/evidence-map.md` table mapping control IDs to file locations — the agent checks it first and assessments get faster and more accurate.

## Stage 1 — Run the compliance specialist

Every prompt must state **which controls file** to assess and **which evidence sources are authorized**. The agent will not touch a source you don't name; if you name none, it uses only the local `evidence/` folder.

**Basic run, local evidence only:**

```
Use the compliance-specialist agent to assess controls/<framework>_controls.md.
Authorized evidence sources: local evidence/ folder only.
```

**Authorizing connected tools** (only name tools your organization permits agents to access):

```
Use the compliance-specialist agent to assess controls/<framework>_controls.md.
Authorized evidence sources: local evidence/ folder, the "Compliance" space
in Confluence, and the Policies folder in Google Drive. Do not search Slack or Jira.
```

**Scoped run** (useful for large frameworks, or re-assessing one area after adding evidence):

```
Use the compliance-specialist agent to assess only Annex A (sections A.7.2 through A.7.5)
of controls/<framework>_controls.md. Authorized evidence sources: local evidence/ folder only.
```

**Re-run after supplying requested evidence:**

```
I've added the requested evidence to evidence/. Use the compliance-specialist agent to
re-assess the controls marked "Insufficient Evidence" in findings/<framework>_findings.md
and update that findings file. Authorized evidence sources: local evidence/ folder only.
```

Output: `findings/<framework>_findings.md` — per-control determinations with cited evidence, plus a consolidated **Evidence Request List** grouped by owner. That list is your ask-list for stakeholders.

## Stage 2 — Run the report writer

State the **findings file** and the **format you want** (`csv` or `markdown`). If you don't specify a format, you get markdown.

**CSV register** (flat file that loads cleanly into Excel/Google Sheets):

```
Use the compliance-report-writer agent to build a CSV gap analysis report
from findings/<framework>_findings.md.
```

**Markdown report** (executive summary, gap register, evidence requests grouped by stakeholder, detailed findings):

```
Use the compliance-report-writer agent to build a markdown gap analysis report
from findings/<framework>_findings.md.
```

**Custom output location:**

```
Use the compliance-report-writer agent to build a CSV report from
findings/<framework>_findings.md and save it to reports/2026-Q3-privacy-gap-analysis.csv.
```

Output: `reports/<framework>_gap_analysis.csv` or `.md` (or your custom path).

## The expected loop

First runs surface many "Insufficient Evidence" determinations — that is by design, not failure. The cycle is:

1. Assess → get findings with an evidence request list.
2. Circulate the evidence requests to the owners named in the report (Engineering, HR, Privacy/Legal, etc.).
3. Drop the returned artifacts into `evidence/` (update `evidence-map.md` if you use one).
4. Re-run the specialist on the insufficient controls.
5. Regenerate the report.

Repeat until the remaining gaps are true gaps, not missing paperwork.

## Tips for effective prompts

- **One framework per run.** Run each framework as a separate assessment — mixing them muddies the findings file and the report.
- **Always state evidence-source authorization explicitly.** This is the control point for tool-access restrictions; the agent treats unnamed sources as off-limits. A standing default can be recorded in section 9 of `organization-profile.md`, but per-run instructions win.
- **Say what you want the report to emphasize** if you have an audience in mind, e.g. "build a markdown report from findings/... — the primary audience is the engineering leadership team," and the report writer will keep the stakeholder sections in plain language for that group.
- **Don't ask the report writer to reassess.** If a determination looks wrong, add evidence and re-run the specialist — the report writer is deliberately barred from changing judgements.
- **Check the Data Quality Notes** section at the end of markdown reports; it flags controls with missing fields or an incomplete organization profile.
