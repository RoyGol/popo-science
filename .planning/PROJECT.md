# Popo Science — Study App

## What This Is

A Hebrew web app that helps a grade-4 student study for science tests by turning source material (PDFs, slide decks) into structured study chapters with theory, embedded videos, and self-marking multiple-choice quizzes. Initially built for one specific test on body systems (skin, skeleton, joints, muscles) on 2026-05-26 — but designed to be reusable for future tests and subjects.

## Core Value

The student can study independently — read, watch, and practice — and walk into the test feeling ready. Anything that gets in the way of that (broken Hebrew, confusing UI, unreliable access) is a P0 problem.

## Requirements

### Validated

<!-- Shipped and confirmed valuable. -->

- ✓ Single-file `index.html` covering 4 chapters from the May 26 test scope — Phase 0 (initial build)
- ✓ Theory written in simple grade-4 Hebrew with bulleted explanations and simplified SVG diagrams — Phase 0
- ✓ Embedded YouTube videos from the school presentation, distributed by chapter — Phase 0
- ✓ 80 MCQs total (20 per chapter) with hint button and post-submit explanation — Phase 0
- ✓ Hebrew RTL layout with kid-friendly font (Heebo), gradients, and progress indicators — Phase 0
- ✓ Per-chapter and overall progress persisted in `localStorage` — Phase 0

### Active

<!-- Current scope. Building toward these. -->

- [ ] App accessible from her phone/tablet via a stable URL by ~2026-05-19 (gives her a week of real use before the test)
- [ ] Chapter content (theory, videos, questions) extracted from `index.html` into a separate data structure (JSON or JS module) so that adding a new subject doesn't require editing the app code
- [ ] One additional sample subject added as proof-of-concept for the reusability refactor
- [ ] Short README on how to add a new test/subject (file layout, fields, gotchas)

### Out of Scope

<!-- Explicit boundaries. Includes reasoning to prevent re-adding. -->

- Native mobile app (iOS/Android) — a deployed responsive web app works fine on phones and tablets, no install needed
- Multi-user / accounts / login — built for a single family member, no auth needed
- Backend / database — progress lives in `localStorage`, content is static; a server adds cost and ops for zero benefit
- Teacher dashboard / classroom features — not the use case; this is a parent-built study aid, not a SaaS
- Audio narration (TTS) — nice-to-have, not blocking for the May 26 test
- Photorealistic anatomy diagrams extracted from the source PDFs — current simplified SVGs are sufficient for memorization; revisit only if she struggles

## Context

- Source material: two Hebrew PDFs in `files/` — one is the teacher's exam announcement (topics + page range), the other is the school's slide deck on skin/skeleton/joints/muscles (~36 slides with diagrams, summary tables, and 7 YouTube video links)
- The student is in 4th grade, native Hebrew speaker. The app must read naturally to her — no academic register, no English jargon
- Built by her parent, not by a dev team. Optimize for "I can open this and ship a change in 5 minutes" over enterprise polish
- Original test: skin (העור) — 8 functions, 3 layers, sense cells; skeleton (השלד) — 206 bones, 5 roles, 4 bone types, S-shaped spine; joints (מפרקים) — sutured/ball/hinge, structure (cartilage/fluid/ligaments); muscles (שרירים) — voluntary vs involuntary, tendons, contraction/relaxation
- Parent indicated other tests are "probably yes" in the future — so the reusability refactor is real, not speculative

## Constraints

- **Timeline**: Hard deadline 2026-05-26 for the original test. Deployment must land by ~2026-05-19 to leave her a week of usable runway.
- **Tech stack**: Single-file HTML + TailwindCSS via CDN + vanilla JS. No build step. No dependencies to install. Anyone with a browser can run it locally.
- **Language**: Hebrew, RTL, grade-4 reading level. No mixed-language UI strings.
- **Offline-tolerant**: Once loaded, the app works without internet (except YouTube videos, which need network). LocalStorage for state.
- **Privacy**: No telemetry, no analytics, no third-party scripts beyond Tailwind CDN and Google Fonts. Child user.

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Single-file `index.html` with Tailwind CDN, no build step | Parent needs to edit and ship in minutes; no Node toolchain in the path | ✓ Good (Phase 0 shipped same day) |
| Simplified SVG diagrams instead of extracting PDF images | PDF image extraction is fragile; SVG renders crisp on any screen; concepts > photorealism for memorization | — Pending (validate after she uses it) |
| Embed YouTube videos directly (iframe) rather than re-hosting | Free, reliable, already curated by her teacher | ✓ Good |
| `localStorage` for progress, no backend | Single-user app, no need for sync; eliminates an entire class of ops | ✓ Good |
| Defer reusability refactor to Phase 2 (after deployment) | Test on 2026-05-26 is the priority; refactor doesn't help her study | — Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition:**
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone:**
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state (did she pass the test? what did she actually use?)

---
*Last updated: 2026-05-17 after initialization*
