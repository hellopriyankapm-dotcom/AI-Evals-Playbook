# Glossary — every term, in plain English

No jargon walls. If a word shows up in a lesson, it's defined here in one or two sentences,
PM-first.

---

**Eval (evaluation)** — A systematic way to measure whether your AI's output is *good*. Not a
gut check — a repeatable measurement you (and others) can trust.

**Vibe-check** — Judging AI quality by eyeballing a few outputs and going "yeah, seems fine."
The thing this course replaces. Fine for a demo; dangerous as a quality bar.

**Trace** — One real record of your AI doing its job: the input it got, the steps it took, and
the output it produced. "Looking at your data" means reading traces.

**Application-level eval** — Evaluating *your specific feature* (e.g., "does our support bot
answer refund questions correctly?"), as opposed to evaluating a raw model on generic
benchmarks. This is where PMs and product teams work.

**The Three Gulfs** — A map of where AI products break (from Shreya Shankar):
- *Gulf of Comprehension* — the gap between you and **your data**: you don't actually know what
  your real inputs and outputs look like.
- *Gulf of Specification* — the gap between you and **the prompt**: what you meant vs. what you
  actually told the AI to do.
- *Gulf of Generalization* — the gap between **a few examples and the messy real world**: it
  works on your test cases but not on everything users throw at it.

**Error analysis** — The core eval skill: read a batch of real outputs, note what went wrong,
then group those notes into patterns. Two steps:

**Open coding** — Step 1 of error analysis. Read each output and write a short, freeform note
about what happened — no preset categories yet.

**Axial coding** — Step 2 of error analysis. Group your freeform notes into a handful of named,
recurring themes.

**Failure mode** — A named, recurring way your AI gets things wrong (e.g., "invents a policy
that doesn't exist," "ignores the user's budget"). The output of error analysis.

**Pareto failure modes** — The few failure modes that cause most of your problems. Fix these
first.

**Rubric** — The written rule that decides pass vs. fail for one thing you care about. Good
rubrics are specific enough that two people would grade the same output the same way.

**Binary (pass/fail) eval** — A rubric that gives a yes/no answer instead of a fuzzy 1–10
score. Recommended: "did it ignore the budget? yes/no" beats "rate budget-handling 1–10."

**Eval dataset (test set)** — A collection of test inputs you run your AI on to measure
quality. Can start with 3 examples; grows to dozens or hundreds.

**AI-generated test cases** — Using an AI (e.g., "generate 50 diverse customer questions about
refunds") to build your test set fast instead of hand-writing every example.

**Grader** — Whatever assigns the pass/fail (or score) to each output. Two kinds:

**Code evaluator** — A simple deterministic rule that checks something objective: did the
output contain the required disclaimer? did it route to a human when asked? Cheap, fast, never
subjective. Catches only what you explicitly program.

**LLM-as-judge** — Using an AI to grade subjective qualities (tone, helpfulness, policy
adherence) the way a human reviewer would. Flexible, but you must check it agrees with humans
before trusting it.

**Ground truth** — The "correct" labels, decided by a human. You compare your automated grader
against ground truth to see if the grader can be trusted.

**Precision (for evals)** — Of the failures your automated grader flagged, what % were *real*
failures? Low precision = it cries wolf.

**Recall (for evals)** — Of all the *actual* failures, what % did your grader *catch*? Low
recall = it misses real problems.

**Alignment (of a grader)** — How closely your automated grader's verdicts match a human's.
High precision + high recall = a trustworthy grader you can run at scale.

**Prompt versioning** — Tracking your prompt as v1, v2, v3… and scoring each version against the
*same* test set, so you can tell whether a change actually made things better.

**RAG (Retrieval-Augmented Generation)** — When your AI "looks things up" in a knowledge base
before answering. The extra thing to evaluate: did it retrieve the *right* information?

**Agent / tool use** — When your AI "takes steps" — calls tools, plans, acts (e.g., books a
flight, queries a database). The extra thing to evaluate: did it follow a *sensible path*
(the trajectory), not just land a final answer?

**Trajectory** — The sequence of steps an agent took to reach its answer. You evaluate the
path, not only the destination.

**Multi-turn** — A back-and-forth conversation. The extra thing to evaluate: does quality hold
up by turn 5, not just on the first reply?

**Drift** — When your AI's quality quietly changes over time — because the world changed, usage
changed, or the model was updated underneath you. Why you re-check on a schedule.

**Regression** — A change (new prompt, new model) that makes quality *worse* on things that
used to work. The reason you run a check *before* shipping changes.

**Quality gate / CI for evals** — A check that runs automatically before a change ships, blocking
it if eval scores drop. As a PM you ask for this; you don't build it.

**Monitoring** — Watching a few quality numbers on live production traffic over time.

**Guardrail** — An eval that runs in real time and blocks/retries/falls back when an output
fails (e.g., refuses to send a response containing a banned claim).

**Eval report** — A short, plain-language summary of how good your AI is, what's failing, and
what you're doing about it — written for stakeholders, not engineers.
