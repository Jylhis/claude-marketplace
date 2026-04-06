# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin marketplace — a collection of plugins that users install via `/plugin marketplace add Jylhis/claude-marketplace`. Each plugin bundles skills, agents, hooks, and/or MCP server configs for a specific domain.

## Repository Layout

- `.claude-plugin/plugin.json` — top-level marketplace manifest (name: `jylhis-plugins`)
- `plugins/<name>/` — each plugin is self-contained with its own `.claude-plugin/plugin.json`
- `plugins/<name>/skills/<skill>/SKILL.md` — skill definitions (the main content type)
- `plugins/<name>/.mcp.json` — optional MCP server configuration (e.g., rust-analyzer via nix)
- `skills/` — top-level marketplace-management skills (e.g., `import-skills`)

## Current Plugins

See `.claude-plugin/marketplace.json` for the full list of plugins with descriptions, versions, and tags.

## Key Conventions

- Plugin names use kebab-case
- Each plugin directory must have `.claude-plugin/plugin.json` with `name`, `description`, and `author`
- Skills live in `plugins/<plugin>/skills/<skill-name>/SKILL.md` with YAML frontmatter
- Some skills have `references/`, `assets/`, and `evals/` subdirectories
- MCP servers use nix (`nix run nixpkgs#<pkg>`) for tool provisioning — no system-wide installs assumed
- After creating/modifying plugins, run the `plugin-dev:plugin-validator` and `plugin-dev:skill-reviewer` agents
- When adding or removing plugins, update `.claude-plugin/marketplace.json` as the source of truth

## Enabled Official Plugins

This repo uses `skill-creator`, `claude-md-management`, `commit-commands`, and `plugin-dev` from `claude-plugins-official` (configured in `.claude/settings.json`).

## Importing Skills

The `/import-skills` skill handles pulling skills from external GitHub repos. It validates licenses, creates/merges plugins, attributes sources in READMEs, and runs quality checks. See `skills/import-skills/SKILL.md`.
