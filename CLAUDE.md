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

- **rust-dev** — 29 Rust skills + rust-analyzer LSP via nix (`.mcp.json`)
- **golang-dev** — 36 Go skills (concurrency, patterns, security, troubleshooting, etc.)
- **cpp-dev** — C++ development skills (scaffold)
- **python-dev** — Python development skills (scaffold)
- **nix-dev** — Nix/NixOS development skills (scaffold)
- **productivity** — 1 skill for session management and workflows
- **skill-creator** — 1 skill for creating and improving skills

## Key Conventions

- Plugin names use kebab-case
- Each plugin directory must have `.claude-plugin/plugin.json` with `name`, `description`, and `author`
- Skills live in `plugins/<plugin>/skills/<skill-name>/SKILL.md` with YAML frontmatter
- Some skills have `references/`, `assets/`, and `evals/` subdirectories
- MCP servers use nix (`nix run nixpkgs#<pkg>`) for tool provisioning — no system-wide installs assumed
- After creating/modifying plugins, run the `plugin-dev:plugin-validator` and `plugin-dev:skill-reviewer` agents

## Enabled Official Plugins

This repo uses `skill-creator`, `claude-md-management`, `commit-commands`, and `plugin-dev` from `claude-plugins-official` (configured in `.claude/settings.json`).

## Importing Skills

The `/import-skills` skill handles pulling skills from external GitHub repos. It validates licenses, creates/merges plugins, attributes sources in READMEs, and runs quality checks. See `skills/import-skills/SKILL.md`.
