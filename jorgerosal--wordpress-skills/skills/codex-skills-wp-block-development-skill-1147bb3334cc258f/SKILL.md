---
name: wp-block-development
description: WordPress block editor review for Codex. Use when reviewing block.json, editor components, save and render patterns, attributes, InnerBlocks, deprecations, build setup, or the Interactivity API in Gutenberg blocks. Use when this capability is needed.
metadata:
  author: jorgerosal
---

# Codex WordPress Block Development Review

## Purpose

Use this skill when Codex should review WordPress block code across both PHP and JavaScript or JSX, with special attention to `block.json`, editor behavior, rendering, and block lifecycle correctness.

## Focus Areas

- `block.json` schema and registration fields
- `edit` and `save` implementation quality
- Render callbacks and render files
- Attribute schemas, deprecations, and validation issues
- `InnerBlocks`, `useBlockProps`, and editor component patterns
- Interactivity API and source/build workflow concerns

## Workflow

1. Identify whether the code is a single block, block library, theme block, or mixed plugin.
2. Validate `block.json` and registration flow first.
3. Review `edit`, `save`, and dynamic rendering behavior.
4. Check for block-specific risks such as nondeterministic save output, deprecated patterns, and broken `InnerBlocks` handling.
5. Pull only the needed shared reference docs before finalizing findings.

## Reference Files

Load only the references you need from:

- `../../claude-skills/wp-block-development/references/block-json-guide.md`
- `../../claude-skills/wp-block-development/references/editor-patterns.md`
- `../../claude-skills/wp-block-development/references/dynamic-blocks-guide.md`
- `../../claude-skills/wp-block-development/references/interactivity-api-guide.md`

## Output

- Include both PHP and JS or JSX file references where relevant
- Group findings by severity
- Explain block-editor impact, frontend impact, or validation impact
- Suggest fixes that align with current Gutenberg patterns

---
> Source: [jorgerosal/wordpress-skills](https://github.com/jorgerosal/wordpress-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
