# Compliance Gap Analysis Project

This project runs framework gap analyses using two custom agents. Supply your own licensed or public-domain control catalogs under `gap-analysis/controls/` — copyrighted ISO/NIST control text is not included.

## Layout

- `controls/` — your controls reference markdown files (inputs); see `controls/README.md` for format. Use paths like `controls/<framework>_controls.md`
- `organization-profile.md` — org context for applicability judgements; must be filled in before assessments
- `evidence/` — evidence artifacts supplied by the user (see its README)
- `findings/` — structured findings written by the compliance-specialist agent
- `reports/` — final CSV or markdown reports written by the compliance-report-writer agent

## Workflow

1. **Assess** — launch the `compliance-specialist` agent with: your controls markdown file path (e.g. `controls/<framework>_controls.md`), and which evidence sources are authorized for the run (local `evidence/` folder and/or named connected tools). Evidence-source authorization is per-run and user-controlled — never assume a connected tool is allowed; section 9 of organization-profile.md may record a standing default. Output: `findings/<framework>_findings.md`.
2. **Report** — launch the `compliance-report-writer` agent with: the findings file path and the output format the user asked for (`csv` or `markdown`). Output: `reports/<framework>_gap_analysis.<csv|md>`.

Run frameworks as separate assessments. The specialist never guesses: controls without adequate evidence come back "Insufficient Evidence" with a list of what to supply, and re-running after adding evidence to `evidence/` is the expected loop.
