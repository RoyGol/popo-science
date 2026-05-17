# Project State

## Project Reference

See: `.planning/PROJECT.md` (updated 2026-05-17)

**Core value:** The student can study independently and walk into the 2026-05-26 test feeling ready.
**Current focus:** Phase 1 — Deploy to a stable URL

## Phase Status

| Phase | Status | Started | Completed |
|-------|--------|---------|-----------|
| Phase 0 — MVP Study App | ✓ Complete | 2026-05-17 | 2026-05-17 |
| Phase 1 — Deploy to URL | ◆ Active (not yet started) | — | — |
| Phase 2 — Reusability Refactor | ○ Pending | — | — |

## Active Work

**Phase 1 — Deploy to URL**
- Hard deadline: 2026-05-19 (gives ≥ 7 days before test)
- Next action: Decide deployment target (Netlify Drop / GitHub Pages / Vercel) and ship
- Blockers: none

## Recent Activity

- 2026-05-17 — Project initialized. PROJECT.md, REQUIREMENTS.md, ROADMAP.md, config.json created.
- 2026-05-17 — Phase 0 shipped: `index.html` with 4 chapters, 80 MCQs, embedded videos, Hebrew RTL.
- 2026-05-17 — Git repo initialized in `popo-science/` (commit `ccf7b4e`).

## Notes for Future Claude Sessions

- `gsd-sdk` detects `project_root` as `G:\AI` (parent dir). This project deliberately writes its planning files inside `popo-science/.planning/` instead. If you run GSD slash commands, they may target the wrong root — write files manually here.
- GSD subagents are not installed globally. Don't try to spawn `gsd-roadmapper` etc. — they'll fail.
- The student is in 4th grade. All Hebrew text must read naturally at that level. No academic register.
