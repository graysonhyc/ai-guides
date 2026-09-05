[← Back to the guide directory](../README.md)

# Grok Bot: Night Shift briefing and an AI agent team

Build the workflow from my video: a morning AI briefing, followed by a Researcher → Writer → Reviewer team that leaves a draft for you to approve.

> **Last verified:** 5 September 2026
>
> **Works with:** Grok Bot. This is Grayson Ho’s practical setup guide, with original example prompts and links to the official documentation.

## 1. Install and sign in

Use the download link in the [official getting-started guide](https://docs.x.ai/grok-bot/get-started). Check its current account eligibility before installing. Open Grok Bot and complete the Cursor sign-in flow. You do not need to connect email or social accounts for the public-news example below.

## 2. Create Night Shift

Choose **New → Create new agent** in the sidebar. Open **Bot actions → Edit Profile** and name the Bot **Night Shift**. Give it this description:

```text
Prepare a concise morning AI-news briefing using public sources.
Use UK English, preserve original source links, and distinguish verified facts from uncertainty.
Keep results in this conversation for my review. Never send emails or publish content without my explicit approval.
```

Open the Bot from the sidebar to give it a task. The recording shows a Bot labelled “AI News Reporter” whose conversation also refers to Night Shift; use whichever name you choose consistently in your own setup. [Official Bot setup](https://docs.x.ai/grok-bot/bots).

## 3. Run the briefing once

Paste this original prompt:

```text
Prepare an AI-news briefing for the previous calendar day in Europe/London time.

Use TechCrunch, Hacker News, OpenAI’s official news and Anthropic’s official news as starting points. Follow Hacker News submissions to the original source.

Choose up to five useful stories for creators and founders. Remove duplicates. Open each original article and check its headline, publication date and supporting facts. Include only stories whose date falls in the requested calendar day. If a date or claim cannot be verified, omit it and explain the gap briefly. Never invent a story or URL.

Return an email-style briefing: a subject line, the covered date, and numbered stories. Each story needs a headline, one sentence explaining why it matters, and the original source link. Keep the body under 300 words. Fewer verified stories are better than filling the list.

Keep the briefing in this conversation. Save the briefing and research notes as dated files on the cloud computer and tell me their paths. Do not send an email or publish anything.

Run this once now. Do not create a recurring schedule yet.
```

Read the output and open the links yourself. Check the covered date, duplicates and whether the summaries match the articles. Open **Agent Computer** from the conversation to inspect the saved files. Access that needs a login should use the takeover flow so you enter credentials yourself. [Getting started and reviewing results](https://docs.x.ai/grok-bot/get-started).

## 4. Schedule the checked workflow

Once the one-time result is useful, ask:

```text
Save the briefing process we just checked as a reusable skill.
Create a routine owned by Night Shift to run it every day at 07:00 Europe/London.
Keep the previous-calendar-day requirement and the review-only output.
If a source is unavailable, report that limitation; do not reuse yesterday’s briefing as new work.
Show me the saved schedule, timezone and next run.
```

Confirm the owner, timezone and next run in the routine settings. Use **Test run** and check its result before relying on the schedule. A 7 a.m. schedule starts the work then; it does not guarantee the completed briefing will be ready at exactly 7 a.m. Set an earlier start if that is your deadline.

Routines can run while your laptop is closed. They still depend on available access and successful runs. [Official routines guide](https://docs.x.ai/grok-bot/skills-routines-and-automations).

## 5. Add the three-Bot team

Create three Bots using the same sidebar flow. These are suggested role descriptions you can adapt:

| Bot | Description |
|---|---|
| Researcher | Select one useful AI story from the verified briefing. Reopen the original source and hand Writer the facts, date, links and uncertainties. Do not write unsupported claims. |
| Writer | Turn Researcher’s evidence into a LinkedIn draft of no more than 150 words for creators and founders. Use plain UK English. Keep claims within the evidence and pass the draft to Reviewer. Do not publish. |
| Reviewer | Reopen the cited sources and check each factual claim, date and product limitation. Return corrections to Writer when needed. Leave the checked draft, supporting links and unresolved questions for Grayson. Do not publish. |

Choose **New** in the sidebar and select the three Bots for a group chat. Send this kickoff:

```text
Work together on one draft based on today’s verified AI-news briefing.
Researcher owns the evidence handoff to Writer. Writer owns the draft handoff to Reviewer.
Reviewer checks the claims against the sources and requests corrections if needed.
Keep the handoffs in this group with the author visible. Leave the checked draft and source links here for my approval. Do not publish or send external messages.
Start with Researcher. Ask me for the briefing if you cannot locate it.
```

Use an `@` mention when you need to assign the next step explicitly. Watch for actual handoffs and checks rather than accepting a statement that the team has finished. [Official collaboration guide](https://docs.x.ai/grok-bot/chat-and-collaboration).

## 6. Keep the shared computer in mind

The Bots share one cloud computer, including files and signed-in sessions. Different Bot names do not isolate their access. Connect only the services needed for this workflow, and keep external sending, publishing and other consequential actions behind approval. [Shared-computer overview](https://docs.x.ai/grok-bot/overview) and [approval controls](https://docs.x.ai/grok-bot/approvals-security-and-privacy).

## Before you leave it running

- Check one complete briefing and one complete team handoff.
- Verify that original links support the final draft.
- Confirm the routine’s timezone and next run.
- Confirm outputs stay in the conversation until you approve an external action.
- Check recent run history if a briefing is missing; fix access or source failures before retrying.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
