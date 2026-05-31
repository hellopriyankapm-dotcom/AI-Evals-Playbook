# Wireframes — low-fidelity layouts

Text/ASCII wireframes for every core screen in [`DESIGN-SPEC.md`](DESIGN-SPEC.md). These show
*layout and hierarchy*, not final visuals. Mobile-first; desktop widens the same structure.

---

## 1. Landing

```
┌─────────────────────────────────────────┐
│              The AI Evals Playbook       │
│                                          │
│   Learn AI Evals in 10 days.             │
│   No code. Just you, your AI feature,    │
│   and 12 minutes a day.                  │
│                                          │
│   For PMs, AI PMs, analysts & anyone     │
│   tired of vibe-checking their AI.       │
│                                          │
│      ┌──────────────────────────┐        │
│      │   Start Day 1 — free  →  │        │
│      └──────────────────────────┘        │
│         (no signup needed)               │
│                                          │
│   You'll walk the trail ↓                │
│   ①─②─③─④─⑤⚑─⑥─⑦─⑧─⑨─⑩🏅               │
│                                          │
│   …and leave with this:                  │
│   ┌────────────────┐                     │
│   │  My Eval Plan  │ ← a real deliverable│
│   │  ▸ failure modes│   for YOUR feature │
│   │  ▸ rubric ▸ … │                     │
│   └────────────────┘                     │
└─────────────────────────────────────────┘
```

---

## 2. Today (home base)

```
┌─────────────────────────────────────────┐
│  🔥 3-day streak        ◔ 3/10   [Plan]  │  ← quiet status row
├─────────────────────────────────────────┤
│                                          │
│            DAY 4                          │
│   From notes to failure modes            │
│                                          │
│   ≈12 min read · 1 exercise              │
│                                          │
│   Why today: turn yesterday's messy      │
│   notes into a ranked list you can fix.  │
│                                          │
│      ┌──────────────────────────┐        │
│      │      Start Day 4   →     │        │
│      └──────────────────────────┘        │
│                                          │
│   [ ← see the whole trail ]              │
└─────────────────────────────────────────┘
```
*One screen, one decision: start today's lesson.*

---

## 3. Path / Trail

```
┌─────────────────────────────────────────┐
│  The Playbook            🔥3   ◔ 3/10    │
├─────────────────────────────────────────┤
│   ●  Day 1  Stop vibe-checking      ✓    │
│   │                                      │
│   ●  Day 2  The Three Gulfs         ✓    │
│   │                                      │
│   ●  Day 3  Look at your data       ✓    │
│   │                                      │
│   ◉  Day 4  Failure modes      ← TODAY   │  ← highlighted/pulsing
│   │                                      │
│   ○  Day 5  Rubrics & test set    ⚑      │  ← halfway flag
│   │                                      │
│   ○  Day 6  Two graders                  │
│   ○  Day 7  Trust your judge             │
│   ○  Day 8  Looks up / takes action      │
│   ○  Day 9  Make it a habit              │
│   │                                      │
│   ○  Day 10 Capstone              🏅     │  ← finish medal
└─────────────────────────────────────────┘
```
*Done = filled ●  ·  Today = ◉  ·  Upcoming = ○. Milestones visible ahead.*

---

## 4. Lesson reader

```
┌─────────────────────────────────────────┐
│  ‹ Day 4            ▓▓▓▓░░░░ (lesson 50%) │  ← sticky progress
├─────────────────────────────────────────┤
│  THE SCENE                               │
│  You've got 20 freeform notes. They feel │
│  like noise. But look closer…            │
│                                          │
│  THE ONE IDEA: cluster, name, and count  │
│  Take your open-coding* notes and group  │
│           ▲ tap = glossary drawer        │
│  …                                       │
│                                          │
│  ┌───────────────────────────────────┐   │
│  │ WORKED EXAMPLE                    │   │  ← tinted card
│  │ Twenty notes collapse into four…  │   │
│  └───────────────────────────────────┘   │
│                                          │
│  ┌───────────────────────────────────┐   │
│  │ “The AI makes mistakes” is a      │   │  ← pull-quote card
│  │  shrug. “It fabricates policies   │   │     + [ Share ]
│  │  30% of the time” is a roadmap.   │   │
│  └───────────────────────────────────┘   │
│                                          │
│      ┌──────────────────────────┐        │
│      │   Do today's exercise →  │        │
│      └──────────────────────────┘        │
│   Tomorrow → turn failure modes into a   │
│   measurement you can trust.             │
└─────────────────────────────────────────┘
```

---

## 5. Exercise worksheet (writes into My Eval Plan)

```
┌─────────────────────────────────────────┐
│  Day 4 · Your turn (12 min)              │
│  Cluster your notes into failure modes.  │
├─────────────────────────────────────────┤
│  Failure modes (name • count • severity) │
│  ┌─────────────────────────┬────┬─────┐  │
│  │ 1  Fabricates a policy   │ 6  │ Hi ▾│  │
│  ├─────────────────────────┼────┼─────┤  │
│  │ 2  Fails to escalate     │ 3  │ Hi ▾│  │
│  ├─────────────────────────┼────┼─────┤  │
│  │ +  add failure mode      │    │     │  │
│  └─────────────────────────┴────┴─────┘  │
│                                          │
│  ⭐ My #1 to fix first:  [ Fabricates… ▾]│
│                                          │
│  💡 Tip: paste your notes into Claude and│
│     ask it to group them — then edit.    │
│                                          │
│      ┌──────────────────────────┐        │
│      │  Mark Day 4 complete  ✓  │        │
│      └──────────────────────────┘        │
│   ↳ saves to your My Eval Plan           │
└─────────────────────────────────────────┘
```

---

## 6. My Eval Plan (persistent workspace)

```
┌─────────────────────────────────────────┐
│  My Eval Plan         ▓▓▓▓░░░░  filling… │
│  Feature: Refund-policy answers          │
│                          [ Export ▾ ]    │
├─────────────────────────────────────────┤
│  ✓ The feature & baseline      (Day 1)   │
│  ✓ Three Gulfs                 (Day 2)   │
│  ✓ What I found in my data     (Day 3)   │
│  ◉ My failure modes            (Day 4)   │  ← in progress
│  ○ Rubric & test set           (Day 5)   │
│  ○ Graders                     (Day 6)   │
│  ○ Trust my judge              (Day 7)   │
│  ○ Extra checks                (Day 8)   │
│  ○ Cadence                     (Day 9)   │
│  ○ Close the loop + report     (Day 10)  │
└─────────────────────────────────────────┘
```
*Export = Markdown / PDF / copy. At Day 10 this is presented as the finished "medal."*

---

## 7. Milestone modal (Day 5 & Day 10)

```
┌─────────────────────────────────────────┐
│                  ⚑                       │
│            Halfway there!                │
│                                          │
│  You can now read your own data and      │
│  name what's breaking — that already     │
│  puts you ahead of most teams.           │
│                                          │
│   ┌─────────────────────────────────┐    │
│   │  [ shareable card preview ]     │    │
│   │  “Day 5 of the AI Evals         │    │
│   │   Playbook — halfway. I can     │    │
│   │   read my AI's data now.”       │    │
│   └─────────────────────────────────┘    │
│                                          │
│   [ Share ]        [ Keep going → ]      │
└─────────────────────────────────────────┘
```
*Day 10 variant: medal 🏅, completed Eval Plan revealed, share card "I built a real eval practice
in 10 days," + 3 next-steps.*

---

## 8. Email capture (after Day 1 completion)

```
┌─────────────────────────────────────────┐
│            Nice — Day 1 done. ✓          │
│                                          │
│  Save your progress and get tomorrow's   │
│  lesson in your inbox?                    │
│                                          │
│   ┌─────────────────────────────────┐    │
│   │  you@work.com                   │    │
│   └─────────────────────────────────┘    │
│      ┌──────────────────────────┐        │
│      │   Save & email me Day 2  │        │
│      └──────────────────────────┘        │
│                                          │
│   [ No thanks, keep going → ]            │
└─────────────────────────────────────────┘
```
*Value-first, skippable. Appears only after the first win, never before.*

---

## 9. Glossary drawer (overlays any screen)

```
┌──────────────────────────┬──────────────┐
│  …lesson text behind…    │  GLOSSARY  ✕ │
│                          │  ┌─────────┐ │
│                          │  │ search… │ │
│                          │  └─────────┘ │
│                          │  Open coding │
│                          │  Step 1 of   │
│                          │  error       │
│                          │  analysis:   │
│                          │  read each   │
│                          │  output and  │
│                          │  write a     │
│                          │  freeform    │
│                          │  note…       │
│                          │              │
│                          │  ‹ related:  │
│                          │  axial coding│
└──────────────────────────┴──────────────┘
```
*Opens to the exact term tapped. Search for any other. The non-technical safety net.*
