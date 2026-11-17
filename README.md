# claude-skills-ranjit

Agent Skills I use with Claude. Each folder is one skill: a `SKILL.md` with instructions, plus any assets it needs.

## Skills

| Skill | What it does |
|---|---|
| [study-site](study-site/) | Turns slides, PDFs, past papers or a topic into an interactive single-file study page: scroll-based % progress, tick-off modules, find, step-through SVG diagrams, practice MCQs, and for courses flashcards plus likely exam questions with solutions. Minimal light/dark theme, scroll restore and copy-image buttons. Teaching style adapts to the subject. |

## Install

**Claude.ai** — zip the skill folder (e.g. `study-site/`) and upload it under **Settings → Skills**.

**Claude Code** — copy the folder into your skills directory:

```bash
git clone https://github.com/Ranjit-choudhary/claude-skills-ranjit.git
cp -r claude-skills-ranjit/study-site ~/.claude/skills/        # all projects
# or: cp -r claude-skills-ranjit/study-site .claude/skills/    # one project
```

Then just ask, e.g. *"Make a study page for operating systems chapter 9, virtual memory"* and attach your material, or call it with `/study-site`.

## Customise

Open `study-site/SKILL.md` and edit the **Settings** table at the top (master index URL, default theme, card style). The page template is in `study-site/assets/template.html`.

## License

MIT
