# Day 2 — The three places AI breaks (the Three Gulfs)

**≈12 min read + one exercise.** Today: a simple map that tells you *where* to look when your AI
disappoints — so you stop guessing.

---

## The scene

Your refund bot gave a bad answer. Why? There are only a few honest possibilities:

- You didn't realize customers paste in *entire email threads*, and the bot choked on the mess.
- Your prompt said "be helpful and concise" but never said "only state our actual policy."
- It works great on the 10 examples you tried, but real customers ask in 500 different ways and
  it falls apart on the weird ones.

Each of these is a different problem with a different fix. Confusing them is why teams flail.
There's a clean map for this.

---

## The one idea: the Three Gulfs

Shreya Shankar's **Three Gulfs** framework names the three gaps where AI applications go wrong.
(A "gulf" is just a gap between two things that should line up.)

### 1. The Gulf of Comprehension — *you ↔ your data*

The gap between what you *think* your inputs and outputs look like and what they *actually* look
like.

You imagine clean, well-formed questions. Reality: typos, forwarded threads, three languages in
one message, someone pasting a PDF. **You can't evaluate what you've never looked at.** This gulf
is why Day 3 (looking at your data) exists — it's the whole game.

### 2. The Gulf of Specification — *you ↔ the prompt*

The gap between what you *meant* and what you actually *told the AI to do.*

Natural language is slippery. "Summarize the key requests" — in bullets or a paragraph? Include
implied requests? How short? Every unstated assumption is a place the AI can wander. Most "the AI
is dumb" moments are really "the instructions were vague."

### 3. The Gulf of Generalization — *a few examples ↔ the messy real world*

The gap between "works on my test cases" and "works on everything users actually do."

The AI nails your 10 examples, so you ship. Then it meets the long tail — the rare, weird,
adversarial inputs — and quietly fails on a slice of them. This is the gulf that hides, because
your demo never touches it.

> **The map:** Comprehension = *do I know my data?* · Specification = *did I say what I meant?* ·
> Generalization = *does it hold up in the wild?*

### Why the map matters

When something breaks, you ask: *which gulf is this?*

- Comprehension problem → go **read more real data** (Day 3).
- Specification problem → **fix the prompt / sharpen the instructions.**
- Generalization problem → **expand your test set** to cover the messy cases (Day 5) and check
  the long tail.

You stop saying "the AI is broken" (useless) and start saying "this is a specification gap"
(actionable). Naming the gulf *is* half the fix.

---

## Worked example

Refund bot invents a "30-day window."

- Is it **Comprehension**? Maybe customers ask about product types you never tested. Partly.
- Is it **Specification**? Almost certainly — the prompt never said *"only state policies from
  this approved list; if unsure, say you'll check."* The AI filled the silence with a guess.
- Is it **Generalization**? Also yes — it behaves on common questions, breaks on rare ones.

Most real failures touch more than one gulf. That's fine. The point is you now have three sharp
questions instead of one vague complaint.

---

## ✍️ Your turn (10 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"Where it tends to break —
the Three Gulfs"**:

1. List **2–3 real failures** you've seen in your feature.
2. For each, tag the most likely **Gulf** (Comprehension / Specification / Generalization) and a
   one-line *why.*
3. Note **which Gulf seems to be your biggest** right now.

Don't overthink it — first instinct is usually right, and you'll refine it once you read your data
tomorrow.

---

> **One line to remember:** *"The AI is broken" tells you nothing. "This is a specification gulf"
> tells you what to do next.*

**Tomorrow →** The single highest-leverage skill in all of evals, and the one almost everyone
skips: actually looking at your data. ([Day 3](day-03.md))

---
*Sources: Shreya Shankar's Three Gulfs framework (after Norman, 1988); Evals for AI Engineers
(Ch.1–2).*
