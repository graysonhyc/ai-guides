[← Back to the guide directory](../README.md)

# Vibe Code Like a Senior Engineer with Agent Skills

Add planning, incremental implementation, testing, review, and launch checks to your AI coding workflow with Addy Osmani's Agent Skills.

> **Last verified:** 26 August 2026
>
> **Works with:** Claude Code, Codex, Cursor, Gemini CLI, GitHub Copilot, and many other agents. Installation and automatic skill activation vary by tool.

## What Agent Skills changes

Coding agents are good at producing code quickly. Left alone, they can also take the shortest path: start before the requirements are clear, change too much at once, skip tests, and call the work finished without runtime evidence.

[Agent Skills](https://github.com/addyosmani/agent-skills) is a collection of 24 structured workflows: 23 engineering skills plus one meta-skill that routes work to the appropriate workflow. The pack covers the full development lifecycle:

```text
DEFINE → PLAN → BUILD → VERIFY → REVIEW → SHIP
```

The skills do not make every output production-ready automatically. They give the agent explicit steps, review gates, common failure patterns, and evidence requirements so you can supervise a more disciplined build.

## The four gaps from the video

| Gap | Skills that address it | What changes |
|---|---|---|
| No approved plan | `spec-driven-development` and `planning-and-task-breakdown` | The idea becomes a written specification and small tasks with acceptance criteria before implementation begins. |
| Inconsistent implementation | `incremental-implementation`, `context-engineering`, and specialist build skills | The agent works in small slices, keeps the relevant project rules in context, and verifies each slice before moving on. |
| Tests left until the end | `test-driven-development` and `browser-testing-with-devtools` | Behaviour is proved during the build with automated tests and runtime checks. |
| No serious final review | `code-review-and-quality`, `security-and-hardening`, and `shipping-and-launch` | The change goes through quality, security, rollout, monitoring, and rollback checks before release. |

## Before you install it

Skills are instructions and supporting files that influence how your agent works. Treat a third-party skill pack like code:

1. Review the repository, licence, `SKILL.md` files, scripts, hooks, and requested tools.
2. Install it in a test project first.
3. Work on a branch and keep changes easy to undo.
4. Review every command before allowing access to credentials, production data, deployments, or destructive actions.

Agent Skills is MIT-licensed, but the repository changes over time. Inspect the version you are about to install.

## Install it

### Universal installer

The quickest route for a supported coding agent is the open Skills CLI:

```bash
npx skills add addyosmani/agent-skills
```

Browse the available skills before installing:

```bash
npx skills add addyosmani/agent-skills --list
```

Installing the complete repository is the simplest way to keep its shared reference checklists available. The project currently warns that a single-skill install copies the selected skill but not the repository-level `references/` directory.

### Claude Code

Inside Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add addyosmani/agent-skills
/plugin install agent-skills@addy-agent-skills
```

If the marketplace command cannot clone over SSH, use the HTTPS repository URL:

```text
/plugin marketplace add https://github.com/addyosmani/agent-skills.git
/plugin install agent-skills@addy-agent-skills
```

### Codex

Codex CLI 0.122 and later can install the native plugin:

```bash
codex plugin marketplace add addyosmani/agent-skills
codex plugin add agent-skills@agent-skills
```

Invoke an installed skill with `@`, for example:

```text
@spec-driven-development Help me define a saved-filters feature for this dashboard.
```

### Gemini CLI

Install the repository's skills directory:

```bash
gemini skills install https://github.com/addyosmani/agent-skills.git --path skills
```

Then verify discovery inside Gemini CLI:

```text
/skills list
```

For Cursor, GitHub Copilot, OpenCode, Windsurf, and other tools, follow the setup guide linked from the Agent Skills repository instead of assuming the same commands apply.

## Run the complete workflow

The native plugin includes eight lifecycle commands:

| Goal | Command | Review gate |
|---|---|---|
| Define the outcome | `/spec` | Approve the specification before code |
| Break it into safe tasks | `/plan` | Check scope, order, and acceptance criteria |
| Implement in slices | `/build` | Review each tested increment |
| Prove the behaviour | `/test` | Require test and runtime evidence |
| Review code quality | `/review` | Resolve important findings before merge |
| Measure web performance | `/webperf` | Compare real measurements, not guesses |
| Reduce unnecessary complexity | `/code-simplify` | Confirm behaviour remains unchanged |
| Prepare the release | `/ship` | Review deployment, monitoring, and rollback |

Start a new feature like this:

```text
Use the Agent Skills lifecycle for this change.

Outcome: Let users save and reuse dashboard filters.
Users: Existing account owners with multiple reports.
Success criteria:
- A user can save, rename, apply, and delete a filter.
- Saved filters persist after sign-out.
- Existing unsaved filter behaviour does not change.

Start with the specification. Inspect the existing code and ask about unresolved
behaviour one question at a time. Do not implement anything until I approve the
specification and plan.
```

Then move through the gates:

```text
/spec   → review and approve what will be built
/plan   → review the tasks, dependencies, and proof required
/build  → implement one small, tested slice at a time
/test   → run the relevant automated and browser checks
/review → assess correctness, clarity, security, and maintainability
/ship   → prepare rollout, monitoring, and rollback; deploy only with approval
```

The repository also provides `/build auto`, which can generate a plan and execute its tasks after one plan approval. Use it only when the scope, environment, and forbidden actions are clear. It should still stop on failures or risky operations, and you should review the result before merge or deployment.

## Start smaller on an existing codebase

Do not force a brand-new lifecycle onto a mature project in one step. Begin with the places where missing evidence creates the most risk:

1. Run `code-review-and-quality` on one representative change.
2. Use `test-driven-development` for the next bug fix or behaviour change.
3. Add `spec-driven-development` for the next feature with unclear requirements.
4. Introduce `shipping-and-launch` before the next meaningful release.
5. Expand the workflow only after the team agrees that the gates are useful.

Existing project rules, tests, review policies, and deployment controls remain the source of truth. A general skill should support them, not silently replace them.

## A final proof prompt

Use this before calling the work complete:

```text
Review this change against the approved specification and plan.

Show me:
1. Each acceptance criterion and the evidence that proves it.
2. Tests added or changed, with the exact results.
3. Runtime or browser checks performed.
4. Important code-review, security, and accessibility findings.
5. Remaining risks, assumptions, and unverified claims.
6. The rollout, monitoring, and rollback plan.

Do not deploy, merge, or dismiss a failing check without my approval.
```

## Official sources

- [Agent Skills repository and installation instructions](https://github.com/addyosmani/agent-skills)
- [Getting started with Agent Skills](https://github.com/addyosmani/agent-skills/blob/main/docs/getting-started.md)
- [Adopting Agent Skills in greenfield and existing projects](https://github.com/addyosmani/agent-skills/blob/main/docs/adoption-guide.md)
- [Codex setup](https://github.com/addyosmani/agent-skills/blob/main/docs/codex-setup.md)
- [Gemini CLI setup](https://github.com/addyosmani/agent-skills/blob/main/docs/gemini-cli-setup.md)
