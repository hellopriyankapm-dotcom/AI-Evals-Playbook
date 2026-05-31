# Day 8 — When your AI looks things up or takes actions

**≈12 min read + one exercise.** Today: simple mental models for evaluating richer AI features —
the ones that search a knowledge base, take multi-step actions, or hold a conversation. No
architecture. Just *what else to check.*

---

## The scene

A "simple" refund bot just answers questions. But your real feature might be fancier:

- It **looks up** your policy docs before answering (that's **RAG**).
- It **takes actions** — checks the order system, issues the refund, emails the customer (that's an
  **agent**).
- It **holds a conversation** across many turns (that's **multi-turn**).

For these, grading only the *final answer* isn't enough — because the answer can be right by luck,
or wrong for a reason you can't see unless you check the steps. Here's the extra thing each one
needs.

---

## The one idea: check the path, not just the destination

### "Looks things up" → RAG → *did it retrieve the right stuff?*

**RAG** (retrieval-augmented generation) means your AI pulls relevant documents into its context
before answering. A RAG answer can fail in two completely different ways:

1. **Retrieval failed** — it grabbed the wrong (or no) documents. Garbage in, garbage out.
2. **Generation failed** — it had the right docs but still answered badly.

So you check **two** things: *Did it find the right information?* and *Did it use that information
correctly?* If the bot cites a refund window, the question becomes: was the correct policy doc even
retrieved? A wrong answer from a *missing* document is a very different fix than a wrong answer from
a *present* one.

> **PM takeaway:** for RAG, always ask "what did it retrieve?" — most RAG failures are retrieval
> failures wearing a generation costume.

### "Takes steps / uses tools" → agents → *did it follow a sensible path?*

An **agent** plans and acts: it calls tools, makes decisions, chains steps. The sequence of steps
it took is called the **trajectory.**

Here, a correct final answer can hide a broken path — it issued the refund, but along the way it
also pulled the *wrong* customer's record and just got lucky. So you evaluate the **trajectory**:

- Did it pick the **right tools** for the job?
- Did it take **sensible steps** in a sensible order?
- Did it **avoid harmful or wasteful actions** (e.g., issuing a double refund)?

> **PM takeaway:** for agents, "right answer" isn't enough. A right answer reached by a reckless
> path will eventually reach a wrong — and expensive — one.

### "Holds a conversation" → multi-turn → *does quality survive turn 5?*

Most demos test the *first* reply. Real users have back-and-forths. **Multi-turn** evaluation
checks whether quality holds up over a whole conversation:

- Does it **remember** what was said three turns ago?
- Does it stay **consistent** (not contradict its earlier answer)?
- Does it **stay on policy** as the user pushes, rephrases, or tries to wear it down?

> **PM takeaway:** evaluate conversations, not just opening lines. Failures love to hide in turn 4.

### You don't need to build any of this

Your job today isn't to engineer trajectory tracking. It's to **know what to ask for** and **what
to check**: "Can we see what the bot retrieved?" "Can we log the steps it took?" "Can we test a
5-turn conversation, not just the first reply?" Asking those questions is what a strong AI PM
brings to the table.

---

## Worked example

The refund bot becomes a refund *agent*: it looks up the order, checks eligibility, and issues the
refund. New things to check beyond "was the reply nice?":

1. **Retrieval:** did it pull the *correct order* and the *current* policy doc? (RAG check)
2. **Trajectory:** did it verify eligibility *before* issuing the refund — not after? Did it issue
   exactly one refund? (agent check)
3. **Multi-turn:** if the customer adds "actually, also cancel my subscription," does it handle
   the new request without forgetting the refund? (multi-turn check)

Same feature, three new eval angles — each catching failures the final-answer check would miss.

---

## ✍️ Your turn (12 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"Extra things to check"**:

1. Classify your feature: **simple answer / looks things up (RAG) / takes steps (agent) /
   multi-turn** (it can be more than one).
2. List the **2–3 extra things** you'd need to check beyond the final output — phrased as plain
   questions you'd ask your team.

If your feature is genuinely just "question in, answer out," write that down — knowing you *don't*
need these checks is a valid, useful answer.

---

> **One line to remember:** *A right answer reached the wrong way is a failure you haven't caught
> yet. Check the path, not just the destination.*

**Tomorrow →** You've built real evals. Now we make sure they keep working — catching problems
*before* they ship and noticing when quality quietly drifts. ([Day 9](day-09.md))

---
*Sources: Evals for AI Engineers (Ch.6 Multi-Turn, Ch.7 RAG, Ch.8 Tool Use & Complex Agents).*
