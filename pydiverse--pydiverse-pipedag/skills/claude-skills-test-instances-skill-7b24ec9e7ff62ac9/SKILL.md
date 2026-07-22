---
name: test-instances
description: > Use when this capability is needed.
metadata:
  author: pydiverse
---

# Test Instances

## Instance definitions

Test instances are defined in `tests/fixtures/instances.py`. The `@with_instances()` decorator parametrizes tests across backends. Instance names map to pytest markers via `INSTANCE_MARKS`. Sub-backends are defined in `conftest.py:sub_backends`:
- `duckdb` includes `parquet_backend`
- `s3` includes `parquet_s3_backend`
- `ibm_db2` includes `parquet_s3_backend_db2`

## Pytest flags

Backend selection (opt-in unless in `default_options`):
- `--s3`, `--postgres`, `--duckdb`, `--mssql`, `--ibm_db2`, `--snowflake`
- `--ibis`, `--pdtransform`, `--polars`, `--dask`, `--prefect`
- `--no-postgres`, `--no-duckdb`, `--no-lock_tests` (disable defaults)

Default-enabled: `postgres`, `duckdb`, `polars`, `lock_tests`.

## CI matrix (from `.github/workflows/tests.yml`)

| Job | Flags |
|---|---|
| smoke_test | (defaults) |
| postgres_test | `--ibis --pdtransform --no-duckdb` |
| duckdb_test | `--ibis --pdtransform --no-postgres --no-lock_tests` |
| s3_test | `--s3 --ibis --pdtransform --no-duckdb --no-postgres --no-lock_tests` |
| mssql_test | `--mssql -m mssql --ibis --pdtransform --no-postgres --no-duckdb` |
| db2_test | `--ibm_db2 -m ibm_db2 --pdtransform --no-postgres --no-duckdb` |

---
> Source: [pydiverse/pydiverse.pipedag](https://github.com/pydiverse/pydiverse.pipedag) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
