# Phase 2: Reusability Refactor

**Status:** ○ Planned (execution deferred until after the 2026-05-26 test)
**Mode:** mvp
**Created:** 2026-05-17

## Goal

Extract chapter content out of `index.html` into a separate data layer so that adding a new test/subject becomes a *content task*, not a code task. Prove the abstraction by adding a second sample subject. Document the schema so anyone (including future-Roy in 6 months) can add a subject by reading a single short README.

## Requirements (from REQUIREMENTS.md)

- **REUSE-01**: Chapter content lives in a separate data file, not inline inside `index.html`
- **REUSE-02**: Adding a new subject = drop in a new data file, no JS/HTML changes to the shell
- **REUSE-03**: A second sample subject exists as proof-of-concept
- **REUSE-04**: Short README documents the data schema

## Phase Success Criteria

1. `index.html` contains app shell only (render, quiz logic, persistence) — no chapter content
2. Each subject lives in its own data file under `data/`
3. App auto-discovers subjects and lists them when there's more than one
4. Adding a third subject requires only: drop a data file in `data/` and add one `<script>` tag (or — if we go further — just drop the file)
5. README is ≤ 1 page with a copy-pasteable worked example
6. A second subject ships in the repo and works end-to-end (theory, videos, quizzes, progress)

## Plans (sequential — each depends on the previous)

| # | Plan | Goal | Complexity |
|---|------|------|------------|
| 01 | Extract content + dynamic load | Move CHAPTERS out of `index.html`, load via a registry pattern, namespace localStorage per subject | M |
| 02 | Subject picker + second subject | Add picker UI when ≥2 subjects, ship a second sample subject as proof | M |
| 03 | README for adding a subject | Document schema with worked example | S |

**Why sequential, not parallel:** Plan 02's picker only makes sense after Plan 01's extraction. Plan 03 documents the resulting structure, so it must come last.

## Key Design Decisions

| Decision | Why |
|---|---|
| Registry pattern via `<script>` tag (not `fetch()` + JSON) | Works for both `file://` and `https://`. No CORS issues for local testing. Browser-native, no build step. |
| One data file per subject (not one big subjects.json) | Drop-in additions, smaller diffs, easier to author one subject without touching others |
| Namespace localStorage as `popoProgress::<subjectId>::v1` | Per-subject progress without collisions. Bump `v1` if schema changes. |
| Auto-migrate existing `popoScienceProgress_v1` key | Don't wipe the daughter's progress when refactor ships |
| Subject picker shown only when `SUBJECTS.length > 1` | Single-subject case (current state) stays exactly as it is — no extra click |

## Deferral

This phase is planned but **execution is deferred until after the 2026-05-26 test**.

**Why:**
- The working app is what she's studying from. Refactoring carries breakage risk. Risk to her test prep > the value of refactoring earlier.
- If no more subjects materialize, this phase may not even be worth executing.

**Trigger to execute:**
- Test on 2026-05-26 has been taken AND another subject is on the horizon, OR
- Parent explicitly wants to refactor regardless (curiosity / cleanup)

## Open Questions for Pre-Execution

1. What should the second sample subject be? (Real upcoming test? Throwaway placeholder like multiplication tables? A different grade-4 science chapter?) — **defer until trigger**
2. Should the subject picker support URL-based routing (`#/subject/<id>`)? — nice-to-have, can defer to a later refinement
3. Where does the README live: `data/README.md` or `docs/adding-subjects.md`? — opt for `data/README.md` (close to the thing it documents)

---
*Last updated: 2026-05-17 after initial planning*
