---
name: wp-accessibility-review
description: WordPress accessibility review for Codex. Use when reviewing semantic HTML, keyboard access, focus behavior, form labels, ARIA usage, and accessible interaction patterns in themes, blocks, plugins, and admin screens. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress Accessibility Review

## Purpose

Use this skill when Codex should review WordPress UI implementation for accessibility issues in structure, interaction, and assistive-technology support.

## Focus Areas

- Semantic markup
- Keyboard accessibility
- Focus management
- Forms and labels
- Modals, tabs, accordions, and admin interactions

## Workflow

1. Identify whether the surface is frontend, block output, or admin UI.
2. Check structural semantics and keyboard access first.
3. Review focus behavior, forms, and ARIA usage.
4. Load only the needed shared references from `../../claude-skills/wp-accessibility-review/references/`.
5. Report findings with severity, file references, and practical fixes.

## References

- `../../claude-skills/wp-accessibility-review/references/semantic-and-form-patterns.md`
- `../../claude-skills/wp-accessibility-review/references/interactive-a11y-patterns.md`

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
