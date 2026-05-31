# Day 3 — Look at your data (the skill that beats everything)

**≈12 min read + one exercise.** Today: the one habit that separates people who are good at evals
from everyone else. It's almost embarrassingly simple, and almost nobody does it.

---

## The scene

A team spends two weeks arguing about which fancy eval tool to buy. Meanwhile, the actual problem
— the bot mishandles anything mentioning "chargeback" — was sitting in the first ten real
conversations, in plain sight. Nobody had read them.

Here's the punchline of modern evals, straight from the people who teach it to OpenAI and
Anthropic: **the highest-leverage thing you can do is read your AI's actual outputs.** Not
dashboards. Not aggregate scores. The raw stuff.

---

## The one idea: read the traces, write what you see

A **trace** is one real record of your AI doing its job — the input it got and the output it
produced (and, for fancier features, the steps in between).

**Error analysis** is the craft of reading a batch of traces and noticing what's actually
happening. It has two steps. Today is step one: **open coding.**

### Open coding (today)

"Coding" here means *labeling* — nothing to do with programming. **Open** means you don't bring
preset categories; you just read and react.

The whole method:

1. Pull **15–20 real outputs** of your feature. Real ones — from production or honest test usage,
   not the three cherry-picked demo cases.
2. Read each one fully. For each, write **one short, plain-language note**: what went well, what
   went wrong, anything surprising.
3. Be specific. Not "bad answer" — write *"claimed a 30-day refund window we don't offer"* or
   *"correct, but the tone was robotic and cold."*
4. Don't fix anything yet. Don't categorize yet. Just see clearly.

That's it. It feels too simple to be powerful. It is the opposite of too simple.

### Why this beats everything

- **It surfaces failures you'd never have guessed.** Your imagination is a worse test set than
  reality. (This is you crossing the Gulf of Comprehension from Day 2.)
- **It's the only way to know what to measure.** You can't write a rubric for a failure you've
  never seen. Tomorrow's failure modes come *directly* from today's notes.
- **It kills "vibes-driven" debates.** "I feel like it's gotten worse" loses to "here are 8
  outputs where it invented a policy."

> Practitioners like Hamel Husain make this point constantly: when someone asks which fancy eval
> to build first, the honest answer is almost always *go read your own data first.*

### Two tips that make it painless

- **Put it in a spreadsheet.** One row per output. Columns: `input`, `output`, `your note`. That's
  your whole tool. No code, no platform.
- **Read the scary ones.** Frustrated users, weird inputs, long messages. The boring "thanks, that
  helped" traces teach you nothing; the messy ones teach you everything.

---

## Worked example

Five rows from a refund-bot open-coding pass:

| input | output | note |
|---|---|---|
| "can I get a refund after 3 weeks?" | "Yes! You have 30 days." | ❌ invented a 30-day policy (we have none) |
| "REFUND NOW or I'm calling my lawyer" | "Sorry to hear that. Our policy is…" | ❌ legal threat — should route to human, didn't |
| "how do refunds work" | "Refunds are processed to your original payment method in 5–7 days." | ✅ correct + clear |
| "merci, comment ça marche?" | "I can help! Refunds are…" *(in English)* | ⚠️ answered French question in English |
| "[pastes 40-line email thread]" | "Could you clarify your question?" | ⚠️ choked on a real-world messy input |

Look how much you already know after five rows: an invented-policy problem, a missing escalation
path, a language gap, a messiness gap. *None* of that was visible from the dashboard.

---

## ✍️ Your turn (15 min — the most important exercise of the week)

In [`my-eval-plan-template.md`](my-eval-plan-template.md), fill in **"What I found reading my
data"**:

1. Pull **15–20 real outputs** of your feature into a spreadsheet (input, output, note).
2. Read every one. Write **one specific note** per output.
3. Deliberately include the messy, angry, and weird ones.

Resist the urge to fix or categorize. Just see. Tomorrow you'll turn these notes into a ranked
list of what's actually breaking.

---

> **One line to remember:** *You cannot evaluate what you have not read. Looking at your data is
> not the boring prerequisite to the real work — it **is** the real work.*

**Tomorrow →** You've got a pile of notes. Now we turn that pile into a short, ranked list of named
failure modes — the thing you'll actually measure. ([Day 4](day-04.md))

---
*Sources: Evals for AI Engineers (Ch.3 Error Analysis, Ch.11 Data Analysis for Traces); Hamel
& Shreya via [Lenny's Newsletter](https://www.lennysnewsletter.com/p/evals-error-analysis-and-better-prompts).*
