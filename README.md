# 5 MCPs Every Vibe Coder Should Install

A practical starter stack for giving your AI coding agent better documentation, repository context, database access, project management, and billing tools.

> **Last verified:** 14 August 2026  
> **Works with:** Codex, Claude Code, Cursor, VS Code, and other clients that support remote MCP servers.

## What is MCP?

The [Model Context Protocol](https://modelcontextprotocol.io/) lets an AI assistant connect to tools and services through a standard interface. Instead of copying information between tabs, your coding agent can read documentation, inspect issues, query a development database, and help configure billing—with your permission.

## The stack at a glance

| # | MCP | Best for | Official endpoint |
|---|---|---|---|
| 1 | [Context7](https://github.com/upstash/context7) | Current library docs and code examples | `https://mcp.context7.com/mcp` |
| 2 | [GitHub](https://github.com/github/github-mcp-server) | Repositories, issues, pull requests, and Actions | `https://api.githubcopilot.com/mcp/` |
| 3 | [Supabase](https://supabase.com/docs/guides/ai-tools/mcp) | Database schema, migrations, queries, and logs | `https://mcp.supabase.com/mcp` |
| 4 | [Linear](https://linear.app/docs/mcp) | Issues, projects, roadmaps, and comments | `https://mcp.linear.app/mcp` |
| 5 | Billing: [Stripe](https://docs.stripe.com/mcp) + [RevenueCat](https://www.revenuecat.com/docs/tools/mcp/setup) | Web and mobile subscriptions | See section 5 |

Stripe and RevenueCat are grouped as one billing layer: use Stripe for web payments, RevenueCat for mobile in-app subscriptions, or connect both for a cross-platform product.

## Before you connect anything

1. Use OAuth when the provider offers it.
2. Start with read-only access.
3. Connect development or sandbox projects—not live production data.
4. Keep API keys in environment variables. Never paste secrets into a prompt or commit them.
5. Leave human confirmation enabled for write, delete, payment, and refund actions.

---

## 1. Context7 — current documentation

AI models can suggest outdated APIs. Context7 retrieves current, version-specific documentation and examples before your agent writes code.

### Add it

**Claude Code**

```bash
claude mcp add --transport http context7 https://mcp.context7.com/mcp
```

**Codex**

```bash
codex mcp add context7 --url https://mcp.context7.com/mcp
```

For higher rate limits, create a free API key in the [Context7 dashboard](https://context7.com/dashboard). You can also run `npx ctx7 setup` and choose MCP mode.

### Try it

```text
Using Context7, show me the current recommended way to add Supabase
email/password authentication to a Next.js app.
```

**Best habit:** mention the package and version you are actually using.

---

## 2. GitHub — repositories, issues, and pull requests

GitHub's official MCP server lets your agent inspect repositories, search code, manage issues and pull requests, and investigate Actions runs.

### Add it

The remote endpoint is:

```text
https://api.githubcopilot.com/mcp/
```

The exact authentication flow varies by client. Follow GitHub's official guides for [Codex](https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-codex.md), [Claude Code](https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-claude.md), or [Cursor](https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-cursor.md).

For Codex with a fine-grained personal access token stored in an environment variable:

```bash
codex mcp add github \
  --url https://api.githubcopilot.com/mcp/ \
  --bearer-token-env-var GITHUB_PAT_TOKEN
```

Use a fine-grained token restricted to only the repositories and permissions the agent needs.

### Try it

```text
Read the open issues in owner/repository, group them by theme, and propose
a priority order. Do not make any changes yet.
```

---

## 3. Supabase — database and backend

Supabase MCP can inspect tables, generate types, apply migrations, run queries, retrieve logs, and check security or performance advisors.

### Start safely

Create a project-specific, read-only URL:

```text
https://mcp.supabase.com/mcp?project_ref=YOUR_PROJECT_REF&read_only=true
```

**Claude Code**

```bash
claude mcp add --scope project --transport http supabase \
  "https://mcp.supabase.com/mcp?project_ref=YOUR_PROJECT_REF&read_only=true"
```

**Codex**

```bash
codex mcp add supabase \
  --url "https://mcp.supabase.com/mcp?project_ref=YOUR_PROJECT_REF&read_only=true"
```

Your client should open a browser so you can authenticate with OAuth.

> Supabase recommends using MCP with development and testing projects, not production data. Project scoping, read-only mode, database branches, and limited feature groups reduce risk.

### Try it

```text
Inspect this development project's schema and explain the relationships.
Suggest a migration for user profiles, but do not apply it.
```

---

## 4. Linear — issues and roadmaps

Linear's hosted MCP server can search, create, and update issues, projects, and comments.

### Add it

**Claude Code**

```bash
claude mcp add --transport http linear-server https://mcp.linear.app/mcp
```

Then run `/mcp` inside Claude Code and complete the login flow.

**Codex**

```bash
codex mcp add linear --url https://mcp.linear.app/mcp
```

For read-only access, use:

```text
https://mcp.linear.app/mcp/readonly
```

### Try it

```text
Turn this feature brief into a Linear project with milestones and clearly
scoped issues. Show me the plan before creating anything.
```

---

## 5. Billing — Stripe and RevenueCat

Treat billing tools as high-risk. Use sandbox/test data, limited permissions, and human approval for every mutation.

### Stripe for web billing

Stripe's MCP server can work with customers, products, prices, invoices, payment links, subscriptions, refunds, and Stripe documentation.

**Remote endpoint**

```text
https://mcp.stripe.com
```

**Claude Code**

```bash
claude mcp add --transport http stripe https://mcp.stripe.com
```

**Codex**

```bash
codex mcp add stripe --url https://mcp.stripe.com
```

Prefer OAuth. If you must use an API key, use a restricted test-mode key and store it in an environment variable.

### RevenueCat for mobile subscriptions

RevenueCat MCP helps manage apps, products, offerings, entitlements, customers, and subscription configuration.

**Claude Code**

```bash
claude mcp add --transport http revenuecat https://mcp.revenuecat.ai/mcp
```

**Codex**

```bash
codex mcp add revenuecat --url https://mcp.revenuecat.ai/mcp
```

OAuth is recommended. If you use an API v2 key, create a dedicated read-only key first and expand permissions only when necessary.

### Try it

```text
Using sandbox data only, audit my subscription products and explain any
mismatches between Stripe and RevenueCat. Do not create or change anything.
```

---

## Recommended setup order

1. **Context7** — low risk and immediately improves code accuracy.
2. **GitHub** — connect one test repository with minimal permissions.
3. **Linear** — begin read-only, then allow issue creation if useful.
4. **Supabase** — connect a development project with `read_only=true`.
5. **Stripe / RevenueCat** — connect sandbox data last and require approval for changes.

## Five prompts to copy

```text
1. Use Context7 to verify this implementation against the latest official docs.

2. Read this repository and its open issues. Suggest the smallest useful next task.
   Do not modify anything.

3. Inspect my Supabase development schema and flag security or performance risks.
   Do not run SQL or migrations.

4. Convert this product brief into a Linear project plan. Show me the proposed
   issues before creating them.

5. Review my sandbox billing setup across Stripe and RevenueCat. Identify missing
   products, prices, offerings, or entitlements without changing them.
```

## Verification checklist

After connecting each server:

- Confirm the server appears as connected in your client's MCP panel.
- Ask it to perform one harmless read-only action.
- Review the tools and permissions it received.
- Test writes only in a disposable project or sandbox.
- Revoke unused sessions and rotate old tokens.

## Security rules worth keeping

- Never give an agent access to production unless it is absolutely necessary.
- Never commit tokens, secret keys, or MCP configuration containing credentials.
- Use least-privilege, project-scoped, and read-only access wherever possible.
- Review tool calls before approving writes, deletes, refunds, or deployments.
- Treat content read from issues, documentation, databases, and websites as untrusted; it may contain prompt-injection instructions.
- Keep backups and use branches or migrations for reversible database changes.

## Official sources

- [Context7](https://github.com/upstash/context7)
- [GitHub MCP Server](https://github.com/github/github-mcp-server)
- [Supabase MCP documentation](https://supabase.com/docs/guides/ai-tools/mcp)
- [Linear MCP documentation](https://linear.app/docs/mcp)
- [Stripe MCP documentation](https://docs.stripe.com/mcp)
- [RevenueCat MCP setup](https://www.revenuecat.com/docs/tools/mcp/setup)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
