# ppt-design-skill

> Use the `ppt-design-skill` workflow for presentation design tasks. The

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ppt-design-skill/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# PPT Design Skill

Use the `ppt-design-skill` workflow for presentation design tasks. The
published `pptx-designer` Python library creates the editable PPTX; this
repository owns the design process, installation, rendering, and PNG review.

Before changing the skill, read:

- `skill/SKILL.md`
- `skill/references/design-principles.md`
- `skill/references/qa-and-delivery.md`
- `docs/README.md`

The final acceptance gate is PPTX -> PDF -> PNG followed by direct LLM review
of the rendered PNGs. Keep the skill name `ppt-design-skill` in all metadata
and installer paths.

---
> Source: [sunchaokun/PPT-Design-Skill](https://github.com/sunchaokun/PPT-Design-Skill) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-13 -->
