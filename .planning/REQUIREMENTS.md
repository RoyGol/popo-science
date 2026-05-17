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

### Deployment (Phase 1)

- [ ] **DEPLOY-01**: App accessible via a public HTTPS URL
- [ ] **DEPLOY-02**: URL works on her phone and tablet (responsive layout already in place — verify)
- [ ] **DEPLOY-03**: URL is short / memorable enough to type or bookmark easily
- [ ] **DEPLOY-04**: Deployment process is one command/click so updates can ship same-day

### Reusability (Phase 2)

- [ ] **REUSE-01**: Chapter content (theory blocks, videos, questions, diagrams) lives in a separate data file, not inline inside `index.html`
- [ ] **REUSE-02**: Adding a new subject = drop in a new data file, no JS/HTML changes required to the app shell
- [ ] **REUSE-03**: A second sample subject exists in the codebase as proof-of-concept
- [ ] **REUSE-04**: Short README documents the data schema and how to add a new subject

## v2 Requirements

Deferred. Not in current roadmap.

### Content & Quiz

- **CONT-V2-01**: Mixed "final exam" mode that draws questions from all chapters
- **CONT-V2-02**: Spaced-repetition / focus-on-wrong-answers review mode
- **CONT-V2-03**: Real labeled anatomy diagrams (extracted or licensed) instead of simplified SVGs — only if she struggles with the current visuals
- **CONT-V2-04**: Audio narration of theory blocks (helpful for kids who prefer listening)

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
| DEPLOY-01 → DEPLOY-04 | Phase 1 | Pending |
| REUSE-01 → REUSE-04 | Phase 2 | Pending |

**Coverage:**
- v1 requirements: 19 total (11 done, 8 pending)
- Mapped to phases: 19
- Unmapped: 0 ✓

---
*Requirements defined: 2026-05-17*
*Last updated: 2026-05-17 after initial definition*
