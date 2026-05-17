# Roadmap: Popo Science Study App

**Mode:** Vertical MVP — each phase delivers an end-to-end usable capability
**Phases:** 3 (Phase 0 already complete)
**Granularity:** Coarse

## Phase Summary

| # | Phase | Goal | Requirements | Status |
|---|-------|------|--------------|--------|
| 0 | MVP Study App | Daughter can study from this PC | CONT-01..06, UX-01..05 | Complete ✓ |
| 1 | Deploy to a URL | Daughter can study from phone/tablet | DEPLOY-01..04 | Complete ✓ |
| 2 | Study mode improvements | Mixed final exam, wrong-answer review, mastery UI | STUDY-01..04 | Complete ✓ |

---

## Phase 0: MVP Study App

**Goal:** Single-file HTML app covering the May 26 test material — theory, videos, and 20 MCQs per chapter.
**Mode:** mvp
**Status:** Complete ✓ (shipped 2026-05-17, commit `ccf7b4e`)

**Requirements covered:**
- CONT-01: 4 chapters covering exam scope
- CONT-02: Grade-4 Hebrew theory text
- CONT-03: Visual diagrams (SVG)
- CONT-04: Embedded YouTube videos
- CONT-05: 20 MCQs per chapter (80 total)
- CONT-06: Hint button + post-submit explanation
- UX-01: Hebrew RTL + Heebo font
- UX-02: Per-chapter and overall progress bars
- UX-03: `localStorage` persistence
- UX-04: Tabbed interface per chapter
- UX-05: Reset-per-chapter button

**Success criteria (met):**
1. ✓ Daughter can open `index.html` and see all 4 chapters
2. ✓ Each chapter shows theory + videos + quiz tabs
3. ✓ Submitting a quiz answer shows correctness, explanation, and updates progress
4. ✓ Closing the browser and reopening preserves answered questions
5. ✓ All text is in grade-4 Hebrew, RTL layout

---

## Phase 1: Deploy to a Stable URL

**Goal:** Daughter can open the study app from her phone or tablet via a bookmarkable URL, not just from this PC. Target: live by 2026-05-19 so she has a week of mobile use before the test.
**Mode:** mvp
**Status:** Complete ✓ (shipped 2026-05-17 — well ahead of deadline; gives her 9 days of mobile runway)
**Live URL:** https://palevioletred-crow-274361.hostingersite.com/
**Host:** Hostinger

**Requirements covered:**
- DEPLOY-01: Public HTTPS URL ✓
- DEPLOY-02: Works on phone and tablet ✓
- DEPLOY-03: Memorable / bookmarkable URL ✓ (auto-subdomain, bookmark-once)
- DEPLOY-04: One-step redeploy ✓ (via Hostinger upload)

**Success criteria (met):**
1. ✓ URL is live: https://palevioletred-crow-274361.hostingersite.com/
2. ◇ Mobile verification: implicit — responsive layout in place, but actual phone/tablet test deferred to first real use
3. ◇ Hebrew RTL on mobile: same — implicit, verify on first use
4. ✓ `localStorage` works on any modern mobile browser
5. ✓ Redeploy via Hostinger is one-step
6. ✓ URL is bookmarkable

**Approach taken:** Hostinger — parent already had account/infra. Originally also pushed to GitHub (`https://github.com/RoyGol/popo-science`) as a code backup, but deployment is from Hostinger.

**UI hint**: no

---

## Phase 2: Study Mode Improvements

**Goal:** Help the daughter prepare for the 2026-05-26 test with test-simulation practice and focused review on her actual weak spots — without architectural changes.
**Mode:** mvp
**Status:** Complete ✓ (shipped 2026-05-17, commit `66a2d0d`)

**Re-scoping note:** Phase 2 was originally planned as a "reusability refactor" (extracting content, multi-subject support, README). That plan was deleted and replaced on 2026-05-17 after Roy clarified the priority should be "improvement on the existing material for studying for this test." The reusability work moved to v2 in REQUIREMENTS.md. Details in `.planning/phases/phase-2/PHASE.md` and in memory `feedback_prioritize_immediate_user_over_architecture.md`.

**Requirements covered:**
- STUDY-01: "מבחן סופי" mixed-question mode
- STUDY-02: "שאלות לחזרה" wrong-answer review mode
- STUDY-03: Mastery progress UI (correct/answered per chapter)
- STUDY-04: Best exam score tracking

**Success criteria (met):**
1. ✓ Daughter can launch a randomized 20-question final exam from the home screen
2. ✓ Each new exam picks a different random set
3. ✓ Best exam score preserved across sessions
4. ✓ "שאלות לחזרה" surfaces every wrong-on-first-try question across all chapters
5. ✓ Re-answering correctly in review mode updates chapter progress and removes the question from the pool
6. ✓ Home cards show mastery (correct/answered), not just completion
7. ✓ No data migration, no regressions in the existing chapter quiz/theory/videos flow

**UI hint**: no (no new UI surfaces beyond the two new home cards and one shared `specialView` container)

---

## Out of Roadmap (Deferred or Out of Scope)

Tracked in REQUIREMENTS.md under v2 / Out of Scope:
- Final-exam mixed-quiz mode
- Spaced-repetition / focus-on-wrong-answers review
- Real labeled anatomy diagrams
- Audio narration
- Authoring helper script
- Native mobile app, accounts, backend, teacher dashboard

---

## Roadmap Status

All three planned phases shipped on 2026-05-17. Next moves are reactive:

- **Until 2026-05-26 (the test):** respond to anything the daughter surfaces while using the app (content errors, confusing questions, missing topics). Edit `index.html` → re-upload to Hostinger.
- **After the test:** consult `REQUIREMENTS.md` v2 list for next priorities (real anatomy diagrams, audio narration, flashcards, multi-subject reusability — if more tests come up).

---
*Roadmap created: 2026-05-17 — manually generated inline (GSD agents not installed)*
*Last updated: 2026-05-17 after Phase 2 (re-scoped) shipped*
