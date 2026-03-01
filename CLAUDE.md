# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A MkDocs Material documentation site at [claudeblattman.com](https://claudeblattman.com) — a guide for non-developers building AI workflows with Claude Code. Content lives in `docs/`. Skills, agents, and templates are downloadable markdown files in `skills/`, `agents/`, and `templates/`.

## Local Preview

```bash
pip install -r requirements.txt   # pinned: mkdocs-material[imaging]==9.7.2
mkdocs serve
# Open http://localhost:8000
```

The `[imaging]` extra powers social card generation and requires system libraries (`libcairo2-dev`, `libfreetype6-dev`, etc.). These are installed automatically in CI but must be installed manually for local builds if you want social cards.

## Deployment

Push to `main` — GitHub Actions runs `mkdocs gh-deploy --force` automatically (~2 min turnaround). No manual deploy step.

## Adding Content

**New page:** Create `.md` in the appropriate `docs/` subdirectory, then add it to the `nav:` section of `mkdocs.yml`.

**New skill:** Sanitize it (see below), save to `skills/[skill-name].md`, and add a section to `docs/setup/skill-reference.md` with: what it does, MCP dependencies, installation instructions, full skill in a code block, and customization points. Skills that share a companion reference file (like the prompt bundle) use a subdirectory: `skills/[skill-name]-references/`.

**Every content page** should open with:

```markdown
# Page Title

!!! warning "Early Preview"
    This site is growing weekly. Current as of [MONTH YEAR].
```

Update the date whenever making substantive changes.

## Sanitization Checklist (Skills / Agents / Templates)

Run all four passes before committing skill-related changes:

1. **Personal identifiers** — names, phone numbers, emails, institutions
2. **Hardcoded paths** — replace `/Users/...`, `~/Dropbox/...` with `~/Documents/` or `~/.claude/`
3. **Project-specific references** — grant names, study locations, project names
4. **Manual read-through** — automated grep misses context; read every file end-to-end

## Site Architecture

| Directory | Purpose |
|-----------|---------|
| `docs/` | All site content (59 markdown pages) |
| `docs/essentials/` | Foundational AI tools (chatbots, prompting, dictation) |
| `docs/setup/` | Installation and configuration guides |
| `docs/toolkit/` | Claude Code setup, skills guide, MCP setup |
| `docs/workflows/` | Real-world workflow patterns |
| `docs/tax-workflow/` | Tax season case study |
| `docs/system/` | Advanced topics (agents, continuous improvement) |
| `docs/downloads/` | Reference library and real examples |
| `skills/` | 20+ downloadable slash-command skill files |
| `skills/prompt-references/` | Companion file (`formatting-core.md`) for the prompt skill bundle |
| `skills/tips-integrate-references/` | Companion file (`scanning-rules.md`) for the tips-integrate skill |
| `agents/` | Writing and methodology reviewer agents |
| `templates/` | Starter templates (CLAUDE.md, goals.yaml, email policy, calendar policy, triage config) |
| `overrides/` | MkDocs Material theme customizations |
| `mkdocs.yml` | Full site config: nav structure, theme, plugins, extensions |

Navigation hierarchy is defined entirely in `mkdocs.yml` under `nav:`. File location in `docs/` and nav position are independent — both must be set when adding a page.

## Style Guidelines

- Short sentences, short paragraphs
- Tables for structured information
- Admonitions for callouts: `!!! tip`, `!!! warning`, `!!! note`
- Cross-link generously between pages
- Voice: accessible, direct, slightly informal — not corporate, not condescending
- Include "current as of [MONTH YEAR]" on any time-sensitive page
