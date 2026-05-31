# The AI Evals Playbook

**A 10-day, no-fluff course that teaches AI Evals to product people — no coding required.**

You ship an AI feature. It demos well. Then the edge cases roll in, support tickets pile up,
and when someone asks "is the quality actually good?" all you have is a gut feeling. This
course replaces the gut feeling with a practice.

In 10 short days (≈12 minutes of reading + one hands-on exercise each), you'll go from
*vibe-checking* your AI to running a **disciplined, data-driven eval practice** you can defend
to your team, your boss, and yourself.

---

## Who this is for

- **AI Product Managers** who own an LLM feature and need to drive its quality
- **Product Managers** adding AI to an existing product
- **Product Analysts** who measure things and want to measure AI properly
- **Non-technical PMs** who feel locked out of "the eval conversation"

> Hamel & Shreya's *Evals for AI Engineers* is the canonical book — written for engineers.
> **This course translates that craft into plain product language.** You will not write code.
> Every exercise is doable with a spreadsheet, an AI chat window (Claude or ChatGPT), and your
> own product's real outputs.

**Prerequisites:** you have (or can get access to) one real AI feature and a sample of its
actual outputs. That's it.

---

## What you'll walk away with

By Day 10 you'll have a **one-page Eval Plan** for a real feature — failure modes, a rubric, a
small test set, a grader, a trust check, and a cadence. That's the "5k finish line": not just
completed lessons, but a working artifact you can use Monday morning.

---

## How the 10 days work

Each day is one idea, one example, one exercise — built so the exercises stack into your Eval
Plan.

| Day | What you'll learn |
|----|-------------------|
| 1 | Stop vibe-checking your AI — what an eval actually is |
| 2 | The three places AI breaks (the Three Gulfs) |
| 3 | Look at your data — the skill that beats everything |
| 4 | From notes to failure modes |
| 5 | Turn "good" into a measure: rubrics & a tiny test set |
| 6 | Two kinds of graders: code vs LLM-as-judge |
| 7 | Can you trust your judge? Precision & recall |
| 8 | When your AI looks things up or takes actions (RAG, agents, multi-turn) |
| 9 | Make it a habit: catch regressions & drift |
| 10 | Close the loop & communicate it (capstone) |

Start at [`curriculum/overview.md`](curriculum/overview.md) → then
[`curriculum/day-01.md`](curriculum/day-01.md).

Keep your work in [`curriculum/my-eval-plan-template.md`](curriculum/my-eval-plan-template.md).
Stuck on a term? [`GLOSSARY.md`](GLOSSARY.md) defines every one in plain English.

---

## What's in this repo

```
README.md                          ← you are here
GLOSSARY.md                        ← every term, in plain English
curriculum/
  overview.md                      ← the 10-day map + how to take the course
  day-01.md … day-10.md            ← the lessons
  my-eval-plan-template.md         ← your running worksheet (the deliverable)
design/
  DESIGN-SPEC.md                   ← couch-to-5k-style UX spec for the web version
  wireframes.md                    ← low-fi wireframes of every screen
```

The `design/` folder specs a future web experience (inspired by
[couchto5k.ai](https://couchto5k.ai)). The course itself is fully usable as the Markdown files
above today.

---

## Sources & credits

This course stands on the shoulders of the people who made evals a discipline:

- **Hamel Husain & Shreya Shankar** — *Evals for AI Engineers* (O'Reilly, 2026) and their
  [Maven course](https://maven.com/parlance-labs/evals). The Three Gulfs, error analysis, and
  the "look at your data" mindset come from their work.
  ([Hamel's LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/))
- **Chantal Cox** (Adobe) & **Aman Khan** (Google), and **Anthropic's** LinkedIn Learning
  videos — code-vs-LLM-judge, precision/recall for evals, the 5-step eval workflow.
- **Lenny Rachitsky**'s newsletter and **Aakash Gupta**'s
  [*AI Evals for PMs*](https://www.news.aakashg.com/p/ai-evals) for the PM framing.

Course written by Priyanka Das · *The Outcome Memo*.
