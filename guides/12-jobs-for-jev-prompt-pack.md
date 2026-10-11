# 12 Jobs for Jev: the prompt and resource pack

**Status:** companion guide for the YouTube video "12 Jev use cases" (October 2026). The prompts match the PDF shown in the video. Model names, features and pricing change, so check TypeSafe's docs before you estimate a workflow.

Jev is TypeSafe's decision model. It doesn't write sentences. You give it a question and the answers it's allowed to give, and it returns a choice, a score or a yes/no, with a confidence. Your own code decides what happens next.

Each prompt below is a brief you can paste into Claude Code, Codex or another coding agent. Swap the bracketed examples for your own categories, files and rules.

📄 **Prefer the designed version?** [Download the 15-page PDF](12-jobs-for-jev.pdf).

## How to use this pack

1. **Define** the decision and the allowed answers.
2. **Set a fallback** for when confidence is low.
3. **Review** real examples before you automate any action.

- **Use the prompt as a brief.** Ask your agent to show its plan, the files it changed and its tests before it runs anything consequential.
- **Keep the decision bounded.** Give Jev a fixed set of labels or a defined scale. Keep the action in ordinary code.
- **Keep a person in the loop.** Choose a confidence threshold and make uncertain or high-impact cases easy to review.
- **Bring your own data.** Start with a small, permissioned test set. The prompts contain no sample results.

---

## Easy

### 01 · Triage customer enquiries

Route routine messages quickly, and make uncertain ones easy for a person to catch.

```text
Build an automation where every incoming enquiry is sent to Jev to pick one of: billing, bug, question. Return the category and confidence. If confidence is under 60%, route it to a person; otherwise route it automatically.
```

- **Bring:** a permissioned set of sample enquiries, three labels, and the inbox or queue you want to route into.
- **Keep it bounded:** start in preview mode. Keep the under-60% path human-reviewed, and log the label and confidence.
- **First test:** one clear billing request and one ambiguous message. Check the uncertain one stays with a person.
- **Resources:** [Jev question primitives](https://docs.typesafe.ai/primitives) · [models and pricing](https://docs.typesafe.ai/models)

### 02 · Screen CVs against must-haves

Apply a defined checklist consistently, then leave hiring decisions to a person.

```text
Here are the CVs in applications/ and the job description. For each CV, ask Jev yes/no on my must-haves: [years of experience, tools used], then score fit 1–5. Rank the ones that pass, and draft a personalised email or message for the top 5 only.
```

- **Bring:** a real job description, a small set of CVs you're authorised to process, and job-related must-haves.
- **Keep it bounded:** no protected characteristics or proxies for them. Don't auto-reject or contact candidates; a person reviews before any hiring action.
- **First test:** one CV that meets the must-haves and one that misses a job-related requirement. Have a person review both.
- **Resources:** your organisation's hiring policy and privacy guidance.

### 03 · Categorise rows in Google Sheets

Turn a free-text column into one of the categories you keep in a Config sheet.

```text
Build me a Google Sheets add-on. When I add a column whose heading matches a category set in a Config sheet (e.g. Expense category: groceries, transport, subscriptions, rent, other), call Jev for every row with that row's text and the category set, and write the chosen category into the row.
```

- **Bring:** a copy of the spreadsheet with a Config tab, a text column and a destination column.
- **Keep it bounded:** add a preview or undo path. Never overwrite the source text, and report rows with no confident match.
- **First test:** one obvious category, one borderline row and one blank cell. Check the source text is untouched.
- **Resources:** [Google Apps Script for Sheets](https://developers.google.com/apps-script/guides/sheets) · [Jev question primitives](https://docs.typesafe.ai/primitives)

### 04 · Sort your Downloads folder

Classify files into a known set of folders, then move them only after you approve the plan.

```text
Look at every file in ~/Downloads. Use Jev to pick one folder for each from: Invoices, Receipts, Contracts, Screenshots, Photos, Videos. Move each file into its folder.
```

- **Bring:** a test copy of the folder and a fixed list of destination folders.
- **Keep it bounded:** produce a dry-run table first. Don't delete or overwrite, and ask before moving anything outside the test copy.
- **First test:** three copied files, two of them with the same filename. Check nothing is overwritten.
- **Resources:** your operating system's file permissions and your backup.

### 05 · Tag competitor ads

Build a structured swipe file from ads you're allowed to review.

```text
For ads I have manually saved or am authorised to access, ask Jev to choose a hook type, offer and angle from my tag lists. Save the tags and the source URL beside each ad in a database.
```

- **Bring:** a small set of ads you collected by hand, their source URLs, and fixed tag lists.
- **Keep it bounded:** don't scrape the Meta Ad Library without permission. Keep the advertiser and source link with every record.
- **First test:** a handful of hand-collected ads. Check every tag sits beside its source link and can be corrected.
- **Resources:** [Meta Ad Library](https://www.facebook.com/ads/library) (check its access rules first)

---

## Intermediate

### 06 · Search notes and B-roll by meaning

Match a query to a paragraph or a clip description even when the exact words differ.

```text
Build a search tool over my notes and my B-roll library. Split notes into paragraphs; for clips use the description. When I type a query, ask Jev which candidate matches best and open it.
```

- **Bring:** a folder of notes, a clip manifest with written descriptions, and a query box.
- **Keep it bounded:** only return a candidate from the supplied list. Show the source filename, and let me choose when the match is uncertain.
- **First test:** search for an idea your notes describe in different words. Check it opens the exact paragraph or clip.
- **Resources:** [Jev Choice questions](https://docs.typesafe.ai/primitives) · your own B-roll manifest

### 07 · Filter before the big model

Make a cheap relevance decision before you send a big pile of material to an agent.

```text
Before Claude reads any new transcript in creator-references-library/, ask Jev yes/no: is this reel on-topic for my channel? Only pass the yeses to Claude.
```

- **Bring:** a local reference library, your channel's relevance criteria, and a review folder for uncertain items.
- **Keep it bounded:** don't send private or unlicensed material to a third party. Save enough context for a person to audit each decision.
- **First test:** one relevant transcript and one clearly unrelated one. Check only the relevant one reaches the larger agent.
- **Resources:** [TypeSafe developer docs](https://docs.typesafe.ai/introduction)

### 08 · Route skills and models

Pick from the tools you already have installed, instead of making an agent read a long list every time.

```text
Write a Claude Code hook that runs on every prompt. Send the prompt and my skill names and descriptions to Jev and ask it to pick one skill. Then make a /jev command that asks Jev to choose the model: Haiku for simple jobs, Opus for hard ones.
```

- **Bring:** an up-to-date list of installed skill names and descriptions, and the model aliases you can use.
- **Keep it bounded:** only accept names from the list. Add a safe default for uncertain answers, and keep the final choice visible and reversible.
- **First test:** a simple task, a hard task and an unfamiliar prompt. Check the unfamiliar one falls back to the safe default.
- **Resources:** [Jev Choice questions](https://docs.typesafe.ai/primitives) · TypeSafe's [skill-suggestion cookbook](https://docs.typesafe.ai/cookbooks/skill_suggestion)

---

## Advanced

### 09 · Build a feed slop filter

A starter for the yes/no pattern behind the community projects in the video.

```text
Build a browser extension that evaluates each visible post against my written "AI slop" criteria. Ask Jev to choose "slop" or "keep" only. If it chooses "slop" above my confidence threshold, collapse the post; otherwise leave it visible. Include an obvious per-post undo and a global pause switch.
```

- **Bring:** your own definition of "slop", a test feed or posts you have permission to use, and a confidence threshold.
- **Keep it bounded:** keep filtering reversible. Don't hide posts because of who wrote them or their viewpoint.
- **First test:** two permitted posts, one that matches your criteria and one that doesn't. Check undo and pause work.
- **The projects in the video** (credit the builders and use their originals):
  - AI slop filter by Robin Bilgil: [x.com/RBilgil/status/2100976648552169805](https://x.com/RBilgil/status/2100976648552169805)
  - Unclutter by Kitze: [x.com/thekitze/status/2100595129874817340](https://x.com/thekitze/status/2100595129874817340) · [github.com/kitze/unclutter](https://github.com/kitze/unclutter)
  - A live BS meter by Chetaslua: [x.com/chetaslua/status/2100473581251748216](https://x.com/chetaslua/status/2100473581251748216)
  - json-render + Jev by Chris Tate: [x.com/ctatedev/status/2101022101750571357](https://x.com/ctatedev/status/2101022101750571357)

### 10 · Design a smarter task app

Suggest a tag and an urgency as someone types, using only the tags they've chosen.

```text
Build a small to-do app. As the user types a task, send the text and my tag list [Finance, Clients, Content, Admin, Personal] to Jev to pick one tag, and ask Jev yes/no: is this urgent? Update the tag and priority live.
```

- **Bring:** a small task app, a fixed tag list and a clear definition of "urgent".
- **Keep it bounded:** show suggestions as editable. An uncertain urgency score shouldn't change deadlines or send notifications.
- **First test:** one task with an obvious tag and urgency, then an ambiguous one. Check the suggestions stay editable.
- **Resources:** [Jev Choice and yes/no questions](https://docs.typesafe.ai/primitives)

### 11 · Pick B-roll for each line

Decide whether a line needs a cutaway, then pick a clip from a described library.

```text
For each sentence in transcript.md, ask Jev yes/no: does this line need B-roll? If yes, ask Jev to choose the best clip from b-roll-manifest.json by its description. Flag anything under 70%.
```

- **Bring:** a transcript, a B-roll manifest with useful descriptions, and a confidence threshold.
- **Keep it bounded:** never invent a clip. Flag uncertain matches for a person, and keep the spoken line correctly timed.
- **First test:** one line that clearly needs a visual, one that doesn't, and one in between. Check every chosen clip exists in the manifest.
- **Resources:** your own transcript and manifest. Check the rights to every clip.

### 12 · Choose an editing effect

Pick a known effect for each line, or explicitly pick none.

```text
Run npx hyperframes catalog --json to get the effect list. For each sentence in transcript.md, ask Jev to pick one effect from that list (or "none"). Apply the picks and build the HyperFrames composition.
```

- **Bring:** the current effect catalogue, a transcript aligned to its video, and a short list of visual rules for your channel.
- **Keep it bounded:** check every effect name against the current catalogue. Use "none" when an effect doesn't help, and review the edit before rendering.
- **First test:** one line with a number, one describing a UI, and one plain line. Check every chosen effect exists.
- **Resources:** run `npx hyperframes catalog --json` locally · [Jev Choice questions](https://docs.typesafe.ai/primitives)

---

## Resource shelf

- [TypeSafe developer docs](https://docs.typesafe.ai/introduction): Jev concepts, API setup and integration guides
- [Questions and primitives](https://docs.typesafe.ai/primitives): Choice, Score and yes/no patterns
- [Models and pricing](https://docs.typesafe.ai/models): check current names and rates before estimating a workflow
- [TypeSafe's launch post](https://typesafe.ai/blog/introducing-system-one-models-and-jev): how TypeSafe describes System One decision models
- [Google Apps Script guides for Sheets](https://developers.google.com/apps-script/guides/sheets)
- [Meta Ad Library](https://www.facebook.com/ads/library): use it by hand or through an approved access path
- [OpenAI Decisions API](https://developers.openai.com/api/docs/guides/decisions): OpenAI's related typed-decision API

The speed and cost figures quoted in the video ("up to 200× faster, 400× cheaper") are TypeSafe's own claims, based on its System One workflows. Measure on your own data before you rely on them.
