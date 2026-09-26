---
name: copywriting-skill
description: | Use when this capability is needed.
metadata:
  author: COPPSARY
---

# copywriting-skill

> Catalogue stub — full skill: [judicael-s/Copywriting-skill](https://github.com/judicael-s/Copywriting-skill)

## Decision tree

1. **Is the full skill already installed?**
   - Global: `grep -q "^das:" ~/.agents/skills/copywriting-skill/SKILL.md 2>/dev/null && echo "pointer" || echo "installed"`
   - Project: `grep -q "^das:" .agents/skills/copywriting-skill/SKILL.md 2>/dev/null && echo "pointer" || echo "installed"`
   - No `das:` block → full skill installed, invoke and proceed
   - `das:` block present → go to step 2

2. **Detect scope, then install:**

   ```bash
   [ -e ~/.agents/skills/copywriting-skill ] && echo "global" || echo "project"
   ```

   **Global:**
   ```bash
   npx skills add judicael-s/copywriting-skill --skill copywriting-skill -g -y
   ```

   **Project:**
   ```bash
   npx skills add judicael-s/copywriting-skill --skill copywriting-skill -y
   ```
   > **Claude Code:** send either command as a chat message starting with `!` to run it without leaving the conversation.

## Invoke after install

5 skills available:

| Skill | Triggers |
|---|---|
| `copywriting-skill` | "copywriting", "landing page copy", "web copy", "headline copy" |
| `seo-copywriting` | "SEO copy", "search-optimized content" |
| `social-copywriting` | "LinkedIn post", "X post", "social copy" |
| `french-copywriting` | "French copy", "French landing page" |
| `tone-of-voice` | "tone of voice", "brand voice guide" |

## What it does

Persuasion-driven copy toolkit grounded in proven frameworks (AIDA, PAS, FAB). Covers the full product marketing stack:

- **Landing pages** — hero copy, value prop, social proof, objection handling, CTA
- **Feature pages** — outcome-first framing, benefit vs. feature discipline
- **Pricing pages** — anchoring, tier naming, CTA per plan
- **Email sequences** — subject lines, preview text, body, single CTA
- **Headlines** — formula library (curiosity, specificity, transformation)
- **Anti-AI layer** — detects and removes AI writing tells before delivery

## When NOT to use

- Short UI labels and error messages — use `ux-writing-skill`
- Conversion rate optimization of existing flows — use `coreyhaines-marketing`
- Auditing existing copy for AI patterns — use `humanize-text`

---
> Source: [COPPSARY/Motionly](https://github.com/COPPSARY/Motionly) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
