---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
metadata:
  author: scaling-group
---

# Writing Skills

## Directory Structure

Put skills in `guidance/skills/`, we have linked `.agents/skills/` to this folder, so they can be loaded automatically.

```
guidance/
  skills/
    skill-name/
      SKILL.md              # Main reference (required)
      supporting-file.*     # Only if needed
```

## SKILL.md Structure

```markdown
---
name: skill-name-with-hyphens
description: "Use when [specific triggering conditions and symptoms]"
---

Other details here

```
Don't forget the quotes around `description`.

---
> Source: [scaling-group/eve](https://github.com/scaling-group/eve) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
