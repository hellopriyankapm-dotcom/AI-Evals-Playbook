# Day 6 — Two kinds of graders: code vs LLM-as-judge

**≈12 min read + one exercise.** Today: how grading gets automated so you're not hand-checking
outputs forever — and the simple rule for which tool fits which job.

---

## The scene

Hand-grading 10 test cases on Day 5? Totally fine. But your AI handles *thousands* of real
interactions. You can't read them all, and neither can your team. To measure quality at that
scale, the grading has to run by itself.

There are exactly two ways to automate a grader. The skill is knowing which one each of your
failure modes needs. (You don't build either one — but you decide which is right and tell your
team. That decision is yours.)

---

## The one idea: two graders, two jobs

### 1. Code evaluators — for things that are objective

A **code evaluator** is a simple, deterministic rule that checks something with a clear yes/no
answer. No judgment, no opinion — it either happened or it didn't.

**Use it for:** required disclaimers present, output is valid (e.g., a properly formatted date),
a banned word is absent, the system routed to a human when it should have.

**The classic example (insurance bot):** if a customer says *"I want to talk to a human,"* the
system **must** hand off to a human agent. A code evaluator checks: did the message contain that
request, and did the hand-off actually fire? It's not subjective — it happened or it didn't.

- ✅ **Strengths:** fast, basically free, never misses what it's told to check.
- ⚠️ **Limit:** it only catches exactly what you programmed. It can't judge "was this *helpful*?"

### 2. LLM-as-judge — for things that need judgment

An **LLM-as-judge** uses an AI to grade the *subjective* qualities — tone, helpfulness, empathy,
clarity, policy adherence — the way a human reviewer would. It's *"closer to human annotation"*:
it reads the output and reasons about quality.

**Use it for:** "Is the tone calm and professional?" "Did it actually answer the question?" "Does
this follow our refund policy in spirit?" — the things a checklist of keywords can't capture.

- ✅ **Strengths:** flexible, catches nuanced failures, scales to thousands of outputs.
- ⚠️ **Catch:** it's an AI grading an AI — so you must verify it agrees with humans before you trust
  it. (That's literally tomorrow's whole lesson.)

### They're layers, not rivals

You don't choose one *or* the other for your product — you use **both, on different checks.** Code
evaluators handle the objective, compliance-style rules; LLM-judges handle the subjective quality
calls. Together they watch your whole system continuously.

> **The rule:** *Objective and rule-shaped? → code evaluator. Subjective and judgment-shaped? →
> LLM-as-judge.*

### Writing an LLM-judge prompt (you can absolutely do this)

An LLM-judge is just a well-written prompt. The recipe:

1. **State the one thing to judge** (keep it binary, like Day 5).
2. **Give the rule** — your rubric.
3. **Ask for a verdict + a reason.** Example:

> *"You are grading a customer-support reply. RULE: it PASSES only if every refund policy it
> mentions is on this approved list: [list]. Otherwise it FAILS. Here is the customer message:
> {input}. Here is the reply: {output}. Answer PASS or FAIL, then one sentence explaining why."*

That's a real LLM-judge. No code — just a clear prompt and your rubric.

---

## Worked example

Refund bot, mapping each failure mode to a grader:

| Failure mode | Grader | Why |
|---|---|---|
| Fabricates a non-existent policy | **LLM-judge** | Needs to compare claims to approved policy *in meaning*, not keywords |
| Fails to escalate legal/angry cases | **Code eval** | Objective: did the hand-off action fire? Yes/no |
| Answers in the wrong language | **Code eval** | Objective: detect input language vs output language |
| Robotic / cold tone | **LLM-judge** | Pure judgment call |

Notice the split: the crisp, rule-shaped checks go to code; the "read it and judge" checks go to
the LLM. That mapping *is* the skill.

---

## ✍️ Your turn (12 min)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"My graders"**:

1. For each of your failure modes, decide: **code evaluator or LLM-as-judge?** Write one line of
   *why.*
2. Pick one **subjective** failure mode and **draft its LLM-judge prompt** using the recipe above.

---

> **One line to remember:** *Code evals check what must always be true. LLM-judges check what a
> thoughtful human would notice. You need both.*

**Tomorrow →** An LLM grading your AI sounds a little like asking the fox about the henhouse. So
before you trust it: does your judge actually agree with humans? There's a clean way to find out.
([Day 7](day-07.md))

---
*Sources: Chantal Cox & Aman Khan, "Automated evals: Code evaluators and LLM-as-judge" (LinkedIn
Learning); Evals for AI Engineers (Ch.5 Implementing Automated Evaluators).*
