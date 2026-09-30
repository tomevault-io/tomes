---
name: finreport-helper
description: Use when working with the body is harmless. The frontmatter violates the agentskills.io spec in two
metadata:
  author: maoyadongsh
---

# Frontmatter mismatch fixture

The body is harmless. The frontmatter violates the agentskills.io spec in two
ways: the name uses uppercase and underscores and does not match the directory
name, and the description is empty. Admission must fail closed on spec
violations even though no threat pattern is present.

---
> Source: [maoyadongsh/siq-agent-security](https://github.com/maoyadongsh/siq-agent-security) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
