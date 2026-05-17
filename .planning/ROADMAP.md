# Roadmap: Popo Science Study App

**Mode:** Vertical MVP — each phase delivers an end-to-end usable capability
**Phases:** 3 (Phase 0 already complete)
**Granularity:** Coarse

## Phase Summary

| # | Phase | Goal | Requirements | Status |
|---|-------|------|--------------|--------|
| 0 | MVP Study App | Daughter can study from this PC | CONT-01..06, UX-01..05 | Complete ✓ |
| 1 | Deploy to a URL | Daughter can study from phone/tablet | DEPLOY-01..04 | Complete ✓ |
| 2 | Reusability refactor | Adding a new subject takes < 1 hour | REUSE-01..04 | Pending ○ |

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

## Phase 2: Reusability Refactor

**Goal:** Extract chapter content out of the inline `CHAPTERS` array in `index.html` into a standalone data file (or files), and demonstrate the abstraction by adding a second subject. After this phase, adding a new test/subject is a content task, not a code task.
**Mode:** mvp
**Status:** Pending ○
**Trigger to start:** After Phase 1 ships AND after the 2026-05-26 test (no point doing this before — the test is the priority).

**Requirements covered:**
- REUSE-01: Content in a separate data file
- REUSE-02: Drop-in subject mechanism
- REUSE-03: Sample second subject as proof
- REUSE-04: README documenting the schema

**Success criteria:**
1. `index.html` contains the app shell (rendering, quiz logic, persistence) but no chapter content
2. Each subject lives in its own data file (e.g. `data/science-grade4-bodies.json` and one more)
3. App auto-discovers / lists available subjects (or has a simple subject selector)
4. Adding a new subject requires only: drop a data file in the right place + maybe one line in an index
5. README with the schema is < 1 page and includes a worked example
6. A second subject is in the repo and works end-to-end (theory, videos, quizzes)

**Suggested approach:**
- Move `CHAPTERS` array into `data/science-bodies-grade4.json`
- Add a tiny `subjects/index.json` that lists available subjects
- Add a landing page or subject picker if there are >1 subjects
- Refactor `localStorage` keys to be namespaced per subject (so progress doesn't collide)

**UI hint**: yes (subject picker UI may be needed)

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

## Decision: Phases Are Sequenced, Not Parallel

Even though Phase 1 (deploy) and Phase 2 (refactor) touch different concerns, they run sequentially because:
1. Phase 1 is time-critical (test on 2026-05-26); Phase 2 is not
2. Touching the same `index.html` from both at once risks merge friction for a single-parent dev
3. Phase 1 validates whether the current single-file structure is even worth refactoring — if she barely uses it on mobile, Phase 2 may get descoped

---
*Roadmap created: 2026-05-17 — manually generated inline (GSD agents not installed)*
