# The AI Evals Playbook — Study Notes

*The whole story, start to finish. Read it like a book, not a checklist.*

> **How this differs from the course.** The [10-day course](overview.md) is a training plan — one
> idea and one exercise a day, done *on your own feature*. These notes are the same material told
> as a single, flowing read: about 35 minutes, no exercises, no homework. Read this when you want
> the *why* and the shape of the whole thing in one sitting. Then go *do* it, a day at a time, in
> the course. When a word is unfamiliar, [`GLOSSARY.md`](../GLOSSARY.md) defines everything in
> plain English.
>
> We'll follow one feature the whole way through — a customer-support **refund assistant** — and
> watch it travel from *"seems fine"* to *measured, trusted, and improving.* One story, eleven
> stops.

---

## 1. The trap that catches almost everyone

Picture a product manager who has just shipped an AI assistant that answers customer questions
about refunds. It's launch week. She opens it, types in three questions, gets three sensible
answers, and tells the team: *"Quality looks great."* Everyone nods. Ship it.

Six weeks later, support is drowning. Customers are quoting a *"30-day refund window"* the company
has never offered — the assistant invented it, confidently, hundreds of times. When the CEO asks
the obvious question — *"so how good is this thing, actually?"* — the honest answer is: **nobody
knows.** There were never any numbers. There was a feeling.

That feeling has a name: the **vibe-check**. Open the product, poke it a few times, decide it
seems good. It isn't evil — it's how every single one of us starts, and it's a perfectly fine first
glance. The trouble is what it can't do. It doesn't *scale* (your assistant handles thousands of
conversations; you looked at three). It doesn't *catch slow decline* (the day quality starts
slipping, the vibe still feels fine). And it *can't be handed to anyone else* (your gut isn't a
document a teammate can run).

The gap between *"it seems good"* and *"here's exactly how good it is, and here's what's breaking"*
— that gap is the whole subject of these notes. Closing it is a craft, and the craft has a name.

---

## 2. What an eval actually is — and why it's *your* job now

An **eval** is a repeatable way to measure whether your AI's output is good. The key word is
*repeatable*: it gives the same answer no matter who runs it, and you can defend it to other people.
That's the entire difference from a vibe-check. A vibe-check is a private opinion. An eval is a
measurement you can show the CEO.

The mindset that makes someone good at this is borrowed from quality assurance: **decide what
"good" means *before* you look, then check against it.** Define the target, then measure. Not the
other way around.

Here's the part that surprises people: this is now a *product* job, not just an engineering one.
In classic software, the spec said "the button turns blue," and engineers made it turn blue —
deterministic, testable, done. With AI, the same input can produce different outputs, and "good" is
a *judgment call*: tone, helpfulness, correctness, safety. Somebody has to own that judgment, write
it down, and defend it. In most teams, the person closest to the user and the business — the
product person — is the one who can. That's why evals went, in the space of a couple of years, from
an obscure engineering concern to *the* hot skill for people who build AI products.

It helps to know where you sit. There are three layers to modern AI, and you only need to care
about one:

- **Pre-training** — building a foundation model from scratch. Costs hundreds of millions. Not you.
- **Post-training** — the big labs tuning a model to follow instructions and behave. Not you.
- **The application layer** — *you*, taking an existing model (Claude, GPT) and wiring it into your
  specific feature. **This is where you live.** And here's the catch that makes evals
  unavoidable: there is no public benchmark for "our refund assistant." Nobody has measured *your*
  product but you. You have to define what good means for it, because no one else can.

Once you *have* evals, they quietly pay you back in three ways. They **monitor** quality over time,
so you spot decline before customers do. They act as **guardrails**, catching a bad output in real
time and blocking or retrying it. And they drive **improvement**, telling you *what* to fix so that
each change actually moves the needle instead of just moving things around. Monitor, guardrail,
improve — keep those three in mind; everything ahead serves one of them.

So that's the destination. The rest of these notes is the route: look at your data, find what's
breaking, turn "good" into a number, make sure you can trust that number, and keep the whole thing
honest over time. It starts with a map.

---

## 3. The three places AI breaks

When the refund assistant gives a bad answer, *why* did it? It feels like a hundred possible
reasons. It's really only three, and naming the right one is half the fix. This is **Shreya
Shankar's Three Gulfs** — a "gulf" being just a gap between two things that ought to line up.

**The Gulf of Comprehension** is the gap between *you and your data* — between what you *think* your
inputs look like and what they *actually* look like. You picture clean, well-formed questions.
Reality is typos, forwarded email threads, three languages in one message, someone pasting a PDF.
You cannot evaluate what you've never looked at, which is exactly why the next stop is *reading your
data*.

**The Gulf of Specification** is the gap between *you and the prompt* — between what you *meant* and
what you actually *told the AI to do*. Natural language is slippery. "Be helpful and concise" never
said "only state our real, approved policies." Every unstated assumption is a door the AI will
wander through. Most "the AI is so dumb" moments are really "the instructions were vague."

**The Gulf of Generalization** is the gap between *a few examples and the messy real world* —
between "works on my ten test cases" and "works on the five hundred ways real people actually ask."
The assistant nails your demo, so you ship; then it meets the long tail of rare, weird, adversarial
inputs and quietly fails on a slice of them. This is the gulf that hides, because your demo never
touches it.

The power of the map is that when something breaks, you stop saying *"the AI is broken"* (useless)
and start asking *"which gulf is this?"* (actionable). A comprehension problem? Go read more real
data. A specification problem? Sharpen the prompt. A generalization problem? Expand your test set to
cover the messy cases. When the refund assistant invents that 30-day window, it's mostly a
*specification* gulf — the prompt never forbade guessing — with a dash of *generalization*, since
it only misbehaves on the rarer questions. Real failures often touch more than one gulf, and that's
fine. The point is you now hold three sharp questions where you used to have one vague complaint.

Notice that every one of those three fixes starts with the same instruction: *go look at your
data.* So let's do exactly that — because it turns out to be the single most powerful thing on this
entire list.

---

## 4. The one skill that beats everything: look at your data

Here is a true and slightly embarrassing story about how teams actually work. A team spends two
weeks debating which expensive eval *tool* to buy. Meanwhile the real problem — the assistant
mishandles anything mentioning "chargeback" — was sitting in the first ten real conversations, in
plain sight, the whole time. Nobody had read them.

The highest-leverage move in all of evals is also the least glamorous: **read your AI's actual
outputs.** Not dashboards. Not aggregate scores. The raw conversations. The people who teach this
craft to engineers at OpenAI and Anthropic say it constantly, and it still feels too simple to be
true. It is the opposite of too simple.

The unit you read is a **trace**: one real record of your AI doing its job — the input it got, the
output it produced, and (for fancier features) the steps in between. The craft of reading a batch
of traces and noticing what's really happening is called **error analysis**, and its first move is
**open coding**. Don't let the word scare you: "coding" here means *labeling*, nothing to do with
programming, and "open" means you arrive with no preset categories — you just read and react.

The method fits in a breath. Pull fifteen to twenty *real* outputs — from production or honest test
usage, not the three cherry-picked demo cases. Read each one fully, and write **one short,
plain-language note**: what went well, what went wrong, anything that surprised you. Be specific.
Not "bad answer," but *"claimed a 30-day refund window we don't offer"* or *"correct, but the tone
was robotic and cold."* Don't fix anything. Don't categorize yet. Just see clearly.

Five rows of that on the refund assistant already tell you almost everything:

| input | output | note |
|---|---|---|
| "can I get a refund after 3 weeks?" | "Yes! You have 30 days." | ❌ invented a 30-day policy we don't have |
| "REFUND NOW or I'm calling my lawyer" | "Sorry to hear that. Our policy is…" | ❌ legal threat — should route to a human, didn't |
| "how do refunds work" | "Refunds go to your original payment in 5–7 days." | ✅ correct + clear |
| "merci, comment ça marche?" | "I can help! Refunds are…" *(in English)* | ⚠️ answered a French question in English |
| "[pastes 40-line email thread]" | "Could you clarify your question?" | ⚠️ choked on a messy real-world input |

Look how much surfaced in five rows: an invented-policy problem, a missing escalation path, a
language gap, a messiness gap. *None* of it was visible from a dashboard. This is also you crossing
the Gulf of Comprehension in real time — your imagination was a far worse test set than reality
turned out to be. Two small tricks make it painless: keep it in a spreadsheet (one row per output;
columns for input, output, and your note — that's the whole tool), and deliberately read the
*scary* ones. The frustrated users, the weird inputs, the long messages. "Thanks, that helped"
teaches you nothing; the messy ones teach you everything.

Now you've got a pile of notes. On its own it feels like noise. The next move turns it into a plan.

---

## 5. From a pile of notes to a ranked list of named problems

Look closely at those notes and a pattern jumps out. *"Invented 30-day policy," "made up a return
address," "guessed at a discount"* — those aren't three problems. They're the **same** problem
wearing three outfits: the assistant **fabricates policies.** Name it once, and suddenly you can
count it, measure it, and fix it. That move — from scattered notes to named patterns — is the
second half of error analysis, sometimes called **axial coding**. It's where the fog becomes a
to-do list.

The method is just *group, name, count, rank.* Group the notes that are really the same underlying
problem. Name each group as a **behavior**, specifically — *"Fabricates a policy that doesn't
exist," "Fails to escalate legal threats"* — not as a vibe like *"accuracy issues"* or *"bad tone
sometimes,"* which are too mushy to measure. Count how often each one showed up in your sample. Then
rank by **frequency × severity**. You'll usually land on three to six **failure modes** — a named,
recurring way your AI gets things wrong. That's the sweet spot; more and you're slicing too thin,
fewer and you're probably still too vague.

Two judgment calls matter here. The first is the **Pareto move**: almost always, a couple of failure
modes cause most of your pain. You don't fix everything — you fix the top one or two, ship, and
re-measure. That's how evals become momentum instead of an endless backlog. The second is that
**severity counts as much as frequency.** A failure that happens 2% of the time but exposes you to
a lawsuit (missing the escalation on a legal threat) outranks a cosmetic tone issue that happens
30% of the time. Rank by how often *times* how badly it hurts, and trust your product judgment on
the "how badly" — that judgment is exactly what you bring that an engineer might not.

For the refund assistant, twenty notes collapse into something like this:

| # | Failure mode | Count (/20) | Severity | Priority |
|---|---|---|---|---|
| 1 | Fabricates a policy that doesn't exist | 6 | High | 🔥 #1 |
| 2 | Fails to escalate legal/angry cases | 3 | High | 🔥 #2 |
| 3 | Answers in the wrong language | 2 | Medium | #3 |
| 4 | Chokes on long/messy pasted input | 2 | Low | later |
| — | (7 outputs were just fine ✅) | 7 | — | — |

That's a plan, not a feeling. (You can hand the notes to Claude or ChatGPT and ask it to draft the
grouping in two minutes — but *you* own the final list. The AI is a fast sorter; it hasn't read the
data the way you have.) "Fabricates policy" is your #1 — six hits, high severity. So that's the one
you'll turn into an actual measurement next.

---

## 6. Turning "good" into a number — the turning point

This is the hinge of the whole story. Up to now you've been *looking*; from here on you're
*measuring*. And the very first thing to measure reveals why most quality debates go nowhere.

Two teammates read the same refund-assistant answer. One says "7 out of 10." The other says "4."
They argue for ten minutes, and neither is wrong — because "7/10" means nothing. It's a vibe
wearing a number's clothing. Now change the question. Suppose the rule is: *"FAIL if the answer
states any refund policy that isn't on our approved list."* Both teammates look. Both say **FAIL.**
No argument. That's the entire power of a good **rubric** — a written rule that decides pass-or-fail
for *one* thing you care about.

The single most useful tip in these notes is this: **make it binary. Pass or fail. Not 1–10.** It
sounds like a downgrade. It's the opposite, for three reasons. First, 1–10 scores are *fake
precision* — nobody can reliably tell a 6 from a 7, so the disagreement feels like measurement but
is really just noise. Second, binary *forces a clear definition* — to say pass or fail you must
define exactly what failure *is*, and that act of definition is the valuable thinking. Third, binary
is *actionable*: "30% fail this check" tells you precisely what to fix, while "average 6.4 out of
10" tells you nothing you can act on. A good rubric is specific enough that two people grade the
same output the same way — so test yours on yesterday's examples, and if you and a teammate
disagree, the rubric is too vague. Sharpen it. Write one rubric per failure mode, starting with
your #1.

A rubric needs something to run against, which is an **eval dataset** — a test set — just a
collection of inputs you run your AI on to check quality. Start *tiny*: three examples is a
legitimate start, ten is great, and you grow it over time. Build it two ways at once. Pull **real
inputs** that trigger your failure mode (your traces from the looking-at-data step are gold), and
**generate** more by asking an AI: *"Give me 30 diverse customer questions about refunds — angry
ones, non-English ones, vague ones."* That generated batch is the fast way to cover the messy long
tail — which, you'll remember, is the Gulf of Generalization. And cover the hard cases *on purpose*:
a test set of only easy questions will always look wonderful and teach you nothing.

Underneath all of this — every eval you will ever run, no matter how sophisticated — sits one
simple five-step loop:

```
1. DRAFT the thing you're testing (a prompt)
2. CREATE a test set that represents reality
3. RUN your AI on each case → collect outputs
4. GRADE each output against your rubric (pass/fail)
5. CHANGE one thing & REPEAT → did the score go up?
```

Step 5 is the magic. The score becomes an **objective baseline**: change the prompt, re-run, and
*see* whether you helped or hurt instead of guessing. Concretely, run the assistant on ten cases,
mark each against the fabrication rubric, and you get — say — **6 out of 10.** That 60% is your
baseline. When you tweak the prompt next week and it hits 9 out of 10, you'll *know* you improved
it. And you need no special software to start: a spreadsheet of test cases with a pass/fail column
is a real eval. The only problem is that hand-grading ten cases is fine, and hand-grading ten
thousand is not. So the grading has to start running by itself.

---

## 7. Who does the grading: code checks vs. an AI judge

There are exactly two ways to automate grading, and the skill is knowing which one each failure
mode needs. (You won't *build* either — but you'll decide which is right and tell your team, and
that decision is genuinely yours.)

A **code evaluator** is a simple, deterministic rule that checks something with a clear yes/no
answer — no judgment, no opinion. It either happened or it didn't. Use it for the rule-shaped
things: a required disclaimer is present, the output is a validly formatted date, a banned word is
absent, the system actually routed to a human when it should have. For the refund assistant: if any
answer quoting a refund *amount* must include the line *"final amounts are confirmed by our team,"*
a code evaluator just checks whether that exact sentence is there. It's fast, basically free, and
never misses what you told it to watch for — but it only catches *exactly* what you programmed. It
can't tell you whether an answer was *helpful*.

An **LLM-as-judge** uses an AI to grade the *subjective* qualities — tone, helpfulness, empathy,
clarity, whether something follows policy in spirit — the way a human reviewer would. Instead of
matching keywords, it reads the output and reasons about whether it's actually good. Use it for "is
the tone calm and professional?", "did it actually answer the question?", "does this honor our
refund policy in spirit?" It's flexible, it catches nuance, and it scales to thousands of outputs —
but there's a catch we'll deal with in the next section: it's an AI grading an AI, so you have to
prove it agrees with humans before you trust it.

These two aren't rivals; they're **layers.** You use both, on different checks — code evaluators for
the objective, compliance-style rules, LLM-judges for the subjective quality calls. The rule of
thumb writes itself: *objective and rule-shaped → code; subjective and judgment-shaped → LLM-judge.*
Mapped across the refund assistant's failure modes, the split is clean:

| Failure mode | Grader | Why |
|---|---|---|
| Fabricates a non-existent policy | **LLM-judge** | Must compare claims to the approved policy *in meaning* |
| Fails to escalate legal/angry cases | **Code eval** | Objective: did the hand-off action fire? Yes/no |
| Answers in the wrong language | **Code eval** | Objective: input language vs. output language |
| Robotic / cold tone | **LLM-judge** | A pure judgment call |

And an LLM-judge is less mysterious than it sounds — it's just a well-written prompt. State the one
thing to judge (keep it binary), give it the rule (your rubric), and ask for a verdict plus a
reason: *"You're grading a support reply. It PASSES only if every refund policy it mentions is on
this approved list: [list]. Otherwise FAIL. Customer message: {input}. Reply: {output}. Answer PASS
or FAIL, then one sentence of why."* That's a real LLM-judge — no code, just a clear prompt and your
rubric. Which raises the obvious, slightly nervous question: can you actually trust an AI to grade
your AI?

---

## 8. Can you trust the judge?

Suppose your LLM-judge reports that the assistant fabricates a policy 8% of the time. Comforting —
unless the judge is wrong. Maybe it's missing half the real fabrications. Maybe it's flagging
perfectly good answers. If your measuring tape is bent, every number you report is bent too. So
before you rely on an automated grader at scale, you do one humble thing: **check it against a
human.** And the human is you.

The method is short. Take a sample of outputs — twenty is plenty to start. Grade each one yourself,
by hand, pass or fail, using your rubric; *this* is your **ground truth**, the correct labels
decided by a person. Then have the LLM-judge grade the same twenty. Compare. Where do you agree?
Where do you disagree? Two numbers describe how good your judge is, and they sound technical but are
really common sense.

**Precision** asks: *"are the alerts real?"* — of the failures your judge flagged, what fraction were
actually failures? Low precision means your judge cries wolf: it flags good answers, you waste time
chasing ghosts, and people stop trusting the eval. **Recall** asks: *"is anything slipping
through?"* — of all the failures that really exist, what fraction did the judge catch? Low recall
means silent misses: your dashboard says "97% good" while customers keep hitting failures the judge
never noticed. Recall is the more dangerous one, precisely because the misses are invisible. The
whole picture fits in a little grid:

| | Judge says FAIL | Judge says PASS |
|---|---|---|
| **Really a fail** | ✅ caught it | ❌ missed it (hurts recall) |
| **Really fine** | ❌ false alarm (hurts precision) | ✅ correct |

You want both high — catch the real failures *and* don't cry wolf. Walk it through once with
numbers: you hand-label twenty answers and find 5 are real fabrications, 15 are clean. Your judge
flags 6. Of those 6, four were real and two were false alarms → **precision = 4/6 ≈ 67%.** Of the 5
real fabrications, it caught four and missed one → **recall = 4/5 = 80%.** Verdict: recall's decent,
precision's shaky. You don't scrap the judge — you *coach* it, the same way you'd coach a new
reviewer: sharpen the rule in its prompt, drop in a couple of example pass/fail outputs so it
calibrates, and re-test against your twenty. Re-run, precision climbs past 90%, and *now* you turn
it loose on the full traffic. (You don't need exact arithmetic, either — "it agreed with me 17 out
of 20 times, and the misses were all false alarms" is a real, useful read.)

When a judge agrees with humans on both counts, something quietly wonderful has happened: you've
effectively *cloned a trusted reviewer*, one that keeps grading thousands of outputs while you
sleep. That's the prize. And the technique outlives AI — precision and recall are how you measure
*any* automated check against human judgment. Learn it once, use it forever. An unvalidated judge,
by contrast, isn't a measurement at all; it's a second opinion you haven't earned the right to
trust.

Everything so far has quietly assumed the simplest possible feature: a question goes in, an answer
comes out. Plenty of real features are fancier — and they hide failures in places the final answer
never shows.

---

## 9. The trickier features: check the path, not just the destination

Your real feature might do more than answer. It might **look things up** before replying (that's
**RAG**). It might **take actions** — check the order system, issue the refund, email the customer
(that's an **agent**). It might **hold a conversation** across many turns (**multi-turn**). For all
three, grading only the final answer isn't enough, because the answer can be right by luck or wrong
for a reason you can't see unless you check the steps.

**When it looks things up (RAG),** ask *did it retrieve the right stuff?* A RAG answer can fail two
completely different ways: retrieval failed (it grabbed the wrong documents, or none) or generation
failed (it had the right documents and still answered badly). So you check two things — *did it find
the right information,* and *did it use that information correctly.* A wrong answer from a *missing*
document needs a totally different fix than a wrong answer from a *present* one. The PM takeaway:
always ask "what did it retrieve?" — most RAG failures are retrieval failures wearing a generation
costume.

**When it takes steps (an agent),** ask *did it follow a sensible path?* An agent plans and acts —
it calls tools, makes decisions, chains steps — and the sequence it took is its **trajectory.** Here
a correct final answer can hide a broken path: it issued the right refund, but along the way it
pulled the *wrong* customer's record and simply got lucky. So you evaluate the trajectory itself:
did it pick the right tools, take sensible steps in a sensible order, and avoid harmful or wasteful
actions like issuing a double refund? A right answer reached by a reckless path will, sooner or
later, reach a wrong and expensive one.

**When it holds a conversation (multi-turn),** ask *does quality survive turn 5?* Most demos test
only the first reply; real users have back-and-forths. Does the assistant remember what was said
three turns ago, stay consistent rather than contradict itself, and hold the line on policy as the
user rephrases and pushes? Failures love to hide in turn 4.

You don't need to *build* trajectory tracking or retrieval logging. Your job is to **know what to
ask for**: "Can we see what the bot retrieved?" "Can we log the steps it took?" "Can we test a
five-turn conversation, not just the opening line?" Asking those questions is exactly what a strong
AI PM brings to the table. (And if your feature genuinely is just question-in, answer-out, knowing
you *don't* need these checks is itself a useful, valid answer.)

By now you've built something real. The last risk is that it quietly stops working when everyone's
attention moves on.

---

## 10. Keeping it alive: regressions and drift

Here's the cruel twist. You did all the work — found the failure modes, wrote the rubrics, validated
the judge. Quality's good. Three months later it's bad again, and nobody noticed until customers
did. Two things always happen to AI products over time, and an eval you run *once* catches neither.
An eval that runs *on a schedule* catches both.

The first is **regression**: someone tweaks the prompt or swaps the model, and something that used
to work breaks. The defense is a **quality gate** — every time the prompt or model changes, run your
test set *first* and compare the score to the previous version. If it drops, the change doesn't ship
until it's fixed. This is where **prompt versioning** earns its keep: track your prompt as v1, v2,
v3, and score each against the *same* test set, so "is v3 better than v2?" becomes a number instead
of an argument. Engineers call the automated form of this a **CI check** — it runs on every change
and blocks the bad ones — and you don't build it, you *ask* for it. Your one sentence is: *"Before
we ship a prompt or model change, it has to pass our eval set — can we make that a required check?"*
That sentence makes you the PM who prevents fire drills instead of running them.

The second is **drift**: nothing changes on your side, but the world does, and quality slowly
slides. Your inputs change (new products, new slang, new edge cases your original test set never
imagined), and the *model itself* can change under you (vendors update models, and behavior shifts
without warning — a well-known study once found a model's accuracy on a task swing dramatically
between two versions months apart). The defense is cheap and humble: pick a cadence — weekly is a
good default — re-sample real production outputs, re-score them, and watch the number over time. A
slow slide from 92% → 88% → 84% is drift, and you want to see it as a gentle trend on your own
dashboard, not as a cliff your customers discover for you. Keep the test set fresh, too — swap in
new real examples periodically, because a test set frozen at launch slowly stops describing your
actual product.

And keep a human in the loop. Automated graders do the heavy lifting, but the best teams still
spot-check a handful of real traces by hand each week. It keeps your judgment calibrated and catches
the brand-new failure mode your automated checks were never told to look for — which is really just
the looking-at-your-data habit from earlier, repeated forever, in small doses. The whole habit fits
in one breath: *check before every change, re-sample every week, refresh the test set, and keep
reading a few real outputs by hand.* It's about twenty minutes a week, and it buys you "we caught it
early" instead of "the customer caught it."

There's one move left — the one that turns all this measurement into something the business actually
cares about.

---

## 11. Closing the loop: improve it, then prove it

Here's the thing nobody says out loud: **an eval that doesn't change the product is just expensive
journaling.** The point was never the score. The point is a better product — and being able to prove
it to the people who decide where time and money go. Two moves close the loop: *improve*, then
*communicate.*

To **improve**, point the same five-step loop from before at your #1 failure mode — look at the
failures, measure a baseline, change one thing, re-measure, keep it or revert. Your levers, cheapest
first: **fix the prompt** (the most common and cheapest fix — *"only state policies from this list;
if unsure, say you'll check"* kills a lot of fabrication, and most Specification-gulf problems die
right here); **fix the inputs or retrieval** (if it's a RAG feature pulling the wrong docs, fix
retrieval before blaming the model); or **change the architecture or model** (add a guardrail, add
an escalation step, or upgrade the model — the heavy lever, for when prompt fixes plateau). The
discipline that makes you trustworthy is the same one from the start: change one thing, re-run the
eval, compare to baseline. Up? Keep it. Not? Revert and try again. You're no longer guessing whether
you helped — you can see it.

To **communicate**, write a short **eval report** — for stakeholders, not engineers. The same facts
can land as "trust me, it's good" or as a crisp case that earns you resources and credibility, and
the difference is five plain lines: *what we measured* (the feature and its top failure modes), *how
good it is* (pass rates in plain numbers), *what's still failing* (honestly, the top remaining
problem), *what we're doing about it* (the next fix and its expected impact), and *how we know it
won't rot* (your cadence — the smoke detector from the last section). For the refund assistant it
reads like this:

> **Refund Assistant — Eval Report (this month)**
> **Measured:** policy accuracy, escalation of legal/angry cases, language match.
> **Quality:** policy-accuracy check now passes **91%** (was 60% at the start of the month);
> escalation **100%**; language match **96%**.
> **Still failing:** ~9% of answers on rare product types still state an unverified policy.
> **Next fix:** add those product types to the approved-policy source; expect 91% → ~97%.
> **How we keep it honest:** 30-case eval gate on every prompt change; 50 real conversations
> re-scored weekly; test set refreshed monthly.

Five lines. A busy executive gets it in thirty seconds; a skeptical one can't poke a hole in it.
Numbers plus honesty beat adjectives every time. And this report does something bigger than report:
it changes how leadership *sees* AI quality — from a black box they take on faith into something a
product person owns, measures, and steers. It's the artifact that gets your program funded instead
of cut, and (not coincidentally) the kind of document compliance and governance teams increasingly
need as AI oversight tightens.

---

## 12. Where this leaves you

Walk back over the whole arc. You started where almost everyone starts — opening the product, trying
a few things, calling it good. Then you gave that instinct a spine. You learned what an eval really
is and why owning it is now a product job. You got a map of the three places AI breaks. You did the
unglamorous, decisive thing — *read your actual data* — and turned a pile of notes into a ranked
list of named failure modes. You made "good" measurable with binary rubrics and a small test set,
chose the right grader for each problem, and *proved* you could trust the AI judge with precision
and recall. You learned to check the path and not just the destination for the trickier features.
You built a habit that catches regressions and drift before customers do. And you closed the loop —
turning results into a fix and a five-line report that makes you the most credible person in the
room.

**In one breath:** *You don't need to be an engineer to own AI quality. You need to look at your
data, measure what matters, prove you can trust the measurement, and keep it honest over time. That
is the job — and now it's yours.*

When you're ready to do it for real — on *your* feature, one bite a day — start the
[10-day course](overview.md) at [Day 1](day-01.md), and keep your work in the
[Eval Plan template](my-eval-plan-template.md). Reading it through was the map. The course is the
walk.

---

*These notes are an original synthesis of: Hamel Husain & Shreya Shankar, **Evals for AI
Engineers** (error analysis, rubrics, automated evaluators, RAG/agents/multi-turn, CI/CD, improving
agents); Shreya Shankar's **Three Gulfs** framework (after Norman, 1988); the LinkedIn Learning
courses on a typical eval workflow, automated evals (code evaluators & LLM-as-judge, precision/
recall), and evaluation reports as stakeholder artifacts; Hamel's [LLM Evals
FAQ](https://hamel.dev/blog/posts/evals-faq/); and Lenny's Newsletter, [Why AI evals are the
hottest new skill](https://www.lennysnewsletter.com/p/why-ai-evals-are-the-hottest-new-skill).
Concepts are credited to their authors; all wording and the running example here are original.*
