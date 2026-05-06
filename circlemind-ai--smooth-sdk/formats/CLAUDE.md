# smooth-sdk

> Always use `poetry run` to execute Python commands (tests, scripts, etc.) to ensure the correct virtualenv is used.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/smooth-sdk/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agents Guide

## Running commands

Always use `poetry run` to execute Python commands (tests, scripts, etc.) to ensure the correct virtualenv is used.

```bash
# Tests
poetry run pytest tests/ -v

# Single test file
poetry run pytest tests/test_models.py -v

# Python scripts
poetry run python -c "..."
```

## Project setup

```bash
poetry env use 3.14
poetry install --extras test
```

---
> Source: [circlemind-ai/smooth-sdk](https://github.com/circlemind-ai/smooth-sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-06 -->
