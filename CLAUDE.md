# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Hebrew web app that helps a grade-4 student study for science tests. Built initially for a test on body systems (skin, skeleton, joints, muscles) on **2026-05-26**, but designed to extend to future subjects.

The audience is a single specific kid (the project owner's daughter). Optimize all UX, copy, and visual choices for that real user — not for a generic "users" abstraction.

## Tech stack

- **Single-file app**: `index.html` contains everything (markup, styles via Tailwind CDN, content, logic). No build step, no `package.json`, no Node toolchain.
- **TailwindCSS**: loaded from CDN (`cdn.tailwindcss.com`).
- **Hebrew web font**: Heebo, loaded from Google Fonts.
- **State**: vanilla JS, `localStorage` for progress persistence.
- **Videos**: YouTube `<iframe>` embeds (URLs come from the school's slide deck).

There is intentionally no framework, no bundler, no test runner. Edit-save-refresh is the dev loop.

## Running it

Just open `index.html` in any browser. There is no dev server. There are no commands to memorize.

Production deployment (Phase 1, in progress) will use Netlify Drop / GitHub Pages / Vercel — all zero-config static hosting.

## Project structure

```
popo-science/
├── index.html              The entire app
├── files/                  Source material (Hebrew PDFs from the teacher)
├── .planning/              GSD planning docs (PROJECT.md, ROADMAP.md, REQUIREMENTS.md, etc.)
└── CLAUDE.md               This file
```

## Architecture (inside index.html)

- `CHAPTERS` (top of `<script>`): an array of 4 chapter objects, each containing `theory`, `videos`, `questions`. **All content lives here for now** — extracting this into a separate data file is Phase 2.
- `DIAGRAMS`: a map of named SVG/HTML diagram renderers referenced by theory blocks via `diagram: 'name'`.
- Rendering: `renderHome()` → chapter cards; `openChapter(id)` → 3-tab view (theory / videos / quiz); each tab has its own `render*` function.
- Quiz: `bindQuiz()` attaches click handlers per question (select option → check → show explanation → save to localStorage).
- Storage key: `popoScienceProgress_v1`.

## Things to know before editing

- **RTL is everywhere.** `<html dir="rtl" lang="he">`. Don't break this. Tailwind utilities like `ml-*` still mean "margin-left" — under RTL they visually appear on the right. Test in browser.
- **Hebrew at grade-4 reading level.** No academic register, no English jargon. When in doubt, simpler. The bar for a hint or explanation is: "would a 9-year-old understand this on first read?"
- **Don't translate UI strings to English** — every visible string is Hebrew, deliberately.
- **The test is on 2026-05-26.** Until then, don't refactor in ways that risk breaking the working app. After the test, Phase 2 (reusability refactor) is fair game.
- **Progress is precious.** If you change the shape of localStorage data, also bump the storage key version (`popoScienceProgress_v1` → `_v2`) so old corrupted state doesn't crash the app.

## Adding or editing content

- **A new question**: add an object to the relevant chapter's `questions: [...]` array. Fields: `q`, `options` (4 strings), `correct` (0-3), `hint`, `explain`.
- **A new theory block**: add an object to the relevant chapter's `theory: [...]` array. Fields: `heading`, `body` (HTML allowed), `list` (array of HTML strings), `extra` (a callout note), `diagram` (key into `DIAGRAMS`).
- **A new diagram**: add a renderer to `DIAGRAMS` returning an HTML string. Reference it from a theory block.
- **A new video**: add `{ title, url }` (use the YouTube `/embed/...` URL, not the watch URL).
- **A new chapter** (e.g. extending the test scope): add a chapter object to `CHAPTERS` with `id`, `title`, `subtitle`, `emoji`, `color` (Tailwind gradient classes), `theory`, `videos`, `questions`.

## GSD context

This project uses GSD planning artifacts in `.planning/`:
- `PROJECT.md` — what this is, who it's for, what's in/out of scope
- `REQUIREMENTS.md` — what must be true to call it done
- `ROADMAP.md` — phases and success criteria
- `STATE.md` — current focus and recent activity
- `config.json` — workflow preferences

**Note**: `gsd-sdk` resolves `project_root` to the parent `G:\AI` directory, not this folder. If you invoke GSD slash commands here, they may try to write files in the wrong place. Until that's fixed, write planning files manually into `popo-science/.planning/`. GSD subagents are also not installed globally — don't try to spawn them.
