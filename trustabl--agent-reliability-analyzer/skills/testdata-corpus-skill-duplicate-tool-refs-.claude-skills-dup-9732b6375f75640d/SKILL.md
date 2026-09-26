---
name: dup-skill
description: Use when working with a skill with duplicate tool references, used for reading a file the user names.
metadata:
  author: trustabl
---

# Dup Skill (synthetic test fixture)

Reads a file the user names. This is a synthetic Trustabl test fixture with
no dynamic execution, no external references, and no side-effecting tools —
it exists solely to exercise CSKILL-061 (duplicate allowed-tools entries) in
isolation. If the read fails, it stops and reports the failure rather than
guessing.

---
> Source: [trustabl/agent-reliability-analyzer](https://github.com/trustabl/agent-reliability-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
