---
name: clean-up-docs-push
description: Code cleanup, docs update, and git push workflow Use when this capability is needed.
metadata:
  author: leshchenko1979
---

## Workflow

1. **Code Cleanup** (use `code-cleanup-specialist` subagent):
   - Run linter checks on modified files
   - Fix any code quality issues
   - Run test suite to verify everything passes

2. **Update Docs**:
   - Update `README.md` - add new features to Features table and update tool descriptions
   - Update `docs/` folder - check all relevant files and update with new features

3. **Git Push**:
   - Create descriptive commit
    - Push to remote

---
> Source: [leshchenko1979/fast-mcp-telegram](https://github.com/leshchenko1979/fast-mcp-telegram) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-30 -->
