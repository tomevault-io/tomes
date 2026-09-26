---
name: bound-skill
description: Use when working with a skill bound to one specific agent, used for reading files that agent points it at.
metadata:
  author: trustabl
---

# Bound Skill (synthetic test fixture)

This is a synthetic Trustabl test fixture used to exercise the
skill_is_agent_specific predicate. It is intentionally coupled to a
specific agent via the `agent:` frontmatter field and is not meant to be
reused across agents. It only reads files the user points it at — no
dynamic-context execution, no external URLs, no bundled scripts, and no
prompt-injection markers, so CSKILL-071 is the only skill-scope rule
expected to fire. If a read fails, it stops and reports the failure rather
than guessing.

---
> Source: [trustabl/agent-reliability-analyzer](https://github.com/trustabl/agent-reliability-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
