---
name: idempotent-script-design
description: Use this skill when writing scripts, cron jobs, data pipelines, or any automated process that may be run multiple times. Design every operation to be safely re-runnable without side effects.
metadata:
  author: aiming-lab
---

# Idempotent Script Design

An idempotent operation produces the same result whether run once or ten times.

**Techniques:**
- **Check before create:** `CREATE TABLE IF NOT EXISTS`, `mkdir -p`, check file existence before writing.
- **Upsert instead of insert:** Use `INSERT ... ON CONFLICT DO UPDATE` in SQL.
- **Atomic writes:** Write to a temp file, then rename — prevents corrupt partial output.
- **Track progress:** Write a completion marker or checkpoint so reruns skip done work.

**Testing idempotency:** Run your script twice on the same input and verify the output is identical.

**Anti-patterns:**
- Appending to a file without checking if the data is already there.
- Inserting rows without checking for duplicates.

---
> Source: [aiming-lab/ClawArena](https://github.com/aiming-lab/ClawArena) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
