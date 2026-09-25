---
name: wp-wpcli-and-ops
description: WordPress WP-CLI and operations review for Codex. Use when reviewing custom CLI commands, search-replace plans, multisite operations, maintenance scripts, cron or cache workflows, or deployment-time WordPress operations. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress WP-CLI and Ops Review

## Purpose

Use this skill when Codex should review WordPress operational workflows built around WP-CLI, including custom commands, multisite tasks, search-replace plans, and maintenance scripts.

## Focus Areas

- Custom `WP_CLI::add_command()` quality
- Search-replace and DB safety
- Multisite targeting and `--url` / `--network` scope
- Automation reliability, batching, and logging

## Workflow

1. Identify command implementations and operational docs.
2. Check destructive scope and targeting first.
3. Review validation, dry-run support, and rollback thinking.
4. Load only the needed shared references from `../../claude-skills/wp-wpcli-and-ops/references/`.
5. Report findings with severity, file references, impact, and safer patterns.

## References

- `../../claude-skills/wp-wpcli-and-ops/references/command-patterns.md`
- `../../claude-skills/wp-wpcli-and-ops/references/multisite-and-search-replace.md`
- `../../claude-skills/wp-wpcli-and-ops/references/automation-and-safety.md`

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
