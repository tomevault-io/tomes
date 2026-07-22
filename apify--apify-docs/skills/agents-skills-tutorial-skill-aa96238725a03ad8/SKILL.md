---
name: tutorial
description: Create structured tutorials for Apify Academy or Platform documentation. Use when user says "create a tutorial", "write a tutorial", "build a step-by-step guide", "convert this guide into a tutorial", or "tutorial for [topic]". Handles tutorial structure, learning objectives, prerequisites, step-by-step instructions, code examples, and troubleshooting sections. Use when this capability is needed.
metadata:
  author: apify
---

# Tutorial creation

## Process

1. **Identify tutorial type** - platform tutorial, academy tutorial, or integration tutorial
2. **Research** - read related docs, check existing tutorials for style reference
3. **Create front matter** - title (sentence case), description (140-160 chars), sidebar_position, slug
4. **Write 8-section structure**:
   1. Introduction with learning objectives
   2. Prerequisites (tools, accounts, knowledge)
   3. Step-by-step instructions (numbered, action verbs)
   4. Code examples (complete, runnable, tested)
   5. Testing and verification (expected results)
   6. Troubleshooting (common issues + fixes)
   7. Summary (what was learned)
   8. Next steps (links to related content)
5. **Quality check** - run `pnpm lint:md` and `vale` before finishing

Each step should have a clear action verb, expected result, and verification. Code examples must be complete - no pseudocode.

For the detailed 8-section template, see `.agents/skills/tutorial/references/tutorial-template.md`.
For edge cases and process notes, see `.agents/skills/tutorial/references/process.md`.

---
> Source: [apify/apify-docs](https://github.com/apify/apify-docs) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-12 -->
