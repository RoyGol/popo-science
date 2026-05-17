# Plan 03: README for Adding a Subject

**Phase:** 2 (Reusability Refactor)
**Status:** ○ Pending
**Depends on:** Plan 01, Plan 02 (the structure must exist before it can be documented)
**Blocks:** (none — last plan in Phase 2)

## Goal

Write a single short markdown doc that lets anyone — including future-Roy after a six-month break — add a new subject to the app in under 30 minutes by reading nothing else.

## Requirements covered

- **REUSE-04**: Short README documents the data schema ✓

## Context

The audience for this README is:
1. **Future-Roy** when he wants to add the next subject (probably 1–6 months from now)
2. **Other Claude sessions** that might be asked to add content
3. **Possibly Roy's daughter** if she's curious how the app works (don't write it for her specifically, but keep it clear)

So: short, concrete, copy-pasteable. Not exhaustive reference docs.

## Tasks

### 1. Create `data/README.md`

Structure (target ≤ 1 page when rendered):

```markdown
# Adding a Subject

This folder holds subject content. Each `.js` file = one subject.

## TL;DR — Add a new subject in 5 steps

1. Copy an existing file, e.g. `cp data/science-bodies-grade4.js data/my-new-subject.js`
2. Edit the new file: change `id`, `title`, `subtitle`, `emoji`, `chapters`
3. Add `<script src="data/my-new-subject.js"></script>` to `index.html` (near the existing data scripts)
4. Refresh — your subject appears in the picker
5. Test all questions work; deploy

## Schema

(Show the subject object schema with field-by-field comments.)

## Theory blocks

(List of supported fields: heading, body, list, extra, diagram. Show one example of each.)

## Questions

(Schema for question objects. Notes on hint and explain.)

## Diagrams

(How to reference existing diagrams; how to add a new one to `DIAGRAMS` in index.html.)

## Worked example

(A complete tiny subject — 1 chapter, 1 theory block, 2 questions, no videos — that someone can copy-paste and modify.)

## Gotchas

- File must be saved as UTF-8 (Hebrew won't render correctly otherwise)
- YouTube embed URLs use `/embed/<id>`, not `/watch?v=<id>`
- `correct` is a 0-based index into `options` (so `correct: 0` = first option)
- Each subject gets its own localStorage namespace; adding a subject doesn't affect others
- After uploading to Hostinger, hard-refresh in case of cache
```

### 2. Inline JSDoc in `index.html` (optional but recommended)

Add JSDoc-style comments above `registerSubject` so IDEs (and future Claude) get inline hints:

```js
/**
 * @typedef {Object} Subject
 * @property {string} id            Unique slug (kebab-case)
 * @property {string} title         Hebrew title shown in picker and hero
 * @property {string} subtitle      Short Hebrew tagline
 * @property {string} emoji         One emoji for the subject card
 * @property {string} [testDate]    ISO date if there's a target test
 * @property {Chapter[]} chapters   Ordered list of chapters
 */
window.registerSubject = (subject) => { window.SUBJECTS.push(subject); };
```

Mirror this for `Chapter`, `TheoryBlock`, `Question` types.

### 3. Update project-level docs

- `CLAUDE.md`: update the "Adding or editing content" section to reference `data/README.md` as the source of truth.
- `.planning/PROJECT.md`: in the Validated requirements list, add the REUSE-01..04 entries (move from Active when Phase 2 executes).
- `.planning/STATE.md`: mark Phase 2 complete, update current focus.

(These are routine artifact updates after phase completion, but listed here so they're not forgotten.)

### 4. Test the README

After writing, follow it literally to add a stub third subject. If any step is unclear or missing, fix the README. Then delete the stub subject before committing.

## Files

**Created:**
- `data/README.md`

**Modified:**
- `index.html` (JSDoc comments — optional)
- `CLAUDE.md` (reference the new README)
- `.planning/PROJECT.md`
- `.planning/STATE.md`
- `.planning/REQUIREMENTS.md` (mark REUSE-01..04 done)

## Acceptance Criteria

- [ ] `data/README.md` exists and is ≤ 1 page when rendered (rough check: under ~120 lines of markdown)
- [ ] The TL;DR section is genuinely 5 steps or fewer
- [ ] A worked example is present and copy-pasteable
- [ ] Self-test passed: a stub third subject was added by literally following the README, with no extra knowledge needed
- [ ] `CLAUDE.md` updated to point at `data/README.md` as the canonical source for adding content
- [ ] Planning docs reflect Phase 2 completion (PROJECT.md, STATE.md, REQUIREMENTS.md)

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| README becomes a wall of text trying to cover everything | Strict ≤ 1 page rule. Anything optional or advanced goes in a "Notes" section, not the TL;DR. |
| Schema documentation drifts from real code | The worked example doubles as schema documentation — and it's testable (copy-paste should work). |
| Future-Roy doesn't read the README and asks Claude to figure it out | That's actually fine — Claude will read `data/README.md` and follow it. Net same outcome. |

## Non-goals

- Reference docs for every Tailwind class used
- A web-based subject authoring tool (deferred to v2 — AUTH-V2-01)
- Internationalization guidance (Hebrew-only for now)
- Migration guide (no schema versioning yet — handle on first breaking change)

## Estimated complexity

**S** — documentation only. 20–40 minutes of writing + a self-test pass.

---
*Last updated: 2026-05-17 after initial planning*
