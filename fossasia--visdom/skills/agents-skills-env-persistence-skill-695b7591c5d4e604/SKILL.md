---
name: env-persistence
description: Safely modify environment serialization, reload data, and view layout persistence. Use when changing env save/load formats or storage behavior. Use when this capability is needed.
metadata:
  author: fossasia
---

# Skill: Environment Persistence

## When to Use

Use this skill for persistence format changes and env reload/view layout behavior.

## Core Workflow

1. Map data writes/reads for `jsons` and `reload` structures.
2. Apply changes in server utility/handler paths that serialize or restore env state.
3. Keep backward compatibility with existing env JSON files.
4. Preserve view/layout behavior and environment tree organization.
5. Validate save/fork/delete and restart/reload workflows end-to-end.

## Guardrails

- Do not introduce breaking env format changes without migration handling.
- Keep env path handling sanitized and scoped.
- Preserve compare and standard env behaviors.

## Documentation

- [Skill reference](references/REFERENCE.md)
- `py/visdom/utils/server_utils.py`
- `py/visdom/server/handlers/web_handlers.py`
- `py/visdom/server/app.py`
- `AGENTS.md`
- `CONTRIBUTING.md`

## Assets

- See `assets/README.md` and store templates/resources in `assets/`.

## Tests

- Follow the default flow in `references/TESTS.md`.

---
> Source: [fossasia/visdom](https://github.com/fossasia/visdom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
