---
name: animate-css-skill
description: | Use when this capability is needed.
metadata:
  author: COPPSARY
---

# animate-css-skill

> Catalogue stub — full package: [msrbuilds/animate-css-skill](https://github.com/msrbuilds/animate-css-skill)

## Decision tree

1. **Is the package already installed?**
   Check: your agent's skills directory contains `animate-css-skill` with content beyond this stub.
   - Yes → invoke `animate-css-skill` and proceed
   - No → go to step 2

2. **Which agent are you on?**
   - Claude Code → `npx skills add msrbuilds/animate-css-skill` — or send `! npx skills add …` as a chat message (add `-g` for global, omit for project-only)
   - Cursor → `npx skills add msrbuilds/animate-css-skill`
   - Other → `npx skills add msrbuilds/animate-css-skill` or see [GitHub README](https://github.com/msrbuilds/animate-css-skill)

## Install command

```bash
npx skills add msrbuilds/animate-css-skill
```

## Invoke after install

- Skill name: `animate-css-skill`
- Trigger phrases: "Animate.css", "CSS animation library", "bounce animation", "fadeIn", "animate-css"

## What it does

Applies Animate.css v4.1.1 animations across HTML, React/JSX components, and WordPress PHP templates. Covers the full Animate.css class catalogue (attention seekers, bouncing, fading, flipping, rotating, sliding, zooming, specials) with correct CDN or npm setup. Adds scroll-triggered reveals using the Intersection Observer API, RTL-aware directional flipping for right-to-left layouts, and `prefers-reduced-motion` compliance to respect user accessibility preferences.

## When NOT to use

- Custom keyframe animations built from scratch (use `css-animation-skill`)
- Interactive gesture-driven animations requiring JavaScript state (use `framer-motion-skills`)

---
> Source: [COPPSARY/Motionly](https://github.com/COPPSARY/Motionly) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
