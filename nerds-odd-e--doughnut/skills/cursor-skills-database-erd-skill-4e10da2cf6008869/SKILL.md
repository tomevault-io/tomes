---
name: database-erd
description: >- Use when this capability is needed.
metadata:
  author: nerds-odd-e
---

# Database ERD export

`docs/database-erd.md` is generated from the live MySQL catalog (foreign keys and PK/UK/FK columns). **Do not hand-edit the Mermaid block**; re-run the exporter after schema changes.

## When to run

- A new or changed Flyway migration alters tables, columns, or constraints
- You need the ERD to match the current migrated schema

## Steps

1. Ensure MySQL is reachable on **127.0.0.1:3309** with user **`doughnut`** (local dev defaults from `scripts/shell_setup.sh` / `process-compose`).

2. Ensure at least one migrated schema exists (Flyway has run). The script picks, in order: **`doughnut_development`**, then **`doughnut_test`**, then **`doughnut_e2e_test`**, unless **`DOUGHNUT_ERD_SCHEMA`** is set to a specific catalog.

3. From the repo root:

```bash
CURSOR_DEV=true nix develop -c python3 scripts/export_database_erd.py
```

Or:

```bash
CURSOR_DEV=true nix develop -c pnpm export:database-erd
```

4. Commit the updated `docs/database-erd.md` with the migration (or immediately after).

## Overrides (optional)

| Variable | Default |
|----------|---------|
| `DOUGHNUT_ERD_SCHEMA` | (auto: development → test → e2e) |
| `DOUGHNUT_ERD_MYSQL_HOST` | `127.0.0.1` |
| `DOUGHNUT_ERD_MYSQL_PORT` | `3309` |
| `DOUGHNUT_ERD_MYSQL_USER` | `doughnut` |
| `DOUGHNUT_ERD_MYSQL_PASSWORD` | `doughnut` |

## Implementation

- Script: `scripts/export_database_erd.py`
- Output: `docs/database-erd.md`
- Omits **`flyway_schema_history`** from the diagram

---
> Source: [nerds-odd-e/doughnut](https://github.com/nerds-odd-e/doughnut) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
