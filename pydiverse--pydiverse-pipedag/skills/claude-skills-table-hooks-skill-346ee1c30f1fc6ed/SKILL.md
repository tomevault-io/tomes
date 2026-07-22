---
name: table-hooks
description: > Use when this capability is needed.
metadata:
  author: pydiverse
---

# Table Hooks

Each data framework (pandas, polars, SQLAlchemy, ibis, pydiverse.transform) has a table hook registered on the store via `@Store.register_table()`. Hooks implement `materialize()` and `retrieve()`.

## ParquetTableStore hook overrides

The ParquetTableStore overrides hooks to write/read parquet files instead of SQL tables. Key hooks:
- `PandasTableHook` — uses PyArrow for parquet I/O
- `PolarsTableHook` — uses native polars parquet I/O with PyArrow fallback (GCS credential issues)
- `SQLAlchemyTableHook` — uses DuckDB `COPY ... TO` for parquet export
- `_ParquetPyArrowMixin` — shared PyArrow-based reading logic for view resolution

## View resolution

Views (`View` objects) support source unions, column renaming, sorting, and limits. The `_resolve_view_paths()` method resolves a table's view chain to actual parquet file paths for reading.

---
> Source: [pydiverse/pydiverse.pipedag](https://github.com/pydiverse/pydiverse.pipedag) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
