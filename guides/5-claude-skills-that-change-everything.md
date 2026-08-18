[← Back to the guide directory](../README.md)

# 5 Claude Skills That Change Everything

Five skills that help Claude pressure-test ideas, run a disciplined build workflow, create more distinctive interfaces, work with PDFs, and test web apps like a user.

> **Last verified:** 18 August 2026
>
> **Works with:** Claude Code. Several of these skills also support Codex and other agents that follow the Agent Skills standard.

## The five skills at a glance

| # | Skill | Best for |
|---|---|---|
| 1 | [`grill-me`](https://www.aihero.dev/skills-grill-me) | Finding unanswered questions before you commit to an idea |
| 2 | [Superpowers](https://github.com/obra/superpowers) | Turning an idea into a spec, plan, tested implementation, and review |
| 3 | [`frontend-design`](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md) | Giving a UI a deliberate visual direction instead of a generic AI look |
| 4 | [PDF](https://github.com/anthropics/skills/tree/main/skills/pdf) | Reading, extracting, creating, editing, and checking PDFs |
| 5 | [`webapp-testing`](https://github.com/anthropics/skills/tree/main/skills/webapp-testing) | Exercising browser flows, capturing screenshots, and inspecting console output |

## Before you install anything

Skills are instructions and supporting files that an agent loads when needed. Treat third-party skills like code:

1. Open the source and read the `SKILL.md` file.
2. Check any scripts, hooks, or dependencies it includes.
3. Review what tools and files it expects to access.
4. Install it in a test project first.
5. Keep Git commits or branches so changes remain easy to undo.

Claude Code discovers personal skills in `~/.claude/skills/` and project skills in `.claude/skills/`. A project skill is shared through Git; a personal skill is available across your own projects.

---

## 1. `grill-me` — pressure-test the idea first

`grill-me` interviews you about a rough idea until the hidden decisions and assumptions become visible. Use it for a feature, product direction, business decision, article, or any other idea that is still vague.

### Install it

Install only this skill:

```bash
npx skills@latest add mattpocock/skills --skill=grill-me
```

Then start a fresh conversation and run:

```text
/grill-me
```

### Give it a useful starting point

```text
/grill-me

I want to add an AI support assistant to our SaaS product. I know it should answer
questions from our documentation, but I have not decided its scope, escalation path,
or success metric.
```

Be willing to answer “I don’t know.” If a question needs something visual or interactive to answer, build a small prototype instead of guessing.

**Best time to use it:** before writing the spec or implementation plan.

---

## 2. Superpowers — use a complete development workflow

Superpowers is a collection of composable skills for software development. Its workflow moves from brainstorming and specification through planning, small implementation tasks, test-driven development, review, and verification.

### Install it in Claude Code

Use Anthropic’s official plugin marketplace:

```text
/plugin install superpowers@claude-plugins-official
```

Restart Claude Code after installation if the plugin does not appear immediately.

### Try it

```text
Help me add saved filters to this dashboard. Start by understanding the existing
code and clarifying the behaviour. Do not implement anything until I approve the
design and plan.
```

The important part is not a magic prompt. Let the workflow create review gates:

1. Agree on what you are building.
2. Review the proposed design.
3. Approve the implementation plan.
4. Build in small, testable tasks.
5. Review the result against the original requirements.

**Best time to use it:** when a task is large enough that “just start coding” is likely to create rework.

---

## 3. `frontend-design` — make the design fit the product

Anthropic’s `frontend-design` skill pushes Claude to choose an intentional aesthetic direction, typography, colour system, layout concept, and signature element before building. It also asks Claude to critique generic choices and keep accessibility and responsive behaviour in view.

### Install it

In Claude Code, open the plugin manager:

```text
/plugin
```

Search for **frontend-design** in Anthropic’s official marketplace and install it. The source skill is available in the [`anthropics/claude-code`](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design) repository for review.

### Try it with a real brief

```text
Use the frontend-design skill to build a landing page for an independent ceramics
studio. The audience is design-conscious home buyers. The page's one job is to
drive workshop bookings. Avoid a generic SaaS layout. Show me the visual direction,
type choices, colour tokens, and a small wireframe before writing code.
```

Give the skill real content and constraints. Include:

- the product and audience;
- the page’s single job;
- brand references or qualities;
- required content and interactions;
- framework and component-library constraints; and
- accessibility and responsive requirements.

**Best time to use it:** before the first UI implementation, or when an existing interface feels templated and needs a coherent redesign.

---

## 4. PDF — read, create, and edit documents

Anthropic’s PDF skill contains workflows and scripts for common document tasks, including extracting text and tables, creating and merging PDFs, working with forms, adding annotations or watermarks, and using OCR for scanned documents.

### Install it

Review the [PDF skill source](https://github.com/anthropics/skills/tree/main/skills/pdf), including its scripts and licence, then install it through the skill or plugin installer available in your agent.

If your client supports the `skills` command-line installer:

```bash
npx skills@latest add anthropics/skills --skill=pdf
```

### Try it safely

```text
Use the PDF skill to extract the headings and tables from ./reports/q2-report.pdf.
Return a Markdown summary and a CSV for each table. Do not modify the original PDF.
Flag any pages where OCR confidence appears low.
```

For a generated document:

```text
Create a PDF proposal from proposal.md. Use the brand colours in brand-guide.md,
include page numbers, and render a review copy. Do not overwrite an existing file.
```

**Best time to use it:** when the output must be a reliable document artifact rather than a block of copied text.

> PDFs can contain private, contractual, medical, or financial information. Remove unnecessary sensitive data and inspect the output before sharing it.

---

## 5. `webapp-testing` — test the app like a user

The `webapp-testing` skill uses browser automation to navigate an application, interact with controls, take screenshots, and inspect browser output. This catches problems that a unit test may miss: broken flows, invisible buttons, navigation mistakes, validation issues, and console errors.

### Install it

Review the [webapp-testing skill source](https://github.com/anthropics/skills/tree/main/skills/webapp-testing) and its supporting scripts, then install it through your agent’s skill installer.

If your client supports the `skills` command-line installer:

```bash
npx skills@latest add anthropics/skills --skill=webapp-testing
```

### Give it a bounded test mission

```text
Use the webapp-testing skill against http://localhost:3000.

Test this flow:
1. Open the sign-up page.
2. Submit an invalid email and verify the error is understandable.
3. Create an account with the supplied test credentials.
4. Create and rename one project.
5. Capture screenshots at each major step.
6. Report browser console errors and failed network requests.

Do not access production, send real messages, or create paid resources.
```

Run it against local, staging, or disposable test environments. Supply test accounts and define which actions are forbidden.

**Best time to use it:** after the main flow works locally and before you call the feature finished.

---

## A practical workflow using all five

1. Run `grill-me` to uncover assumptions in the idea.
2. Use Superpowers to turn the agreed idea into a design and implementation plan.
3. Invoke `frontend-design` for the visual direction and interface build.
4. Use PDF only if the feature reads or produces documents.
5. Finish with `webapp-testing` against the acceptance criteria.

## Five prompts to copy

```text
1. /grill-me — pressure-test this idea until the unresolved decisions are explicit.

2. Turn this approved idea into a design and implementation plan. Wait for my
   approval before coding.

3. Use frontend-design. Propose a specific visual direction for this product and
   critique it for generic AI-design defaults before implementation.

4. Use the PDF skill to extract this document into structured Markdown and CSV.
   Preserve the source file and flag uncertain OCR.

5. Use webapp-testing to exercise the acceptance criteria in staging. Capture
   evidence and report failures, but do not modify production data.
```

## Official and primary sources

- [`grill-me` guide and source link](https://www.aihero.dev/skills-grill-me)
- [Superpowers repository](https://github.com/obra/superpowers)
- [`frontend-design` source](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md)
- [Anthropic PDF skill](https://github.com/anthropics/skills/tree/main/skills/pdf)
- [Anthropic webapp-testing skill](https://github.com/anthropics/skills/tree/main/skills/webapp-testing)
- [Claude Code skills documentation](https://code.claude.com/docs/en/slash-commands)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
