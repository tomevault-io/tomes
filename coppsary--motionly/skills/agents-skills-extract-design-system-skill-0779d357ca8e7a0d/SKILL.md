---
name: extract-design-system
description: | Use when this capability is needed.
metadata:
  author: COPPSARY
---

# extract-design-system

> Catalogue stub — full package: [arvindrk/extract-design-system](https://github.com/arvindrk/extract-design-system)

## Decision tree

1. **Is the skill already installed?** Check `~/.design-agent-skills/skills/` for `extract-design-system` or related directories.
   - Yes → invoke and proceed
   - No → go to step 2

2. **Shell access?** Yes → install below. No → show user the command (Claude Code: send with `!` as a chat message — add `-g` for global or omit for project-only).

## Install command

```bash
npx skills add arvindrk/extract-design-system
```

## Invoke after install

- Skill name: `extract-design-system`
- Triggers: "extract design system", "reverse-engineer tokens", "extract tokens from website"

## What it does

Reverse-engineers a design system from any publicly accessible website. Scrapes and analyzes CSS to extract color palettes, typography scales, spacing systems, border radii, and box shadows, then outputs a `tokens.json` (W3C-compatible) and `tokens.css` (CSS custom properties) ready for local use. Also available as a standalone CLI tool for scripted extraction pipelines.

## When NOT to use

- Figma-source token extraction — use the Figma MCP (`figma-official-skills`) or `figma-variables-tokens-generator`
- Stitch/DESIGN.md output format — use `extract-design-md` (taste-design-stitch)
- Building a token architecture from scratch — use `design-tokens-skill`

---
> Source: [COPPSARY/Motionly](https://github.com/COPPSARY/Motionly) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
