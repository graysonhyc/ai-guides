[← Back to the guide directory](../README.md)

# Jev: Quick Start and Demo Guide

Jev, from TypeSafe AI, returns structured decisions that an app can use: choose a route, rank an option, or evaluate a condition. Start with one small decision in your own project.

**Sources checked:** 19 September 2026. This is a documentation-based starter; I have not independently reproduced the demos or benchmarked the API.

## 1. Try a decision in the Playground

Open the [TypeSafe Playground](https://console.typesafe.ai/) and sign in. Access may depend on your account's early-access status. Follow the [official quick start](https://docs.typesafe.ai/introduction/quickstart) if the interface changes.

Use this original sample state:

> A customer can sign in, but exporting their monthly report produces an empty file. Their invoice and subscription look correct.

Ask a Choice question: “Which team should handle this request?” Supply three choices: `billing`, `technical`, and `sales`, each with a short description. Inspect the selected answer and its probabilities. Change the message and compare the result.

## 2. Make a small API request

Create an API key in your TypeSafe dashboard and set `TYPESAFE_API_KEY` in your local environment. Keep it out of browser code and version control. Run this adapted example from a terminal:

```bash
curl --fail-with-body https://api.typesafe.ai/v1/systemone \
  -H "Authorization: Bearer $TYPESAFE_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary @- <<'JSON'
{
  "model": "jev-latest",
  "state": "A customer can sign in, but exporting their monthly report produces an empty file.",
  "questions": {
    "route": {
      "type": "choice",
      "instructions": "Which team should handle this request?",
      "criteria": {
        "billing": "Invoices, payments, or subscriptions",
        "technical": "Broken features or integration errors",
        "sales": "Product fit or purchasing questions"
      }
    }
  }
}
JSON
```

Inspect `answers.route.choice`, `probabilities`, and `confidence`. Handle HTTP errors before using the result. This example follows the [documented request format](https://docs.typesafe.ai/introduction/quickstart); no live request was made for this guide.

## 3. Choose the right question

| Primitive | Use it for |
|---|---|
| Choice | Selecting from options your code defines. |
| Score | Evaluating against an ordered rubric. |
| Noul | Assessing a statement on a 0–1 scale. |

You can ask multiple focused questions about the same state. Avoid combining several unrelated judgments into one vague question. See the [introduction](https://docs.typesafe.ai/introduction).

Choice and Score expose confidence; Noul does not carry that field. For an uncertain answer, route to review or a fallback. Choose thresholds from tests on your own cases, rather than treating one threshold as universally safe. See [confidence](https://docs.typesafe.ai/confidence) and [application patterns](https://docs.typesafe.ai/patterns).

## 4. Build one useful feature

Original starter prompt for your coding agent:

```text
Read TypeSafe's current quick start and API documentation. Add a small,
server-side support-ticket router to my existing project using Jev.
Use only billing, technical, and sales as allowed routes. Keep the API key
in an environment variable. Show the decision and confidence for review;
do not send messages or change customer records. Handle API failures and
uncertain answers. Test normal, ambiguous, empty, and irrelevant input.
Explain how to run it and what has actually been verified.
```

Then evaluate a small set of messages with expected routes. Record accuracy, failures and end-to-end latency before allowing the feature to take action.

## 5. Understand the demos in the video

- **Colour sorting:** a visual simulation. The rendered demo shows 150,000 virtual sweets; my narration says 100K. The screen count is the correct count for that demo. Its animation speed is not a measurement of model processing time.
- **AI town:** the shown example reports 50 decisions in 0.59 seconds; this is demo evidence, not a benchmark reproduced here.
- **Wikipedia:** the displayed comparison is 0.544 seconds versus 4.694 seconds of model time, excluding page loading.
- **Other examples:** model routing, Doom, chess, page cleanup, Melee and simulated driving illustrate possible uses. A demo does not establish performance in your app; the chess footage includes both a win on time and a loss.

TypeSafe's [launch article](https://typesafe.ai/blog/introducing-system-one-models-and-jev) explains its own demos and methodology. It attributes the 193.6× faster and 444.6× cheaper claims to selected workflow evaluations and says these are toward the higher end of expected real-world gains. The video's rounded figures are not universal guarantees. See the linked [workflow evaluations](https://evals.typesafe.ai/).

## Official sources

- [TypeSafe AI](https://typesafe.ai/)
- [Jev introduction](https://docs.typesafe.ai/introduction)
- [Quick start and request examples](https://docs.typesafe.ai/introduction/quickstart)
- [Confidence](https://docs.typesafe.ai/confidence)
- [Application patterns](https://docs.typesafe.ai/patterns)
- [Launch article and demo context](https://typesafe.ai/blog/introducing-system-one-models-and-jev)

---

Created by [Grayson Ho](https://github.com/graysonhyc).
