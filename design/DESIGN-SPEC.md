# Design Spec — The AI Evals Playbook (web experience)

A couch-to-5k-inspired design for delivering the 10-day course as a calm, encouraging, hard-to-put-
down web app. Implementation-agnostic (no stack decided yet). The Markdown course works today; this
spec is the blueprint for the web version that makes it *spread*.

> **North star:** the moment someone lands, they should think *"oh — I could actually do this,"*
> and every day after, *"that took 12 minutes and I have something to show for it."*

---

## 1. Design principles (the reason it goes viral)

1. **One clear thing today.** Like couch-to-5k's "today's run," the home screen shows exactly one
   action: *Start Day N.* No menus to get lost in, no 200-lesson syllabus to intimidate. Focus is
   the feature.
2. **Always a visible finish line.** A 10-node trail you can see start to end. Progress is the
   product. People finish things they can see the end of.
3. **You leave with an artifact, not a certificate.** The **My Eval Plan** fills in as you go. By
   Day 10 you have a real, exportable deliverable for a real feature. *(This is the big upgrade over
   couch-to-5k, which leaves you only with the habit.)*
4. **Confidence is the UX goal.** Plain language, every term one tap from a definition, encouraging
   microcopy. The emotional arc matters as much as the content: *intimidated → curious → capable →
   confident.*
5. **No fluff, visually too.** Generous whitespace, one idea per screen, calm palette. The design
   should feel like a good book, not a dashboard.
6. **Built to be shared.** Milestone moments produce shareable cards; the whole thing is free and
   link-friendly. Every finisher is a potential evangelist.

---

## 2. Information architecture

```
Landing  →  Day 1 (no signup required to start)
   │
   ├─ Path (the 10-node trail — the "home base")
   │     └─ Day N  →  Lesson reader  →  Exercise worksheet  →  Mark complete → milestone?
   │
   ├─ My Eval Plan (persistent workspace, grows each day)
   └─ Glossary (drawer, reachable from any term, anywhere)
```

- **Soft-paced, not locked.** Days are recommended one per day (the couch-to-5k cadence), but
  nothing is hard-locked — an eager learner can continue. A gentle nudge ("one day at a time builds
  the habit") preserves pacing without nagging.
- **No-signup start.** Day 1 is fully open. The email ask comes *after* the first win (see §6).

---

## 3. Screens (the core five)

### 3.1 Landing
- One-sentence promise: *"Learn AI Evals in 10 days. No code. Just you, your AI feature, and 12
  minutes a day."*
- The audience line: *"For PMs, AI PMs, analysts, and anyone who's tired of vibe-checking their
  AI."*
- A preview of the 10-node trail + the finish-line artifact ("you'll leave with this →" thumbnail of
  a filled Eval Plan).
- Single primary CTA: **Start Day 1 — free.** No signup wall.

### 3.2 Today (the home base after you start)
- Big, singular focus: `Day N`, the title, `≈12 min read · 1 exercise`, and a one-line *why today
  matters.*
- One primary button: **Start Day N.**
- Quiet secondary row: streak flame · progress ring (`N/10`) · link to My Eval Plan.
- Everything else recedes. This screen answers exactly one question: *what do I do right now?*

### 3.3 Path / Trail
- A **vertical trail** (a running-route motif) with 10 nodes top to bottom.
- States per node: **done** (filled + check), **today** (pulsing/highlighted), **upcoming** (soft
  outline).
- **Day 5** and **Day 10** nodes are visually special (a flag / a medal) — you can *see* the
  halfway and finish milestones coming, which pulls you forward.
- Tap any node → that day. Top of screen: streak + "30% complete."

### 3.4 Lesson reader
- Calm, **one-idea-per-scroll** reading view. Generous line height, readable measure (~65–75 chars).
- **Components in the flow:**
  - *Cold-open* block (slightly larger, sets the scene).
  - Body text with **tappable terms** → glossary drawer.
  - *Worked example* in a tinted card.
  - *"One line to remember"* styled as a big pull-quote card with a **Share** button (screenshot-
    ready — this is a viral surface).
  - *Tomorrow →* teaser at the end (creates the cliffhanger pull).
- Sticky slim progress bar for the lesson itself.

### 3.5 Exercise worksheet
- The day's single exercise, rendered as an **interactive worksheet** (fields/checklist), not a wall
  of instructions.
- Writes directly into **My Eval Plan** (the relevant section), so doing the exercise *is* building
  the deliverable.
- Primary action: **Mark Day N complete** → advances the trail, lights the node, fires a milestone
  if Day 5 or 10.

---

## 4. The two signature surfaces

### 4.1 My Eval Plan (persistent workspace — the differentiator)
- One growing document, one section per day, mirroring
  [`curriculum/my-eval-plan-template.md`](../curriculum/my-eval-plan-template.md).
- Each completed exercise fills its section; a progress meter shows the plan filling up.
- **Exportable** (Markdown / PDF / copy-to-clipboard) at any time — but especially at Day 10, where
  it's presented as the finished "medal."
- This is *why someone recommends the course*: "I took a 10-day thing and walked out with a real
  eval plan for my product."

### 4.2 Glossary drawer
- Slides in from the side over any screen. Every term in [`GLOSSARY.md`](../GLOSSARY.md), searchable.
- Every defined term in any lesson is tappable → opens the drawer to that entry. Nobody ever hits a
  word they can't instantly decode. (Critical for the non-technical audience.)

---

## 5. Milestone moments (the shareable surfaces)

- **Day 5 — Halfway badge:** celebratory modal: *"You can now read your own data and name what's
  breaking. That already puts you ahead of most teams."* → shareable card.
- **Day 10 — Finish:** the big one. Confetti-light celebration, the completed Eval Plan revealed as
  the trophy, and a **share card**: *"I just built a real eval practice for my AI product in 10
  days."* Plus three next-steps (run it on a second feature · share your plan · pass the course on).
- Share cards are clean, branded, and quote-driven (reuse the "one line to remember" lines). These
  are the engine of organic growth — design them as first-class, not an afterthought.

---

## 6. Email capture (free + value-first)

- **When:** after **Day 1 is completed** — never before the first win.
- **The ask:** *"Save your progress and get tomorrow's lesson in your inbox?"* Email only.
- **The value exchange:** progress sync across devices + a daily nudge email (mirrors couch-to-5k's
  reminder that drives completion).
- **Daily nudge email:** short, warm, one line of what today unlocks + a deep link to the Today
  screen. These both boost completion *and* feed the Outcome Memo Substack audience.
- Skippable (you can keep going without it) — respect first, capture second. Trust is what gets
  shared.

---

## 7. Visual system

- **Mood:** calm, paper-like, book-meets-app. Warm off-white background, generous space, soft
  shadows, rounded cards. Not a SaaS dashboard.
- **Color:** a neutral warm base + **one** encouraging accent color (used for progress, primary
  actions, and completion). Restraint signals calm and confidence.
- **Type:** a readable **serif for headings** (gives the "this is a real course / book" feel) + a
  clean **sans for body**. Large body size, relaxed line height — readability over density.
- **Motif:** the running-route **trail** ties the whole thing to couch-to-5k; **progress ring** and
  **streak flame** for momentum; subtle **micro-animations** on completion (a node lighting up).
- **Tone of voice:** plain, encouraging, specific. "You've got this," never "leverage synergies."
  Microcopy does emotional work — celebrate small wins explicitly.

---

## 8. Accessibility & platform

- **Mobile-first**, fully responsive. People will do a 12-minute lesson on a phone in a coffee line.
- **WCAG AA**: contrast, focus states, keyboard navigation, screen-reader labels, respects reduced-
  motion.
- Readable at a glance; no essential information conveyed by color alone (node states also use
  icons/shape).
- Fast and lightweight — calm includes "loads instantly."

---

## 9. How this maps to (and beats) couch-to-5k

| couch-to-5k | This course | The upgrade |
|---|---|---|
| One run shown today | One lesson shown today | Same focus principle |
| Week-by-week plan you can see | 10-node trail you can see | Same "visible finish line" |
| Audio coach encourages you | Encouraging microcopy + milestones | Same emotional support |
| You finish with a *habit* | You finish with a habit **+ a real Eval Plan artifact** | **Tangible take-home deliverable** |
| Progress tracked | Progress tracked **+ a visible "you are here" on the eval lifecycle** | **Mental model, not just a counter** |
| — | Glossary drawer on every term | **Nobody gets left behind by jargon** |

---

## 10. Future (noted, not in this phase)

- **Embedded micro-tools** that make exercises even more hands-on (out of scope now): a
  precision/recall *judge-agreement calculator*, an *AI test-case generator* helper, a *rubric
  builder*. These would deepen "hands-on" without adding fluff.
- Optional accounts for saving multiple Eval Plans (one per feature).
- A lightweight community / "share your finished plan" gallery.

See [`wireframes.md`](wireframes.md) for low-fidelity layouts of every screen above.
