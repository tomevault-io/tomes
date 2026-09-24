---
name: skillforge
description: Create a reusable project skill after checking existing capabilities and conventions. Use when this capability is needed.
metadata:
  author: codejunkie99
---

# Skillforge — the skill that creates skills

When a new capability is needed:

1. **Check for duplicates.** Read `skills/_index.md`. If a similar skill exists,
   extend it instead of creating a new one.
2. **Check memory.** Read `memory/semantic/LESSONS.md` for related patterns.
3. **Draft the skill.** Create `skills/<name>/SKILL.md` with:
   - YAML frontmatter (name, version, triggers, tools, preconditions, constraints)
   - Plain-language instructions (destinations and fences, not driving directions)
   - A self-rewrite hook at the bottom
4. **Register it.** Add an entry to `skills/_index.md` and append a JSON line
   to `skills/_manifest.jsonl`.
5. **Log it.** Append a record to `memory/semantic/DECISIONS.md` explaining
   why this skill was created.

## What good skills look like
- State the destination ("verify tests pass before commit"), not the exact
  command sequence.
- Include 2–3 examples of correct behavior when it clarifies intent.
- Include 1 example of a failure and what was learned from it.
- Keep the whole file under 100 lines.

## Self-rewrite hook
After every 5 skills created, or on any failed creation:
1. Read the last 5 skillforge entries from episodic memory.
2. If better trigger patterns or constraint structures have emerged,
   update this file and the template it implies.
3. Commit: `skill-update: skillforge, <one-line reason>`.

---
> Source: [codejunkie99/agentic-stack-desktop](https://github.com/codejunkie99/agentic-stack-desktop) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
