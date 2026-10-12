# REA: let Claude Code reverse engineer an app feature, with evidence

**Status:** companion guide for the "REA" short (October 2026). Facts were checked against REA's README, its website and the GitHub API on 12 October 2026. REA releases often, so check the README before relying on a command.

REA ("Reverse Engineer Anything") is a free, open-source MCP server and agent skill. It lets a coding agent such as Claude Code or Codex inspect an app without its source code, explain how a feature works, show the evidence behind each conclusion, and build a version for your own project. Analysis runs locally.

## Links

- [REA on GitHub](https://github.com/morluto/rea): README, install, supported agents, and the "What you can analyze" table
- [rea.tools](https://rea.tools/): guides and case studies
- [Showcases](https://rea.tools/showcase/): how Notion copies text and HTML (Electron), DX-Ball's sound-pan calculation (a 1996 Windows game), an Android authenticator, a CTF flag checker
- [Disclaimer](https://github.com/morluto/rea/blob/main/DISCLAIMER.md): responsible-use rules

## What's true

| Claim in the video | What the source says |
| --- | --- |
| Free, 145K+ stars | MIT licence. 145,774 stars on 12 October 2026 (GitHub API). |
| An MCP server plus a skill | Setup adds REA's MCP server and matching workflow instructions to your agent. The skill is published as `reverse-engineer-anything`. |
| Claude Code or Codex | Also Cursor, Gemini CLI, Grok Build and others (see the README's supported agents). |
| Desktop apps, Electron apps, websites | Plus .NET assemblies, Android APKs, firmware and more. Static JavaScript and .NET inspection need no extra tools. |
| Drives a decompiler like Hopper | Native binaries need Hopper, Ghidra or IDA. Setup can install the Hopper demo with your approval. Commercial tools need their own licence. |

## Setup

### 0. Check Node.js

REA needs Node.js 22.x (22.19 or later), 24.x (24.11 or later), or 26+, plus npm.

```bash
node -v
```

### 1. Run the setup command

```bash
npx rea-agents setup
```

Pick your agents (for example Claude Code and Codex), review the proposed changes, and approve them. Setup backs up your existing configuration. Restart your agent afterwards.

For native apps, let setup install the Hopper demo, or point REA at an existing Hopper, Ghidra or IDA installation. You can skip this if you only analyse JavaScript or Electron apps and websites.

To update later:

```bash
npx rea-agents@latest setup
```

### 2. Ask your agent

REA's own example prompt:

```text
Understand how search works in the Notes app, show me the evidence, and build a
similar feature for my project.
```

My starter prompt adds the structure that makes the answer checkable:

```text
Use REA to investigate <APP> (at <PATH>). I own it or I'm allowed to examine it.

1. Work out how <FEATURE> works. Start from the app itself; don't guess from its
   website or documentation.
2. For every claim, show the evidence: the file, symbol or address, and what it
   proves.
3. List anything you couldn't confirm as an open question instead of filling the gap.
4. Then build a minimal version of <FEATURE> for my project in <STACK>, with tests,
   and say which parts follow the evidence and which are your own design.
```

### 3. Check what comes back

- **How it works:** a plain-English explanation of the feature's flow.
- **Where it found each piece:** file paths, offsets or addresses you can open yourself. In the Notion case study, REA points to `preload.js:1:22764–22828` for the exposed clipboard API.
- **Your version:** code for your project. Read it like any other agent output, and run the tests.

### Terminal only (no agent)

```bash
npx -y rea-agents@latest analyze-javascript-application /absolute/path/to/app --json
```

## One rule

Only point REA at software you own or are authorised to examine. REA's disclaimer limits it to lawful research, education, interoperability, software preservation, and analysis of software you own or are authorised to examine. Use licensed copies of commercial tools such as Hopper or IDA.
