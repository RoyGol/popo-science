# Plan 01: Extract Chapter Content + Dynamic Load

**Phase:** 2 (Reusability Refactor)
**Status:** ○ Pending
**Depends on:** (none — this is the first plan in Phase 2)
**Blocks:** Plan 02, Plan 03

## Goal

Move the `CHAPTERS` array and all chapter content (theory, diagrams, videos, questions) out of `index.html` into a standalone data file at `data/science-bodies-grade4.js`. Have `index.html` discover and load subjects via a tiny registry pattern. Namespace `localStorage` per subject so multi-subject support (Plan 02) works without progress collisions.

After this plan: the app renders identically to today, but the chapter content is no longer hard-coded in `index.html`.

## Requirements covered

- **REUSE-01**: Chapter content in a separate data file ✓ (full coverage)

## Context (read before starting)

- `index.html` currently contains a `const CHAPTERS = [...]` literal inside the main `<script>` block, ~600+ lines of Hebrew content.
- `DIAGRAMS` (the SVG/HTML diagram registry) stays in `index.html` for now — diagrams are app shell, not subject content. Subjects reference them by name (`diagram: 'skinLayers'`). Future subjects can either reuse existing diagrams or — if needed — add their own diagram renderers in their data file.
- The current localStorage key is `popoScienceProgress_v1`. Daughter has been using the app — **her progress must not be wiped** by this refactor.
- App is deployed at https://palevioletred-crow-274361.hostingersite.com/ (Hostinger). Test by uploading and refreshing.

## Tasks

### 1. Define the subject registry pattern

In `index.html`, near the top of the main `<script>` tag (before any other logic), add:

```js
window.SUBJECTS = window.SUBJECTS || [];
window.registerSubject = (subject) => { window.SUBJECTS.push(subject); };
```

This must run BEFORE the data file scripts execute. Place the registry definition at the very top of the main `<script>`, and load data files via `<script>` tags placed *before* the main app script.

### 2. Create `data/science-bodies-grade4.js`

Wrap the existing `CHAPTERS` array in a `registerSubject({...})` call. Schema:

```js
registerSubject({
  id: 'science-bodies-grade4',
  title: 'מדעים — גוף האדם',
  subtitle: 'עור, שלד, מפרקים, שרירים — לכיתה ד׳',
  emoji: '🧠',
  testDate: '2026-05-26', // optional, for display
  chapters: [ /* the existing CHAPTERS array, moved verbatim */ ]
});
```

Keep all chapter content byte-identical to today (no rewriting). Cut-and-paste from `index.html`.

### 3. Wire up `index.html` to the registry

Replace the inline `const CHAPTERS = [...]` with:

```js
const activeSubject = window.SUBJECTS[0]; // single-subject case for now (Plan 02 handles multi)
if (!activeSubject) {
  document.body.innerHTML = '<div class="p-8 text-center text-rose-600">לא נטענו נושאים. בדוק שקובץ הנתונים נטען.</div>';
  throw new Error('No subjects registered');
}
const CHAPTERS = activeSubject.chapters;
```

Update the hero header to optionally show `activeSubject.title` / `subtitle` (or keep the current hardcoded hero — they happen to match the current subject; we can address that more thoroughly in Plan 02).

### 4. Add the data file `<script>` tag

In `<body>`, before the main app `<script>`:

```html
<script src="data/science-bodies-grade4.js"></script>
<script>
  /* main app script — keep as is */
</script>
```

### 5. Namespace localStorage per subject

Change `STORAGE_KEY`:

```js
const STORAGE_KEY = `popoProgress::${activeSubject.id}::v1`;
```

### 6. Migrate existing progress (one-time)

In `loadProgress()`, add a migration step:

```js
function loadProgress() {
  try {
    // One-time migration from pre-refactor key
    const legacy = localStorage.getItem('popoScienceProgress_v1');
    if (legacy && !localStorage.getItem(STORAGE_KEY)) {
      localStorage.setItem(STORAGE_KEY, legacy);
      // optional: localStorage.removeItem('popoScienceProgress_v1');
    }
    return JSON.parse(localStorage.getItem(STORAGE_KEY)) || {};
  } catch { return {}; }
}
```

Don't delete the legacy key (defensive — let it linger so a botched migration can be rolled back manually).

### 7. Local smoke test before deploying

Open `index.html` in browser (file://). Verify:
- All 4 chapters render
- All 80 questions present
- Previous progress shows up (the migration worked)
- Submitting a new answer persists and survives reload

If file:// blocks the `<script src="data/..." >` for any reason, fall back to inlining data as a `<script>` block. (Should not happen — `<script src>` works fine with relative paths on file://.)

### 8. Deploy and verify

Upload changed/new files to Hostinger. Open the live URL. Confirm:
- Page loads (no JS errors in console)
- Chapters render
- Progress is preserved (the migration ran)
- Questions answer correctly, explanations show

## Files

**Created:**
- `data/science-bodies-grade4.js`

**Modified:**
- `index.html` (remove `CHAPTERS` literal, add registry, add migration, add `<script src>` tag, update STORAGE_KEY)

## Acceptance Criteria

- [ ] `index.html` no longer contains the `CHAPTERS = [...]` literal
- [ ] `data/science-bodies-grade4.js` exists and exports the subject via `registerSubject()`
- [ ] On load, the app behaves identically to before the refactor for the existing subject
- [ ] Daughter's existing progress is preserved (the localStorage migration works on first load after deploy)
- [ ] Removing/renaming the data file `<script>` tag results in a clear Hebrew error message, not a blank page
- [ ] localStorage key follows the new namespaced format (`popoProgress::science-bodies-grade4::v1`)
- [ ] Deployed version on Hostinger shows the same UI as before

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Hebrew content in a JS file gets mojibake'd if saved with wrong encoding | Save UTF-8 (no BOM needed for modern browsers). Spot-check after upload. |
| Migration fails silently and daughter loses progress | Wrap migration in try/catch; keep legacy key in place; test locally before deploy |
| Script load order: data file races the main app | Use plain `<script>` tags (not `async`/`defer`/`type=module`) — they execute in document order, registry pattern works |
| Hostinger CDN caches old `index.html` | Hard refresh after deploy; if persistent, bump a `?v=2` query string on the script tags |

## Non-goals (deferred to other plans or future)

- Subject picker UI → Plan 02
- Second sample subject → Plan 02
- Documentation → Plan 03
- URL routing (`#/subject/id/chapter/x`) → not in Phase 2
- Auto-discovery without `<script>` tags (e.g. dir listing) → not possible client-side; Plan 03 documents the `<script>` tag step

## Estimated complexity

**M** — mostly mechanical (cut/paste content), but the localStorage migration is a real correctness concern. Maybe 30–60 minutes of careful work + 10 min of testing.

---
*Last updated: 2026-05-17 after initial planning*
