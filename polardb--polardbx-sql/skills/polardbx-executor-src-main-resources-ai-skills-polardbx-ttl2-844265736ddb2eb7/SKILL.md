---
name: polardbx-ttl20
description: | Use when this capability is needed.
metadata:
  author: polardb
---

# PolarDB-X TTL 2.0 — Cold Data Archiving & Auto-Add Range Partitions

Generate correct TTL (Time-to-Live) definitions and archive table statements for PolarDB-X 2.0 Enterprise Edition (AUTO mode). This skill covers two scenarios:

1. **Cold data archiving / data expiration**: Analyzes table schemas, recommends row-based or partition-based archiving strategy, produces production-ready SQL.
2. **Auto-add Range partitions (add-only, no cleanup)**: Configures TTL mechanism to automatically pre-create future Range partitions, preventing write failures.

**Scope**: PolarDB-X 2.0 Enterprise Edition + AUTO mode database only.

## ⚠️ CRITICAL: Read the Reference Guide First

**You MUST read the relevant reference guide in full BEFORE generating any SQL:**
- TTL archiving / data expiration: [references/ttl20-user-guide.md](references/ttl20-user-guide.md)
- Auto-add Range partitions only: [references/auto-add-range-parts.md](references/auto-add-range-parts.md)

TTL syntax is unique to PolarDB-X and cannot be guessed from MySQL knowledge. Answering from memory WILL produce incorrect syntax.

## Core Workflow

### Scenario A: Cold Data Archiving / Data Expiration

1. Read [references/ttl20-user-guide.md](references/ttl20-user-guide.md) in full.
2. Gather required information from the user (table name, CREATE TABLE statement, TTL time column, retention period, whether archiving is needed).
3. Analyze table schema and determine archiving strategy (broadcast → not supported; single table → ROW only; partition-based only when Range partition on TTL column, no GSI, no MAXVALUE).
4. Generate complete SQL statements in order: TTL definition → local index (row-based only) → archive table creation → enable cleanup.

### Scenario B: Auto-Add Range Partitions (Add-Only, No Cleanup)

1. Read [references/auto-add-range-parts.md](references/auto-add-range-parts.md) in full.
2. Confirm the table uses a time-type Range partition column (`DATE`/`DATETIME`/`TIMESTAMP`). Integer-type columns are NOT supported.
3. Determine partition interval and pre-allocation count.
4. Generate `ALTER TABLE ... MODIFY TTL SET ... TTL_CLEANUP = 'OFF'` statement.
5. Always include the immediate trigger step: `ALTER TABLE ... CLEANUP EXPIRED DATA WITH TTL_CLEANUP = 'OFF';`

## TTL SQL Quick Reference

**Correct ALTER TABLE TTL syntax:**
```sql
ALTER TABLE `table_name`
MODIFY TTL
SET
TTL_ENABLE = 'ON',
TTL_CLEANUP = 'OFF',
TTL_EXPR = `time_col` EXPIRE AFTER 3 MONTH TIMEZONE '+08:00',
TTL_JOB = CRON '0 0 2 */1 * ? *' TIMEZONE '+08:00',
TTL_PART_INTERVAL = INTERVAL(1, MONTH),
ARCHIVE_TYPE = 'ROW',
ARCHIVE_TABLE_PRE_ALLOCATE = 3,
ARCHIVE_TABLE_POST_ALLOCATE = 48;
```

**TTL_EXPR by column type:**
- DATETIME/TIMESTAMP/DATE: `` TTL_EXPR = `col` EXPIRE AFTER N {DAY|MONTH|YEAR} TIMEZONE '+08:00' ``
- INT/BIGINT (Unix seconds): `` TTL_EXPR = FROM_UNIXTIME(`col`) EXPIRE AFTER N {DAY|MONTH|YEAR} TIMEZONE '+08:00' ``
- INT/BIGINT (Unix milliseconds): `` TTL_EXPR = FROM_UNIXTIME(`col`/1000) EXPIRE AFTER N {DAY|MONTH|YEAR} TIMEZONE '+08:00' ``
- INT/BIGINT (non-timestamp, monotonic): `` TTL_EXPR = `col` EXPIRE OVER M PARTITIONS ``

**ARCHIVE_TYPE values:** `'ROW'` | `'PARTITION'` | `'SUBPARTITION'` — no other values exist.

**Create archive table:**
```sql
/*+TDDL:cmd_extra(ENABLE_ASYNC_DDL=true, PURE_ASYNC_DDL_MODE=true)*/
CREATE TABLE `{table_name}_arc`
LIKE `{table_name}`
ENGINE = 'Columnar' ARCHIVE_MODE = 'TTL';
```

## Key Constraints

1. **Broadcast tables** do NOT support TTL at all. Do NOT recommend converting broadcast tables to another type solely for TTL.
2. **SINGLE tables DO support TTL** using `ARCHIVE_TYPE = 'ROW'`. Do NOT tell users TTL requires partitioned tables.
3. **Row-based archiving** requires a local index on the TTL column (single-column or composite with TTL column as first column).
4. **Partition-based archiving** requires: Range partition on TTL column + NO MAXVALUE partition + NO GSI/UGSI.
5. **TTL_CLEANUP must stay 'OFF'** until archive table creation completes — to avoid permanent deletion of data that should have been archived.
6. **LOCAL PARTITION (TTL 1.0) is DEPRECATED** — never recommend it for new tables.

## ANTI-PATTERNS — These Do NOT Exist in PolarDB-X

- ❌ `TTL = col + INTERVAL 14 DAY`
- ❌ `TTL_ACTION = ARCHIVE`, `TTL_COLUMN = 'col'`
- ❌ `TTL_CONDITION = '...'`, `TTL_JOB_INTERVAL = '...'`
- ❌ `TTL BY col INTERVAL ...`
- ❌ `TTL_ARCHIVE = true`, `TTL_ARCHIVE_TABLE = ...`, `TTL_ARCHIVE_STORAGE_POLICY = ...`, `TTL_DELETE_BATCH_SIZE = ...`
- ❌ `CREATE STORAGE POLICY ...` / `ARCHIVE COLD DATA` — these do not exist in PolarDB-X
- ❌ `LOCAL PARTITION BY RANGE ...` (TTL 1.0, deprecated)

## Version Requirements

- Row-based archiving: instance version >= `5.4.19-20240927`
- Partition-based archiving: instance version >= `5.4.20-20250328`

## Full Reference

- Cold data archiving / data expiration (complete workflow, decision tree, all examples, EXPIRE OVER, migration from TTL 1.0, management operations): [references/ttl20-user-guide.md](references/ttl20-user-guide.md)
- Auto-add Range partitions (first-level monthly/daily, second-level subpartitions, management commands): [references/auto-add-range-parts.md](references/auto-add-range-parts.md)

---
> Source: [polardb/polardbx-sql](https://github.com/polardb/polardbx-sql) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
