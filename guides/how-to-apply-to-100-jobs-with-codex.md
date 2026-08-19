[← Back to the guide directory](../README.md)

# How to Apply to 100 Jobs with Codex

A reusable folder structure and prompt library for preparing more job applications without sending generic answers or inventing experience.

> **Last verified:** 20 August 2026
>
> **The rule:** Codex can organise information, draft from evidence, and fill approved fields. You review every claim and submit every application yourself.

## What this system does

The workflow separates four things that often get mixed together:

1. **Your source of truth** — the career history and evidence that remain the same across applications.
2. **The employer’s request** — the job description, application form, and questions for one role.
3. **Working drafts** — analysis and drafts that may still contain mistakes.
4. **Approved submission files** — the exact CV and answers you personally checked.

That separation makes it easier to tailor applications quickly without losing track of which version is true, current, or ready to use.

## The complete folder structure

Create this on your own computer. Keep it private because it will contain personal information.

```text
Job Applications/
├── README.md
├── application-tracker.csv
│
├── 00-Profile/
│   ├── Master-CV.pdf
│   ├── Master-CV.md
│   ├── Career-Evidence.md
│   ├── Role-Preferences.md
│   └── Links.md
│
├── 01-Templates/
│   ├── Application-Answers-Template.md
│   ├── Role-Analysis-Template.md
│   └── Submission-Checklist.md
│
├── 02-Applications/
│   └── 2026-08-Company-Role/
│       ├── 00-Source/
│       │   ├── Job-Description.pdf
│       │   ├── Application-Form.pdf
│       │   └── Company-Notes.md
│       │
│       ├── 01-Working/
│       │   ├── Role-Analysis.md
│       │   ├── Evidence-Map.md
│       │   ├── Draft-Answers.md
│       │   └── Tailored-CV-Draft.md
│       │
│       ├── 02-Approved/
│       │   ├── Final-Answers.md
│       │   ├── Tailored-CV.pdf
│       │   └── Submission-Checklist.md
│       │
│       └── 03-Receipt/
│           ├── Submission-Confirmation.pdf
│           └── Follow-Up.md
│
└── 99-Archive/
```

Name each application folder with the date, company, and role:

```text
YYYY-MM-Company-Role
```

Examples:

```text
2026-08-Acme-Product-Designer
2026-08-Northstar-Growth-Lead
```

Use a consistent name so folders sort naturally and Codex cannot confuse one application with another.

---

## 1. `00-Profile` — build your source of truth

This folder contains facts that Codex may reuse across applications.

### `Master-CV.pdf`

Your current, complete CV. Keep this as the stable source rather than replacing it with every tailored version.

### `Master-CV.md`

A text version of the master CV. Markdown is easier for an agent to search, quote, and edit precisely than a PDF.

### `Career-Evidence.md`

Create an evidence library using this structure:

```markdown
# Career evidence

## Achievement 1

- Employer or project:
- Role:
- Situation:
- What I personally did:
- Tools or skills used:
- Result:
- Metric and how it was measured:
- Source that verifies it:
- Safe to include publicly: yes/no

## Achievement 2

- Employer or project:
- Role:
- Situation:
- What I personally did:
- Tools or skills used:
- Result:
- Metric and how it was measured:
- Source that verifies it:
- Safe to include publicly: yes/no
```

Do not add a metric because it sounds impressive. If you cannot verify it, leave it out or describe the outcome without a number.

### `Role-Preferences.md`

Record the constraints that should stop you wasting time on a poor-fit role:

```markdown
# Role preferences

- Target roles:
- Seniority:
- Industries:
- Location or time-zone limits:
- Remote, hybrid, or office preference:
- Minimum compensation:
- Visa or work-authorisation constraints:
- Non-negotiables:
- Skills I want to use more:
- Roles I do not want:
```

### `Links.md`

Keep the approved URLs you regularly paste into forms:

```markdown
# Links

- LinkedIn:
- Portfolio:
- GitHub:
- Personal website:
- Relevant case study:
```

Avoid putting passwords, identity documents, references’ private details, or secret links in this file.

---

## 2. `01-Templates` — keep every application consistent

Templates save time without forcing every employer to receive the same answer.

### `Application-Answers-Template.md`

```markdown
# Application answers

## Question 1

**Employer's question:**

**Word or character limit:**

**Evidence used:**

**Draft:**

**Final approved answer:**

**Truth check:** Every claim verified / Needs review
```

Duplicate the block for every question.

### `Role-Analysis-Template.md`

```markdown
# Role analysis

## Basics

- Company:
- Role:
- Location:
- Salary range:
- Application deadline:

## Requirements

### Must have

-

### Nice to have

-

## Evidence match

| Requirement | Evidence from my files | Strength | Gap or question |
|---|---|---|---|
| | | Strong / Partial / None | |

## Decision

- Fit score:
- Strongest reasons to apply:
- Honest gaps:
- Apply, investigate, or skip:
```

### `Submission-Checklist.md`

```markdown
# Submission checklist

- [ ] Company and role are correct on every file
- [ ] Contact details are current
- [ ] Dates and job titles match the master CV
- [ ] Every achievement is supported by Career-Evidence.md
- [ ] No experience, skill, qualification, or metric was invented
- [ ] Every application question is answered directly
- [ ] Character and word limits are respected
- [ ] Tone sounds like me
- [ ] Tailored CV opens correctly and has the right filename
- [ ] Personal data is only included where required
- [ ] I reviewed the completed form before submission
- [ ] I—not the automation—clicked the final submit button
```

---

## 3. `02-Applications` — one clean package per role

Create a new company-and-role folder before Codex drafts anything.

### `00-Source`

Store only material supplied by the employer or collected before drafting:

- the full job description;
- a full-page capture or PDF of the application form;
- company research and notes; and
- any stated word limits or application instructions.

Keeping these files separate prevents an early draft from being mistaken for a source.

### `01-Working`

This is the scratch space. Nothing here is approved for submission.

- `Role-Analysis.md` breaks down requirements and gaps.
- `Evidence-Map.md` connects each claim to your real experience.
- `Draft-Answers.md` contains unapproved responses.
- `Tailored-CV-Draft.md` contains an editable role-specific CV.

### `02-Approved`

Move or export a file here only after personal review.

- `Final-Answers.md` is the exact approved wording for the form.
- `Tailored-CV.pdf` is the file you will upload.
- `Submission-Checklist.md` records the final quality check.

Do not let browser automation pull text from `01-Working`. Point it only at the approved folder.

### `03-Receipt`

Save the confirmation page or email and note the next action:

```markdown
# Follow-up

- Submitted:
- Contact:
- Expected response window:
- Follow-up date:
- Interview notes:
- Outcome:
```

---

## 4. Track the pipeline

Create `application-tracker.csv` with these columns:

```csv
id,company,role,source_url,date_found,deadline,status,date_submitted,follow_up_date,contact,folder,notes
```

Suggested status values:

```text
Researching
Drafting
Ready for review
Submitted
Interview
Offer
Rejected
Withdrawn
Skipped
```

The tracker tells you what needs attention. It should not become a target that rewards low-quality applications. Measure interviews and relevant conversations, not only the number submitted.

---

## Reusable Codex prompts

Replace the bracketed text before using each prompt.

### Prompt 1 — interview me and build the evidence library

```text
Use the /grill-me skill to interview me about my career and build a truthful evidence
library for job applications.

Ask about projects, responsibilities, decisions, challenges, skills, outcomes, and
metrics. Challenge vague claims. If I cannot verify a number, mark it as unverified
rather than improving or guessing it.

After the interview, draft updates for:
- 00-Profile/Master-CV.md
- 00-Profile/Career-Evidence.md
- 00-Profile/Role-Preferences.md

Show me the proposed changes before editing any files. Never invent experience,
metrics, qualifications, employers, dates, or skills.
```

### Prompt 2 — analyse a role before applying

```text
Read these files:
- 00-Profile/Master-CV.md
- 00-Profile/Career-Evidence.md
- 00-Profile/Role-Preferences.md
- 02-Applications/[APPLICATION]/00-Source/Job-Description.pdf
- 02-Applications/[APPLICATION]/00-Source/Application-Form.pdf

Create 01-Working/Role-Analysis.md using the role-analysis template.

Separate must-have requirements from preferences. For each requirement, cite the exact
evidence from my profile files. Mark missing evidence as a gap. Do not infer that I have
a skill simply because it is common for my role.

Finish with Apply, Investigate, or Skip and explain the recommendation.
```

### Prompt 3 — draft truthful application answers

```text
Draft answers for every question in the captured application form.

Use only claims supported by 00-Profile/Master-CV.md and
00-Profile/Career-Evidence.md. In 01-Working/Evidence-Map.md, map every material claim
to its source before writing the answer.

Requirements:
- answer the employer's actual question;
- respect every word or character limit;
- use specific examples where evidence exists;
- keep the tone direct and natural;
- acknowledge a gap instead of hiding it; and
- never invent experience, dates, metrics, skills, qualifications, or motivation.

Write the drafts to 01-Working/Draft-Answers.md. Label anything that needs my personal
context with [NEEDS INPUT]. Do not move anything to 02-Approved.
```

### Prompt 4 — create a role-specific CV

```text
Create a role-specific CV for [COMPANY] — [ROLE].

Use 00-Profile/Master-CV.md as the factual source and the job description as the
prioritisation guide. You may reorder, shorten, and clarify true information. You may
not add or strengthen a claim beyond the evidence.

Show a change summary containing:
- sections reordered;
- bullets rewritten;
- keywords added and the evidence supporting each one;
- information removed; and
- gaps you deliberately did not cover.

Save the draft to 01-Working/Tailored-CV-Draft.md. Wait for my approval before creating
the final PDF in 02-Approved.
```

### Prompt 5 — run the truth and quality check

```text
Review the current application package as a sceptical fact-checker.

Compare:
- 01-Working/Draft-Answers.md
- 01-Working/Tailored-CV-Draft.md
- 01-Working/Evidence-Map.md
- 00-Profile/Master-CV.md
- 00-Profile/Career-Evidence.md
- all files in 00-Source

Flag:
- claims with no evidence;
- numbers, dates, titles, or skills that do not match;
- answers that avoid the question;
- generic language that could be sent to any company;
- wording that exaggerates my responsibility;
- missing personal context; and
- word-limit problems.

Do not silently fix factual uncertainty. Ask me to resolve it.
```

### Prompt 6 — fill the approved form, but do not submit

```text
Use browser control to fill the application at [URL].

Source contact and work-history fields from 00-Profile. Source application answers and
the CV only from 02-Approved. Do not use drafts from 01-Working.

You may:
- fill text fields;
- select options only when the approved answer is explicit;
- upload 02-Approved/Tailored-CV.pdf; and
- stop to ask me about any missing or ambiguous field.

You must not:
- invent an answer;
- agree to legal declarations for me;
- provide demographic information without asking;
- send messages or contact references;
- bypass a CAPTCHA;
- make a payment; or
- click the final submit button.

Pause on the final review page and give me a field-by-field summary. I will inspect the
application and submit it myself.
```

---

## The five-step workflow

1. Build and maintain the truthful profile in `00-Profile`.
2. Capture the complete role and application in a new `00-Source` folder.
3. Ask Codex to analyse the role and draft from mapped evidence.
4. Review every claim, then create the final files in `02-Approved`.
5. Let browser control fill approved content, stop on the review page, and submit it yourself.

## Privacy and safety rules

- Keep the real `Job Applications` folder private; do not push personal CVs or application data to a public GitHub repository.
- Store passwords and authentication codes in a password manager, never in these files.
- Redact identity documents, home addresses, salary history, and references’ details when they are not required.
- Check the employer’s instructions before using automation.
- Do not use automation to bypass rate limits, CAPTCHAs, screening safeguards, or application rules.
- Do not apply indiscriminately. Use the fit analysis to skip roles that are irrelevant or outside your constraints.
- Personally approve every answer, declaration, uploaded file, and final submission.

---

If this guide helped, star the repository and share it with another job seeker.

Created by [Grayson Ho](https://github.com/graysonhyc).
