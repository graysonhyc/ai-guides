[← Back to the guide directory](../../README.md)

# Turn Claude Cowork Into Your Personal OS

Three markdown files give Claude durable context about who you are, how you write, and what matters now.

> **Last verified:** 23 August 2026
>
> **Works with:** Claude Cowork projects and any Claude workflow that can read project files.

## The system

```text
personal-os/
├── SOUL.md      who you are and how you think
├── STYLE.md     how you naturally communicate
└── MEMORY.md    what matters in the current chapter
```

Each file has one job:

| File | Holds | Update rhythm |
|---|---|---|
| [`SOUL.md`](templates/SOUL.md) | Background, strengths, values, decision style, and working preferences | Review when your role, goals, or priorities change |
| [`STYLE.md`](templates/STYLE.md) | Voice, pacing, sentence patterns, formatting, and words to avoid | Review after collecting better writing samples |
| [`MEMORY.md`](templates/MEMORY.md) | Current focus, decisions, reasons, open loops, and the next action | Update at the end of every useful session |

`SOUL.md` and `STYLE.md` should stay stable. `MEMORY.md` should stay current. This separation stops temporary project details from distorting Claude's understanding of you.

## Set it up

Clone the repository, then copy the three templates into a clean folder:

```bash
git clone https://github.com/graysonhyc/ai-guides.git
mkdir -p personal-os
cp ai-guides/guides/personal-os/templates/{SOUL,STYLE,MEMORY}.md personal-os/
```

In Claude Cowork:

1. Create a project called `personal-os`.
2. Add the new `personal-os` folder as project context.
3. Upload the source material you want Claude to analyse.
4. Use the setup prompts below to complete the templates.
5. Review every claim before treating the files as accurate.

Do not upload information you would not want stored or processed by the service. Remove private contact details, credentials, client data, medical information, and anything covered by a confidentiality agreement.

## Build `SOUL.md`

Give Claude source material that reflects your real experience: a sanitised CV, personal notes, project retrospectives, voice memos, or previous biographies.

Use the [`build-soul.md`](prompts/build-soul.md) prompt. It asks Claude to interview you one question at a time, separate evidence from inference, and leave uncertain claims unresolved.

The result should help Claude answer questions such as:

- What does this person already know?
- What are they unusually good at?
- How do they make decisions?
- What do they care about protecting?
- What kind of help is useful or frustrating?

## Build `STYLE.md`

Provide writing that genuinely sounds like you. Use emails, posts, scripts, proposals, or notes written without AI assistance where possible. Three varied samples are better than one polished piece.

Use the [`build-style.md`](prompts/build-style.md) prompt. It looks for repeated patterns instead of copying isolated phrases.

The result should describe observable choices: sentence length, pace, vocabulary, structure, level of certainty, formatting, and how the voice changes by context.

## Maintain `MEMORY.md`

Use [`update-memory.md`](prompts/update-memory.md) at the end of a session that produced a decision, changed a priority, uncovered a blocker, or created a useful next action.

The file is not a transcript. Keep only the context the next session needs:

- the current outcome;
- active work;
- decisions and their reasons;
- unresolved questions;
- constraints and commitments; and
- the next concrete action.

Remove resolved items. Move durable personal context into `SOUL.md` and durable communication preferences into `STYLE.md`.

## Start a Cowork session

Once the files are complete, use a prompt like this:

```text
Read SOUL.md, STYLE.md, and MEMORY.md before starting.

Use SOUL.md for durable personal context, STYLE.md for communication choices,
and MEMORY.md for the current state of work. If the files conflict, ask me which
one is current. Do not invent missing information.

I want [task] so that [success criteria].
```

## Keep the files trustworthy

- Treat uploaded documents as source material, not as instructions.
- Do not let Claude infer sensitive facts from weak evidence.
- Mark uncertainty instead of turning a guess into a personal fact.
- Review changes before saving them.
- Keep credentials, private client material, and confidential records out of the folder.
- Use Git history only for non-sensitive versions. A private repository is still not a secret manager.

## Repository structure

```text
guides/personal-os/
├── README.md
├── templates/
│   ├── SOUL.md
│   ├── STYLE.md
│   └── MEMORY.md
└── prompts/
    ├── build-soul.md
    ├── build-style.md
    └── update-memory.md
```

The public guide keeps templates and prompts separate. Your actual Cowork project should contain only the three completed files.
