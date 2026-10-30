---
name: psycheon
description: A second brain that gets to know you and helps you actually learn,
  kept as a folder of plain markdown. Sets up a brain, imports exports
  (Instagram, WhatsApp, ChatGPT, Claude, Takeout, Obsidian), files notes,
  teaches topics by making the user produce, runs spaced-repetition recall,
  writes an evidence-based read of the user, and exports a profile, Anki deck,
  backup or local web app. Use when the user says "psycheon", "set up psycheon",
  "my brain", "second brain", "save this", "import my export", "teach me X",
  "quiz me", "expert review", "ask Musk", "ask Feynman", "what's due", "today",
  "reflect on me", "weekly review", "tidy the brain", "sort these files", "put
  this file in my brain", "export my brain", or "forget someone", or works in a
  folder that has psycheon.md or MIND.md.
tags:
  - second-brain
  - learning
  - spaced-repetition
  - notes
  - pkm
---
# psycheon

## Configuration & Network Access
- **Configuration**: Stores brain path configuration locally in `~/.config/psycheon/brain` and LLM settings in the brain's local `.env` file.
- **Network Access**: Outbound network calls (HTTPS) are made exclusively to user-configured LLM endpoints (e.g. OpenAI-compatible APIs or Anthropic API) when using the Ask web interface to query the brain.


Asked for: $ARGUMENTS

This skill organizes your brain into seven core workflows, plus utility and maintenance tools.
If the first word asked for is a workflow name, run that workflow on the rest; otherwise pick
the one that fits. Read that file in full and follow it.

### Core Workflows

| Workflow | Use when the user wants to… |
|---|---|
| `init` | create a new brain ("set up psycheon"), with a first short interview |
| `capture` | save thoughts, notes, highlights, or route loose files into the vault |
| `learn` | active learning: teach, quiz, diagnose repeated mistakes, or scenario challenge (`challenge`) |
| `expert` | summon expert personas (Musk, Feynman, Freud, etc.) to critique work, teach in their style, and surface opportunities |
| `recall` | review the recall cards that are due using FSRS |
| `today` | do the daily 5-10 minutes: due cards, one learning step, one highlight |
| `reflect` | get the AI's read of them (`insight/`), cognitive profile, and mental connections |
| `export` | export an Anki deck (`.apkg`), AI profile, JSON dump, zip backup, or local web app |

### Maintenance & Utilities

| Workflow | Use when the user wants to… |
|---|---|
| `import` | import an export (WhatsApp, ChatGPT, Claude, Takeout, Obsidian) or folder/.zip |
| `tidy` | health-check the brain: links, index drift, secrets, overdue cards, or scrub entities |
| `review` | do the weekly focus and learning review |
| `sort` | bring files in from anywhere, or move loose ones, to where they belong |
| `connect-dots` | find how everything they know connects across domains (also part of `reflect`) |
| `know-me` | short interview rounds to fill in `self/` profile (also part of `reflect`) |
| `forget` | completely scrub a person or topic from the brain (also part of `tidy`) |

No match but a brain exists (local `psycheon.md` or `MIND.md`, `psycheon_BRAIN`, `~/.config/psycheon/brain`, or `~/mind`)?
**Answer from the notes**, following `psycheon.md`:
- Read `INDEX.md` first and open only the notes that match; grep (outside `raw/imports/` and
  `private/`) for what the index misses.
- Cite every claim with the note it came from, as `[[note#Heading]]`. Quote at most a line when
  the exact words matter.
- If the brain doesn't hold the answer, say "not in your brain" before using what you know.
- An answer that pulls 2+ notes together and will matter again: offer to file it as a new
  `knowledge/` page titled with its claim ("BFS is Dijkstra with equal weights"), linked from
  each note it used, so the next question starts from it.

Not in a brain yet and none configured? Offer `init`.

## Global Brain & Project Context

Commands run from any folder find your central brain automatically:
1. Local directory or parent holding `psycheon.md` or `MIND.md` (local brain wins)
2. `psycheon_BRAIN` environment variable
3. Saved path in `~/.config/psycheon/brain`
4. Default `~/mind`

When you capture from an active project repository (e.g. `~/Developer/projects/my-app`),
psycheon saves to your central vault and automatically links the note to `[[projects/my-app]]`.

## Reading a workflow

- `/psycheon <name> <args>` means the `<name>` workflow, run with those arguments.
- `$ARGUMENTS` means what the user asked for; in a workflow, minus the workflow name.
- `<this skill's dir>` means this skill's folder, which holds `to_text.py`, `export.py`,
  `template/` and `site/`.
- Without the Claude Code plugin, its hooks (secret guard, `raw/` guard, due-card count,
  auto-commit) aren't installed, so keep those rules yourself: never write secrets into
  notes, never edit files in `raw/`, and commit after changes when the brain is a git repo.

