[← Back to the guide directory](../README.md)

# 5 Claude Files Nobody Talks About

Set up Claude Code once so your project carries its context, tools, permissions, repeatable workflows, and specialist agents into future sessions.

> **Last verified:** 18 August 2026
>
> **Works with:** Claude Code projects. User-level equivalents live under `~/.claude/` and apply across your projects.

## The five files and folders at a glance

| # | File or folder | What it controls | Share in Git? |
|---|---|---|---|
| 1 | `CLAUDE.md` | Durable project context and working rules | Yes |
| 2 | `.mcp.json` | Shared project MCP servers | Yes, without secrets |
| 3 | `.claude/settings.json` | Project settings, permissions, plugins, and hooks | Yes, after review |
| 4 | `.claude/skills/` | Repeatable knowledge and workflows | Yes |
| 5 | `.claude/agents/` | Specialist subagents with focused instructions and tools | Yes |

## Starter structure

```text
your-project/
├── CLAUDE.md
├── .mcp.json
└── .claude/
    ├── settings.json
    ├── skills/
    │   └── review-api/
    │       └── SKILL.md
    └── agents/
        └── code-reviewer.md
```

Use shared files for team-approved configuration. Keep personal preferences in `CLAUDE.local.md` or `.claude/settings.local.json`, and keep credentials out of every committed file.

---

## 1. `CLAUDE.md` — the project brief

`CLAUDE.md` contains instructions Claude should know in every session: architecture, commands, conventions, boundaries, and definitions of done.

Create it in the project root:

```markdown
# Project guide

## Product

This is a booking platform for independent fitness studios. The customer-facing
app lives in `apps/web`; the API lives in `apps/api`.

## Stack

- TypeScript and Node.js
- Next.js for the web app
- PostgreSQL with migrations in `apps/api/db/migrations`
- Vitest for unit tests and Playwright for end-to-end tests

## Working rules

- Follow the existing patterns in the nearest module.
- Never edit an existing production migration; add a new migration.
- Do not change public API response shapes without flagging the compatibility risk.
- Keep user-visible copy in sentence case.

## Validation

- Run `npm run lint` after code changes.
- Run the tests for the package you changed.
- For checkout changes, also run `npm run test:e2e -- checkout`.

## Definition of done

- The requested behaviour works.
- Relevant tests pass.
- Error, empty, and loading states are handled.
- Documentation is updated when behaviour or setup changes.
```

### What belongs here

- facts that are useful in almost every session;
- commands Claude cannot reliably infer;
- rules that are specific and verifiable;
- important folder or ownership boundaries; and
- safety constraints and required checks.

### What does not belong here

- secrets or credentials;
- a full copy of your documentation;
- long procedures used only occasionally—make those skills; or
- vague advice such as “write good code.”

Keep it focused. Claude Code loads applicable `CLAUDE.md` files automatically, and it can also import another file with `@path/to/file`.

---

## 2. `.mcp.json` — shared project tools

`.mcp.json` defines project-scoped Model Context Protocol servers. Claude Code reads it from the project root, and the file can be checked into Git so everyone gets the same tool definitions.

The safest way to create it is through Claude Code:

```bash
claude mcp add --transport http --scope project context7 https://mcp.context7.com/mcp
```

That produces a project configuration shaped like this:

```json
{
  "mcpServers": {
    "context7": {
      "type": "http",
      "url": "https://mcp.context7.com/mcp"
    },
    "internal-api": {
      "type": "http",
      "url": "${INTERNAL_API_URL:-http://localhost:8787}/mcp",
      "headers": {
        "Authorization": "Bearer ${INTERNAL_API_TOKEN}"
      }
    }
  }
}
```

Claude Code supports environment-variable expansion such as `${VAR}` and `${VAR:-default}`. Commit the variable name, never the token value.

### Security checklist

- Prefer OAuth where it is available.
- Start with read-only permissions.
- Connect development or sandbox projects first.
- Do not commit API keys, tokens, cookies, or production credentials.
- Review project MCP servers before approving them; they can expose external tools to the agent.
- Use `claude mcp reset-project-choices` if you need to review project-server approvals again.

Use `/mcp` inside Claude Code to inspect connection status and authenticate supported servers.

---

## 3. `.claude/settings.json` — the control panel

Project settings configure shared behaviour such as enabled plugins, permissions, environment values, and hooks. Add the JSON schema for editor validation:

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "enabledPlugins": {
    "frontend-design@claude-plugins-official": true
  },
  "permissions": {
    "allow": [
      "Bash(npm run lint)",
      "Bash(npm test *)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)"
    ]
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$(jq -r '.tool_input.file_path')\""
          }
        ]
      }
    ]
  }
}
```

Treat that as a pattern, not a blind paste. Only allow exact commands your project uses, make sure hook dependencies such as `jq` and Prettier exist, and test hooks on a branch.

### Choose the right scope

| Scope | File | Use it for |
|---|---|---|
| User | `~/.claude/settings.json` | Your defaults across all projects |
| Project | `.claude/settings.json` | Team-approved settings committed to Git |
| Local | `.claude/settings.local.json` | Personal overrides for this project; normally gitignored |

Use `/permissions` to see which rules are active and where they came from. Deny rules take precedence over ask and allow rules.

Hooks run automatically, so keep them narrow and deterministic. A formatter after file edits is a good hook; a complex product decision belongs in a skill or the conversation.

---

## 4. `.claude/skills/` — repeatable workflows

A skill is a folder whose entry point is `SKILL.md`. Claude loads the skill’s description so it can discover the capability, but loads the full instructions only when the skill is used.

Create `.claude/skills/review-api/SKILL.md`:

```markdown
---
name: review-api
description: Reviews API endpoint changes for validation, authorization, compatibility,
  error handling, and tests. Use when an API handler, route, controller, or public
  response shape changes.
---

# Review API changes

1. Read the changed endpoint and its tests.
2. Compare request and response shapes with the public contract.
3. Check input validation, authentication, and authorization separately.
4. Check error responses and logging for sensitive data.
5. Identify backward-incompatible changes.
6. Run the narrowest relevant tests.

Return:

- findings ordered by severity, with file and line references;
- missing tests;
- compatibility risks; and
- the validation commands you ran.

Do not modify files unless the user explicitly asks for fixes.
```

Invoke it directly:

```text
/review-api
```

Or ask naturally: “Review these API changes for compatibility and missing authorization checks.”

Skills can also contain templates, examples, reference files, and scripts. Link those supporting files from `SKILL.md` and load them only when relevant.

**Rule of thumb:** put always-needed facts in `CLAUDE.md`; put an occasional procedure or body of reference material in a skill.

---

## 5. `.claude/agents/` — specialist subagents

Custom subagents run focused work in a separate context and return their result to the main conversation. A project agent is a Markdown file with YAML frontmatter.

Create `.claude/agents/code-reviewer.md`:

```markdown
---
name: code-reviewer
description: Reviews a completed code change for correctness, security, regressions,
  and missing tests. Use after implementation and before merging.
tools: Read, Grep, Glob, Bash
model: inherit
maxTurns: 20
---

You are a careful, read-only code reviewer.

Review the requested diff and the surrounding code. Prioritise concrete defects over
style preferences. Check correctness, authorization, data loss, concurrency, backward
compatibility, error handling, and test coverage.

Do not edit files. Return findings ordered by severity. For each finding, include the
file, line, impact, and smallest credible fix. If there are no actionable findings,
say so and mention any tests you could not run.
```

Ask Claude to use it:

```text
Use the code-reviewer subagent to review my current diff. Do not change any files.
```

### Design agents narrowly

- Give each agent one clear responsibility.
- Grant only the tools it needs.
- Restate critical restrictions in the agent body.
- Set a turn limit for bounded work.
- Keep write-capable agents away from the same files when running in parallel.
- Review the returned evidence before accepting a recommendation.

Use a skill when you want reusable instructions in the main conversation. Use a subagent when the work benefits from its own context—for example, reading many files, running a focused investigation, or performing an independent review.

---

## A sensible setup order

1. Add a short `CLAUDE.md` with the project facts and validation commands.
2. Add `.mcp.json` only for tools the team actually needs.
3. Start `.claude/settings.json` with editor schema validation and conservative permissions.
4. Turn repeated procedures into skills one at a time.
5. Add specialist agents when context isolation or independent review has a clear benefit.

## Verify the setup

Open Claude Code in the project and check:

```text
/memory
/mcp
/permissions
/skills
/agents
```

Then run one harmless test for each layer:

- ask Claude to summarize the project rules;
- call one read-only MCP tool;
- inspect active permissions;
- invoke the example skill; and
- ask the example agent for a read-only review.

Commit the setup only after you understand and trust every shared setting, hook, server, skill, and agent definition.

## Official sources

- [How Claude remembers your project](https://code.claude.com/docs/en/memory)
- [Claude Code settings](https://code.claude.com/docs/en/settings)
- [Configure permissions](https://code.claude.com/docs/en/permissions)
- [Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp)
- [Extend Claude with skills](https://code.claude.com/docs/en/slash-commands)
- [Create custom subagents](https://code.claude.com/docs/en/sub-agents)
- [Automate workflows with hooks](https://code.claude.com/docs/en/hooks-guide)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
