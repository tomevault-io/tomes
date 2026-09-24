---
name: enpire
description: Inspect, test, and extend ENPIRE robot tools, tasks, calibration, and PLD workflows. Use when this capability is needed.
metadata:
  author: NVlabs
---

# ENPIRE repository workflow

1. Read `AGENTS.md` and `enpire/env/docs/source_provenance.yaml`.
2. Read `enpire/env/docs/REAL_WORLD_WORKFLOWS.md` and
   `enpire/env/docs/DEPENDENCIES.md` for real tasks.
3. Run `uv run enpire tools list` to inspect optional capability bundles.
4. Add characterization tests before changing migrated Forge behavior.
5. Run the narrow unit test, then `uv run pytest -q tests/enpire`.
6. Run `uv run ruff check enpire tests/enpire`.
7. Do not run real motion or credentialed network tests without explicit user authorization.

Use only external environment credentials. Never write or print them.

---
> Source: [NVlabs/ENPIRE](https://github.com/NVlabs/ENPIRE) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
