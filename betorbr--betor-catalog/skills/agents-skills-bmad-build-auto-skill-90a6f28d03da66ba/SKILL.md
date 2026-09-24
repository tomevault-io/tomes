---
name: bmad-build-auto
description: One iteration of an unattended development loop. Use when invoked by name Use when this capability is needed.
metadata:
  author: betorbr
---

Run the following command exactly once without changing the current working directory. Replace `{project-root}` with the absolute path to the project root and `{skill-root}` with the absolute path to this skill's directory:

```bash
uv run --no-cache "{project-root}/_bmad/scripts/render_skill.py" --project-root "{project-root}" --skill "{skill-root}"
```

- On success, read and follow the one absolute `workflow.md` instruction printed to stdout.
- On failure (including `uv` being unavailable), report the command output and HALT. Do not run any workflow source directly.

---
> Source: [betorbr/betor-catalog](https://github.com/betorbr/betor-catalog) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
