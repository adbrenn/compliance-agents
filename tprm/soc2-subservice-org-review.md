---
name: soc2-subservice-org-review
description: Complete the SSAE Subservice Organization Internal Control Evaluation Checklist from a vendor's SOC 1/SOC 2 report - extract opinion, scope, period, and exceptions, answer the review procedures, populate the CUEC table, map the reviewer's company controls to each CUEC (from an attached control list or by prompting), and write the completed review as a new Markdown file. Use when asked to review a vendor/provider/subservice SOC report, complete a subservice organization review, or map CUECs.
---

# SOC Subservice Organization Review

Completes the **SSAE – Subservice Organization Internal Control Evaluation Checklist** for one service provider, using the provider's SOC report as the source of truth, and saves the finished review as a new Markdown file.

## Inputs

| Input | Required | Notes |
|---|---|---|
| Provider SOC report (PDF or text) | Yes | SOC 1 / SOC 2 / SOC 3, Type I or II. Bridge letter too, if one exists. |
| Checklist template (.md) | No | If attached, use it exactly. Otherwise use the embedded template at the bottom of this skill. |
| Company control list (xlsx, csv, md, pdf, docx) | No | Used to map CUECs to company controls. If missing, prompt the reviewer (Step 5). |
| Reviewer name | Yes | Ask if not given. |

If the SOC report is not attached, stop and ask for it. Do not complete any field from memory or general knowledge of the vendor.

## Ground rules

- **Every answer must be traceable to the report.** Cite the section and page, e.g. "(Section I, p. 3)". If something isn't in the report, write "Not stated in report" — never guess.
- **Never invent company controls or control IDs.** Only use controls from the attached control list or ones the reviewer provides. Anything unmapped is marked as a gap pending reviewer input.
- Quote CUECs verbatim from the report. Don't paraphrase or merge them.
- Proposed applicability (Y/N) calls are suggestions; the reviewer confirms them.
- Keep the template's headings, order, and wording. Replace every `[Service Provider]` placeholder with the provider's name. Delete the heading "Do Not Use This Page for Subservice Organization Evaluations. Make a Copy and Delete This Heading." and change the title to drop "[Template]".

## Workflow

### Step 1 — Intake

1. Read the full SOC report (use the pdf skill for PDFs; read every page, including Section IV test results and any appendices).
2. Read the template if attached, and the control list if attached.
3. Confirm with the reviewer, in one message:
   - Reviewer name (for "Review Completed By").
   - **Required report type** for this provider — which boxes to tick under "Required Report Type" (SOC 1 Type II, SOC 2 Type II + which Trust Services Criteria, SOC 3). Offer a suggestion based on the services the provider performs (e.g. hosting/infrastructure → SOC 2 Type II Security + Availability + Confidentiality; payroll/billing/financial processing → SOC 1 Type II), but let the reviewer decide.
   - Whether a company control list exists (if not already attached).

### Step 2 — Extract report facts

Pull the following and keep the page references:

| Template field | Where to look | What to write |
|---|---|---|
| Service Provider's Name | Cover, Section I | Legal entity name as stated in the report. |
| Type of SSAE Provided | Cover, Section I | e.g. "SOC 2 Type II — Security, Availability, Confidentiality". Note the attestation standard cited (e.g. AT-C 205/320, SSAE 18/21). |
| Required Report Type | Reviewer (Step 1) | Tick `[x]` for the required items only. |
| Services Provided by [Provider] | Section III system description | 2–4 sentence summary of the in-scope system/services, plus the services **we** use from them. Note any services we use that are **not** in scope. |
| Report Opinion | Section I (auditor's opinion) | Unqualified / Qualified / Adverse / Disclaimer, auditor firm name, opinion date. If qualified, summarize the basis for qualification. |
| Time Period Covered | Section I | Type II: start–end dates. Type I: "as of" date. Flag if the period ended more than 3 months before today and note whether a bridge letter was provided. |
| Exceptions from Testing | Section IV | Table or list of every exception: control ID, control description (short), exception noted, management response, and your assessment of impact to us. If none: "No exceptions noted (Section IV, p. X)." |

Also capture (used in Review Procedures / Results):
- **Subservice organizations** and whether each is carved out or inclusive, plus any Complementary Subservice Organization Controls (CSOCs). Carved-out subservice orgs we depend on may need their own review — flag them.
- Whether the report's scope (system, locations, TSC) covers the services we actually use.
- Nature of testing (inquiry, observation, inspection, reperformance) and sample sizes where given.

### Step 3 — Review Procedures

Keep the six template bullets verbatim. Under each, add an indented sub-bullet with the finding and page reference, e.g.:

```
- Reviewing the service auditor's opinion.
    - Unqualified opinion issued by <Firm> on <date> (Section I, p. 2).
```

For "Evaluating the sufficiency of the testing", comment on test types used and whether the period/sample coverage is adequate for a Type II. For the last bullet, point to the CUEC table.

### Step 4 — Populate the CUEC table

1. Find the CUECs — usually titled "Complementary User Entity Controls" or "User Entity Control Considerations" in Section III (sometimes mapped per control objective/criterion in Section IV). Extract every one. Include CSOCs only if the reviewer asks; otherwise mention them in Review Results.
2. One row per CUEC. In column 1, quote the CUEC verbatim and append its reference, e.g. `Customers are responsible for ... (Sec. III, p. 41; CC6.1)`.
3. Propose **Applicable (Y/N)** based on the services we use. For N, fill "Reasoning if Not Applicable" and write "N/A" in the control columns.
4. Show the reviewer the proposed list (CUEC # + short summary + proposed Y/N + reasoning) and ask them to confirm or correct it before mapping controls.

### Step 5 — Map company controls to applicable CUECs

**If a control list is attached:**
1. Parse it (control ID, name, description, owner, framework mapping if present).
2. For each applicable CUEC, find the control(s) whose description actually satisfies the CUEC's requirement. Put the control description (short) in "Company Control in Place" and the ID(s) in "SOC 1 / 2 Company Program Control ID".
3. Rate each match as **Strong**, **Partial**, or **None**. Present all mappings to the reviewer in one batch with the rationale for each and ask them to confirm, change, or supply controls for Partial/None items.

**If no control list is attached:**
1. Tell the reviewer that controls are needed to finish the table, and offer two options: attach a control list now, or answer CUEC-by-CUEC.
2. If answering directly, present the applicable CUECs in batches of about 5. For each, ask: *"What company control meets this CUEC, and what is its control ID?"* The reviewer may answer "none" or "don't know".
3. Record answers exactly as given.

**For both paths — gaps:**
- If no control meets an applicable CUEC, put "No control identified" in the control column, "—" in the ID column, and ask the reviewer for the remediation plan (owner + target date). If they don't provide one, write "Remediation plan pending — reviewer to provide".
- If a control only partly meets the CUEC, fill in the control, then describe the missing part in the remediation column.
- Write "No gap" in the remediation column for fully covered CUECs.

### Step 6 — Review Results and Conclusion

**Review Results** — short bullets covering:
- Opinion type and any qualification.
- Scope fit (services we use vs. in-scope system; required vs. provided report type — call out mismatches such as Type I when Type II is required, or missing TSCs).
- Period coverage and bridge letter status.
- Exceptions and their impact on us.
- Carved-out subservice organizations we rely on.
- CUEC coverage: X total, Y applicable, Z mapped to controls, N gaps.

**Conclusion** — one of the following, with a 1–3 sentence justification:
- **Reliance supported** — unqualified opinion, scope matches requirement, no significant exceptions, all applicable CUECs covered.
- **Reliance supported with follow-up** — minor exceptions, partial CUEC gaps with remediation plans, bridge letter needed, or carved-out subservice orgs to review.
- **Reliance not supported** — qualified/adverse/disclaimer opinion, required report type or scope not provided, significant exceptions affecting our services, or material CUEC gaps without remediation.

Present the proposed conclusion to the reviewer for sign-off; they may override it. Record their final choice.

### Step 7 — Sign-off and output

1. **Review Completed By:** the reviewer's name. **Review Completed Date:** today's date (YYYY-MM-DD) unless the reviewer gives another.
2. Save a **new** Markdown file (never overwrite the template):
   `SSAE Subservice Organization Review - <Provider Name> - <Period End YYYY-MM-DD>.md`
   Save to the user's selected folder if one is connected; otherwise to the outputs folder. Present the file to the user.

### Step 8 — Verify before delivering

Check the finished file and fix anything that fails:
- [ ] No `[Service Provider]` placeholders, template-warning heading, or empty required fields remain.
- [ ] Every CUEC in the report appears in the table (compare counts).
- [ ] Every applicable CUEC has a control or an explicit gap and remediation entry.
- [ ] Every control ID in the table came from the control list or the reviewer.
- [ ] Every exception in Section IV is listed.
- [ ] Dates, auditor name, and opinion match the report.
- [ ] Markdown tables render: one row per line, `|` inside cell text escaped as `\|`, line breaks inside cells written as `<br>`.

End by telling the reviewer the conclusion, the number of gaps, and any open items (pending remediation plans, bridge letter, subservice org reviews).

## Embedded template (use when no template is attached)

```markdown
# SSAE \- Subservice Organization Internal Control Evaluation Checklist \[Template\]

# Do Not Use This Page for Subservice Organization Evaluations. Make a Copy and Delete This Heading.


### **Service Provider's Name:**


### **Type of SSAE No. 21 Provided (i.e., SOC 1 or 2, Type I or II):**


### Required Report Type:

* [ ] SOC 1 Type II
* [ ] SOC 2 Type II
    * [ ] Security
    * [ ] Availability
    * [ ] Confidentiality
    * [ ] Privacy
    * [ ] Processing Integrity
* [ ] SOC 3


### **Services Provided by** \[Service Provider\]:


### **SSAE No. 21 Report Opinion:**


### **Time Period Covered by SSAE No. 21 Report:**


### **Exceptions from Testing in SSAE No. 21 Report:**


### **Review Procedures Included:**

- Reviewing the service auditor's opinion.
- Verifying the scope of the report as it relates to the services provided to us by the service organization, including the services provided by subservice organizations.
- Obtaining an understanding of the control objectives and related controls by management at the service organization.
- Evaluating the sufficiency of the testing of controls performed by the service auditor.
- Evaluating the results of testing performed by the service auditor.
- Reviewing the user entity control considerations disclosed in the report and determining with management the impact on our audit, including additional procedures such as testing user controls. (Please see the next page for a detailed mapping).


### \[Service Provider\] **Complementary User Entity Controls**

| **User Entity Control Required** | **Applicable to Our Company (Y/N)** | **Reasoning if Not Applicable** | **If Applicable, Company Control in Place to Meet CUEC** | **SOC 1 / 2 Company Program Control ID** | **If a Gap is Identified, What is the Remediation Plan?** |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

### **Review Results:**


### **Conclusion:**


### **Review Completed By:**

### **Review Completed Date:**
```
