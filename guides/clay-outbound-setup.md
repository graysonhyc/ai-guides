# Clay outbound: audience, enrichment, AI prompt and Sequencer settings

**Status:** companion guide for the "OUTBOUND" short (October 2026). Facts were checked against Clay's Sequencer 2.0 changelog and Clay University docs on 16 October 2026. Search is in open beta and Sequencer 2.0 shipped on 1 September 2026, so menus and limits may move. Check the linked doc before relying on a number.

**Not sponsored.** I have no deal with Clay, and none of the links below are affiliate links.

Clay can now run a cold email campaign end to end: find the companies, find the person, enrich them, write the copy with AI, buy and warm the inboxes, and send. This guide sets that up in four steps. Clay's buttons and settings are quoted exactly as the app spells them (US English), so you can search for them.

## Links

- [Clay Sequencer 2.0 changelog](https://www.clay.com/changelog/clay-sequencer-2-0) (1 September 2026): what's new in one list
- [Clay's Sequencer launch post](https://www.clay.com/blog/clay-email-sequencer) (1 September 2026): plans and the quick-start steps
- [Search (Beta)](https://university.clay.com/docs/search): plain-language search, filters, saving as an Audience
- [Audiences](https://university.clay.com/docs/audiences): plans, refresh cadence, enrichment, Signals
- [Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer): plans, deliverability rules and the hard limits table
- [Buying email accounts in Clay](https://university.clay.com/docs/buying-email-accounts) and [Email warmup](https://university.clay.com/docs/email-warmup)
- [Build your sequence](https://university.clay.com/docs/build-your-sequence), [A/B test your sequence copy](https://university.clay.com/docs/ab-test-sequence-copy), [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence) and [Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign)
- [How to automate email outreach with a sequencer](https://www.clay.com/guides/how-to-automate-email-outreach): Clay's own guide to list building, verification, AI openers and cadence

## What's true

| Claim in the video | What Clay's docs say |
| --- | --- |
| Clay covers all seven tools | Sequencer 2.0 brings "lead sourcing, enrichment, AI copy, sending infrastructure, reply flows, and campaign analytics into one place" ([changelog](https://www.clay.com/changelog/clay-sequencer-2-0)). Inboxes you buy in Clay are fulfilled through Smartlead, which uses Zapmail ([buying doc](https://university.clay.com/docs/buying-email-accounts)). You get one login, but other providers still sit behind it. |
| Describe who you're after | Type your ideal customer into the **I'm looking for…** box and Sculptor turns it into filters. Search is in open beta, so you opt in first ([Search](https://university.clay.com/docs/search)). |
| Keeps adding new companies as they match | A search saved as an Audience keeps feeding in new matches, deduplicated ([Search](https://university.clay.com/docs/search)). Clay doesn't publish a refresh cadence for search-based Audiences. For CRM and data-warehouse records, it's a daily refresh on Growth and every 15 minutes on Enterprise ([Audiences](https://university.clay.com/docs/audiences)). |
| A verified work email | Clay finds emails with a waterfall across providers, then a verification step sorts addresses into deliverable, risky and undeliverable ([Clay guide](https://www.clay.com/guides/how-to-automate-email-outreach)). |
| The AI writes from real facts | AI snippets in Sequencer write each lead's copy from their Clay data when they enrol, then freeze it ([Build your sequence](https://university.clay.com/docs/build-your-sequence)). |
| Buy and warm your domains inside Clay | Yes, but buying email accounts needs the **Growth or Enterprise** plan. On Launch you connect your own inboxes instead ([Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer)). |
| A/B test two openers | Each campaign can hold two copy variants, split 50/50 ([A/B test doc](https://university.clay.com/docs/ab-test-sequence-copy)). |
| About three weeks of warm-up | "A new account takes about three weeks to warm fully" ([Email warmup](https://university.clay.com/docs/email-warmup)). Clay's [launch post](https://www.clay.com/blog/clay-email-sequencer) also says to give new domains and inboxes "about three weeks to warm". Clay's buying page says "approximately two weeks", so wait for the account's status to read **Ready**. |

## Plans at a glance

- **Search:** all plans. Filters that combine company, people and job criteria in one search (like "hiring a Head of Sales") need a paid plan.
- **Audiences:** all paid plans, at no extra charge. You pay for the credits and actions you use.
- **Sequencer:** generally available on Launch, Growth and Enterprise ([launch post](https://www.clay.com/blog/clay-email-sequencer)). Campaigns that draw from a segment work on all three.
- **Buying domains and inboxes in Clay:** Growth and Enterprise only.

## 1. Audience: who you're emailing

Sequencer campaigns enrol **people**, not companies. Job-posting filters, however, only work on a **Companies** search. So this takes two saves: first the companies that are hiring, then the people at them who'll read your email.

### 0. Turn on the new Search

From the Clay homepage, open **Find leads** and click the settings gear to switch on the new search experience. It's in open beta.

### 1a. Find the companies

Choose **Companies**, then type this into **I'm looking for…**:

```text
Software companies with 50 to 200 employees that are hiring a Head of Sales
```

Sculptor turns it into filters and highlights each one it set. Open the **Filters** panel and check three things:

- **Industry:** software (narrow it to B2B SaaS if that's your market).
- **Headcount:** 50 to 200.
- **Job postings:** an open Head of Sales role. Add a location filter if you only sell in some regions.

Under **Excluded companies**, pick an existing Audience of customers so you don't cold-email them. Then click **Continue** → **Save to Companies**.

### 1b. Find the decision-maker at each company

The role they're hiring for is empty by definition, so email whoever is doing the hiring. At a 50 to 200-person company, that's usually the founder, CEO or the head of revenue. Choose **People**, scope it with **Target companies** to the companies you found in 1a ([Search](https://university.clay.com/docs/search)), and describe the people:

```text
Founders, CEOs, Chief Revenue Officers and VPs of Sales
```

Click **Continue** → **Save to People**. This People Audience is what your campaign sends to.

### What auto-save does

New matches land in a **draft** first ([Search](https://university.clay.com/docs/search)). New and existing records are shown side by side, so you can qualify them before anything syncs. If you turn on **auto-save**, matches skip the draft and go straight into **All companies** or **All people**.

My advice: leave auto-save off for the first batch and read 20 or so rows. Turn it on once the matches look right, because from then on the list keeps growing without a review step.

Filtering doesn't cost credits, and the core data points that come back with search results are included ([Search](https://university.clay.com/docs/search)). You start paying in step 2.

## 2. Enrichment: what the AI gets to write from

Add these columns to the People Audience from 1b (**Enrich** → **Add enrichment table**), or in a Clay table that feeds it ([Audiences](https://university.clay.com/docs/audiences), [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence)). Each one becomes a field you can filter on and use in your copy.

| Column | How to get it in Clay | Why it matters |
| --- | --- | --- |
| Decision-maker | Already there from 1b: name, title, company. Add **Enrich Person** if you also want their profile URL or phone. | The person and their role. |
| Work email | The **Work Email** waterfall. It asks one provider, and if there's no match, tries the next. | Clay calls waterfalls "the most reliable way to lift email coverage on a list" ([source](https://university.clay.com/docs/get-leads-ready-to-sequence)). |
| Email validation | An email verification step after the waterfall. Send to deliverable addresses only (Clay's example filter is `Email Status = Valid`). Hold risky and catch-all addresses, and drop undeliverable ones. | One bad batch can hurt the whole domain. [Clay's guide](https://www.clay.com/guides/how-to-automate-email-outreach) treats this as the step that protects everything else. |
| Company size | Comes back with the company search. People read company fields from their primary account in Audiences. | A fact the AI can use without guessing. |
| Recent news and signals | **Signals** → pick a type (job change, funding, hiring spikes). Set **Include changes within the last** (3 months, 6 months or 1 year) and a **Frequency**. | The "why now" for the email. The Head of Sales opening is your first signal. A second one makes the opener specific. |

**Order matters.** Enrichments on an Audience run at the same time and can't read each other's output ([Audiences](https://university.clay.com/docs/audiences)). Validation needs the email first, so build the find-then-validate pair as columns in a Clay table or in Workflows. Then send the results back into the Audience with **Upsert Audiences Record**.

**Turn on auto-enrich (optional).** The **Auto-enrich new records** toggle enriches new people as they join the segment, usually within 15 minutes. It suits a live list, but it also spends credits every day the list grows.

### The credit caveat

- **Filter before you enrich.** In [Audiences](https://university.clay.com/docs/audiences), Bulk Enrich will enrich your whole dataset if you don't apply a segment. Filter to the segment you mean, click **Run 10 rows**, and check the output before running the rest.
- **Set a credit budget** on the enrichment before running it. You can raise it as the output proves itself.
- **Every enrichment, signal and AI step costs credits.** Signals show a **Cost** row before they run. Provider prices vary and aren't listed in these docs, so check the cost in the app before you scale up.
- **Sending costs credits too:** 1 action credit per lead enrolled in a campaign, plus data credits for each AI snippet ([Build your sequence](https://university.clay.com/docs/build-your-sequence)). The campaign editor shows an estimate before you launch.

## 3. AI email prompt: facts, not a mail merge

`Hi {{first_name}}, I wanted to reach out` is what [Clay's own guide](https://www.clay.com/guides/how-to-automate-email-outreach) calls a mail merge, not personalisation. The fix is to let the AI write from the facts you enriched in step 2.

Paste the template below as an **AI snippet** in the first email (type `/` in the message body, then choose **AI snippet**; see [Build your sequence](https://university.clay.com/docs/build-your-sequence)). Wherever you see `[/field]`, type `/` inside the **Snippet brief** and pick that field from your lead data. Use your own field names.

```text
Write the first two sentences of a cold email to [/first name], who is
[/job title] at [/company name].

Use only these facts, and never add one:
- Open role: [/hiring signal]   (for example "Head of Sales, posted 9 days ago")
- Company size: [/employee count]
- Recent change: [/signal summary]   (funding, a job change or a hiring spike; may be blank)

Sentence 1, under 25 words: name the open role and what it suggests about
their plans. Write like a peer who noticed it, not a template.

Sentence 2, under 25 words: link that to one problem a new sales leader faces
in their first 90 days. Use the company size or the recent change if it's filled in.

Rules:
- No greeting, no compliments, no mention of our product or company.
- Plain words. No exclamation marks, no emojis.
- If a fact is blank, leave it out. Never guess a number, date or name.
- Output only the two sentences.
```

Then fill in **Campaign goals** in the **AI context** section of the left sidebar. Every snippet in the campaign uses it, so you don't have to repeat it in each brief:

```text
We help <what you sell> for <who it's for>. This campaign goes to founders and
sales leaders at software companies that are hiring their Head of Sales.
A good outcome is a reply agreeing to a 15-minute call.
```

Write the rest of the email yourself, once: one line on what you do, and a soft ask.

**Example output.** The facts: Priya, CEO at Acme Ledger (fictional), hiring a Head of Sales posted 9 days ago, 85 employees, raised a Series A in the last 60 days.

> Saw Acme Ledger is hiring a Head of Sales, which usually means founder-led selling is about to get a quota. With a Series A just closed, whoever takes that seat will need pipeline in their first 90 days, not a clean-up project.

Before launch, check the prompt holds up:

- **Preview across many leads.** Step through leads with the **Preview** arrows and click **Refresh** to rerun the snippet. Clay writes each snippet once, when the lead enrols, and never rewrites it.
- **Check data coverage.** **Lead setup** warns you when fewer than 70% of leads have every field the sequence needs. Fill the gaps in step 2, or turn off **Require variable data** on a variable and give it a **Fallback value**.
- **Prefer a table column?** Clay's guide uses the same idea as an AI column with a `SKIP` fallback, then filters those rows out. That works in a table, but not in a snippet, because a snippet's output gets sent.

## 4. Sequencer 2.0: inboxes, steps, A/B test, launch

### 4a. Buy domains and inboxes (Growth or Enterprise)

**Campaigns** → **Email Accounts** tab → **Add Email Accounts** → **Buy email accounts with Smart Senders** ([Buying email accounts](https://university.clay.com/docs/buying-email-accounts)).

1. **Search for alternative domains.** Clay starts from your company domain. Buying separate domains keeps cold email from hurting your main domain's reputation.
2. **Pick the number of inboxes per domain.** Each domain holds up to 5, but [Clay advises](https://university.clay.com/docs/getting-started-with-sequencer) 3, with 5 at most. Decide now: you can't add inboxes to a domain later, and deleting one inbox deletes every inbox on that domain.
3. **Add personas.** These are the reps who'll handle replies (first name, last name and profile picture). Auto-balance spreads inboxes evenly across them.
4. **Set the forwarding domain** to your main domain, so visitors to the new domains land on your real site.
5. **Confirm the order.** You pay in credits, at target prices of $4.50 per inbox per month and $15 per domain per year. Clay doesn't refund a domain you cancel part-way through the year.

Inboxes take a couple of days to provision.

**On Launch?** Choose **Bring your own** instead ([Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer)). You'll need a one-time authorisation from your Google Workspace or Microsoft admin, and you'll have to switch warm-up on for each account yourself.

### 4b. Warm up for about three weeks

Inboxes you buy in Clay arrive with warm-up already running, and Clay manages the volume ([Email warmup](https://university.clay.com/docs/email-warmup)). Under **Email accounts**, each inbox shows **Warming up** and then **Ready** once it's through the roughly three-week window. Don't send campaign volume until it reads **Ready**.

You'll see odd emails going in and out while it warms. That's normal: they're warm-up traffic with other accounts in a shared pool, and none of it reaches your leads. If you connected your own inboxes, Clay recommends keeping warm-up on at all times, even after they're ready.

### 4c. Daily volume (keep it conservative)

| Setting | Value | Source |
| --- | --- | --- |
| Emails per inbox per day | About 20 | [Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer) |
| Hard cap on inboxes bought in Clay | 30 per day | [Sequencer limits table](https://university.clay.com/docs/getting-started-with-sequencer) |
| **Min time between emails (min)** | 20 by default (allowed: 3 to 30) | [Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign) |
| Inboxes per domain | 3, 5 at most | [Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer) |
| Open and click tracking | Off by default. Leave it off. | [Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer) |
| Bounce rate | Stop at 5% or above and check your list and inboxes | [Getting started with Sequencer](https://university.clay.com/docs/getting-started-with-sequencer) |

Sizing it (my maths): 3 domains × 3 inboxes × 20 emails = about 180 emails a day, follow-ups included. More inboxes, not more emails per inbox, is how you send more.

In **Settings** → **Schedule**, choose **Custom schedule** ([Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign)). Set **Timezone** to your senders' timezone (it defaults to America/New_York), tick Monday to Friday under **Send on days**, and set **Start time** and **End time** to business hours. Or pick the **Optimized for deliverability** preset.

### 4d. Email steps

A sequence holds up to four emails, and the first one does most of the work ([Build your sequence](https://university.clay.com/docs/build-your-sequence)). [Clay's guide](https://www.clay.com/guides/how-to-automate-email-outreach) suggests three to five touches over two to three weeks. Here's my starting layout (change the waits to suit your market):

| Step | Wait before it | **Send as reply** | Content |
| --- | --- | --- | --- |
| Email 1 | — | — | The AI snippet from step 3, one line on what you do, and a soft ask |
| Email 2 | **Wait 3 days** | On | One-line nudge with a new angle |
| Email 3 | **Wait 5 days** | On | A short proof point, like a result or a customer type |
| Email 4 | **Wait 7 days** | Off (new subject) | A polite close-out: "should I stop here?" |

- **Plain text.** Sequences send plaintext by default. Leave **Enable HTML** off for cold email.
- **Variables:** type `/` to insert a field. Each one is required by default, so a lead with a blank field waits instead of getting an email with a hole in it.
- **Spintax** varies the wording between sends (up to five options) so emails aren't identical. It isn't tracked, so use it for greetings and sign-offs, not for testing.
- **Spam check and test send:** check the score in the left sidebar, then use **Send test email** to send one to yourself before launch.

### 4e. A/B test two openers

Steps from Clay's [A/B test doc](https://university.clay.com/docs/ab-test-sequence-copy):

1. In the **Sequence** tab, click **A/B test**. Clay copies your sequence as **Variant B** and splits enrolment 50/50.
2. On Email 1, click **Test body** and rewrite the opening.
3. Test a single difference. Variant A keeps the AI snippet. In Variant B, replace the snippet with one fixed line, such as:

   ```text
   Quick one about the Head of Sales role you're hiring for.
   ```

   This shows whether the AI opener earns its data credits.
4. Both variants share the same number of emails, waits and schedule. Only the subject and body text can differ.
5. Read the result in **Analytics** → **Compare**. Replies lag sends by days, so wait until most sends in both columns are at least three days old (Clay shows that share) and the counts are big enough to mean something.
6. Click **End test**, choose the **Winning sequence**, and confirm with **Select winning sequence**. New leads get the winner, and leads already enrolled keep the copy they were sent.

### 4f. Launch

Before launch (see [Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign) and [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence)):

- **Exclusions:** in **Lead setup**, exclude segments of existing customers, do-not-contact lists and accounts already in a conversation. Add competitor and customer domains to the **Blocklist**. Exclusions are view-only while the campaign is Active, so pause it to change them.
- **Cooldown window:** a new campaign starts at **None**. Set 60 or 90 days so the same person isn't in two campaigns at once.
- **Enrolment settings:** **Pause lead on segment exit** is on by default, so leave it on. Turn on **Pause leads at the same company on reply** if you email more than one person per company.
- **Budget:** in workspace settings → **Budgets** → **Create**, set a **Credit limit**. When the limit is hit, new leads stop enrolling.
- **Final checks:** set the email field and the exact number of steps now. Launching locks the number and order of steps, and the lead email field stays locked even when paused. To change the number of steps later, you build a new campaign.

Click **Launch campaign**. The modal shows how many leads it'll enrol, warns you if the spam check scored badly, and shows the **Estimated total cost**. Pick your budget, then **Confirm and launch**.

From then on, the campaign keeps checking the People Audience and enrols new leads as they qualify. That's the payoff: the list keeps refilling after the first batch runs out. A lead's sequence stops when they reply (out-of-office replies don't count), and **Pause** reopens the copy, waits and settings for editing.

## One rule

Clay's own advice is to test small before going big: run 10 rows, preview many leads, and send a test email to yourself. A cold campaign is hard to undo once it's sent. Build it on a list you'd be happy to read out loud, and leave a couple of months before you email the same person again.
