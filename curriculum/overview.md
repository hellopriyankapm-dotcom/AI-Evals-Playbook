# The AI Evals Playbook — Course Overview

**10 days. ~12 minutes of reading a day. One exercise a day. No code.**
By the end you'll have a real eval practice and a one-page Eval Plan for your own AI feature.

---

## The promise

Most product people "evaluate" their AI by opening it, trying a few things, and going *"yeah,
that's pretty good."* That's a vibe-check. It feels like measurement. It isn't.

This course gives you the real thing — the same craft taught to engineers at OpenAI and
Anthropic — **translated into plain product language and stripped of everything you don't need.**
You'll learn to look at your data, find what's actually breaking, turn "good" into a measurement
you can trust, and keep it honest over time.

**You don't need to code. You need a feature, its real outputs, and 12 minutes a day.**

---

## How to take this course

1. **Pick one real AI feature** before Day 1. The whole course is hands-on *on that feature*.
   (No feature at work? Use any AI product you can poke at — a chatbot, a writing tool, a search
   assistant.)
2. **Do one day at a time, in order.** Like a training plan, the days build. Don't sprint ahead.
3. **Keep your work in [`my-eval-plan-template.md`](my-eval-plan-template.md).** Every exercise
   adds one section. By Day 10 it's your finished Eval Plan.
4. **When a word is unfamiliar, check [`GLOSSARY.md`](GLOSSARY.md).** Everything is defined in
   plain English.

> **Rule of the course:** if a sentence doesn't help you *do* something, we cut it.

---

## The map

You're walking the **eval lifecycle**, one step a day:

```
LOOK AT YOUR DATA  →  MEASURE  →  VALIDATE  →  AUTOMATE  →  IMPROVE
   (Days 1–4)        (Day 5)     (Days 6–7)   (Days 8–9)   (Day 10)
```

| Day | Title | The one idea | The win you bank |
|----|-------|--------------|------------------|
| 1 | **Stop vibe-checking your AI** | An eval is *systematic* measurement of quality — and it's your job now | Named your feature + its baseline |
| 2 | **The three places AI breaks** | The Three Gulfs: data, prompt, real-world | A map of where to look |
| 3 | **Look at your data** | Read real outputs; the single highest-leverage eval skill | 15–20 outputs read, notes written |
| 4 | **From notes to failure modes** | Cluster notes into named, countable failure patterns | Your top 3 failure modes |
| 5 | **Turn "good" into a measure** | Binary pass/fail rubrics + a tiny test set | A rubric + 10 test cases |
| 6 | **Two kinds of graders** | Code evaluators vs LLM-as-judge — and when to use each | A grader chosen per failure mode |
| 7 | **Can you trust your judge?** | Precision & recall: does your grader agree with humans? | A trust verdict on your judge |
| 8 | **When your AI looks things up or takes actions** | What to *also* check for RAG, agents, multi-turn | Extra checks for your feature |
| 9 | **Make it a habit** | Catch regressions before they ship; re-check for drift | Your eval cadence |
| 10 | **Close the loop & communicate it** | Turn results into fixes + a stakeholder eval report | Your finished one-page Eval Plan |

**Halfway badge (Day 5):** *you can now read your own data and name what's breaking.*
**Finish line (Day 10):** *you have a working eval practice and a plan you can use Monday.*

---

## What "good" looks like when you're done

You'll be able to answer, for your feature, without flinching:

- *What actually breaks, and how often?* (failure modes, ranked)
- *How do you measure it?* (rubric + test set + grader)
- *Can you trust that measurement?* (precision/recall on your judge)
- *How do you keep it from rotting?* (cadence for regressions + drift)
- *What are you doing about the top problem?* (the next fix)

That's not a vibe. That's an eval practice. Let's start →
[**Day 1**](day-01.md).
