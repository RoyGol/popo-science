# Plan 02: Subject Picker + Second Sample Subject

**Phase:** 2 (Reusability Refactor)
**Status:** ○ Pending
**Depends on:** Plan 01 (extraction must be complete)
**Blocks:** Plan 03

## Goal

When more than one subject is registered, show a landing screen that lets the user pick a subject before diving into chapters. Each subject has independent progress. Ship a real second sample subject in the repo to prove the multi-subject pattern actually works end-to-end (not just in theory).

After this plan: the app supports an arbitrary number of subjects, and adding one is a content-only operation.

## Requirements covered

- **REUSE-02**: Adding a new subject = drop in a data file ✓
- **REUSE-03**: Second sample subject exists ✓

## Context

- Plan 01 introduced the `SUBJECTS` registry; this plan exercises it.
- The second sample subject should be **real** content, not lorem ipsum — but doesn't need to be 4 full chapters with 80 questions. A couple of chapters and 10–20 questions is enough to prove the pattern.
- Open question (defer to execution time): what should the second subject be? Candidates:
  - Another upcoming science chapter (if one exists)
  - A math topic the daughter is working on
  - A "demo" subject like "טבלת הכפל" (multiplication tables) — useful AND a good demo
  - A non-school topic she likes (animals, planets, history) — increases engagement

## Tasks

### 1. Author the second subject's content

Pick a topic (see Context). Author content following the schema in `data/science-bodies-grade4.js`:
- 1–3 chapters
- 5–10 questions per chapter (less than the full 20 — this is a proof, not a full study tool)
- Theory blocks: keep it short, grade-4 Hebrew
- Videos: optional — if good YouTube videos exist in Hebrew, embed them; otherwise omit
- Diagrams: reuse existing `DIAGRAMS` if applicable, or skip (diagrams are optional per block)

Save as `data/<subject-id>.js` (e.g. `data/math-multiplication-grade4.js`).

### 2. Add the `<script>` tag for the second subject

In `index.html`, add a sibling `<script>` tag right after the first one:

```html
<script src="data/science-bodies-grade4.js"></script>
<script src="data/math-multiplication-grade4.js"></script>
```

Confirm both subjects appear in `window.SUBJECTS` (length 2).

### 3. Subject picker UI

Add a new top-level view: subject picker. State machine becomes:
- `view = 'subjects'` → show subject picker grid
- `view = 'chapters'` → show chapter grid for `currentSubject`
- `view = 'chapter'` → show a chapter (existing tabbed view)

The current `renderHome()` becomes `renderChapters()`. A new `renderSubjects()` shows a grid of subject cards (similar styling to chapter cards). Each card shows: emoji, title, subtitle, chapter count, question count, progress %.

Initial logic:
- If `SUBJECTS.length === 1`: skip the picker entirely, behave exactly as today
- If `SUBJECTS.length > 1`: show the picker on initial load

### 4. Wire up navigation

- Subject card click → set `currentSubject`, switch to `renderChapters()`
- "→ חזרה לכל הנושאים" button (similar to the existing "→ חזרה לכל הפרקים") appears in the chapter grid only when `SUBJECTS.length > 1`
- Hero header dynamically updates to show the current subject's title/subtitle when one is selected

### 5. Per-subject localStorage

Already wired in Plan 01 (`popoProgress::<subjectId>::v1`). Verify nothing collides when switching between subjects:
- Answer a question in subject A → close → open subject B → that answer should NOT appear
- Switch back to A → the answer is still there

### 6. Per-subject overall progress bar

The header progress bar (today: aggregated across the single subject's chapters) should show progress *within the current subject*, not globally. When in the subject picker view, hide the progress bar (or show "Pick a subject to start").

### 7. Smoke-test locally then deploy

- Test single-subject case: temporarily comment out the second `<script>` tag → app behaves exactly like today
- Test multi-subject: both tags loaded → picker appears, navigation works, progress isolated
- Deploy to Hostinger and re-verify

## Files

**Created:**
- `data/<second-subject-id>.js`

**Modified:**
- `index.html`:
  - Add second `<script>` tag
  - Add `renderSubjects()` function and subject-picker UI block
  - Add `currentSubject` state and view router
  - Update header rendering to be subject-aware
  - Update progress bar to be per-subject

## Acceptance Criteria

- [ ] With only the science subject registered (single subject), the app looks and behaves *exactly* as today (no picker, no back button to subjects, identical hero)
- [ ] With two subjects registered, the picker appears on load
- [ ] Picking a subject enters its chapter grid
- [ ] Answering a question in one subject does not affect the other's progress
- [ ] Going back to the picker and into the other subject shows the correct chapters and questions
- [ ] The second sample subject has real, working content (theory + questions; videos optional) — not placeholder text
- [ ] Adding a third subject requires only: drop a data file + add one `<script>` tag (test this by writing a stub third subject as part of verification — then deleting it before commit)

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Picker UI clutters the experience for single-subject users (current state) | Hide picker entirely when `SUBJECTS.length === 1` — no behavior change for the daughter |
| Per-subject localStorage migration from Plan 01 only handled one key; second subject starts at 0 progress | That's correct — second subject is new content; no historical data exists |
| Authoring a second subject for the demo's sake produces low-quality content | Pick something genuinely useful (next test, a topic she's interested in). Don't ship throwaway demo content. |
| Adding a third subject still requires HTML editing (the `<script>` tag) | Acceptable for now — documented in Plan 03 README. Could be solved later with a `<script>`-tag generator step or a manifest file, but YAGNI for now. |

## Non-goals

- Eliminating the per-subject `<script>` tag step (could be done via a `data/index.js` that explicitly imports/lists all subjects, but adds little; defer)
- Cross-subject search / mixed quiz mode (out of phase scope; v2)
- Subject categories / folders / tagging
- Subject deletion / archiving UI

## Estimated complexity

**M** — UI work is straightforward (copy chapter card pattern → subject card pattern), but authoring real second-subject content is the time sink. Probably 45–90 min for the UI + however long the content takes (depends on subject scope).

---
*Last updated: 2026-05-17 after initial planning*
