# Day 10 — Close the loop & communicate it (capstone)

**🏁 Finish line.** Ten days ago you vibe-checked your AI. Today you finish with a real eval
practice and a one-page plan you can use Monday. Let's bring it home.

**≈12 min read + one exercise.** Today: turn eval results into an actual product improvement, and
write the report that makes you the most credible person in the room.

---

## The scene

You've found your failure modes, measured them, validated your grader, and set a cadence. Here's
the thing nobody tells you: **an eval that doesn't change the product is just expensive
journaling.** The point was never the score. The point is a better product — and being able to
prove it to the people who decide where time and money go.

Two moves close the loop: **improve**, then **communicate.**

---

## The one idea, part 1: turn results into improvements

You have a ranked list of failure modes and a way to measure each. Now run the improvement loop —
the same one from Day 5, pointed at your #1 problem:

```
LOOK at the failures  →  MEASURE (baseline)  →  CHANGE one thing  →  RE-MEASURE  →  keep or revert
```

For most failure modes, your levers (cheapest first) are:

1. **Fix the prompt.** The most common, cheapest fix. Vague instruction → sharp instruction. (Your
   Day 2 "Specification gulf" problems usually die here.) *"Only state policies from this list; if
   unsure, say you'll check"* fixes a lot of fabrication.
2. **Fix the inputs / retrieval.** If it's a RAG feature pulling the wrong docs, fix retrieval
   before blaming the model (Day 8).
3. **Change the architecture or model.** Add a guardrail, add an escalation step, or upgrade the
   model — the heavier lever, used when prompt fixes plateau.

The discipline that makes you trustworthy: **change one thing, re-run your eval, compare to
baseline.** If the number went up, keep it. If not, revert and try again. You're no longer guessing
whether you helped — you can *see* it. That's the entire game, and you now play it.

## The one idea, part 2: communicate it (the eval report)

The same facts can land as "trust me, it's good" or as a crisp case that gets you resources and
credibility. The difference is a short **eval report** — written for stakeholders, not engineers.

A good eval report is five plain lines:

1. **What we measured** — the feature and the top failure modes.
2. **How good it is** — the pass rates, in plain numbers ("passes our policy-accuracy check 88% of
   the time, up from 60% last month").
3. **What's still failing** — honestly, the top remaining problem.
4. **What we're doing about it** — the next fix and expected impact.
5. **How we know it won't rot** — your cadence (the smoke detector from Day 9).

Why this matters for *you*: it changes how leadership sees AI quality — from a black box they have
to take on faith into something a product person **owns, measures, and steers.** This report is the
artifact that gets your program funded instead of cut. It's also, not coincidentally, the kind of
document compliance and governance teams need as AI oversight tightens.

> Write the report so a busy executive gets it in 30 seconds and a skeptical one can't poke a hole
> in it. Numbers + honesty beats adjectives every time.

---

## Worked example — a finished eval report

> **Refund Assistant — Eval Report (this month)**
> **Measured:** policy accuracy, escalation of legal/angry cases, language match.
> **Quality:** Policy-accuracy check now passes **91%** (was 60% at the start of the month).
> Escalation check passes **100%**. Language match **96%**.
> **Still failing:** ~9% of answers on rare product types still state an unverified policy.
> **Next fix:** adding those product types to the approved-policy source; expect 91% → ~97%.
> **How we keep it honest:** 30-case eval gate on every prompt change; 50 real conversations
> re-scored weekly; test set refreshed monthly.

Five lines. Anyone in the company now understands exactly how good this AI is and trusts the person
who wrote it. *That's* the finish line.

---

## ✍️ Your turn (15 min) — complete your Eval Plan

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"Closing the loop"** — and
your plan is done:

1. Take your **#1 failure mode** and write the **next fix you'll ship** (start with the prompt).
2. Write your **one-paragraph eval report** using the five-line structure above.
3. Scroll up through your finished plan: feature, gulfs, failure modes, rubric, test set, graders,
   trust verdict, cadence, and now a fix + report. **That's a complete eval practice — yours.**

---

## 🎉 You did it

Ten days ago, "is our AI good?" was a shrug. Now you can answer it with data, defend the answer,
hand the practice to someone else, and keep it honest over time. You went from couch to 5k.

**What to do next:**
- **Run this on a second feature** — it's twice as fast now.
- **Share your Eval Plan** with your team and make the weekly cadence real.
- **Pass the course on.** If it made you more confident, it'll do the same for the next PM. That's
  how good practices spread.

> **The line to remember from the whole course:** *You don't need to be an engineer to own AI
> quality. You need to look at your data, measure what matters, and keep it honest. That's the job —
> and now it's yours.*

---
*Sources: Evals for AI Engineers (Ch.12 Improving LLM Agents); "Types of AI docs" (evaluation
reports as stakeholder artifacts); Anthropic & Hamel/Shreya on the analyze → measure → improve
loop.*
