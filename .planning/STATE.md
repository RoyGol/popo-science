# Project State

## Project Reference

See: `.planning/PROJECT.md` (updated 2026-05-17)

**Core value:** The student can study independently and walk into the 2026-05-26 test feeling ready.
**Current focus:** All planned phases shipped. Reactive mode — respond to her real-world use over the next 9 days.
**Live URL:** https://palevioletred-crow-274361.hostingersite.com/ (Hostinger — re-upload `index.html` to push updates)

## Phase Status

| Phase | Status | Started | Completed |
|-------|--------|---------|-----------|
| Phase 0 — MVP Study App | ✓ Complete | 2026-05-17 | 2026-05-17 |
| Phase 1 — Deploy to URL | ✓ Complete | 2026-05-17 | 2026-05-17 |
| Phase 2 — Study Mode Improvements (re-scoped) | ✓ Complete | 2026-05-17 | 2026-05-17 |

## Active Work

None — three phases shipped same day. The next meaningful triggers are:

- **Daughter surfaces a content error or confusion** → edit `index.html`, re-upload to Hostinger, push to GitHub.
- **2026-05-26 (the test)** → after the test, review what was actually useful vs. unused; revisit the v2 backlog in REQUIREMENTS.md only if more tests / subjects are coming.

## Recent Activity

- 2026-05-17 — Project initialized. PROJECT.md, REQUIREMENTS.md, ROADMAP.md, config.json created.
- 2026-05-17 — Phase 0 shipped: `index.html` with 4 chapters, 80 MCQs, embedded videos, Hebrew RTL (commit `ccf7b4e`).
- 2026-05-17 — Pushed code to GitHub: https://github.com/RoyGol/popo-science.
- 2026-05-17 — Phase 1 shipped: deployed to Hostinger at https://palevioletred-crow-274361.hostingersite.com/.
- 2026-05-17 — Phase 2 initially planned as "reusability refactor" (3 plans, deferred to post-test). Re-scoped after user feedback: should help with this test, not future-proof.
- 2026-05-17 — Phase 2 shipped (re-scoped): "מבחן סופי" mode, "שאלות לחזרה" mode, mastery progress UI (commit `66a2d0d`). **Re-upload `index.html` to Hostinger to make it live.**

## Notes for Future Claude Sessions

- `gsd-sdk` detects `project_root` as `G:\AI` (parent dir). This project deliberately writes its planning files inside `popo-science/.planning/`. If you run GSD slash commands, they may target the wrong root — write files manually here.
- GSD subagents are not installed globally. Don't try to spawn `gsd-roadmapper` etc. — they'll fail.
- The student is in 4th grade. All Hebrew text must read naturally at that level. No academic register.
- Hostinger deployment is **manual**: editing `index.html` and committing/pushing does NOT update the live site. Roy must re-upload `index.html` via Hostinger control panel.
- See memory `feedback_prioritize_immediate_user_over_architecture.md` — when planning future phases, prioritize what helps the immediate user before their deadline over architectural cleanup.
