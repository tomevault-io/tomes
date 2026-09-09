---
name: python-linter
description: Lint and format Python files using ruff. Activates automatically when Python files are touched. Use to check code quality and fix style issues. Use when this capability is needed.
metadata:
  author: EchoYue-lp
---

## Python Linter

You have access to a Python linting script. When the user works with `.py` files:

1. Run the linter to check for issues
2. Report findings grouped by severity
3. Suggest auto-fixes where available

### Quick Check

Python available: !`python3 --version 2>&1 || echo "not installed"`

### Usage

```
run_skill_script("python-linter", "scripts/lint.sh", "<file_or_directory>")
```

The script outputs JSON with lint results grouped by file.

---
> Source: [EchoYue-lp/echo-agent](https://github.com/EchoYue-lp/echo-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
