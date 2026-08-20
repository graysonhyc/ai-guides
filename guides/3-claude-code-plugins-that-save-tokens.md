[← Back to the guide directory](../README.md)

# 3 Claude Code Plugins That Save Tokens

Three community-built tools that target three different sources of Claude Code token waste: long replies, unnecessary code, and oversized context.

> **Last verified:** 20 August 2026
>
> **Works with:** Claude Code. Caveman and Ponytail also support several other coding agents; Headroom can sit in front of multiple agent and LLM clients.

## The three tools at a glance

| Tool | What it changes | Best for |
|---|---|---|
| [Caveman](https://github.com/JuliusBrussee/caveman) | Makes the agent's prose shorter while preserving code, commands, errors, and technical details | Cutting verbose output |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | Pushes the agent towards the smallest safe implementation that fulfils the task | Avoiding over-engineered code |
| [Headroom](https://github.com/headroomlabs-ai/headroom) | Compresses large tool results and other context before model calls | Working with logs, JSON, search results, and large codebases |

These tools work at different points in the flow:

```text
Large inputs and tool results ── Headroom ──> Claude ── Ponytail ──> Less code
                                              └── Caveman ───────> Shorter prose
```

They are third-party projects, not official Anthropic plugins. Review their source, hooks, dependencies, licences, and requested access before installing them.

---

## 1. Caveman — make Claude say less

Caveman changes how the agent communicates. It removes filler, repetition, long introductions, and unnecessary explanation but keeps technical content intact.

This mainly reduces **output tokens**. Use it when Claude reaches the right answer but spends too many tokens narrating the work.

### Install the Claude Code plugin

Enter these as two separate prompts inside Claude Code:

```text
/plugin marketplace add JuliusBrussee/caveman
```

```text
/plugin install caveman@caveman
```

If Claude Code asks you to reload the plugin, run:

```text
/reload-plugins
```

### Choose an intensity

Start with the lightest mode:

```text
/caveman lite
```

The available modes are:

| Mode | Behaviour | Good use case |
|---|---|---|
| `lite` | Removes filler but keeps natural sentences | Everyday development |
| `full` | Uses shorter sentences and fragments | Focused coding sessions |
| `ultra` | States each fact once with minimal prose | Small, familiar tasks |

If Claude Code displays namespaced plugin commands, use `/caveman:caveman lite` instead.

Turn it off when you need polished documentation, careful teaching, or nuanced communication:

```text
/caveman off
```

You can inspect local usage and estimated savings with:

```text
/caveman-stats
```

### Try it

```text
/caveman lite

Find the cause of this failing test, make the smallest safe fix, and report the
cause, changed files, and verification result.
```

**Best time to use it:** routine implementation, debugging, and code review where concise status updates are enough.

**Skip it for:** user-facing copy, detailed tutorials, high-stakes explanations, or any task where tone and context matter more than brevity.

> Caveman also offers a separate local proxy for reducing input tokens. This guide uses the lighter Claude Code plugin so that each tool has one clear job.

---

## 2. Ponytail — make Claude build less

Ponytail changes what the agent builds. Before adding code, it works down this ladder:

1. Does this need to exist?
2. Does the codebase already contain it?
3. Can the standard library handle it?
4. Is there a native platform feature?
5. Is a suitable dependency already installed?
6. Can one line solve it safely?
7. Only then, write the minimum new implementation.

The goal is not code golf. Ponytail explicitly preserves necessary validation, security, accessibility, error handling, and data-loss protection.

### Install the Claude Code plugin

Ponytail's automatic activation uses small Node.js lifecycle hooks, so make sure `node` is available on your system path.

Enter these as two separate prompts inside Claude Code:

```text
/plugin marketplace add DietrichGebert/ponytail
```

```text
/plugin install ponytail@ponytail
```

Run `/reload-plugins` if Claude Code asks you to activate the new plugin.

### Use it

Ponytail defaults to its `full` mode. You can switch modes explicitly:

```text
/ponytail lite
/ponytail full
/ponytail ultra
```

If namespaced commands are shown, use `/ponytail:ponytail full`.

Turn it off with:

```text
/ponytail off
```

or tell Claude `stop ponytail`.

### Try it

```text
/ponytail full

Add a date field to this form. Inspect the existing stack first. Reuse native
features or installed dependencies where they satisfy the requirements. Preserve
validation and accessibility. Show me the final diff and verification result.
```

For an existing change that feels overbuilt, run:

```text
/ponytail-review
```

Ponytail also includes `/ponytail-gain`, which reports its measured effect. Treat the project's published savings as vendor benchmarks, not a guarantee for your codebase or model.

**Best time to use it:** feature work, refactors, scripts, and internal tools where agents tend to introduce new abstractions or dependencies too early.

**Skip it for:** tasks whose explicit goal is extensible architecture, framework design, or a production abstraction that has already been justified. Even then, it can still be useful as a review pass.

---

## 3. Headroom — make Claude read less

Headroom targets **input tokens**. It can compress structured data, logs, tool output, retrieved documents, and conversation context before they reach the model. It keeps a local copy of the original content so the agent can retrieve exact details when needed.

Headroom is different from the first two tools: it is a local proxy and MCP integration rather than a simple marketplace skill.

### Install it

The recommended installation uses [`uv`](https://docs.astral.sh/uv/) to keep the Python CLI in its own environment:

```bash
uv tool install --python 3.13 "headroom-ai[all]"
```

Headroom requires Python 3.10 or later. The npm package is a TypeScript SDK and does **not** install the `headroom` command.

### Launch Claude Code through Headroom

From the project you want to work on, run:

```bash
headroom wrap claude
```

The wrapper starts the local proxy and launches a Claude Code session routed through it. Use the wrapper whenever you want Headroom active.

By default, the wrapper can also register Serena for semantic code navigation. If you only want compression, launch it without the added code-memory integration:

```bash
headroom wrap claude --code-memory none
```

Verify that traffic is actually passing through Headroom:

```bash
headroom doctor
```

To inspect performance and savings:

```bash
headroom perf
headroom dashboard
```

The dashboard requires the proxy to be running.

### Try it on the right workload

Headroom is most useful when a task would otherwise load a large amount of repetitive or structured context:

```text
Inspect these application logs and JSON exports. Find the first causal error,
trace it to the relevant code path, and keep exact references for any evidence
used in the conclusion.
```

It may provide little benefit when the session only reads a few small source files. Headroom also protects recent or analysis-critical code by default, so do not expect every code block to be compressed.

To remove the durable Claude integration later, run:

```bash
headroom unwrap claude
```

**Best time to use it:** large logs, database results, JSON, broad searches, RAG output, and long codebase investigations.

**Skip it for:** short sessions with small inputs, or environments where a local proxy does not fit your security or network policy.

---

## Recommended setup order

Install one tool at a time and measure it before adding the next. This isolates each tool's effect on your workflow.

1. Install **Caveman** in `lite` mode and compare output length for a few normal tasks.
2. Add **Ponytail** and compare the resulting diff size, dependencies, tests, and correctness.
3. Add **Headroom** when you have an input-heavy task and confirm that the proxy is active.
4. Keep only the tools that produce a measurable improvement without reducing quality.

Caveman and Ponytail usually complement one another: one shortens prose and the other reduces unnecessary implementation. Headroom's proxy can also steer output verbosity, so test it separately from Caveman before combining them.

## A fair way to measure the result

Use the same repository, model, prompt, and starting commit for each comparison.

Record:

- input, cache, and output tokens;
- total cost or plan usage where available;
- files and lines changed;
- new dependencies;
- test and lint results;
- time to completion; and
- whether the answer actually fulfilled the task.

A smaller answer is not a saving if it omits important information. Less code is not a win if it removes required validation. Compressed context is not useful if the agent loses the evidence needed to solve the problem.

## Copy-and-paste installation checklist

Run the first four commands as separate prompts inside Claude Code:

```text
/plugin marketplace add JuliusBrussee/caveman
/plugin install caveman@caveman
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

Then, in your terminal:

```bash
uv tool install --python 3.13 "headroom-ai[all]"
headroom wrap claude --code-memory none
headroom doctor
```

Start conservatively:

```text
/caveman lite
/ponytail full
```

## Troubleshooting

### A plugin installs but is not active

Run `/reload-plugins`, or restart Claude Code. Open `/plugin` and check the **Installed** and **Errors** tabs.

### Ponytail does not activate automatically

Confirm that `node` is available to the non-interactive shell Claude Code uses. You can still invoke the skill manually with `/ponytail`.

### Headroom is installed but the command is missing

Run `uv tool list` and make sure the uv tools directory is on your system path. The npm package does not provide the CLI.

### Headroom shows little or no saving

Confirm the session was launched with `headroom wrap claude`, then run `headroom doctor`. Test it with a genuinely large structured input; small files and recent code may pass through unchanged by design.

## Primary sources

- [Caveman repository and installation guide](https://github.com/JuliusBrussee/caveman)
- [Ponytail repository, behaviour, benchmarks, and installation guide](https://github.com/DietrichGebert/ponytail)
- [Headroom repository and Claude Code wrapper instructions](https://github.com/headroomlabs-ai/headroom)
- [Headroom MCP documentation](https://github.com/headroomlabs-ai/headroom/blob/main/docs/content/docs/mcp.mdx)
- [Anthropic's Claude Code plugin documentation](https://code.claude.com/docs/en/discover-plugins)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
