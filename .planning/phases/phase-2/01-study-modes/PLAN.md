# Plan 01: Study Modes (Final Exam + Wrong-Answer Review + Mastery UI)

**Phase:** 2 (Study Mode Improvements)
**Status:** ✓ Complete (shipped 2026-05-17, commit `66a2d0d`)

## Goal

Ship three test-prep features into `index.html` in one pass:
1. A randomized "final exam" mode that draws questions from across all chapters
2. A "review wrong answers" mode that pools every question she got wrong on first try
3. A home screen that shows mastery (correct count) not just completion (answered count)

All in `index.html` — no new files, no data schema changes, no migration. Backward compatible with existing `localStorage`.

## Requirements covered

- **STUDY-01**: Final exam mode ✓
- **STUDY-02**: Wrong-answer review mode ✓
- **STUDY-03**: Mastery progress UI ✓
- **STUDY-04**: Best exam score tracking ✓

## What shipped

### New HTML
- One new `<section id="specialView">` container that hosts both the final exam UI and the review mode UI (only one is active at a time)
- Inside it: a back button to the home screen and a `<div id="specialContent">` for dynamic content

### New JS functions (in `index.html`)
- `getAllWrongQuestions()` — scans `loadProgress()` across all chapters, returns flat array of questions answered incorrectly, each annotated with `_chapterId`, `_origIdx`, `_chapterTitle`, `_chapterEmoji` so the review mode can render context and write answers back to the right chapter
- `shuffle(arr)` — Fisher-Yates shuffle (used for exam randomization)
- `startFinalExam(count = 20)` — builds randomized question pool, switches view, calls `renderFinalExam()`
- `renderFinalExam()` — renders header, progress bar, question list, and (when all submitted) a final score panel with encouragement based on score band
- `renderExamQuestion(q, idx, ex)` / `bindExamQuestions()` — per-question rendering and click handling for the exam (doesn't write to chapter progress; tracks local state in `currentExam`; updates `popoBestExamScore` only on full completion)
- `openReviewMode()` — derives wrong-answer set, switches view, calls `renderReviewMode()`
- `renderReviewMode()` — renders header or "כל הכבוד" empty state when no wrong answers; lists each wrong question with the original chapter labeled
- `renderReviewQuestion(q, idx)` / `bindReviewQuestions()` — per-question rendering and click handling; on correct re-answer, persists the new answer back to the original chapter's progress (so the question leaves the review pool on next refresh) and fades the card

### Updated JS functions
- `renderHome()` — adds two new prominent cards at the top of the chapter grid (final exam + review mode); chapter cards now show `correct/answered נכון` instead of `answered/total שאלות`; overall progress text now shows `X% נכון` instead of `X%`
- `updateOverallProgress()` — now computes percentage based on `countCorrect` not `answered.length`, matching the new home-screen logic
- `showHome()` — also hides the new `specialView` container when returning to home

### New localStorage keys
- `popoBestExamScore` (string number) — best final-exam score the daughter has achieved; shown on the exam card

### Backward compatibility
- Existing `popoScienceProgress_v1` schema unchanged
- Review mode derives wrong-answer set on the fly — no new persistent state needed for it
- A user with no prior progress sees the exam card and an empty "review mode" card with a friendly message

## Acceptance criteria (all met)

- [x] Final exam pulls 20 random questions from across all 4 chapters
- [x] Different random set each time `startFinalExam()` runs
- [x] Score shown at end with encouragement copy tuned to score band (18+/15+/10+/<10)
- [x] Best score persists across browser sessions and is displayed on the exam card
- [x] Review mode lists every question the daughter answered incorrectly
- [x] Each review question shows the original chapter (emoji + title) for context
- [x] Re-answering correctly fades the card, updates the persistent chapter progress, and removes the question from the next review session
- [x] Home cards show `correct/answered נכון` after answering at least one question
- [x] Overall progress bar reflects mastery percentage, not just completion
- [x] No regressions in the existing chapter quiz / theory / videos tabs
- [x] No `localStorage` migration required; existing user data continues to work
- [x] `node -e "new Function(inlineJS)"` parses cleanly (68KB, 25 functions)

## Risks (all mitigated)

| Risk | Mitigation |
|------|------------|
| Random shuffle bias from `Array.sort(() => Math.random() - 0.5)` | Used proper Fisher-Yates `shuffle()` instead |
| Review mode forgets which chapter a question came from when writing answer back | Annotated each pooled question with `_chapterId` and `_origIdx` |
| Final exam writes garbage to chapter progress | It deliberately doesn't write to chapter progress at all — only tracks local exam state and `popoBestExamScore` |
| Home screen breaks for users with no progress yet | `correct/answered` falls back to `correct/total שאלות` when nothing answered |
| Hebrew RTL on new cards | Reused existing `chapter-card` class and gradient pattern — same RTL behavior as the working chapter cards |

## Non-goals (deferred)

- Flashcard mode for memorizing names of bones/layers/joints
- Audio narration
- Printable one-page summary
- Per-question time tracking
- Spaced repetition algorithm beyond "wrong → review pool → removed when right"
- A separate "exam history" view (only best score is shown; individual exam runs aren't logged)

## Deployment

Code is committed (`66a2d0d`) and pushed to `https://github.com/RoyGol/popo-science`. To make it live on Hostinger, re-upload `index.html` via the Hostinger control panel (or whatever upload method was used for the initial deploy).

---
*Last updated: 2026-05-17 after Phase 2 shipped*
