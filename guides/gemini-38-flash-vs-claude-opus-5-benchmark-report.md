[← Back to the guide directory](../README.md)

# Gemini 3.8 Flash vs Claude Opus 5: benchmark report and pricing

Here are the full DeepSWE reports behind the video, the two model results and the pricing comparison.

> **Last verified:** 5 September 2026
>
> **Scope:** Published benchmark results and API list prices. I have not independently rerun this benchmark or tested these models on your project.

## Read the full reports

- [DeepSWE live leaderboard](https://deepswe.datacurve.ai/)
- [DeepSWE v1.1 report: execution, grading and reproducibility](https://deepswe.datacurve.ai/blog/deepswe-v1-1)
- [Original DeepSWE report: methodology, results and limitations](https://deepswe.datacurve.ai/blog/deepswe)

Use **v1.1 → Best** to find the configurations shown in the video. The leaderboard was updated on 3 September 2026 and covers 113 tasks.

| Model and effort | Reported PASS@1 | Average cost per task |
|---|---:|---:|
| Gemini 3.8 Flash — high | 74% ±1% | $2.36 |
| Claude Opus 5 — max | 74% ±4% | $11.84 |

Source: [DeepSWE v1.1 leaderboard](https://deepswe.datacurve.ai/). These are different effort settings. The same rounded score does not establish equal performance on every task.

Calculation: $2.36 ÷ $11.84 ≈ 0.199. Gemini's reported cost is roughly one fifth of Opus's in this benchmark, or about 80% lower. This is separate from the API token-price comparison below.

## Compare API prices

Standard paid-tier prices in USD per one million tokens:

| Model | Input | Output |
|---|---:|---:|
| Gemini 3.8 Flash | $0.75 | $3.75 |
| Claude Opus 5 | $5 | $25 |

Sources: [Google Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing) and [Anthropic model pricing](https://platform.claude.com/docs/en/about-claude/pricing).

Gemini's shown rates apply through **31 December 2026**. Google lists $1.50 input and $7.50 output from **1 January 2027**. Output pricing includes thinking tokens. Claude figures are base input/output rates, excluding cache pricing.

Calculation: 1 − 0.75/5 = 85%; 1 − 3.75/25 = 85%. The video's 85% figure refers to these token prices. It is not a guarantee of 85% lower total project spend: token usage, retries, tools, cache and other charges can differ.

## Check what matters for your work

1. Open the full reports and compare the same benchmark version and visible effort settings.
2. Pick a real task with acceptance checks. Keep the task, tools and time budget comparable.
3. Record successful checks, total spend, retries and time for each model.
4. Review failures before choosing a model. A leaderboard is a starting point; your workload may produce different results.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
