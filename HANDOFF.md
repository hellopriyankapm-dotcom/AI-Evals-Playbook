# Handoff & Task Instructions — The AI Evals Playbook

A working brief for anyone picking this up. Read the snapshot, then take a task from the list.
Everything is on branch **`claude/affectionate-cannon-xMVdz`**.

---

## 1. What this project is

A **free, no-code, 10-day course that teaches AI Evals to product people** (PMs, analysts,
non-technical builders), plus a planned **web app** to deliver it. The teaching content is done;
the web app exists as a clickable HTML mockup, not yet a real app.

There are **two ways through the same content**, and both must stay in sync:
- **Do it** — the 10-day "trail" (one idea + one exercise a day → a finished one-page Eval Plan).
- **Read it** — the **Study Notes**, the whole story as one flowing ~35-minute read, no exercises.

---

## 2. Repo map (what's where)

```
README.md                     ← project front door
GLOSSARY.md                   ← every term in plain English
HANDOFF.md                    ← this file
vercel.json                   ← routes "/" → design/preview/launch.html

curriculum/
  overview.md                 ← the 10-day map + how to take the course
  study-notes.md              ← the flowing "read it all at once" version (~5.9k words)
  day-01.md … day-10.md       ← the 10 lessons (scene → one idea → worked example → exercise)
  my-eval-plan-template.md    ← the learner's running worksheet (the deliverable)

design/
  DESIGN-SPEC.md              ← UX spec for the web app (couch-to-5k inspired)
  wireframes.md               ← low-fi wireframes of every screen
  mockup/index.html           ← THE clickable web-app mockup (landing→trail→lesson→plan)
  preview/launch.html         ← hub linking to the three screens (site root)
  preview/study-notes.html    ← styled long-read render of curriculum/study-notes.md
  preview/directions.html     ← the 3 visual directions (Editorial / Aurora / Focus Dark)
  preview/index.html          ← older design-preview page
```

**Design system (Aurora direction, used by mockup + study-notes):**
- Fonts: `Space Grotesk` (headings), `Inter` (UI), `Newsreader` (long-form body in study notes).
- Core tokens (see `:root` in the HTML): `--primary:#5B5BD6`, `--aurora` gradient
  (`#6366F1→#7C8CF8→#22B8A6`), `--bg:#F5F6FB`, `--ink:#13151c`, radius ~14–18px.

---

## 3. Status

| Area | State |
|---|---|
| 10-day curriculum + glossary + template | ✅ done |
| Study Notes (markdown + styled HTML) | ✅ done |
| Web-app mockup (clickable) | ✅ done (mockup only — not a real app) |
| Design spec, wireframes, 3 directions | ✅ done |
| Live deployment | ❌ not deployed (see Task 1) |
| Pull request | ❌ blocked — repo has only this one branch, no base to merge into (see Task 0) |

**Content/copyright note:** the curriculum and study notes are an original synthesis. Frameworks
(Three Gulfs, precision/recall, error analysis) are *ideas* and are credited to their authors;
the running example (a refund assistant) is invented for this playbook. No verbatim source text.
Verified with an n-gram overlap check — the only verbatim matches are the project's own files,
the shared invented example, standard terminology, and the citation list.

---

## 4. How to view / run (no build step — static HTML)

- **Locally:** open any file in `design/` directly in a browser. They're fully self-contained
  (fonts load from Google Fonts CDN; everything else is inlined). Start with
  `design/preview/launch.html`.
- **Deployed (Vercel):** the repo is import-ready. On vercel.com → *Add New → Project* → import
  `hellopriyankapm-dotcom/ai-evals-playbook` → pick this branch → Deploy. `vercel.json` routes
  `/` to the launcher hub.

---

## 5. Tasks (prioritized)

> Convention: branch off `claude/affectionate-cannon-xMVdz`, keep commits small and described,
> push, and don't merge without sign-off.

### Task 0 — Establish a base branch so PRs are possible *(blocker, needs owner decision)*
The repo currently has only `claude/affectionate-cannon-xMVdz`, which is also the default branch,
so there's nothing to open a PR against.
- **Do:** decide on a `main` base (e.g., create `main` from the repo's first commit, or from the
  current state), set it as default, then open a **draft PR** from the feature branch into `main`.
- **Done when:** a draft PR exists and CI (if any) is green.

### Task 1 — Get a live preview URL
- **Do:** deploy via Vercel (import flow above) or `vercel deploy` from an authenticated machine.
- **Done when:** a `*.vercel.app` URL opens the launcher hub and all three screens load on
  desktop + mobile. Share the URL in the PR description.

### Task 2 — Integrate Study Notes into the main app *(highest product value)*
Right now `study-notes.html` is a separate page. Make it a first-class part of `mockup/index.html`.
- **Do:**
  - Add a **Trail ↔ Read** toggle (or nav entry) in the mockup's app bar.
  - Add a landing card: *"Prefer to read it all at once? → Study Notes (35 min)"* beside
    "Start Day 1".
  - Render the study-notes content as an in-app view using the existing component styles (don't
    fork the design system). Reuse `curriculum/study-notes.md` as the source of truth.
- **Done when:** from the mockup you can switch between the day-by-day trail and the flowing read
  without leaving the app, on one shared theme.

### Task 3 — Keep the two formats in sync
The day files and `study-notes.md` cover the same 12 concepts and share the refund-assistant
example.
- **Do:** when content changes in one, reflect it in the other (failure modes, rubric, the eval
  report numbers, the precision/recall worked example must match).
- **Done when:** a spot-check of the worked example (the 6/10 baseline, the 4/6 & 4/5
  precision/recall, the 91% report) is identical across both.

### Task 4 — Decide the real build (turn the mockup into an app)
- **Open question for the owner:** static site (current HTML) vs. a framework (e.g., Next.js on
  Vercel) with progress tracking, the saved Eval Plan, and a glossary lookup.
- **Do:** write a short options memo (effort vs. payoff) in `design/`. Don't build until chosen.

### Task 5 — Polish pass
- Proofread all 10 days + study notes for tone consistency.
- Check every internal link in the markdown resolves.
- Accessibility on the HTML: heading order, color contrast on the Aurora gradient text, focus
  states on cards/buttons.

---

## 6. Conventions & guardrails

- **No code required for learners** — every exercise must be doable with a spreadsheet + an AI
  chat window. Keep that promise in any new content.
- **Plain language** — define jargon in `GLOSSARY.md`, don't assume ML background.
- **One running example** — the refund assistant. New illustrations should extend it, not replace.
- **Attribution** — credit frameworks to their authors; never paste verbatim source text.
- **Design** — reuse the Aurora tokens and the existing components; don't introduce a second
  visual language.
