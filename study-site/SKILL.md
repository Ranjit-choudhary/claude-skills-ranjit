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

1. **Is this for a course?** If yes: which course, which chapter or chunk. A course page gets **revision tools and likely exam questions (with solutions)** on top of the standard features; a non-course page (general topic, one-off explainer) skips them.
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
- **Likely exam questions (course pages):** a final module of questions the exam is likely to ask, drawn from past papers and the syllabus. Write each question in full, tagged `Likely · Qn · xM`, with a complete worked solution inside `details.answer` ("Show solution"). No timed exam mode.
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
| Light theme + dark switch | Light by default; a small sliding sun/moon switch in the header; choice remembered | Use only the CSS variables — no hard-coded colours |
| Scroll restore | Position saved and restored on reopen (after fonts load) | Nothing |
| Reading progress (chapter pages only) | % rises as you scroll: thin bar under the header, % in the sticky strip next to the current section name, and a ring card at the top with modules done / practice answered / correct | Nothing. **Never put this on index pages** |
| Mark as done | Tick box with "Mark as done" at the **bottom** of each module (box on the left); ✓ in the contents | Unique `id` on each module section |
| Find | Search icon in the header opens a small find bar; highlights hits and hides non-matching modules | Nothing |
| Copy image | Bare icon button at the top right of every `figure.fig`, shown on hover (faint on touch screens); copies a PNG, or shows the image to press-and-hold if the clipboard is blocked | Wrap **every** diagram or image in `figure.fig`. Add class `paper` to always-white images (scanned papers) |
| Copy buttons | Same icon on every module heading (copies the module), every `h3` (copies up to the next heading) and every `.pyq` question (question + solution). Copies clean Markdown: `##`/`###` headings, `[Figure: caption]`, equations as `$tex$`. If the clipboard is blocked, a box opens with the text selected | Use `h3` for sub-headings inside a module |
| Equations (maths-heavy subjects) | Uncomment the MathJax block in `<head>`; write `$…$` inline and `$$…$$` display. Normal select-and-copy keeps the LaTeX with no stray line breaks; long inline equations scroll instead of widening the page on phones | At 390px width `document.documentElement.scrollWidth` must be 390 |
| Mobile friendly | Responsive; tables scroll sideways | Keep SVG `viewBox`-based; no fixed widths |
| Practice MCQs | Instant feedback; answers remembered | `data-answer` = 0-based index of the right option |
| Show answer | `details.answer` | Use for every long-form solution |
| Back link | Header links to the course study index | Fill `{{COURSE_INDEX_URL}}` |
| **Course pages only:** revision tools | Cheat sheet (`.cheatsheet`) + flashcards (`.flashdeck`, term/answer cards) | One-page summary of formulas, definitions, key diagrams; 10+ flashcards |
| **Course pages only:** likely exam questions | Module of `.pyq` items tagged `Likely · Qn · xM`, each with a "Show solution" | Style them after the course's past papers; full solutions |

Progress and scores live in the viewer's browser, per page — an index page can't show chapter progress, and nothing syncs across devices.

## 6. Design rules

- Minimal and calm, like a clean paper page: hairline rules, one indigo accent, generous spacing. Fonts: Literata (headings), Source Sans 3 (body), JetBrains Mono (small labels). Content width ~820px.
- Avoid AI-slop: no gradients, hero banners, everything-centred layouts, Inter, or emoji.
- Colour carries meaning: blue = info, gold = exam-important, red = mistake, green = correct/done.
- SVG diagrams: label everything; use `var(--text)`, `var(--accent)` etc. for strokes and fills; text ≥12px at mobile width.

## 7. Course study index pages

For a course index or hub: minimal cards (see settings), same header (find icon + theme switch), scroll restore, light default. **Don't build index pages from the chapter template:** no progress ring, % strip, "Mark as done" tick boxes or stat counters — those belong only on chapter pages.

- **Top of the index:** meta line, title, then **one line** saying which lectures it was built from (e.g. "Built from lectures 21–24 so far."). No intro paragraph describing the modules, what each contains or how long they take.
- **Module cards:** title (linked), section numbers and the "Mark done" toggle only. No status labels under a card ("Ready", "Not built yet" and the like).
- **Leave out:** a full topic-by-topic breakdown of every module, and an exam-pattern / evaluation table copied from the course handout.
- **Past papers used:** a short list (chips) of only the papers the pages were built from, by name and year (e.g. "End-Semester Examination, 2025"). Tutorials used can go in one muted line under it. No table mapping each question to the module or topic where it's solved.

## 8. Build, publish, check

1. Copy `assets/template.html`, fill the `{{placeholders}}`, delete the course-only blocks for non-course pages (or uncomment them for course pages).
2. Publish as an artifact (or save the `.html`). Show it first; check after.
3. Check at desktop and ~390px width, in both themes: every figure has a copy button, equations (if any) copy as LaTeX, the page isn't wider than the screen at 390px, every MCQ has a correct `data-answer`, every question has an answer, no `{{placeholders}}` remain.
4. Add the page link to the master or course index as chosen in step 1. Don't redesign the index.
