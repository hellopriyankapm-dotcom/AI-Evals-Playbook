# The AI Evals Playbook — Study Notes

*The whole story, start to finish. Read it like a book, not a checklist.*

> **How this differs from the course.** The [10-day course](overview.md) is a training plan — a
> single idea and a single exercise each day, worked *on your own feature*. These notes cover the
> same ground as one continuous read: roughly 35 minutes, nothing to fill in. Reach for this when
> you want the *reasoning* and the overall shape in one sitting; then go *practise* it, a day at a
> time, in the course. Any unfamiliar word is defined plainly in [`GLOSSARY.md`](../GLOSSARY.md).
>
> One feature travels with us the entire way — a customer-support **refund assistant** — so you can
> watch it move from *"seems okay"* to *measured, trusted, and steadily improving.* One story,
> eleven stops.

---

## 1. The trap that catches almost everyone

Imagine a product manager who's just launched an AI assistant for refund questions. It's the first
week. She tries a handful of prompts, the replies look reasonable, and she reports back to the
team that quality is in good shape. Heads nod. The feature stays live.

A month and a half later, the support queue is on fire. The assistant has been telling customers
about a *"30-day refund window"* that the business simply doesn't have — and it's been doing so
confidently, again and again. When leadership asks the natural question — *just how good is this
thing?* — there's no real answer to give. No measurements were ever taken. There was only an
impression.

That impression has a name: the **vibe-check**. You open the product, prod it a few times, and
conclude it feels fine. There's nothing shameful about it — it's where everyone begins, and as a
first glance it's perfectly reasonable. What it *can't* do is the problem. It doesn't stretch to
scale (your assistant fields thousands of conversations; you sampled a few). It can't spot a slow
decline (on the day quality starts slipping, your gut still says fine). And it isn't transferable —
an instinct in your head isn't something a colleague can pick up and run.

The distance between *"it feels good"* and *"here is precisely how good it is, and here's what's
going wrong"* — that distance is the entire subject of these notes. Bridging it is a discipline, and
the discipline has a name.

---

## 2. What an eval actually is — and why it's *your* job now

An **eval** is a repeatable method for judging whether your AI's output is any good. *Repeatable* is
the load-bearing word: run it tomorrow, or hand it to a teammate, and you get the same verdict — and
you can stand behind it in front of other people. That's the whole gap from a vibe-check. A
vibe-check is a private hunch; an eval is a result you'd put in front of leadership.

The habit that separates the people who are good at this is borrowed straight from quality
assurance: settle on what *good* means **before** you go looking, and then measure against that
definition — never the reverse.

What surprises a lot of teams is that this lands on the *product* desk now, not only the engineering
one. Old-school software was deterministic: the spec promised a particular behaviour, the code
delivered exactly that behaviour, and you could check it off. AI breaks that contract. Feed it the
same input twice and the output can differ, and "good" turns into a matter of *judgement* — was the
tone right, was it genuinely helpful, was it correct, was it safe? Someone has to own that
judgement, commit it to paper, and defend it, and in most teams the person closest to the user and
the business is the one positioned to do so. That's why, in just a couple of years, evals went from
a niche engineering chore to the headline skill for people who build with AI.

It helps to know where you actually sit. Modern AI stacks up in three layers, and only one of them
is yours to worry about:

- **Pre-training** — creating a foundation model from nothing. A budget in the hundreds of millions.
  Not your table.
- **Post-training** — the big labs shaping a model to follow instructions and stay safe. Also not
  yours.
- **The application layer** — *you*, taking a ready-made model (Claude, GPT) and wiring it into one
  specific feature. **This is your home turf.** And here's what makes evals unavoidable: no public
  leaderboard exists for "our refund assistant." Nobody on earth has measured *your* product except
  you. Defining good for it falls to you, because it can't fall to anyone else.

Once evals exist, they quietly repay you three ways. They **monitor**, tracking quality over time so
a decline shows up on your dashboard before it shows up in your inbox. They act as **guardrails**,
intercepting a bad output in the moment and blocking or retrying it. And they fuel **improvement**,
pointing at *what* to change so each edit genuinely advances things instead of just rearranging
them. Monitor, guard, improve — hold those three loosely in mind; everything ahead is in service of
one of them.

So that's the destination. The remainder of these notes is the route there: study your data, locate
what's failing, convert "good" into a figure, confirm that figure is trustworthy, and keep the whole
arrangement honest as time passes. It opens with a map.

---

## 3. The three places AI breaks

When the refund assistant produces a poor answer, *what went wrong?* It seems like there could be a
hundred causes. There are really only three, and pinning the right one down is most of the cure.
This is **Shreya Shankar's Three Gulfs** framework — where a "gulf" is nothing more than a gap
between two things that ought to be in step.

The **Gulf of Comprehension** sits between *you and your data*: the distance between the inputs and
outputs you *picture* and the ones that *actually arrive*. In your head the questions are tidy and
well-formed. In the wild they're riddled with typos, pasted-in email chains, three languages in a
single message, the occasional attached PDF. You can't assess what you've never laid eyes on — which
is exactly why the very next move is to go and read your data.

The **Gulf of Specification** sits between *you and the prompt*: the distance between what you *had
in mind* and what you genuinely *instructed the AI to do*. Plain language leaks. "Be helpful and
concise" never once said "and only ever state policies from our approved list." Every assumption you
left unspoken is an opening the model will stroll through. Most "why is the AI so dim" moments are,
on inspection, "the instructions were fuzzy" moments.

The **Gulf of Generalization** sits between *a few examples and the real, messy world*: the distance
between "passes my ten test cases" and "holds up across the five hundred ways real people phrase
things." The assistant aces your demo, so out it goes — and then it meets the long tail of rare,
odd, adversarial inputs and fails quietly on some fraction of them. This is the gulf that stays
hidden, because a demo never wanders near it.

The map earns its keep the moment something breaks, because it swaps a useless sentence for a useful
one. Instead of *"the AI is broken,"* you ask *"which gulf is this?"* Comprehension trouble? Go read
more real data. Specification trouble? Sharpen the prompt. Generalization trouble? Widen the test
set until it covers the awkward cases. When the assistant conjures that 30-day window, it's mostly a
*specification* gulf — nothing in the prompt forbade guessing — with a streak of *generalization*,
since it only slips on the less common questions. Plenty of real failures straddle more than one
gulf, and that's fine. What you've gained is three precise questions where you used to have one vague
gripe.

Notice that all three remedies open with the same instruction: *go and look at your data.* So let's
do precisely that — because it turns out to be the single most powerful item on the whole list.

---

## 4. The one skill that beats everything: look at your data

Here's a true and faintly awkward picture of how teams actually behave. A group burns two weeks
debating which pricey eval *platform* to purchase. All the while, the real defect — the assistant
mangles anything that mentions "chargeback" — was sitting in plain view in the first ten real
conversations. Nobody had opened them.

The highest-return move in all of evals is also the least glamorous: **read the outputs your AI is
actually producing.** Not dashboards, not roll-up scores — the raw exchanges. The practitioners who
teach this craft to engineers at the major labs repeat it endlessly, and it still sounds too plain
to matter. It is anything but.

The thing you read is a **trace**: a single real record of the AI doing its job — the input it
received, the output it returned, and (for richer features) the steps it took along the way. The
craft of working through a batch of traces and registering what's truly going on is **error
analysis**, and its opening move is **open coding**. Don't be put off by the term: "coding" here
means *tagging*, with no connection to programming, and "open" means you walk in with no ready-made
buckets — you simply read and respond.

The recipe is short enough to hold in one breath. Gather fifteen to twenty *genuine* outputs — from
production or honest hands-on use, not the three flattering ones from the demo. Read each one
properly, and jot **one brief, plain note**: what worked, what didn't, anything that caught you off
guard. Be concrete. Not "bad answer," but *"quoted a 30-day window we don't offer"* or *"accurate,
but the tone came off cold and mechanical."* Don't repair anything. Don't sort into groups yet. Just
look clearly.

Five rows of this on the refund assistant already hand you most of the picture:

| input | output | note |
|---|---|---|
| "can I get a refund after 3 weeks?" | "Yes! You have 30 days." | ❌ invented a 30-day window we don't have |
| "REFUND NOW or I'm calling my lawyer" | "Sorry to hear that. Our policy is…" | ❌ legal threat — should hand off to a person, didn't |
| "how do refunds work" | "Refunds go to your original payment in 5–7 days." | ✅ accurate and clear |
| "merci, comment ça marche?" | "I can help! Refunds are…" *(in English)* | ⚠️ replied in English to a French question |
| "[pastes 40-line email thread]" | "Could you clarify your question?" | ⚠️ stumbled on a messy real-world input |

See how much falls out of five rows: a fabrication problem, a missing hand-off, a language gap, a
messiness gap. *None* of it was legible from a dashboard. This is also you crossing the Gulf of
Comprehension live — your imagination, it turns out, was a far feebler test set than reality.
Two small habits keep it painless: work in a spreadsheet (one row per output, columns for input,
output, and your note — that's the entire toolkit), and pointedly read the *uncomfortable* ones. The
irritated users, the strange inputs, the sprawling messages. "Thanks, that sorted it" teaches you
nothing; the messy cases teach you everything.

Now you're holding a heap of notes. By itself it feels like static. The next move turns it into a
plan.

---

## 5. From a pile of notes to a ranked list of named problems

Stare at those notes for a moment and a shape emerges. *"Invented a 30-day window," "made up a
return address," "guessed at a discount"* — that isn't three problems. It's one problem in three
disguises: the assistant **fabricates policy.** Name it once and you can suddenly count it, measure
it, and go after it. That step — from loose notes to named patterns — is the back half of error
analysis, sometimes called **axial coding.** It's where the haze hardens into a to-do list.

The method is just *group, name, count, rank.* Cluster the notes that are secretly the same
underlying fault. Name each cluster as a **behaviour**, and be specific about it — *"fabricates a
policy that doesn't exist," "fails to escalate legal threats"* — rather than mush like *"accuracy
issues"* or *"sometimes the tone's off,"* which are too soft to measure. Tally how often each one
turned up in your sample. Then order them by **frequency × severity**. You'll usually settle on three
to six **failure modes** — a named, recurring way the AI goes wrong. That range is the sweet spot:
more and you're shaving too fine, fewer and you're probably still being vague.

Two judgement calls live here. The first is the **Pareto move**: nearly always, one or two failure
modes account for the bulk of the pain. You don't chase them all — you tackle the top one or two,
ship, and re-measure. That's how evals become forward motion instead of a bottomless backlog. The
second is that **severity carries as much weight as frequency.** A fault that strikes 2% of the time
but exposes you to a lawsuit (skipping the hand-off on a legal threat) outranks a cosmetic tone
wobble that strikes 30% of the time. Rank by how often *multiplied by* how much it hurts, and lean on
your product judgement for the "how much" — that judgement is exactly the thing you bring that an
engineer might not.

For the refund assistant, twenty notes condense into something like this:

| # | Failure mode | Count (/20) | Severity | Priority |
|---|---|---|---|---|
| 1 | Fabricates a policy that doesn't exist | 6 | High | 🔥 #1 |
| 2 | Fails to escalate legal/angry cases | 3 | High | 🔥 #2 |
| 3 | Replies in the wrong language | 2 | Medium | #3 |
| 4 | Stumbles on long/messy pasted input | 2 | Low | later |
| — | (7 outputs were perfectly fine ✅) | 7 | — | — |

That's a plan, not a mood. (You can drop the notes into Claude or ChatGPT and have it sketch the
grouping in a couple of minutes — but the final list is *yours*. The model is a quick sorter; it
hasn't sat with the data the way you have.) "Fabricates policy" is your #1 — six hits, high stakes.
So that's the one you'll turn into a real measurement next.

---

## 6. Turning "good" into a number — the turning point

This is the pivot of the whole story. Until now you've been *observing*; from here on you're
*measuring*. And the very first thing you measure exposes why most quality arguments go in circles.

Two colleagues read the same refund-assistant reply. One scores it "7 out of 10." The other says
"4." They go back and forth for ten minutes, and neither is actually wrong — because "7/10" carries
no shared meaning. It's a gut feeling dressed up as a figure. Now flip the question. Suppose the
standard is: *"FAIL if the reply states any refund policy that isn't on our approved list."* Both
colleagues look. Both say **FAIL.** Argument over. That's the entire force of a good **rubric** — a
written rule that calls pass-or-fail on *one* thing you care about.

The single most useful tip in these notes is this: **keep it binary. Pass or fail. Not a 1–10
scale.** It feels like a step down. It's the opposite, for three reasons. First, 1–10 scores are
*counterfeit precision* — nobody can reliably separate a 6 from a 7, so the disagreement looks like
measurement but is really just noise. Second, binary *forces a crisp definition* — to commit to pass
or fail you have to spell out exactly what failure *is*, and that act of spelling-out is the
valuable thinking. Third, binary is *actionable*: "30% fail this check" tells you exactly what to go
fix, whereas "averaging 6.4 out of 10" tells you nothing you can act on. A good rubric is sharp
enough that two people grade the same output identically — so try yours on yesterday's examples, and
if you and a colleague split, the rubric's still too loose. Tighten it. Write one rubric per failure
mode, beginning with your #1.

A rubric needs something to run against, and that's an **eval dataset** — a test set — which is
simply a set of inputs you run the AI on to gauge quality. Begin *small*: three examples is a fair
start, ten is comfortable, and it grows from there. Build it from two directions at once. Pull
**real inputs** that trip your failure mode (the traces you read earlier are pure gold), and
**generate** more by asking an AI: *"Give me 30 varied customer refund questions — some angry, some
not in English, some vague."* That generated batch is the fast route to covering the messy long tail
— which, you'll remember, is the Gulf of Generalization. And cover the hard cases *deliberately*: a
test set made only of easy questions will always look terrific and teach you nothing.

Beneath all of it — every eval you'll ever run, however elaborate — sits one simple five-step loop:

```
1. DRAFT the thing you're testing (a prompt)
2. CREATE a test set that mirrors reality
3. RUN the AI over each case → collect the outputs
4. GRADE each output against your rubric (pass/fail)
5. CHANGE one thing & REPEAT → did the score climb?
```

Step 5 is where the magic lives. The score becomes a **fixed baseline**: adjust the prompt, run it
again, and *watch* whether you helped or hurt instead of guessing. In practice, run the assistant
over ten cases, mark each against the fabrication rubric, and you land on — say — **6 out of 10.**
That 60% is your baseline. When you tune the prompt next week and it reaches 9 out of 10, you'll
*know* you improved it. And none of this needs special tooling to begin: a spreadsheet of test cases
with a pass/fail column is already a real eval. The one snag is that grading ten cases by hand is
fine, while grading ten thousand isn't. So the grading has to start running on its own.

---

## 7. Who does the grading: code checks vs. an AI judge

There are exactly two ways to automate grading, and the skill is matching the right one to each
failure mode. (You won't *build* either — but you'll decide which fits and brief your team, and that
call is genuinely yours.)

A **code evaluator** is a plain, deterministic rule that checks something with an unambiguous yes/no
answer — no opinion involved. It either happened or it didn't. Reach for it on the rule-shaped
things: a mandatory disclaimer is present, the output is a properly formed date, a forbidden word is
absent, the system really did route to a human when it was supposed to. On the refund assistant: if
any reply that quotes a refund *amount* must carry the line *"final amounts are confirmed by our
team,"* a code evaluator simply checks whether that exact sentence is there. It's quick, essentially
free, and never overlooks what you told it to watch — but it only ever catches *what you
programmed.* It can't tell you whether a reply was *helpful.*

An **LLM-as-judge** puts an AI in the grader's seat for the *subjective* qualities — tone,
helpfulness, empathy, clarity, whether something honours a policy in spirit — assessing them the way
a human reviewer would. Rather than matching keywords, it reads the output and reasons about whether
it's any good. Reach for it on "is the tone calm and professional?", "did it genuinely answer the
question?", "does this respect our refund policy in spirit?" It's flexible, it notices nuance, and
it scales to thousands of outputs — but there's a catch we'll handle next: it's an AI grading an AI,
so you have to prove it lines up with humans before you lean on it.

The two aren't competitors; they're **layers.** You run both, on different checks — code evaluators
for the objective, compliance-flavoured rules, LLM-judges for the subjective quality calls. The
rule of thumb writes itself: *objective and rule-shaped → code; subjective and judgement-shaped →
LLM-judge.* Laid across the refund assistant's failure modes, the split is clean:

| Failure mode | Grader | Why |
|---|---|---|
| Fabricates a non-existent policy | **LLM-judge** | Must weigh claims against the approved policy *by meaning* |
| Fails to escalate legal/angry cases | **Code eval** | Objective: did the hand-off fire? Yes/no |
| Replies in the wrong language | **Code eval** | Objective: input language vs. output language |
| Robotic / cold tone | **LLM-judge** | A pure judgement call |

And an LLM-judge is less mysterious than it sounds — it's just a carefully written prompt. Name the
one thing to judge (keep it binary), give it the rule (your rubric), and ask for a verdict plus a
reason: *"You're grading a support reply. It PASSES only if every refund policy it names is on this
approved list: [list]. Otherwise FAIL. Customer message: {input}. Reply: {output}. Answer PASS or
FAIL, then one sentence saying why."* That's a working LLM-judge — no code, just a clear prompt and
your rubric. Which raises the obvious, slightly uneasy question: can you really trust an AI to grade
your AI?

---

## 8. Can you trust the judge?

Say your LLM-judge reports the assistant fabricating a policy 8% of the time. Reassuring — unless the
judge itself is off. Perhaps it's overlooking half the genuine fabrications. Perhaps it's flagging
blameless answers. If your ruler is warped, every figure you quote from it is warped too. So before
you lean on an automated grader at scale, you do one modest thing: **measure it against a human.**
And the human is you.

The method is short. Take a sample of outputs — twenty is ample to begin. Grade each one yourself, by
hand, pass or fail, using your rubric; *that* is your **ground truth**, the correct labels as decided
by a person. Then set the LLM-judge loose on the same twenty. Line them up. Where do you agree? Where
do you part ways? Two figures capture how good the judge is, and although they sound technical
they're really just common sense.

**Precision** asks: *are the alarms real?* — of the failures the judge flagged, what share were
actually failures? Weak precision means the judge cries wolf: it flags clean answers, you burn time
chasing phantoms, and people stop believing the eval. **Recall** asks: *is anything slipping past?*
— of all the failures that genuinely exist, what share did the judge catch? Weak recall means silent
misses: the dashboard reads "97% good" while customers keep hitting failures it never noticed. Recall
is the more dangerous of the two, precisely because its misses are invisible. The whole thing fits in
a small grid:

| | Judge says FAIL | Judge says PASS |
|---|---|---|
| **Really a fail** | ✅ caught it | ❌ missed it (hurts recall) |
| **Really fine** | ❌ false alarm (hurts precision) | ✅ correct |

You want both running high — catch the genuine failures *and* don't cry wolf. Walk it through once
with numbers: you hand-label twenty answers and find 5 are real fabrications, 15 are clean. The judge
flags 6. Of those 6, four were real and two were false alarms → **precision = 4/6 ≈ 67%.** Of the 5
real fabrications, it caught four and missed one → **recall = 4/5 = 80%.** Read: recall's respectable,
precision's shaky. You don't bin the judge — you *coach* it, the way you'd coach a new reviewer:
tighten the rule in its prompt, drop in a couple of worked pass/fail examples so it calibrates, and
re-test against your twenty. Run it again, precision climbs past 90%, and *now* you let it loose on
the full traffic. (You don't need exact arithmetic either — "it agreed with me 17 times out of 20,
and the misses were all false alarms" is a real, useful read.)

When a judge agrees with humans on both counts, something quietly excellent has happened: you've
effectively *duplicated a trusted reviewer*, one that keeps grading thousands of outputs while you
sleep. That's the prize. And the technique outlasts AI — precision and recall are how you weigh *any*
automated check against human judgement. Learn it once, keep it forever. An unvalidated judge, by
contrast, isn't really a measurement at all; it's a second opinion you haven't yet earned the right
to trust.

Everything so far has quietly assumed the simplest possible feature: a question goes in, an answer
comes out. Many real features are richer than that — and they bury their failures in places the final
answer never reveals.

---

## 9. The trickier features: check the path, not just the destination

Your real feature might do more than answer. It might **look things up** before replying (that's
**RAG**). It might **take actions** — query the order system, issue the refund, email the customer
(that's an **agent**). It might **hold a conversation** across many turns (**multi-turn**). For all
three, grading the final answer alone isn't enough, because the answer can be right by luck or wrong
for a reason you'll never spot unless you inspect the steps.

**When it looks things up (RAG),** ask *did it retrieve the right material?* A RAG answer can fail in
two completely separate ways: retrieval misfired (it pulled the wrong documents, or nothing), or
generation misfired (the right documents were in hand and the reply was still poor). So there are
two questions rather than one — *did it surface the correct source,* and, having surfaced it, *did
it answer faithfully from that source?* A wrong reply traced to a *missing* document needs a
completely different remedy than one traced to a *present* document. The PM takeaway: keep asking
"which documents did it actually pull?" — most RAG breakdowns are retrieval breakdowns in a
generation costume.

**When it takes steps (an agent),** ask *did it follow a sensible path?* An agent doesn't merely
answer; it plans, selects tools, makes calls, and strings the steps together — and that ordered
chain of steps is its **trajectory.** Here a correct final answer can disguise a broken path: it
issued the right refund, but en route it opened the *wrong* customer's record and simply got away
with it. So you weigh the trajectory itself — did it reach for the right tools, move through
reasonable steps in a reasonable order, and avoid harmful or wasteful moves like firing off a double
refund? A correct answer arrived at by a reckless route will, given time, arrive at a wrong and
expensive one.

**When it holds a conversation (multi-turn),** ask *does quality survive turn 5?* Most demos test
only the opening reply; real people go back and forth. Does the assistant recall what was said three
turns ago, stay consistent rather than contradict itself, and hold the policy line as the user
rephrases and pushes? Failures love to hide in turn 4.

You don't need to *build* trajectory tracking or retrieval logging. Your job is to **know what to ask
for**: "Which documents did the model pull?" "Can we record the sequence of steps it took?" "Can we
exercise a five-turn exchange in testing, not just the first reply?" Posing those questions is
precisely what a sharp AI PM contributes. (And if your feature really is plain question-in,
answer-out, then realising you *don't* need these checks is itself a useful, valid conclusion.)

By now you've built something real. The last danger is that it quietly stops working once everyone's
attention has moved on.

---

## 10. Keeping it alive: regressions and drift

Here's the cruel twist. You did all the work — surfaced the failure modes, wrote the rubrics,
validated the judge. Quality's good. Three months on it's bad again, and nobody noticed until the
customers did. Two things always happen to AI products over time, and an eval you run *once* catches
neither. An eval that runs *on a schedule* catches both.

The first is **regression**: a prompt edit or a model swap quietly knocks over something that had
been working fine. The defence is a **quality gate.** Whenever the prompt or model is touched, the
test set runs before anything else, and the fresh score is held up against the last one; if it
slipped, the change stays on the bench until that's put right. This is where **prompt versioning**
pays off: track the prompt as v1, v2, v3, and grade each against the *same* test set, so "is v3
better than v2?" resolves to a number rather than a debate. The automated version of this is what
engineers call a **CI check** — it fires on every change and blocks the bad ones — and you don't
build it, you *ask* for it. Your one line: *"No prompt or model change ships until it clears our
eval set — can we make that a hard requirement?"* That single sentence recasts you as the PM who
heads off the fire drills rather than the one fighting them.

The second is **drift**: nothing changes on your side, but the world moves, and quality slowly slides.
Your inputs shift (new products, new slang, fresh edge cases your original test set never imagined),
and the *model itself* can shift beneath you (vendors update models, and behaviour changes with no
notice — one widely cited study found a model's accuracy on a task swinging sharply between two
versions a few months apart). The defence is cheap and humble: choose a cadence — weekly is a sound
default — re-sample real production outputs, re-grade them, and watch the number over time. A gentle
slide from 92% → 88% → 84% is drift, and you want to catch it as a soft trend on your own dashboard,
not as a cliff your customers discover for you. Keep the test set fresh too — periodically swap in
new real examples, because a test set frozen at launch gradually stops describing your actual
product.

And keep a human in the loop. The automated graders carry the bulk of the load, yet the best teams
still read a few real traces by hand every week. It keeps your own judgement calibrated and surfaces
the brand-new failure mode that nobody ever told the automated checks to watch for — which is really
just the look-at-your-data habit from earlier, repeated forever in small doses. The whole routine
fits in a breath: *check before every change, re-sample weekly, refresh the test set, and keep
reading a few real outputs by hand.* Call it twenty minutes a week — the price of catching trouble
yourself instead of hearing about it from a customer.

There's one move left — the one that turns all this measurement into something the business genuinely
cares about.

---

## 11. Closing the loop: improve it, then prove it

Here's what rarely gets said out loud: **an eval that never changes the product is just costly
diary-keeping.** The score was never the point. A better product is the point — along with being able
to demonstrate it to whoever controls the budget and the roadmap. Two moves shut the loop: first you
*improve,* then you *make the case.*

To **improve**, aim that same five-step loop from earlier at your #1 failure mode — look at the
failures, set a baseline, change one thing, re-measure, then keep it or roll it back. Your levers,
cheapest first: **fix the prompt** (the most common and cheapest fix — *"only state policies from
this list; if you're unsure, say you'll check"* kills off a lot of fabrication, and most
Specification-gulf problems die right here); **fix the inputs or retrieval** (if it's a RAG feature
pulling the wrong documents, repair retrieval before you blame the model); or **change the
architecture or model** (add a guardrail, add an escalation step, or upgrade the model — the heavy
lever, for when prompt fixes plateau). The discipline that makes you trustworthy is the same one from
the start: change one thing, run the eval again, compare to baseline. Up? Keep it. Not? Revert and
try the next idea. You've stopped guessing whether you helped — you can see it.

To **communicate**, write a short **eval report** — aimed at stakeholders, not engineers. The same
facts can land as "trust me, it's good" or as a tight, credible case that wins you resources, and the
difference is five plain lines: *what we measured* (the feature and its top failure modes), *how good
it is* (pass rates in plain numbers), *what's still failing* (honestly, the biggest remaining
problem), *what we're doing about it* (the next fix and its expected effect), and *how we know it
won't rot* (your cadence — the smoke detector from the previous section). For the refund assistant it
reads like this:

> **Refund Assistant — Eval Report (this month)**
> **Measured:** policy accuracy, escalation of legal/angry cases, language match.
> **Quality:** policy-accuracy check now passes **91%** (was 60% at the start of the month);
> escalation **100%**; language match **96%**.
> **Still failing:** ~9% of replies on rare product types still state an unverified policy.
> **Next fix:** add those product types to the approved-policy source; expect 91% → ~97%.
> **How we keep it honest:** 30-case eval gate on every prompt change; 50 real conversations
> re-graded weekly; test set refreshed monthly.

Five lines. A busy executive grasps it in thirty seconds; a sceptical one can't find a hole to poke.
Numbers and honesty beat adjectives every time. And the report does something larger than report: it
shifts how leadership *sees* AI quality — from a black box they accept on faith into something a
product person owns, measures, and steers. It's the artifact that gets your programme funded rather
than cut, and — not by coincidence — exactly the kind of document compliance and governance teams
increasingly want as AI oversight tightens.

---

## 12. Where this leaves you

Walk back across the whole arc. You started where nearly everyone starts — opening the product,
trying a few things, pronouncing it good. Then you gave that instinct a backbone. You learned what an
eval really is and why owning it is now a product job. You got a map of the three places AI breaks.
You did the unglamorous, decisive thing — *read your actual data* — and turned a heap of notes into a
ranked list of named failure modes. You made "good" measurable with binary rubrics and a small test
set, matched the right grader to each problem, and *proved* you could trust the AI judge using
precision and recall. You learned to check the path and not just the destination on the trickier
features. You built a habit that catches regressions and drift before customers do. And you closed
the loop — turning results into a concrete fix and a five-line report that leaves you the person in
the room whose read on quality everyone trusts.

**In a breath:** *Owning AI quality was never an engineering credential. It's four habits — read your
data, measure what counts, show the measurement holds up, and keep it honest as time passes. That's
the job, and it's yours now.*

When you're ready to do it for real — on *your* feature, a bite a day — start the
[10-day course](overview.md) at [Day 1](day-01.md), and keep your work in the
[Eval Plan template](my-eval-plan-template.md). Reading this through was the map. The course is the
walk.

---

### A note on sources, originality, and copyright

These notes are an **original synthesis written for this playbook.** They contain no verbatim text
copied from any book, course, article, or other source — every sentence here was composed for these
notes. What's borrowed is *ideas and terminology*, which are credited to the people who developed
them; ideas and framework names aren't subject to copyright, and they're attributed here as a matter
of good practice:

- **Hamel Husain & Shreya Shankar**, *Evals for AI Engineers* — error analysis (open and axial
  coding, themselves rooted in long-standing qualitative-research practice), binary rubrics,
  automated evaluators, RAG / agent / multi-turn evaluation, CI-style quality gates, and the
  improvement loop. ([Hamel's LLM Evals FAQ](https://hamel.dev/blog/posts/evals-faq/))
- **Shreya Shankar's Three Gulfs** framework — Comprehension, Specification, Generalization (building
  on Don Norman's gulfs of execution and evaluation, 1988).
- **LinkedIn Learning** courses on a typical eval workflow, automated evals (code evaluators &
  LLM-as-judge, precision/recall for validating graders), and evaluation reports as stakeholder
  artifacts.
- **Lenny's Newsletter**, [Why AI evals are the hottest new skill](https://www.lennysnewsletter.com/p/why-ai-evals-are-the-hottest-new-skill),
  for the product framing.

The running example — the refund assistant, its failure modes, the sample traces, the rubric, the
numbers, and the report — is **invented for this playbook** and does not reproduce any example from
the sources above.
