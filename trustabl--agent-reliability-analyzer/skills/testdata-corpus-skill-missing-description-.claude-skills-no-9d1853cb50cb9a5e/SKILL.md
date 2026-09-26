---
name: no-desc-skill
description: This is a synthetic Trustabl test fixture used to exercise the Use when this capability is needed.
metadata:
  author: trustabl
---

# No Description Skill (synthetic test fixture)

This is a synthetic Trustabl test fixture used to exercise the
skill_has_description predicate. It intentionally omits the `description:`
frontmatter field. It is otherwise clean: no dynamic-context execution, no
external URLs, no bundled scripts, and no prompt-injection markers, so
CSKILL-070 is the only skill-scope rule expected to fire — except CSKILL-085
(missing purpose language), which also legitimately fires here since the
omitted description carries no purpose phrase either. If a read fails, it
stops and reports the failure rather than guessing.

---
> Source: [trustabl/agent-reliability-analyzer](https://github.com/trustabl/agent-reliability-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
