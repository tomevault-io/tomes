---
name: hello-world
description: Use when working with a minimal example skill. Use when demonstrating how dropmcp turns a SKILL.md folder into an MCP tool.
metadata:
  author: agoda-com
---

# Hello World

This is a starter skill. When an MCP client invokes this tool, it receives this
entire file as text, plus resource links to any supporting files in this folder.

## How skills work

1. Create a folder under your `skills/` directory.
2. Add a `SKILL.md` with YAML frontmatter (`name`, `category`, `description`).
3. Drop any supporting files (scripts, references) alongside it — they become
   `skill://hello-world/<path>` resource links.

Replace this skill with your own.

---
> Source: [agoda-com/dropmcp](https://github.com/agoda-com/dropmcp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
