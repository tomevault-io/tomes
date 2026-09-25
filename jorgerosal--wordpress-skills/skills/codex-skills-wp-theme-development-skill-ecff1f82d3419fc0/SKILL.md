---
name: wp-theme-development
description: WordPress theme review for Codex. Use when reviewing block themes, classic themes, or hybrid themes for theme.json structure, templates, template parts, style variations, global styles, and FSE patterns. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress Theme Development Review

## Purpose

Use this skill when Codex needs to review WordPress theme code, especially `theme.json`, template structure, Full Site Editing patterns, and classic-to-block migration concerns.

## Focus Areas

- Theme type detection: block, classic, hybrid, or child theme
- `theme.json` structure and versioning
- Template hierarchy and required files
- Template parts, block markup, and pattern registration
- Global styles, spacing systems, and style variations
- Migration or compatibility issues between classic and block approaches

## Workflow

1. Detect the theme type and review context first.
2. Validate `theme.json`, required files, and template structure.
3. Check template parts, patterns, style variations, and global style choices.
4. Use shared reference docs for deeper checks only where needed.
5. Report findings with severity, file references, and theme-specific remediation guidance.

## Reference Files

Load only the references you need from:

- `../../claude-skills/wp-theme-development/references/theme-json-guide.md`
- `../../claude-skills/wp-theme-development/references/template-patterns.md`
- `../../claude-skills/wp-theme-development/references/fse-guide.md`
- `../../claude-skills/wp-theme-development/references/classic-to-block-guide.md`

## Output

- Group findings by severity
- Include file references across PHP, HTML, and JSON files
- Explain whether the issue affects block themes, classic themes, or both
- Suggest fixes that match current WordPress theme conventions

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
