# Day 4 — From notes to failure modes

**≈12 min read + one exercise.** Today: turn yesterday's messy pile of notes into a short, ranked
list of named problems — the list that tells you exactly what to measure and fix.

---

## The scene

You've got 20 freeform notes. They feel like noise. But look closer: "invented 30-day policy,"
"made up a return address," "guessed at a discount" — those are the *same problem* wearing three
outfits. The bot **fabricates policies.** Name it once, and suddenly you can count it, measure it,
and fix it.

That move — from scattered notes to named patterns — is the second half of error analysis. It's
called **axial coding**, and it's where the fog turns into a to-do list.

---

## The one idea: cluster, name, and count

Take your open-coding notes and group the ones that are really the same underlying problem. Each
group becomes a **failure mode**: a named, recurring way your AI gets things wrong.

The method:

1. **Group** similar notes together.
2. **Name** each group in plain, specific language — as a *behavior*, not a vibe.
   - Good: *"Fabricates a policy that doesn't exist."* / *"Fails to escalate legal threats."*
   - Weak: *"Accuracy issues."* / *"Bad tone sometimes."* (too vague to measure)
3. **Count** how often each failure mode appeared in your sample.
4. **Rank** by frequency × severity.

You'll usually land on **3–6 failure modes**. That's the sweet spot. More than that and you're
slicing too thin; fewer and you're probably still too vague.

### The Pareto move

Almost always, **a couple of failure modes cause most of your pain.** These are your **Pareto
failure modes.** You don't fix everything — you fix the top one or two first, ship, and re-measure.
That's how you turn evals into momentum instead of an endless backlog.

### Severity matters as much as frequency

A failure that happens 2% of the time but exposes you to legal liability (missing an escalation on
a lawsuit threat) beats a cosmetic tone issue that happens 30% of the time. Rank by **how often ×
how badly it hurts**, and trust your product judgment on the "how badly."

### Let AI do the grunt work (optional, 2 minutes)

You can paste all your notes into Claude or ChatGPT and say:

> *"Here are 20 notes from reviewing my AI feature's outputs. Group them into 3–6 recurring failure
> modes. Name each as a specific behavior and tell me how many notes fall in each."*

Then — and this matters — **review what it gives you.** You own the final list. The AI is a fast
sorter, not the judge. You've read the data; it hasn't.

---

## Worked example

Twenty refund-bot notes collapse into four failure modes:

| # | Failure mode | Count (/20) | Severity | Priority |
|---|---|---|---|---|
| 1 | Fabricates a policy that doesn't exist | 6 | High | 🔥 #1 |
| 2 | Fails to escalate legal/angry cases to a human | 3 | High | 🔥 #2 |
| 3 | Answers in the wrong language | 2 | Medium | #3 |
| 4 | Chokes on long/messy pasted input | 2 | Low | later |
| — | (7 outputs were just fine ✅) | 7 | — | — |

Now you have a plan, not a feeling. "Fabricates policy" is your #1 — six hits and high severity.
That's what you'll build a real measurement for tomorrow.

---

## ✍️ Your turn (12 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"My failure modes"**:

1. Cluster yesterday's notes into **3–6 named failure modes** (do it by hand, or have an AI draft
   it and you edit).
2. **Count** each one across your sample.
3. Assign **severity** (low/med/high) using your product judgment.
4. Circle your **#1 failure mode** — the one you'll measure first.

---

> **One line to remember:** *"The AI makes mistakes" is a shrug. "The AI fabricates policies 30%
> of the time" is a roadmap.*

**Tomorrow →** You've named the enemy. Now we turn your #1 failure mode into an actual measurement
— a rubric and a small test set — so "is it getting better?" becomes a number, not an argument.
([Day 5](day-05.md))

---
*Sources: Evals for AI Engineers (Ch.3 Error Analysis — open & axial coding); Hamel's
[error-analysis workflow](https://hamel.dev/blog/posts/evals-faq/).*
