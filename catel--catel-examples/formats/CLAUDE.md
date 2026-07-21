# catel-examples

> Catel (https://github.com/catel/catel) is an application development platform with the focus on MVVM (WPF). The goal of Catel is to provide a complete set of modular functionality for Line of Business applications written in any .NET technology, from client to server.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/catel-examples/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Catel.Examples

Catel (https://github.com/catel/catel) is an application development platform with the focus on MVVM (WPF). The goal of Catel is to provide a complete set of modular functionality for Line of Business applications written in any .NET technology, from client to server.

Catel.Examples provides example applications written specifically for Catel.

---

## Critical Rules (Read First)

These rules are **non-negotiable**. Violating them causes broken builds, crashes, or downstream breakage.

### 1. Branch Protection (COMPLIANCE REQUIRED)

**Direct commits to protected branches are a policy violation.**

| Protected Branches |
|-------------------|
| `master` |
| `develop` |

**Required workflow:**

1. **Create a feature branch FIRST** — Use naming convention: `feature/issue-NNNN-description`
2. **Make all commits on the feature branch** — Never commit directly to protected branches
3. **Submit a Pull Request** — Changes must be reviewed by a human before merging

```bash
# CORRECT — Always create a feature branch first
git checkout -b feature/issue-1234-fix-description

# NEVER DO THIS — Policy violation
git checkout develop && git commit  # FORBIDDEN

# NEVER DO THIS — Policy violation
git checkout master && git commit  # FORBIDDEN
```

The repository has protected branches that must be respected.

---

## Commands

Single source of truth for all commands:

| Task | Command |
|------|---------|
| **Build** | `dotnet cake --target=build` |
| **Test** | `dotnet cake --target=test` |
| **Build and test** | `dotnet cake --target=buildandtest` |

---

## Architecture & Directories

### Layer Overview

```
Catel.Examples => Source code for the example applications
```

### Directory Guide

| Directory | Editable? | Notes |
|-----------|-----------|-------|
| `*.generated.cs` | No | Leave as-is |
| `*.generated.xaml` | No | Leave as-is |
| `deployment` | No | Deployment / build scripts |
| `doc/dev/` | Yes | Architecture guides |
| `doc/docfx/releases/` | Yes | Website release notes (template-formatted) |
| `doc/docfx/releases/TEMPLATE.md` | Yes | Template for AI formatting |

---

## Writing Code

### Anti-Patterns (Never Do This)

| Anti-Pattern | Why |
|-------------|-----|
| Manual edits to `*.generated.cs`, `*.generated.xaml` | Overwritten on regenerate |

---

### Debugging Methodology

1. **Establish baseline** — What's the known-good state?
2. **One change at a time** — Verify each change before proceeding
3. **Track changes in a table** — Log what you changed and the result
4. **Platform differences are signals** — If X works and Y fails, the difference IS the answer
5. **Revert if worse** — Don't pile fixes on top of failures

---

## Further Reading

| Topic | Document |
|-------|----------|

---
> Source: [Catel/Catel.Examples](https://github.com/Catel/Catel.Examples) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-20 -->
