# Tagalog Mastery Lab — Master Blueprint (Single Source of Truth)

## 1) What we are building
Tagalog Mastery Lab is a set of simple, browser-based learning mini-apps (no build tools required).
Primary audience: beginners.
Primary goal: fast repetition, clarity, consistency, and “it always works.”

## 2) Site layout (information architecture)
- /index.html
  Main Menu that links to each mini-app.
- /verb-tutor/index.html
  Verb Tutor (30 verbs).
- /verb-tutor/goodbye.html
  Exit / end screen.

Each future mini-app gets its own folder:
- /<mini-app-name>/index.html
- /<mini-app-name>/goodbye.html (optional)

## 3) Learner flow (Verb Tutor)
1) Show an action (emoji now; drawing later).
2) Ask: “Ano ang ginagawa niya sa Tagalog?”
3) Reveal: root/past/progressive forms.
4) Learner chooses form and sees an example sentence.
5) Learner optionally plays audio for the example sentence.
6) Next / Previous verb.

UI should look the same on desktop and phone.

## 4) Non-negotiable folder paths
Repo root: /hosmer-tagalog-public/

Shared assets (global):
- /assets/audio/             (ALL verb sentence audio lives here)

Verb Tutor assets (local to verb tutor):
- /verb-tutor/img/verbs/     (optional drawings; one per verb)

## 5) Audio specification (must not drift)
Audio directory:
- /assets/audio/

Filename format:
- vt-<verbId>-<form>.m4a

Allowed forms:
- basic | past | prog

Examples:
- vt-run-basic.m4a
- vt-run-past.m4a
- vt-run-prog.m4a

Correct relative path FROM /verb-tutor/index.html:
- ../assets/audio/

Rule: filenames must be lowercase, no spaces.

## 6) Image specification (optional “drawing table” phase)
Image directory:
- /verb-tutor/img/verbs/

Filename format:
- <verbId>.png

Example:
- /verb-tutor/img/verbs/run.png

Behavior:
- If image exists: show image.
- If image missing: show emoji.

Rule: avoid double extension:
- Correct: run.png
- Wrong: run.png.png

## 7) Verb data standard (content schema)
Each verb entry must include:
- verbId (stable ID used by audio + images)
- english (display text)
- emoji (fallback display)
- Tagalog forms: root, past, prog
- Example sentences: exampleRoot, examplePast, exampleProg

VerbIds for the initial 30:
run, jump, eat, drink, sleep, read, write, sing, dance, walk,
play, swim, talk, listen, watch, cook, draw, open, close, help,
clean, buy, sell, sit, stand, smile, laugh, drive, study, work

Rule: verbId never changes once audio is produced.

## 8) How to add one new verb (repeatable procedure)
1) Choose verbId (lowercase, simple).
2) Add the verb entry in the JS data (verbId + forms + examples).
3) Create three audio files (basic/past/prog) named exactly:
   vt-verbId-basic.m4a
   vt-verbId-past.m4a
   vt-verbId-prog.m4a
   Place them in /assets/audio/
4) Optional: create drawing:
   /verb-tutor/img/verbs/verbId.png
5) Test on phone + desktop:
   - Reveal works
   - Example sentences show
   - Audio plays (if files exist)
   - Next/Prev cycles without breaking

## 9) Quality rules (what “good” means)
- No broken links (menu ↔ mini-app ↔ menu).
- No “nothing happened” moments on mobile (reveal must be visible).
- Audio button must not pretend: only enabled when a form is selected.
- Text remains readable (large enough).
- Consistent behavior across modules.

## 10) QA checklist (before you publish)
- Open /index.html and click into Verb Tutor.
- Test verbs: run, talk, work (sample across the list).
- For each test verb:
  - Reveal works.
  - Basic/Past/Prog shows correct example.
  - Audio plays (if file exists).
- Confirm direct file access:
  - /assets/audio/vt-run-basic.m4a loads
  - /verb-tutor/img/verbs/run.png loads (if using images)

## 11) Versioning (simple and practical)
At the top of each mini-app JS, keep:
- const APP_VERSION = "1.0.0";

When you change behavior, bump version:
- bugfix: 1.0.1
- feature: 1.1.0
- major change: 2.0.0

Keep a short CHANGELOG at the bottom of this file.
