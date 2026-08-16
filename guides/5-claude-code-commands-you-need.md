[← Back to the guide directory](../README.md)

# 5 Claude Code Commands You Need

Five commands that give you more control over usage, context, model choice, mistakes, and repetitive work in Claude Code.

> **Last verified:** 16 August 2026  
> **Works with:** The interactive Claude Code terminal. Some commands are unavailable or behave differently in Claude Code on the web.

## The five commands at a glance

| Command | Use it when you want to |
|---|---|
| `/usage` | Check session cost, plan limits, and activity |
| `/compact` | Free context space without starting a new conversation |
| `/model` | Change the model used by the current session |
| `/rewind` | Restore code, conversation, or both to an earlier checkpoint |
| `/loop` | Repeat a prompt on a schedule while the session stays open |

## Before you start

Open Claude Code inside your project:

```bash
cd your-project
claude
```

Type a slash command at the start of the prompt. Type `/` by itself to browse the commands available in your installed version.

If a command below is missing, update Claude Code:

```bash
claude update
```

---

## 1. `/usage` — see what you have left

Run:

```text
/usage
```

Claude Code shows session cost, plan usage limits, and activity statistics. On supported subscription plans, it can also break down usage by skills, subagents, plugins, and MCP servers.

Use it before a large task so you can decide whether to:

- continue with the current plan;
- split the task into smaller pieces;
- choose a lighter model; or
- leave expensive work until your usage window resets.

Aliases: `/cost` and `/stats`.

**Good habit:** check usage before a long refactor, large code review, or multi-agent workflow—not after it has already consumed your allowance.

---

## 2. `/compact` — free context without losing the task

Long sessions fill the context window with conversation, file contents, and tool output. Run:

```text
/compact
```

Claude Code replaces older conversation history with a summary, preserving the important context so you can continue in the same session.

You can tell it what the summary must preserve:

```text
/compact Keep the accepted architecture, modified file list, failing test output,
and the next three implementation steps.
```

Use `/compact` at a natural break, such as after finishing the backend and before starting the UI.

### `/compact` or `/clear`?

- Use `/compact` when you are continuing the same task.
- Use `/clear` when you are starting a genuinely unrelated task.
- Use `/rewind` when you want to abandon a bad path and return to an earlier point.

**Important:** a summary can omit details. Put durable project rules in `CLAUDE.md`, and explicitly name anything critical in your compact instructions.

---

## 3. `/model` — choose the right model for the task

Run:

```text
/model
```

This opens the model picker for the current session. You can also pass a model name if it is available on your account:

```text
/model sonnet
```

A practical rule:

- use a faster, lower-cost model for straightforward edits, formatting, and routine fixes;
- use a stronger model for architecture, difficult debugging, planning, or ambiguous work.

Changing the model mid-session can make the next response slower because Claude has to read the conversation with the new model. Switch intentionally rather than changing models every few turns.

**Example workflow:**

1. Use a stronger model to plan a complex migration.
2. Save the decisions in the conversation or project documentation.
3. Switch to a faster model for mechanical implementation.
4. Switch back only if the work becomes uncertain or the tests reveal a deeper problem.

---

## 4. `/rewind` — recover from the wrong direction

Run:

```text
/rewind
```

You can also press `Esc` twice when the prompt input is empty.

Claude Code opens a list of earlier prompts. Choose a checkpoint, then select one of the available actions:

- restore code and conversation;
- restore only the conversation;
- restore only the code;
- summarize from the selected point;
- summarize everything before the selected point.

This is useful when Claude edits the wrong files, follows a weak approach, or creates a regression.

### Know the limits

Checkpointing is a safety net, not a replacement for Git.

Claude Code tracks edits made through its file-editing tools, but it may not restore:

- files changed by shell commands such as `rm`, `mv`, or `cp`;
- changes made by background subagents;
- manual edits or changes from other sessions;
- symlinked or hard-linked files.

Before a risky change, create a Git branch or commit a known-good state. After rewinding, inspect the diff and run the tests again.

---

## 5. `/loop` — repeat a prompt while the session stays open

Use `/loop` for polling and recurring checks:

```text
/loop 5m Check whether the deployment finished. If it failed, summarize the error.
```

You can omit the interval:

```text
/loop Check whether CI passed and report any new review comments.
```

Claude then chooses a delay based on what it observes. A bare `/loop` runs Claude Code's built-in maintenance prompt, or the custom prompt in `.claude/loop.md` if your project defines one.

Useful examples:

```text
/loop 10m Check the open pull request. Report new review comments and failing checks.

/loop 15m Check whether the staging health endpoint is responding. Stop reporting once
it is healthy.

/loop 30m /review-pr 1234
```

Press `Esc` while a loop is waiting to stop its next scheduled run.

### What `/loop` does not do

`/loop` schedules repeated prompts. It does not guarantee that a feature will be completed or that tests will eventually pass. The session must remain open, your machine must stay on, and each run still follows your permission settings.

For safer automation:

- give the loop one narrow job;
- state the success and failure conditions;
- tell it what it may change;
- require approval for pushes, deployments, deletions, and other irreversible actions;
- use an event-driven CI notification when available instead of frequent polling.

---

## A practical five-command workflow

Here is how the commands fit together during a real build:

1. Run `/usage` before starting a large task.
2. Use `/model` to match the model to the difficulty.
3. Run `/compact` between major phases of the same task.
4. Use `/rewind` if the implementation goes in the wrong direction.
5. Use `/loop` to check a deployment, pull request, or CI run while the session remains open.

## Copy-and-paste examples

```text
/usage

/compact Preserve the approved plan, modified files, test commands, and open issues.

/model sonnet

/rewind

/loop 5m Check whether CI passed. If it failed, summarize the failing job and propose
the smallest fix. Do not push changes.
```

## Official sources

- [Claude Code commands reference](https://code.claude.com/docs/en/commands)
- [Claude Code checkpointing](https://code.claude.com/docs/en/checkpointing)
- [Run prompts on a schedule with `/loop`](https://code.claude.com/docs/en/scheduled-tasks)
- [Manage Claude Code costs](https://code.claude.com/docs/en/costs)
- [Claude Code best practices](https://code.claude.com/docs/en/best-practices)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
