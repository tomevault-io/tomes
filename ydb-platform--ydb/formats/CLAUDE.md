# ydb

> ./ya make --build relwithdebinfo <folder>

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ydb/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Project

## Build & Test

```bash
# Build
./ya make --build relwithdebinfo <folder>

# Run all tests
./ya make --build relwithdebinfo -tA <folder>

# Run specific test
./ya make --build relwithdebinfo -tA <folder> -F *test-filter*

# Run tests repeatedly (e.g. to catch flakes)
./ya make --build relwithdebinfo -tA <folder> -F *test-filter* --test-retries N
```

- Tests include build
- No `-j`
- No force rebuild
- Use `2>&1 | tail` for test output

## C++

- Use C++20 or earlier

---
> Source: [ydb-platform/ydb](https://github.com/ydb-platform/ydb) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
