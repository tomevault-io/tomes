---
name: ha-code-quality
description: >- Use when this capability is needed.
metadata:
  author: FutureTense
---

# Code Quality & Standards Guide for Keymaster

This skill guides linting, formatting, and static typing enforcement across the
repository.

## Automated Quality Suite (Tox)

Run the full CI lint environment:

```bash
tox -e lint
```

This runs Ruff linting, Ruff formatting check, MyPy across the entire repo
(`mypy .`), and Codespell.

## Individual Quality Tools

Configuration is defined in `pyproject.toml`.

### Ruff Formatting & Linting

```bash
# Check linting errors
ruff check .

# Automatically apply safe fixes
ruff check --fix .

# Format code
ruff format .
```

### Type Checking (MyPy)

```bash
# Check both custom_components and tests
mypy .
```

### Spell Checking (Codespell)

```bash
codespell custom_components/keymaster tests
```

## TypeScript / Frontend Linting

```bash
# Check ESLint
yarn lint

# Fix ESLint issues
yarn lint:fix
```

## Pre-commit / Prek Hooks

Run pre-commit checks locally before committing:

```bash
# Using prek (fast drop-in runner):
prek run --all-files

# Or using pre-commit:
pre-commit run --all-files
```

## Guidelines

- **Python Target**: Configured for Python 3.14 (`target-version = "py314"`).
  Use modern typing syntax (e.g. `list[str]`, `X | Y`,
  `from __future__ import annotations`).
- **Line Length**: Strictly adhere to the **100-character line limit** configured
  in `pyproject.toml`.
- **Async Hygiene**: Use `async_create_task` or HA core async helpers; avoid
  blocking synchronous calls in the event loop.
- **Docstrings & Comments**: Preserve existing docstrings and write clear
  docstrings for new public methods and classes.

---
> Source: [FutureTense/keymaster](https://github.com/FutureTense/keymaster) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
