---
name: study-site
description: Use when making any study page, chapter notes page, revision or exam-prep artifact, or course study index — from slides, PDFs, past papers, tutorial sheets or just a topic name.
---

# Study Site

Build interactive, single-file HTML study pages, published as artifacts (or saved as `.html` files where artifacts aren't available). Every page starts from `assets/template.html`, so the standing features are never forgotten.

## 0. Settings — edit these for yourself

| Setting | Value |
|---|---|
| Master index URL (hub that links every course) | `none` — set it to your hub's URL, or leave `none` to skip index updates |
| Default theme | `light` (a dark toggle is always included) |
| Chapter navigation | Back link to the course index only — no previous/next chapter links |
| Index card style | Minimal: icon, course code, course name — no stats |

## 1. Ask first (one question round)

Ask only what isn't already clear from the request:

1. **Is this for a course?** If yes: which course, which chapter or chunk. A course page gets **exam mode and revision tools** on top of the standard features; a non-course page (general topic, one-off explainer) skips them.
2. **Where should it be listed?** Directly on the master index, inside a course study index (which one), or nowhere. Skip this question if the master index setting is `none`.
3. If the course's study index URL isn't known, ask for it — the page's back link needs it.

If the user has saved notes on how they want a course taught (memory, project instructions, earlier messages), read them and follow them over the defaults below.

## 2. Gather material before building

- Read every attached file fully: slides, notes, past papers, tutorial sheets.
- Collect the past-year questions (PYQs) and tutorial questions belonging to each topic.
- Silently fix errors in the source material; don't point them out unless asked.
- Only then plan the topic list: one `<section class="topic">` per logical topic, small enough to finish in one sitting.

## 3. Teaching rules (all subjects)

- Assume no prior knowledge. Build from basics, define every term on first use, elaborate rather than compress.
- Order inside each topic: **explanation → its diagram immediately after → explanation of the diagram → worked example → PYQs/tutorial questions → practice MCQs.** Never batch diagrams at the end.
- Every diagram gets an explanation. Never ship a bare diagram.
- Mark exam-important points with `.callout.imp` and common traps with `.callout.mistake`.
- **Questions:** write every question out in full before its solution, never condensed. Answer every question; leave none unanswered. Tag PYQs with source, year and marks (e.g. `PYQ 2024 Midsem · 5M`).
- At least 3 practice MCQs per topic, with plausible distractors and a `.why` explanation.
- Diagrams are inline SVG, never ASCII. Use a `.stepper` (one `figure.fig.step` per state) for anything that evolves step by step.
- No study schedules or day plans unless asked.

## 4. Adapt by subject

| Subject type | Emphasis |
|---|---|
| **Theory / proofs** (theory of computation, discrete maths, algorithms) | State diagrams for every automaton; steppers that trace input strings; proof templates (pumping lemma, reductions, induction) as fill-in steps; many small examples |
| **Systems** (operating systems, computer architecture, networks) | Visual-first; steppers for pipelines, scheduling Gantt charts, page replacement, cache lookups; numericals solved step by step; textbook end-of-chapter exercises |
| **Languages / formal notation** (programming languages, compilers) | BNF/EBNF, parse trees and attribute grammars as clean SVG trees; regex built up piece by piece; tutorial questions solved inline |
| **Maths-heavy** (machine learning, statistics, signals) | Intuition first, then the derivation line by line with each step justified; plots in SVG; solved textbook exercises |
| **Descriptive** (biology, management, humanities) | Past-paper driven: group PYQs by theme, model answers at exam length, flowcharts and comparison tables for processes |

Pick the closest row for an unlisted subject. The user's own course notes override this table.

## 5. Page features (built into the template)

| Feature | How it works | Your job |
|---|---|---|
| Light theme + dark toggle | Light by default; a sliding sun/moon switch in the header toggles; choice remembered | Use only the CSS variables — no hard-coded colours |
| Scroll restore | Position saved and restored on reopen | Nothing |
| Progress tracking (chapter pages only) | "Mark as done" per topic; a progress ring with the % done; a sticky strip showing the current section and % done; practice answered/correct counts; ✓ in contents | Unique `id` on each topic section. Exam mode isn't counted. **Never put this on index pages** |
| Search | Filters topics and highlights hits | Nothing |
| Copy image | Hover button on every `figure.fig` copies a PNG (always visible on touch) | Wrap **every** diagram or image in `figure.fig` |
| Mobile friendly | Responsive; tables scroll sideways | Keep SVG `viewBox`-based; no fixed widths |
| Practice MCQs | Instant feedback; answers remembered | `data-answer` = 0-based index of the right option |
| Show answer | `details.answer` | Use for every long-form solution |
| Back link | Header links to the course study index | Fill `{{COURSE_INDEX_URL}}` |
| **Course pages only:** revision tools | Cheat sheet (`.cheatsheet`) + flashcards (`.flashdeck`) | One-page summary of formulas, definitions, key diagrams; 10+ flashcards |
| **Course pages only:** exam mode | Blurred until Start; timer; MCQs graded on Submit; model answers revealed | Mix MCQs (`data-marks`) and long questions styled after the course's past papers; set `data-minutes` |

Progress and scores live in the viewer's browser, per page — an index page can't show chapter progress, and nothing syncs across devices.

## 6. Design rules

- Minimal and calm. Serif body for long reading, sans-serif UI. Content width ~820px.
- Avoid AI-slop: no purple gradients, hero banners, everything-centred layouts, Inter, or emoji confetti.
- Colour carries meaning: blue = info, gold = exam-important, red = mistake, green = correct/done.
- SVG diagrams: label everything; use `var(--text)`, `var(--accent)` etc. for strokes and fills; text ≥12px at mobile width.

## 7. Course study index pages

For a course index or hub: minimal cards (see settings), same header (search + theme toggle), scroll restore, light default. **Don't build index pages from the chapter template:** no progress ring, % strip, "Mark as done" buttons or stat counters — those belong only on chapter pages.

## 8. Build, publish, check

1. Copy `assets/template.html`, fill the `{{placeholders}}`, delete the course-only blocks for non-course pages (or uncomment them for course pages).
2. Publish as an artifact (or save the `.html`). Show it first; check after.
3. Check at desktop and ~390px width, in both themes: every figure has a copy button, every MCQ has a correct `data-answer`, every question has an answer, no `{{placeholders}}` remain.
4. Add the page link to the master or course index as chosen in step 1. Don't redesign the index.
