# Day 5 — Turn "good" into a measure: rubrics & a tiny test set

**🎉 Halfway point.** You can already read your data and name what's breaking — that alone puts you
ahead of most teams. Today you make it measurable.

**≈12 min read + one exercise.** Today: write a rubric a colleague would agree with, build a small
test set, and learn the simple loop that drives every eval.

---

## The scene

Two teammates look at the same refund-bot answer. One says "7 out of 10." The other says "4."
They argue for ten minutes. Neither is wrong, because "7/10" means nothing — it's a vibe wearing a
number's clothing.

Now imagine the rubric was: *"FAIL if the answer states any refund policy not on our approved
list."* Both teammates look, both say **FAIL.** No argument. That's the power of a good rubric: it
turns judgment into something repeatable.

---

## The one idea, part 1: write binary (pass/fail) rubrics

A **rubric** is the written rule that decides pass vs. fail for *one* thing you care about.

The single most useful tip in this whole course:

> **Make it binary. Pass or fail. Not 1–10.**

Why Hamel and Shreya push this hard:

- **1–10 scores are fake precision.** Nobody can reliably tell a 6 from a 7. The disagreement
  *feels* like measurement but it's noise.
- **Binary forces a clear definition.** To say pass/fail you must define *exactly* what failure
  is — which is the valuable thinking.
- **Binary is actionable.** "30% fail this check" tells you precisely what to fix. "Average 6.4/10"
  tells you nothing.

A good rubric is **specific enough that two people grade the same output the same way.** Test it on
yesterday's examples — if you and a teammate disagree, the rubric is too vague; sharpen it.

**Write one rubric per failure mode.** Today, start with your #1.

## The one idea, part 2: build a small test set

An **eval dataset** (test set) is just a collection of inputs you run your AI on to check quality.

- **Start tiny.** Three examples is a legitimate start. Ten is great. You'll grow it over time.
- **Two ways to build it:**
  1. **By hand** — pull real inputs that trigger your failure mode (your Day 3 traces are gold).
  2. **AI-generated** — ask Claude/ChatGPT: *"Generate 30 diverse customer questions about refunds,
     including angry ones, non-English ones, and vague ones."* This is the fast way to cover the
     messy long tail (your Gulf of Generalization from Day 2).
- **Cover the hard cases on purpose.** A test set of only easy questions will always look great and
  teach you nothing. Include the weird, the angry, the edge.

## The loop that ties it together

Every eval, no matter how fancy, is this simple 5-step loop (from Anthropic's eval workflow):

```
1. DRAFT a prompt          → the thing you're testing
2. CREATE a test set       → inputs that represent reality
3. RUN your AI on each     → collect outputs
4. GRADE each output       → against your rubric (pass/fail)
5. CHANGE something & REPEAT→ did the score go up?
```

Step 5 is the magic: the score becomes an **objective baseline.** Change the prompt, re-run, and
you can *see* whether you helped or hurt — instead of guessing. (More on graders tomorrow, and on
versioning your prompt on Day 9.)

> You do **not** need special software to start. A spreadsheet of test cases and a column for
> pass/fail is a real eval.

---

## Worked example

**Failure mode #1:** Fabricates a policy that doesn't exist.

**Rubric (binary):**
> *PASS if every refund policy mentioned appears on our approved-policy list (or the bot says it
> will check / routes to a human). FAIL if it states any policy detail not on the list.*

**Test set (10 cases, mixed sources):** 6 real questions pulled from Day 3 traces + 4
AI-generated edge cases ("refund after 6 months?", a question in Spanish, a vague "money back?",
an angry one). For each, note the ideal behavior.

Run the bot on all 10, mark each PASS/FAIL against the rubric → say **6/10 pass.** That 60% is your
baseline. When you change the prompt next week and it hits 9/10, you'll *know* you improved it.

---

## ✍️ Your turn (15 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"My rubric & test set"**:

1. Write a **binary pass/fail rubric** for your #1 failure mode. Make it specific enough that a
   colleague would grade the same way.
2. Build a **test set of ~10 cases** — some pulled from your real traces, some AI-generated to
   cover edge cases.
3. (Bonus) Run your feature on the 10 cases and mark each pass/fail. That number is your baseline.

---

> **One line to remember:** *A 1–10 score is an opinion with a number taped on. A binary rubric is
> a decision anyone can repeat.*

**Tomorrow →** Grading 10 cases by hand is fine. Grading 10,000 isn't. Tomorrow: the two kinds of
automatic graders, and exactly when to use each. ([Day 6](day-06.md))

---
*Sources: Evals for AI Engineers (Ch.2, Ch.5); Anthropic's "A typical eval workflow" (LinkedIn
Learning); Hamel on [binary evals](https://hamel.dev/blog/posts/evals-faq/).*
