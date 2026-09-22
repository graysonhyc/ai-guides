[← Back to the guide directory](../README.md)

# Open Design: Quick Start for the Open-Source Claude Design Alternative

Open Design is a free, open-source AI design workspace that looks and feels like Claude Design. It runs as a local-first desktop app, drives the coding agents you already have installed, and gives you an interactive canvas where you keep prompting and refining until the design is exactly what you want.

> **Last verified:** 22 September 2026, against the official README and quickstart.
>
> **Licence:** Apache-2.0. Bundled templates and skills keep their own licences (mostly MIT).

## Official links

- Website and downloads: [open-design.ai](https://open-design.ai)
- Source and releases: [github.com/nexu-io/open-design](https://github.com/nexu-io/open-design)
- Quickstart: [open-design.ai/quickstart](https://open-design.ai/quickstart/)

Product access, model support and limits can change. If anything below disagrees with the README, the README wins.

## 1. Install it

Pick one route.

### Desktop app (easiest)

Download the macOS or Windows build from [open-design.ai](https://open-design.ai) or the GitHub Releases page, open it, and connect a coding agent when prompted.

### From source

You need Node.js 24 (Node 22 is not supported), pnpm through Corepack, git, and at least one coding agent installed (Claude Code, Codex, Cursor, Gemini CLI, OpenCode or Qwen).

```bash
git clone https://github.com/nexu-io/open-design
cd open-design
corepack enable && pnpm install
pnpm tools-dev
```

`pnpm tools-dev` starts the daemon and the web interface. Generate a first artifact from the web UI, or from the terminal:

```bash
od skill run open-design-landing --output ./artifact.html
```

### Docker

```bash
git clone https://github.com/nexu-io/open-design.git
cd open-design/deploy
cp .env.example .env
echo "OD_API_TOKEN=$(openssl rand -hex 32)" >> .env
docker compose up -d
```

## 2. Connect your agent and models

Open Design works through the coding agents on your machine, so it uses whatever login or key those agents already have. Register it with the agent you use:

```bash
od mcp install claude    # or: codex, cursor, copilot, hermes, kimi, cline …
```

For model endpoints it accepts any OpenAI-compatible endpoint with your own key (BYOK), with presets for OpenAI, Azure OpenAI, Google Gemini, Ollama and LM Studio. That is how you run it against a local model at no API cost. Credentials live in `.od/media-config.json`; the `/agents/` docs list every supported agent.

## 3. What you can make

- Web, desktop and mobile prototypes (HTML)
- Live dashboards and artifacts
- Multi-slide presentations (deck mode)
- Documents, including multi-page
- Images (through the image models you connect)
- Motion graphics rendered from HTML to MP4

Exports: HTML, PDF, PPTX, ZIP, Markdown and MP4.

## 4. Work the canvas

1. Describe the screen, deck or site you want and pick a design system (the app ships with a large library).
2. Select any element on the canvas, leave a comment or a change request, and send it back to the agent.
3. Repeat until it matches what you pictured, then export.

## Keep it honest

- This is a third-party open-source project. Read its README, licence and the permissions your agent asks for before pointing it at sensitive work.
- "Free" means the software: agents and cloud models you connect may still bill you. Local models through Ollama or LM Studio avoid that.
- Check the README for the current agent list and model presets; they move quickly.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
