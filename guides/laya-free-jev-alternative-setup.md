# Laya: the free Jev alternative, and how to set it up properly

**Status:** companion guide for the "LAYA" short (7 October 2026). Facts were checked against the Laya model card and the sources below on 6–7 October 2026. Model versions, benchmarks and access terms change, so re-check the model card before you rely on a number.

Laya is an open-weights decision model from Convai Innovations. You give it a message and a few options, and it returns one answer with a probability for each option. It never writes a sentence. It was published on Hugging Face on 18 September 2026, three days after TypeSafe launched Jev, the closed model it reproduces.

## Links

- [Laya model card on Hugging Face](https://huggingface.co/convaiinnovations/laya): install, quickstart, benchmarks, the fine-tuning notebook and the "Honest Limits" section
- [TypeSafe AI](https://typesafe.ai/): the company behind Jev; Jev is used through TypeSafe's hosted API
- [Jev documentation](https://docs.typesafe.ai/introduction)
- [Flowtivity: Laya benchmarked honestly](https://flowtivity.ai/blog/laya-open-source-jev-alternative/): an independent write-up of where Laya wins and where it doesn't

## What's true, and what's fine print

| Claim | What the model card says |
| --- | --- |
| Free | Apache 2.0 open weights, 421M parameters (ModernBERT-large backbone) |
| About 8× faster | 32.8 ms p50 for one question against Jev's 236–276 ms. This was measured by the developer on one T4 GPU. CPU-only hosts are much slower. |
| Beats Jev on accuracy | Only after fine-tuning. The base checkpoint scores 0.362 on the typed-decisions benchmark zero-shot, below the 0.461 you'd get by always picking the most common answer. The fine-tuned checkpoint scores 0.766, against 0.727 for Jev. |
| Honest confidence | Checkpoints ship over-confident. Refitting a temperature on your own data brings calibration error from 0.466 to 0.081. |
| Loses on | Wide option sets: 0.425 on Banking77 (77 labels) against Jev's 0.870. Also the 512-token context on the English checkpoint. |

## Setup checklist

### 0. Install and run it locally

```bash
pip install laya
```

The model card's quickstart loads it with `laya.load("convaiinnovations/laya")`, or through `Router().predict(state, questions)` (recommended), which picks the right checkpoint for each input. For an HTTP server that speaks the same `POST /v1/systemone` protocol as TypeSafe's API:

```bash
pip install "laya[serve]"
laya-serve
```

Copy the exact question format from the model card's quickstart; it changes between releases.

### 1. Fine-tune on your own tickets

- Export a few hundred real, anonymised examples. Label each one with the single option you'd want (for example `billing`, `bug`, `refund`).
- Keep 20% aside and don't train on them. You'll need them in step 2.
- Fine-tune with the notebook linked from the model card's "Fine-tune for better accuracy" section. It runs on Kaggle's free T4 GPUs.
- Check accuracy on the held-out set before going further. If it isn't clearly better than always picking your most common label, you need more or cleaner labels.

### 2. Recalibrate its confidence

- Run the fine-tuned model on the held-out tickets it has never seen.
- Fit a temperature for each question type on those results (the notebook includes this step).
- Check the result: when Laya says "90% sure", it should be right about 9 times in 10 on held-out data. If not, don't automate yet.

### 3. Set a threshold and route

- Pick a confidence threshold, for example 0.85, by looking at accuracy above and below it on held-out data.
- At or above the threshold, let the workflow act automatically (tag, route, reply with a template).
- Below it, send the ticket to a person.
- Log every decision and review a sample each week. Move the threshold only with evidence.

A minimal routing sketch, independent of Laya's exact output format:

```python
THRESHOLD = 0.85

def route(ticket, answer, confidence):
    if confidence >= THRESHOLD:
        return auto_handle(ticket, answer)   # e.g. tag + queue a templated reply
    return human_queue(ticket, answer)      # include Laya's guess as a hint
```

## Before you rely on it

- Re-run the benchmark numbers on your own data. The headline figures are the developer's.
- Never let an unreviewed decision trigger something irreversible, such as a refund or an account change.
- Keep the 512-token limit in mind for long emails. The model card describes longer-context checkpoints.
