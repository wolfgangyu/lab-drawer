# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## What This Repo Is

lab-drawer is a collection of Claude Code skills — prompt-based text-processing tools installed via symlinks into `~/.claude/skills/`. There is no build system, no tests, no package.json. Each skill is a standalone Markdown file (plus optional helpers) that teaches an LLM a specific writing discipline.

## Skills

| Directory | Slash Command | Purpose |
|-----------|--------------|---------|
| [humanizer/](humanizer/) | `/humanizer` | Removes 33 AI-writing patterns from English text |
| [humanizer/](humanizer/) (SKILL_zh-TW.md) | `/humanizer-zh` | Same for Traditional Chinese (39 patterns, incl. 6 China-specific) |
| [guardrail/](guardrail/) | — | Diagnoses and optimizes CLAUDE.md files |
| [talk-normal/](talk-normal/) | — | System prompt that reduces LLM verbosity by 56-73% |
| [utils/](utils/) | — | Placeholder for shared tool functions (currently empty) |

## Installing / Using Skills

Each skill is a directory containing a `SKILL.md` (or `SKILL_zh-TW.md`) file. To install:

```bash
# Clone this repo first
git clone https://github.com/wolfgangyu/lab-drawer.git
cd lab-drawer

# Symlink any skill you want
ln -s $(pwd)/humanizer ~/.claude/skills/humanizer
ln -s $(pwd)/guardrail ~/.claude/skills/guardrail
ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal
```

Talk-normal has an extra install step: `cd ~/.claude/skills/talk-normal && bash install.sh`

## Editing Skills

Skills are pure Markdown. To modify a skill:

1. Edit the `SKILL.md` in the relevant directory
2. The YAML frontmatter (`name`, `version`, `description`, `license`, `compatibility`) controls how Claude Code discovers and triggers the skill
3. Changes take effect immediately in the next Claude Code session (no rebuild needed)

## Key Files

- [README.md](README.md) — English index of all skills
- [README_zh-TW.md](README_zh-TW.md) — Traditional Chinese version of the index
- [SKILLS.md](SKILLS.md) — Structured index with descriptions and installation commands
- [.claude/settings.local.json](.claude/settings.local.json) — Local permissions for file-copy operations during setup

## Do NOT introduce

- Build systems, package managers, or dependency files (npm, yarn, pnpm, Makefile, etc.)
- Test harnesses or CI pipelines — skills are prompt-only, tested by human use
- Code files (.js, .ts, .py) — unless placed in utils/ for shared helpers
- Architecture dumps — this repo is a skill collection, not a software project
- Chinese text in CLAUDE.md — future LLM instances read this in English

## Working Style

- Skills are authored in a mix of English and Traditional Chinese depending on target language
- Version numbers follow semantic versioning per skill
- All skills are MIT licensed (see individual SKILL.md frontmatter)
- This repo is a distribution hub; the canonical sources live at github.com/wolfgangyu/{humanizer,guardrail,talk-normal}
