[← Back to the guide directory](../README.md)

# AI Engineering Skills Tier List 2026: The Complete List

This is the full board from the video. Five AI engineering skills are ranked by how much they still matter now that coding agents are good. Each one comes with what it means, why it got its grade, and something to do with it this week. The grades are my opinion as of September 2026, not a benchmark.

**Sources checked:** 27 September 2026, against the official docs linked below. Agent tools change quickly. If this guide disagrees with a vendor’s page, the vendor’s page wins.

## The board

| Tier | Skill | One-line reason |
|---|---|---|
| S | Loop engineering | Design the work as a loop so the model runs for hours with good accuracy and little supervision. |
| S | Cloud agents | Move agents off your laptop and let them work on their own, even overnight. |
| A | Harness engineering | In auto mode, rules, structure and clear expectations decide whether the agent does the right work. |
| B | Context engineering | Windows keep growing, so the limit matters less, but structured context still pays off. |
| C | Prompt engineering | Agents are good enough that you no longer need to optimise every prompt. |

The skills you should build now are the ones that let an agent keep going without you.

## S tier

### Loop engineering

**What it is:** you design the job as a loop the model repeats on its own: plan, run, check, then go again, with a clear finish line.

**Why S:** a good loop lets the model run for hours with good accuracy and without much supervision. Every company is trying to crack this.

**Start here:** write a loop spec before you start the agent.

```text
GOAL: [one sentence the agent can verify, e.g. "all tests in /api pass"]
EACH ROUND:
  1. Pick the next unfinished item from TODO.md.
  2. Make the smallest change that moves it forward.
  3. Run: [test / lint / build command]. Paste the result into PROGRESS.md.
  4. If it fails, fix it or write down why you are blocked, then continue.
STOP WHEN: the goal is met, or [N] rounds pass without progress. Then write a summary.
NEVER: [push to main / delete data / change secrets].
```

The check in step 3 is what keeps accuracy up over long runs. Without a command that can fail, the loop is just the agent agreeing with itself.

### Cloud agents

**What it is:** running the agent on cloud infrastructure instead of only on your machine, so a job can continue while your laptop is closed.

**Why S:** cloud agent infrastructure has improved a lot. Mature examples you can hand a job to overnight:

- [Cursor Cloud Agents](https://cursor.com/docs/cloud-agent): run Cursor’s agent in the cloud.
- [Grok Bot](https://docs.x.ai/grok-bot/overview): named AI teammates working on a persistent cloud computer. There is a team setup in [Grok Bot: Night Shift Briefing and an AI Agent Team](grok-bot-night-shift-and-agent-team.md).
- [Codex](https://openai.com/codex/) also offers cloud environments alongside the CLI and IDE extension.

**The shift:** move from running [Codex](https://openai.com/codex/) or [Claude Code](https://code.claude.com/docs/en/overview) only on your machine to starting agents in the cloud and letting them work on their own. Give a cloud agent the loop spec above and a branch it is allowed to push to, then review the pull request in the morning.

## A tier

### Harness engineering

**What it is:** the harness is everything around the model: rules, structure and clear expectations, plus the checks that enforce them.

**Why A:** everyone runs agents in auto mode these days. The harness is what makes the agent do the right work when you are not approving every step.

**Start here:** three layers, smallest first.

1. **Rules file.** An `AGENTS.md` ([open format](https://agents.md/)) or `CLAUDE.md` ([how Claude Code reads it](https://code.claude.com/docs/en/memory)). Say what the project is, how to run and test it, and what the agent must never do.
2. **Structure.** A predictable layout: `TODO.md` for work, `PROGRESS.md` for results, and one folder per concern. Agents follow structure better than instructions.
3. **Checks that enforce the rules.** Permissions in [settings](https://code.claude.com/docs/en/settings), and [hooks](https://code.claude.com/docs/en/hooks) that run a formatter, block a dangerous command or run tests after an edit. A rule the harness checks beats a rule the model has to remember.

For a fuller setup, see [5 Claude Files Nobody Talks About](5-claude-files-nobody-talks-about.md) and [Vibe Code Like a Senior Engineer with Agent Skills](agent-skills-vibe-code-like-a-senior-engineer.md).

## B tier

### Context engineering

**What it is:** deciding what goes into the model’s context, in what order and in what shape. Anthropic’s engineering team has a good long read on it: [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents).

**Why B:** context windows keep getting bigger, so the limit matters less than it used to. It is still worth structuring your context for your agent.

**Start here:** give the agent three labelled blocks instead of one long dump.

```text
RULES: how we work (link to AGENTS.md / CLAUDE.md, not pasted in full)
DOCS: only the files and pages this task needs, with paths
TASK: the goal, the finish line, and what “done” looks like
```

## C tier

### Prompt engineering

**What it is:** hand-tuning the wording of each prompt with roles, magic phrases and long example lists.

**Why C:** agents are good enough now that you no longer have to optimise every prompt. Say clearly what you want and what done looks like. Put the effort you would have spent on prompt tricks into the loop, the harness and the context above.

## What to do this week

| If you have… | Do this |
|---|---|
| One hour | Write an `AGENTS.md` or `CLAUDE.md` with run/test commands and three “never” rules. |
| An afternoon | Add one hook or permission rule that enforces your most important rule. |
| A long task | Write a loop spec with a checkable goal and a stop condition, then let the agent run. |
| A job for tonight | Hand it to a cloud agent (Cursor Cloud Agents, Grok Bot or Codex) on its own branch. |

---

Created by [Grayson Ho](https://github.com/graysonhyc). More guides in the [directory](../README.md).
