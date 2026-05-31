# Day 1 — Stop vibe-checking your AI

**≈12 min read + one exercise.** Today: what an eval actually is, why it's now *your* job, and
the baseline you'll measure everything against.

---

## The scene

A PM ships an AI assistant that answers customer questions about refunds. Launch week, she opens
it, types three questions, gets three good answers, and tells the team: *"Quality looks great."*

Six weeks later, support is drowning. Customers are getting told about a "30-day refund window"
the company has never offered. When the CEO asks "how good is the AI, actually?", the honest
answer is: *nobody knows.* There were never any numbers. There was a vibe.

That gap — between *"it seems good"* and *"here's how good it is, and here's what's breaking"* —
is the gap this course closes.

---

## The one idea: an eval is systematic measurement of quality

**An eval is a repeatable way to measure whether your AI's output is good** — one that gives you
the same answer no matter who runs it, and that you can defend to other people.

The opposite is the **vibe-check**: open the product, try a few things, decide it's fine. The
vibe-check isn't evil — it's how everyone starts. The problem is it doesn't *scale*, it doesn't
*catch slow decline*, and it *can't be handed to anyone else.* Your AI handles thousands of
inputs; you looked at three.

Here's the mindset shift that makes you good at this:

> **Treat every AI output the way a QA analyst treats a release: define what "good" means *before*
> you look, then check against it.**

### Why this is the PM's job now

In classic software, the spec said "the button turns blue," and engineers made it turn blue.
Deterministic. With AI, the same input can produce different outputs, and "good" is a *judgment* —
tone, helpfulness, correctness, safety. Someone has to own that judgment, write it down, and
defend it.

That someone is you. Evals are how a product person steers an AI product. (This is exactly why
evals went from obscure to *the* hot skill for product builders — Hamel & Shreya call it the new
core competency.)

### Where you operate: the application layer

Three layers exist, and you only need to care about one:

- **Pre-training** — building a foundation model from scratch. Costs hundreds of millions. Not you.
- **Post-training** — labs tuning a model to follow instructions and be safe. Not you.
- **Application** — *you* taking an existing model (Claude, GPT) and wiring it into your specific
  feature. **This is where you live.** There's no public benchmark for "our refund bot." You have
  to define what good means for *your* product. Nobody else can.

### The three jobs an eval does

Once you have evals, they pay off in three ways:

1. **Monitoring** — quietly watching quality over time so you spot decline before customers do.
2. **Guardrails** — catching a bad output in real time and blocking or retrying it.
3. **Improvement** — telling you *what* to fix so each change actually makes things better.

Today you're not building any of these yet. You're naming your target.

---

## Worked example

For the refund bot, a vibe-check says: *"Tried it, seems helpful."*

An eval mindset says: *"'Good' means: (a) the refund policy stated is factually our real policy,
(b) the tone is calm and professional, (c) if the customer is angry or it's a legal threat, it
routes to a human. I will measure each of these against real outputs."*

Same feature. One of these you can improve, defend, and hand off. The other is a feeling.

---

## ✍️ Your turn (10 min)

Open your [`my-eval-plan-template.md`](my-eval-plan-template.md) and fill in **"The feature I'm
evaluating"**:

1. **Pick one real AI feature** you'll use for the whole course.
2. Write **what it's supposed to do** (one sentence) and **who uses it.**
3. Write, honestly, **how you judge "good" today** — your current vibe-check.
4. Write **one real failure you've already seen** (or go find one now by using the feature for
   five minutes).

That's your baseline. Everything you build over the next nine days improves on it.

---

> **One line to remember:** *A vibe-check is what you do before you have an eval. An eval is what
> you show the CEO.*

**Tomorrow →** Before you can fix what's breaking, you need a map of *where* AI products break.
It turns out there are exactly three places. ([Day 2](day-02.md))

---
*Sources: Hamel Husain & Shreya Shankar, Evals for AI Engineers (Ch.1); Hamel's
[LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/); Lenny's Newsletter,
[Why AI evals are the hottest new skill](https://www.lennysnewsletter.com/p/why-ai-evals-are-the-hottest-new-skill).*
