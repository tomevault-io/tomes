---
name: extract-design-md
description: | Use when this capability is needed.
metadata:
  author: COPPSARY
---

# extract-design-md

> Catalogue stub — full skill: [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills/blob/main/plugins/stitch-design/skills/extract-design-md/SKILL.md)

## Decision tree

1. **Is the full skill already installed?**
   Check whether the skill at this location still has a `das:` block:
   - Global: `grep -q "^das:" ~/.agents/skills/extract-design-md/SKILL.md 2>/dev/null && echo "pointer" || echo "installed"`
   - Project: `grep -q "^das:" .agents/skills/extract-design-md/SKILL.md 2>/dev/null && echo "pointer" || echo "installed"`
   - No `das:` block → full skill installed, invoke it and proceed
   - `das:` block present → go to step 2

2. **Detect scope, then install:**

   To detect scope:
   ```bash
   [ -e ~/.agents/skills/extract-design-md ] && echo "global" || echo "project"
   ```

   **Global** (installed with `-g`):
   ```bash
   npx skills add google-labs-code/stitch-skills --skill extract-design-md -g -y
   ```

   **Project** (installed without `-g`):
   ```bash
   npx skills add google-labs-code/stitch-skills --skill extract-design-md -y
   ```
   > **Claude Code:** send either command as a chat message starting with `!` to run it without leaving the conversation.


## Invoke after install

- Skill name: `extract-design-md`
- Trigger phrases: "extract design md", "stitch to DESIGN.md", "DESIGN.md"

## What it does

Extracts design specifications from Google Stitch output into a structured `DESIGN.md` file — the Google Stitch-compatible format for encoding visual design decisions. The resulting file can be version-controlled, shared across agents, and used to maintain design consistency across iterations. Part of Google Labs' official Stitch skills.

---
> Source: [COPPSARY/Motionly](https://github.com/COPPSARY/Motionly) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
