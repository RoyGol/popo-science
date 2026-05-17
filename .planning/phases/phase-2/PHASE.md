# Phase 2: Study Mode Improvements

**Status:** ✓ Complete (shipped 2026-05-17, commit `66a2d0d`)
**Mode:** mvp
**Re-scoped:** 2026-05-17 (see "Re-planning note" below)

## Goal

Improve the existing study app with features that directly help with the 2026-05-26 science test — not architectural changes for hypothetical future use. Specifically: give the daughter test-simulation practice and a way to focus her remaining study time on exactly what she got wrong.

## Requirements (re-scoped — new v1 additions)

- **STUDY-01**: "מבחן סופי" mode — mixed-question quiz drawing N random questions from across all 4 chapters; score shown at end; best score persisted
- **STUDY-02**: "שאלות לחזרה" mode — surfaces every question the daughter got wrong on first try; re-attempting and answering correctly removes it from the review pool and updates her chapter progress
- **STUDY-03**: Home screen shows mastery (correct/answered) per chapter, not just answered count; overall progress bar reflects correctness, not completion
- **STUDY-04**: Best final-exam score persisted in `localStorage` and shown on the exam card

## Phase Success Criteria (all met)

1. ✓ Daughter can launch a randomized final exam from the home screen
2. ✓ Each new exam picks a different random set of 20 questions
3. ✓ Best exam score is preserved across sessions
4. ✓ "שאלות לחזרה" card on the home screen shows count of wrong-answer questions
5. ✓ Review mode lists all wrong-on-first-try questions across all chapters
6. ✓ Re-answering correctly in review mode removes the question from the pool and updates chapter progress
7. ✓ Home screen chapter cards show "X/Y נכון" (correct of answered) instead of just answered count
8. ✓ No data migration required — existing `localStorage` data continues to work; new features derive from it

## Plans

| # | Plan | Status |
|---|------|--------|
| 01 | Study modes (final exam + review + progress UI) | ✓ Complete |

Single plan, ~360 lines of code added to `index.html`. No new files. No data schema changes.

## Re-planning Note

This phase was originally planned (also 2026-05-17) as a "Reusability Refactor" — extracting chapter content into separate data files, adding a second sample subject, writing a schema README. Three plans, sequential. Execution was deferred to post-test "for safety."

That framing was wrong. Roy called it out: "Phase 2 should be improvement on the existing material for studying for this test, not deferral to after the test." The user's daughter is studying for a test in 9 days. Phase 2 should help *her* before *that test*, not abstractly future-proof for hypothetical other subjects.

The three original plans (`01-extract-content`, `02-subject-picker`, `03-readme`) were deleted. If reusability becomes a real need later (after the May 26 test, if more subjects come up), they can be re-planned then with fresh context.

Lesson captured in memory: `feedback_prioritize_immediate_user_over_architecture.md`.

## Deferred (not currently planned, could come back as v2)

- Extracting content into separate data files (former REUSE-01)
- Multi-subject support / subject picker (former REUSE-02, REUSE-03)
- Schema documentation (former REUSE-04)
- Flashcard mode for memorizing Hebrew terminology
- Audio narration of theory blocks
- Printable one-page summary for last-day review

---
*Last updated: 2026-05-17 after Phase 2 shipped (re-scoped)*
