# Project State

## Project Reference

See: `.planning/PROJECT.md` (updated 2026-05-17)

**Core value:** The student can study independently and walk into the 2026-05-26 test feeling ready.
**Current focus:** App is live and ready for use. Phase 2 (reusability refactor) deferred until after the 2026-05-26 test.
**Live URL:** https://palevioletred-crow-274361.hostingersite.com/

## Phase Status

| Phase | Status | Started | Completed |
|-------|--------|---------|-----------|
| Phase 0 — MVP Study App | ✓ Complete | 2026-05-17 | 2026-05-17 |
| Phase 1 — Deploy to URL | ✓ Complete | 2026-05-17 | 2026-05-17 |
| Phase 2 — Reusability Refactor | ○ Pending (post-test) | — | — |

## Active Work

None right now — both shipped phases ahead of the deadline. The next meaningful trigger is the 2026-05-26 test:

- **Before the test**: respond to any feedback she has while using the app (content errors, confusing questions, missing topics). Edit `index.html`, redeploy to Hostinger.
- **After the test**: Phase 2 (reusability refactor) becomes worth doing if more subjects are coming. Otherwise skip.

## Recent Activity

- 2026-05-17 — Project initialized. PROJECT.md, REQUIREMENTS.md, ROADMAP.md, config.json created.
- 2026-05-17 — Phase 0 shipped: `index.html` with 4 chapters, 80 MCQs, embedded videos, Hebrew RTL.
- 2026-05-17 — Git repo initialized in `popo-science/` (commit `ccf7b4e`).
- 2026-05-17 — Pushed code to GitHub: https://github.com/RoyGol/popo-science (code backup; not used for deploy).
- 2026-05-17 — Phase 1 shipped: deployed to Hostinger at https://palevioletred-crow-274361.hostingersite.com/.

## Notes for Future Claude Sessions

- `gsd-sdk` detects `project_root` as `G:\AI` (parent dir). This project deliberately writes its planning files inside `popo-science/.planning/` instead. If you run GSD slash commands, they may target the wrong root — write files manually here.
- GSD subagents are not installed globally. Don't try to spawn `gsd-roadmapper` etc. — they'll fail.
- The student is in 4th grade. All Hebrew text must read naturally at that level. No academic register.
