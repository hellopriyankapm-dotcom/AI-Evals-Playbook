# Day 7 — Can you trust your judge? Precision & recall

**≈12 min read + one exercise.** Today: the check that turns your LLM-judge from "probably fine"
into "proven trustworthy" — using two ideas you already half-know.

---

## The scene

You build an LLM-judge to flag fabricated policies. It says your bot fails 8% of the time. Great
— except, can you *trust the judge*? Maybe it's missing half the real fabrications. Maybe it's
flagging perfectly good answers. If your measuring tape is wrong, every number you report is
wrong.

So before you rely on an automated grader at scale, you do one thing: **check it against a
human.** That human is you.

---

## The one idea: validate the judge against ground truth

**Ground truth** = the correct labels, decided by a person. The method:

1. Take a sample of outputs (20 is plenty to start).
2. **You** grade each one by hand — PASS/FAIL — using your rubric. *This* is ground truth.
3. Have your **LLM-judge** grade the same 20.
4. Compare. Where do they agree? Where do they disagree?

Two numbers describe how good your judge is. They sound technical; they're actually common sense.

### Precision — *"are the alerts real?"*

> Of the failures your judge **flagged**, what fraction were **actually** failures?

Low precision = your judge cries wolf. It flags good answers as bad, you waste time chasing ghosts,
and people stop trusting the eval.

### Recall — *"is anything slipping through?"*

> Of all the failures that **really** exist, what fraction did your judge **catch**?

Low recall = your judge misses real problems. Your dashboard says "97% good" while customers hit
failures it never noticed. This is the more dangerous one — silent misses.

### The plain-English picture

| | Judge says FAIL | Judge says PASS |
|---|---|---|
| **Really a fail** | ✅ caught it | ❌ **missed it** (hurts recall) |
| **Really fine** | ❌ **false alarm** (hurts precision) | ✅ correct |

You want both high: catch the real failures (recall) without crying wolf (precision). When a
judge agrees with humans on both, it's effectively a trusted reviewer that you've cloned — one that
keeps grading thousands of outputs automatically while you sleep. **That's the prize.**

### What if the judge is bad?

Totally normal on the first try. You fix it the same way you'd coach a new reviewer:

- **Sharpen the rubric** in the judge prompt (vague rule → vague grading).
- **Add a few examples** of pass and fail into the prompt so it calibrates.
- **Re-test** against your 20 hand-labeled cases. Repeat until it agrees with you.

Only *then* do you turn it loose at scale. An unvalidated judge isn't a measurement — it's a
second opinion you haven't earned the right to trust.

> This isn't only for AI. Precision and recall are how you measure **any** automated check against
> human judgment. Learn it once, use it forever.

---

## Worked example

You hand-label 20 refund-bot answers: **5 are real fabrications**, 15 are clean.

Your LLM-judge flags **6** as fabrications. You compare:

- Of its 6 flags, **4** were real fabrications, **2** were false alarms → **precision = 4/6 = 67%.**
- Of the 5 real fabrications, it caught **4**, missed **1** → **recall = 4/5 = 80%.**

Verdict: recall's decent, precision's shaky (too many false alarms). You add two example outputs
to the judge prompt and tighten the rule. Re-run: precision climbs to 90%+. *Now* you trust it on
the full traffic.

(You don't need exact math — even "it agreed with me 17 out of 20 times, and the misses were all
false alarms" is a real, useful read.)

---

## ✍️ Your turn (15 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"Do I trust my judge?"**:

1. **Hand-label ~20 outputs** yourself (PASS/FAIL) — that's your ground truth.
2. Run your **LLM-judge** on the same 20 (or simulate it by grading them with your judge prompt in
   a chat window).
3. Count agreements/disagreements; estimate **precision** (real flags ÷ all flags) and **recall**
   (caught ÷ all real failures).
4. Write your **verdict**: trustworthy at scale, or not yet? If not, note what you'll tighten.

---

> **One line to remember:** *An unvalidated judge isn't a measurement — it's a guess with a
> confidence problem. Twenty hand-labeled examples turn it into something you can stand behind.*

**Tomorrow →** Everything so far assumes a simple "question in, answer out" feature. But what if
your AI looks things up, or takes actions? There's a little more to check. ([Day 8](day-08.md))

---
*Sources: Chantal Cox & Aman Khan, "Automated evals" (LinkedIn Learning — precision/recall to
validate graders); Evals for AI Engineers (Ch.4 Collaborative Evaluation, Ch.5); Hamel on
[aligning LLM judges](https://hamel.dev/blog/posts/evals-faq/).*
