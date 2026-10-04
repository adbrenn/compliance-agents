# tprm — Third-party risk assessment from a provider's SOC report

This folder helps you run a third-party risk assessment (TPRM) of a service provider using the provider's **SOC 2 report** (SOC 1 and SOC 3 are also supported). An AI agent reads the report, fills in the **SSAE Subservice Organization Internal Control Evaluation Checklist**, maps the provider's Complementary User Entity Controls (CUECs) to your own controls, and saves the finished review as a new Markdown file.

## What's in this folder

| File | What it is |
|---|---|
| [`soc2-subservice-org-review.md`](soc2-subservice-org-review.md) | The agent skill. It holds the step-by-step instructions the agent follows, the ground rules (cite the report, never invent controls), and the output rules. |
| [`ssae-subservice-org-checklist-template.md`](ssae-subservice-org-checklist-template.md) | The blank checklist the review fills in. Keep this file blank and never overwrite it. |

The skill already embeds a copy of the checklist, so the template file is optional. If you attach it, the agent uses it exactly as written, which is useful if you customize the checklist's wording or layout.

## What you need before you start

- **The provider's SOC report** (PDF or text). SOC 1, SOC 2 or SOC 3, Type I or Type II. Include the bridge letter if the provider issued one. The agent will stop and ask if no report is attached; it will not fill anything in from memory.
- **Your reviewer name**, used for the sign-off.
- **The report type you require** from this provider, for example SOC 2 Type II covering Security and Availability. The agent suggests one based on the services you use, and you decide.
- **A list of your own controls** (optional but recommended). A spreadsheet, CSV, Markdown, PDF or Word file with control IDs and descriptions. Without it, the agent asks you about each control one by one.

## How to set it up

1. Load `soc2-subservice-org-review.md` as a skill in your AI agent tool. In Claude Code, for example, copy it to `.claude/skills/soc2-subservice-org-review/SKILL.md`. Other tools that support skills or custom instructions work too, or you can paste the file's contents into the conversation.
2. Keep `ssae-subservice-org-checklist-template.md` in the same working folder so you can attach it.

## How to run an assessment

1. **Start the review.** Attach the SOC report, plus the template and your control list if you have them, and ask something like:
   > Review the attached SOC 2 report for *Acme Hosting* using the soc2-subservice-org-review skill. My name is Jane Doe. Here is our control list.
2. **Confirm the intake.** The agent asks, in one message, for your name, the report type you require and whether a control list exists.
3. **Check the extracted facts.** The agent pulls the provider's name, report type, auditor opinion, review period, in-scope services and every testing exception from the report, with section and page references. Anything the report doesn't say is marked "Not stated in report".
4. **Confirm the CUEC list.** The agent extracts every CUEC word for word and proposes whether each applies to you, with reasoning. Correct any calls you disagree with before it continues.
5. **Review the control mapping.** The agent maps your controls to each applicable CUEC and rates the match **Strong**, **Partial** or **None**. It only uses controls from your list or ones you give it. For gaps, provide a remediation plan (owner and target date) or it records "Remediation plan pending — reviewer to provide".
6. **Sign off on the conclusion.** The agent proposes one of the following, and you can override it:
   - **Reliance supported**
   - **Reliance supported with follow-up**
   - **Reliance not supported**
7. **Collect the output.** The agent saves a new file named `SSAE Subservice Organization Review - <Provider Name> - <Period End YYYY-MM-DD>.md`, checks it against a final checklist, and reports the conclusion, the number of gaps and any open items.

## What the completed review contains

- Provider, report type, services, auditor opinion, review period and exceptions
- The six standard review procedures, each with the finding and a page reference
- A CUEC table: each requirement, whether it applies to you, your control that meets it and its ID, and a remediation plan for any gap
- Review results, a conclusion and the sign-off name and date

## Tips and limits

- **You make the call.** The agent proposes applicability, mappings and the conclusion, but a person must confirm them. It is not a substitute for professional judgment.
- **Check the citations.** Spot-check a few page references against the report, especially the opinion, the period and the exceptions.
- **Watch for follow-ups.** Pay attention to carved-out subservice organizations you depend on, a report period that ended more than three months ago, and services you use that fall outside the report's scope.
- **One provider per review.** Run the skill separately for each provider.

## Keep confidential material out of this repository

SOC reports are usually restricted-use documents shared under NDA, and completed reviews contain details about your controls. **Don't commit SOC reports or completed reviews to this public repo.** Run assessments in a private location.
