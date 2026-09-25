---
name: wp-plugin-development
description: WordPress plugin architecture review for Codex. Use when reviewing plugin structure, lifecycle hooks, Settings API usage, CPT and taxonomy registration, hook design, i18n, and WordPress.org readiness. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress Plugin Development Review

## Purpose

Use this skill when Codex needs to review the architecture and standards of a WordPress plugin rather than only its security or performance characteristics.

## Focus Areas

- Main plugin file and header quality
- Activation, deactivation, and uninstall flows
- Namespacing, prefixing, and collision avoidance
- Settings API, CPT, taxonomy, and REST registrations
- Hook placement, plugin structure, and i18n
- WordPress.org and Plugin Check readiness

## Workflow

1. Detect the plugin context: WordPress.org, private plugin, mu-plugin, or drop-in.
2. Review the main bootstrap file, structure, and lifecycle hooks first.
3. Check CPTs, taxonomies, settings, REST routes, and i18n patterns.
4. Use shared reference docs only where deeper detail is needed.
5. Report findings with severity, file references, architectural impact, and suggested fixes.

## Reference Files

Load only the references you need from:

- `../../claude-skills/wp-plugin-development/references/architecture-patterns.md`
- `../../claude-skills/wp-plugin-development/references/api-patterns.md`
- `../../claude-skills/wp-plugin-development/references/hooks-guide.md`
- `../../claude-skills/wp-plugin-development/references/oop-patterns.md`

## Output

- Group findings by severity
- Include file references and plugin-context notes where relevant
- Distinguish review blockers from modernization suggestions
- Suggest fixes that fit common WordPress plugin conventions

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
