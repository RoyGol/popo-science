# Requirements: Popo Science Study App

**Defined:** 2026-05-17
**Core Value:** The student can study independently and walk into the 2026-05-26 test feeling ready.

## v1 Requirements

Requirements for the initial test (2026-05-26) plus the reusability work. v1 here = "what must be true for this project to be useful right now."

### Content (Phase 0 — already shipped ✓)

- [x] **CONT-01**: 4 chapters cover the exam scope (skin / skeleton / joints / muscles & tendons)
- [x] **CONT-02**: Each chapter has theory text written in simple grade-4 Hebrew, with bulleted explanations
- [x] **CONT-03**: Each chapter has simplified visual diagrams (SVG/CSS — skin layers, joint structure, joint types, muscle types) to aid memorization
- [x] **CONT-04**: Each chapter has the relevant embedded YouTube videos from the school presentation
- [x] **CONT-05**: Each chapter has 20 multiple-choice questions (80 total) with 4 options each
- [x] **CONT-06**: Each question has an optional "💡 רמז" (hint) button and a full explanation shown after submitting

### UX (Phase 0 — already shipped ✓)

- [x] **UX-01**: Full Hebrew RTL layout with a Hebrew web font (Heebo)
- [x] **UX-02**: Per-chapter and overall progress bars
- [x] **UX-03**: Progress (which questions answered, which correct) persisted across sessions via `localStorage`
- [x] **UX-04**: Tabbed interface per chapter (חומר לימוד / סרטונים / תרגול)
- [x] **UX-05**: Reset-per-chapter button so she can retake quizzes

### Deployment (Phase 1 — shipped ✓)

- [x] **DEPLOY-01**: App accessible via a public HTTPS URL — `https://palevioletred-crow-274361.hostingersite.com/` (Hostinger)
- [x] **DEPLOY-02**: URL works on her phone and tablet (responsive layout in place)
- [x] **DEPLOY-03**: URL is bookmarkable (auto-generated Hostinger subdomain; long but bookmark-once-and-done is fine for the use case)
- [x] **DEPLOY-04**: Deployment process is one-step via Hostinger

### Study Modes (Phase 2 — shipped ✓)

- [x] **STUDY-01**: "מבחן סופי" mode — randomized 20-question mixed exam from across all chapters with score and best-score tracking
- [x] **STUDY-02**: "שאלות לחזרה" mode — pool of all wrong-on-first-try questions; re-answering correctly removes from pool and updates chapter progress
- [x] **STUDY-03**: Home screen shows mastery (correct/answered) per chapter; overall progress shows % correct
- [x] **STUDY-04**: Best final-exam score persisted across sessions and shown on the exam card

### Reusability (re-classified — moved from Phase 2 to v2)

The original REUSE-01..04 requirements were re-scoped out of v1 on 2026-05-17. They may return as v2 if more subjects become a real need after the May 26 test.

## v2 Requirements

Deferred. Not in current roadmap.

### Content & Quiz

- ~~**CONT-V2-01**: Mixed "final exam" mode~~ → shipped as STUDY-01 in Phase 2
- ~~**CONT-V2-02**: Spaced-repetition / focus-on-wrong-answers review mode~~ → shipped as STUDY-02 in Phase 2
- **CONT-V2-03**: Real labeled anatomy diagrams (extracted or licensed) instead of simplified SVGs — only if she struggles with the current visuals
- **CONT-V2-04**: Audio narration of theory blocks (helpful for kids who prefer listening)
- **CONT-V2-05**: Flashcard mode for memorizing Hebrew terminology (bone names, layer names, joint types)
- **CONT-V2-06**: Printable one-page summary for last-day review

### Reusability (moved from former Phase 2)

- **REUSE-V2-01**: Chapter content extracted into separate data files
- **REUSE-V2-02**: Multi-subject support with subject picker
- **REUSE-V2-03**: A second sample subject (if/when other tests come up)
- **REUSE-V2-04**: README documenting how to add a subject

### Authoring

- **AUTH-V2-01**: A simple authoring helper (script or page) that turns a list of questions into the data file format

## Out of Scope

| Feature | Reason |
|---------|--------|
| Native mobile app | A responsive deployed web app works on phones/tablets; no install friction |
| User accounts / auth | Single-family use; no shared state |
| Backend / database | Static content + localStorage is sufficient; backend adds cost and ops |
| Teacher / classroom dashboard | Not the use case |
| AI-generated questions | Quality control matters for a kid's test; questions are hand-written and reviewed |
| Multiplayer / leaderboards | Distracts from solo study |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| CONT-01 → CONT-06 | Phase 0 | Complete ✓ |
| UX-01 → UX-05 | Phase 0 | Complete ✓ |
| DEPLOY-01 → DEPLOY-04 | Phase 1 | Complete ✓ |
| STUDY-01 → STUDY-04 | Phase 2 | Complete ✓ |

**Coverage:**
- v1 requirements: 19 total — all 19 complete ✓
- Mapped to phases: 19
- Unmapped: 0 ✓

---
*Requirements defined: 2026-05-17*
*Last updated: 2026-05-17 after Phase 2 (study mode improvements) shipped*
