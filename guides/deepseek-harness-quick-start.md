[← Back to the guide directory](../README.md)

# Run DeepSeek Harness Locally

DeepSeek Harness is an open-source agent harness: the layer around an AI model that manages capabilities such as tools, memory, sessions, storage, sandboxes, scheduling, and the agent loop.

This guide launches its local Web UI, connects a model, selects a safe workspace, and runs a first test.

> **Last verified:** 29 August 2026<br>
> **Works with:** The DeepSeek Harness developer preview and its Node.js-based local Web UI.

## What makes the harness different?

An AI model generates responses. A harness gives that model a working environment.

| Layer | Responsibility |
|---|---|
| Model | Reasoning and generating responses |
| Harness | Tools, files, memory, permissions, sessions, storage, scheduling, and the loop that decides what happens next |

DeepSeek Harness uses an “everything is a plugin” architecture. Models, tools, skills, sessions, sandboxes, storage, loops, scheduling, and even the UI can be swapped or extended through plugins and configuration.

It also records agent runs in an append-only session log. The Trajectory view can show system prompts, reasoning, tool calls and results, subagent scheduling, and context injection from the same event stream.

## Before you run it

DeepSeek Harness is currently a **developer preview**. Its maintainers explicitly warn that compatibility-breaking changes will happen.

Start safely:

1. Use a disposable test project—not important or production code.
2. Commit or back up the project before giving an agent write access.
3. Remove secrets, credentials, customer data, and private files from the workspace.
4. Review permission prompts before allowing commands or file changes.
5. Read DeepSeek's current [safety notice](https://github.com/deepseek-ai/deepseek-harness/blob/master/SAFETY.md).

You will need:

- [Node.js](https://nodejs.org/) with `npm` and `npx` available;
- a model-provider credential, such as a [DeepSeek API key](https://platform.deepseek.com/); and
- a local folder the agent may safely inspect and modify.

Check that Node.js and npm are available:

```bash
node --version
npm --version
```

## 1. Create a disposable workspace

Make a small test folder or use a throwaway copy of an existing project:

```bash
mkdir deepseek-harness-test
cd deepseek-harness-test
git init
```

Add a harmless file so the first task has something to inspect:

```bash
printf '# DeepSeek Harness test\n' > README.md
git add README.md
git commit -m "Create disposable test workspace"
```

Git may ask you to configure your name and email before the first commit. The important part is having a known-good checkpoint before allowing edits.

## 2. Launch the Web UI

From inside the test workspace, run the official quick-start command:

```bash
npx @deepseek-ai/dsh web
```

The Web UI is served at:

```text
http://127.0.0.1:3080
```

For a normal local launch, DeepSeek Harness opens the UI in your default browser. Keep the terminal process running while you use it.

To start the server without opening a browser automatically:

```bash
npx @deepseek-ai/dsh web --no-open
```

## 3. Configure a model

In the Web UI:

1. Open **Settings → Models**.
2. Select the DeepSeek provider.
3. Enter your DeepSeek API key.
4. Save the configuration.

The model becomes available without restarting the server.

DeepSeek documents its API keys as write-only in the UI. The credential is stored in `$DSH_HOME/.credentials.yaml`; the regular settings file keeps a reference rather than the literal key.

To use another provider, choose **Add provider** and select an installed catalog provider such as Anthropic or OpenAI. Custom gateways and providers with native authentication have additional requirements, so follow the current [model-provider guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md) instead of assuming every service accepts only an API key.

## 4. Select the workspace

The `dsh` process uses the directory where you launched it as its default filesystem location, but a fresh Web UI still needs an explicitly selected workspace.

1. Click **Choose workspace**.
2. Add the test directory where you ran `dsh`.
3. Select that workspace.

If the session composer is unavailable, check the workspace selection first.

## 5. Run a safe first task

Begin with a read-only request:

```text
Summarize this repository, list its files, and explain what each file appears to do.
Do not edit files or run commands that change the workspace.
```

Check that the answer matches the actual folder. Review the run and any requested permissions before trying a write.

Then use one small, reversible task:

```text
Add a short “Purpose” section to README.md explaining that this is a disposable
DeepSeek Harness test. Show me the proposed text before editing the file.
```

After the edit:

```bash
git diff
```

Only move to a real repository after you understand which tools, permissions, model, and workspace the session is using.

## First-test checklist

- [ ] The workspace is disposable or backed up.
- [ ] The folder contains no secrets or private data.
- [ ] A model is configured under **Settings → Models**.
- [ ] The intended workspace is selected.
- [ ] The first prompt is read-only.
- [ ] Permission prompts are reviewed instead of accepted automatically.
- [ ] File changes are inspected with `git diff`.
- [ ] Plugins are changed one at a time only after the default setup works.

## Run from source

If you want to inspect or contribute to the full codebase, use the official repository workflow:

```bash
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
pnpm dsh web
```

`pnpm run build` prepares the repository artifacts. The final command runs those built artifacts without rebuilding them.

Use the `npx` quick start if you only want to try the product. Clone the repository when you specifically need the source, development documentation, or plugin internals.

## Troubleshooting

### The browser does not open

Open `http://127.0.0.1:3080` manually. For remote or SSH sessions, the command may only print the host URL because your SSH client or editor controls port forwarding.

### The composer is disabled

Choose and select a workspace. A fresh UI does not select one automatically.

### `MISSING_CREDENTIAL`

Open **Settings → Models**, store the provider credential, and try again.

### `UNKNOWN_MODEL`

Select a configured model or add the missing model to the provider.

### Model discovery returns `401`

Check the API key. Some custom endpoints do not implement model discovery, in which case their models must be entered manually.

### A command or plugin stops working after an update

Check the official repository and documentation. DeepSeek Harness is a developer preview, so plugin APIs, commands, and configuration may change.

## Official sources

- [DeepSeek Harness product page](https://www.deepseek.com/harness/en/)
- [DeepSeek Harness GitHub repository](https://github.com/deepseek-ai/deepseek-harness)
- [Web UI guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md)
- [Model-provider guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md)
- [DeepSeek Harness documentation](https://deepseek-harness.github.io/deepseek-harness/)

---

If this guide helped, star the repository and share it with another builder.

Created by [Grayson Ho](https://github.com/graysonhyc).
