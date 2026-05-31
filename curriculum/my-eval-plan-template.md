# My Eval Plan — your running worksheet

This is the thing you're building. Each day's exercise fills in one part. By Day 10 it's a
complete, one-page eval plan for a real feature — your "5k finish line."

Copy this file, rename it (e.g. `my-eval-plan-<feature>.md`), and fill it in as you go.

---

## The feature I'm evaluating
*(Day 1)*

- **Feature:** _e.g., "Refund-policy answers in our support chatbot"_
- **What it's supposed to do:** _one sentence_
- **Who uses it:** _e.g., customers self-serving before contacting support_
- **How I judge "good" today (my honest vibe-check):** _____
- **One real failure I've already seen:** _____

## Where it tends to break — the Three Gulfs
*(Day 2)*

| Failure I've seen | Which Gulf? (Comprehension / Specification / Generalization) | Why |
|---|---|---|
| | | |
| | | |

- **My biggest Gulf right now:** _____

## What I found reading my data
*(Day 3 — open coding)*

> Read 15–20 real outputs. One freeform note each. Paste/summarize the notes here.

- Output 1 → _note_
- Output 2 → _note_
- … (15–20)

## My failure modes
*(Day 4 — axial coding)*

| # | Failure mode (named) | How often (out of my sample) | Severity (low/med/high) |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

- **My #1 failure mode to fix first:** _____

## My rubric & test set
*(Day 5)*

**Rubric for failure mode #1 (binary):**
> _"FAIL if the answer ___. PASS otherwise."_ (specific enough that a colleague grades it the same)

**Test set (start with ~10):** hand-written and/or AI-generated.

| # | Test input | Expected/ideal behavior |
|---|---|---|
| 1 | | |
| … | | |

## My graders
*(Day 6)*

| Failure mode | Grader type (code / LLM-judge) | Why |
|---|---|---|
| 1 | | |
| 2 | | |

**Draft LLM-judge prompt (for one subjective mode):**
> _____

## Do I trust my judge?
*(Day 7)*

- Hand-labeled sample size: ___
- Times judge agreed with me: ___ / Disagreed: ___
- **Precision (rough):** of flagged failures, ___% were real
- **Recall (rough):** of real failures, judge caught ___%
- **Verdict:** trustworthy at scale yet? ☐ yes ☐ not yet — what to fix: _____

## Extra things to check (if my AI looks things up / takes actions)
*(Day 8)*

- My feature is: ☐ simple answer ☐ looks things up (RAG) ☐ takes steps (agent) ☐ multi-turn
- 2–3 extra things to check beyond the final answer:
  1. _____
  2. _____

## My eval cadence
*(Day 9)*

- **Before any prompt/model change ships:** _check on test set; block if score drops_
- **Weekly:** _re-sample ___ real outputs and re-score_
- **Owner:** _____
- **Where results live:** _____

## Closing the loop
*(Day 10 — capstone)*

- **Top failure mode → the fix I'll ship next:** _____
- **One-paragraph eval report for stakeholders:**
  > _____
