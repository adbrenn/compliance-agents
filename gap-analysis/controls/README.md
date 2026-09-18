# Controls (bring your own)

This folder is where **you** place control-catalog markdown files for the gap analysis agents.

## Why this folder is empty

Copyrighted control text from standards such as **ISO/IEC 27701**, **ISO/IEC 42001**, and **NIST SP 800-53** is **not** included in this repository and must **not** be committed here.

Obtain controls under a license that permits your use (purchased standard, organizational license, or a public-domain / openly licensed catalog), then add them as markdown files in this directory.

## Expected format

Each control should be a level-4 heading with an ID and name, followed by the requirement text:

```markdown
#### Control-ID — Name

Normative requirement text for this control…
```

Example shape (illustrative IDs only — not real standard text):

```markdown
#### AC-1 — Access Control Policy and Procedures

The organization develops, documents, and disseminates…
```

The `compliance-specialist` agent parses headings in this form and assesses each control in document order.

## Naming convention

Prefer:

```
controls/<framework>_controls.md
```

Examples of filenames (content is yours to supply):

- `controls/iso_27701_controls.md`
- `controls/iso_42001_controls.md`
- `controls/nist_800_53_low_controls.md`

Again: only add content you are licensed to use. **Do not commit ISO 27701 / ISO 42001 / NIST 800-53 copyrighted control text to this repo.**

## Pointing the specialist at your file

When invoking the agent, pass the path to your controls file, for example:

```
Use the compliance-specialist agent to assess controls/<framework>_controls.md.
Authorized evidence sources: local evidence/ folder only.
```

See `../gap-agents/README.md` for the full workflow.
