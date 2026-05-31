# Day 9 — Make it a habit: catch regressions & drift

**≈12 min read + one exercise.** Today: how to keep your evals working *after* the excitement
fades — so quality doesn't quietly rot while everyone's looking elsewhere.

---

## The scene

You did the work. You found failure modes, wrote rubrics, validated a judge. Quality's good. Three
months later it's bad again — and nobody noticed until customers did. What happened?

Two things always happen to AI products over time, and both are beatable if you have a habit:

1. **Regressions** — someone tweaks the prompt or swaps the model, and something that used to work
   breaks.
2. **Drift** — nothing changes on your side, but the world does (new customer questions, a vendor
   silently updates the model), and quality slowly slides.

Evals you run *once* catch neither. Evals that run *on a schedule* catch both.

---

## The one idea: evals only pay off if they keep running

### Catch regressions: a quality gate before every change

Every time the prompt or model changes, **run your test set first and compare the score to the
previous version.** If it drops, the change doesn't ship until it's fixed. This is the single
habit that prevents "we fixed one thing and broke three."

This is where **prompt versioning** earns its keep: track your prompt as **v1, v2, v3…**, and
score each version against the **same** test set. Now "is v3 better than v2?" is a number, not an
argument. (Whoever scores higher on the same test set wins — simple as that.)

Engineers call the automated version of this a **CI check** (it runs on every change and blocks
bad ones). **You don't build it — you ask for it.** Your line is: *"Before we ship a prompt or
model change, it has to pass our eval set. Can we make that a required check?"* That one sentence
makes you the PM who prevents fire drills instead of running them.

### Catch drift: re-check real outputs on a schedule

Pick a cadence — **weekly is a good default** — and re-sample real production outputs, then
re-score them with your rubrics/judge. Watch the number over time. A slow slide from 92% → 88% →
84% is **drift**, and you want to see it as a gentle trend, not a cliff your customers discover for
you.

Why drift is sneaky:
- **Your inputs change.** New products, new slang, new edge cases your original test set never had.
- **The model can change under you.** Vendors update models; behavior shifts without warning. (This
  is real: a well-known study found a model's accuracy on one task swing dramatically between two
  versions months apart.)

The fix is humble and cheap: **keep looking at fresh data.** Refresh your test set periodically with
new real examples so it never goes stale. An eval set frozen at launch slowly stops describing your
actual product.

### Keep a human in the loop

Automated graders do the heavy lifting, but the best teams still **spot-check real outputs by hand**
regularly — a lightweight review of a handful of traces each week. It keeps your judgment
calibrated and catches the brand-new failure mode your automated checks were never told about.
(You're just repeating Day 3, forever, in small doses.)

> **The whole habit in one breath:** *check before every change, re-sample every week, refresh the
> test set, and keep reading a few real outputs by hand.*

---

## Worked example

The refund team's cadence, written on one line each:

- **On every prompt/model change:** run the 30-case eval set; **block the change if pass-rate drops
  below the current version.** (asked engineering to make it automatic)
- **Every Monday:** re-sample 50 real conversations, re-score with the LLM-judge, log the number in
  a shared sheet.
- **Monthly:** swap 10 stale test cases for 10 fresh ones pulled from recent real traffic.
- **Owner:** the PM (you). **Where it lives:** a pinned Slack message + the shared sheet.

It's not heavy. Twenty minutes a week buys you "we caught it early" instead of "the customer caught
it."

---

## ✍️ Your turn (12 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"My eval cadence"**:

1. **Before any change ships:** write the rule (run test set; block if score drops).
2. **Weekly:** write your re-sampling ritual (how many outputs, scored how, logged where).
3. **Owner:** name who owns it (probably you).
4. (Bonus) Draft the one sentence you'll say to engineering to ask for an automated quality gate.

---

> **One line to remember:** *An eval you run once is a photo. An eval you run on a schedule is a
> smoke detector. Only one of them wakes you up before the fire.*

**Tomorrow →** The finish line. We turn all of this into two things: a fix you'll actually ship,
and a one-page report that makes you the most credible person in the room. ([Day 10](day-10.md))

---
*Sources: Evals for AI Engineers (Ch.9 CI/CD for LLM Agents, Ch.10 Interfaces for Human Review);
Anthropic's eval workflow & prompt versioning (LinkedIn Learning).*
