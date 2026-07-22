---
name: agent-ci
description: Run GitHub Actions CI locally with Agent CI to validate changes before pushing. Use when testing, running checks, or validating code changes. Use when this capability is needed.
metadata:
  author: edmundmiller
---

# Agent CI

Run the full CI pipeline locally before pushing. CI was green before you started — any failure is caused by your changes.

## Run

```bash
npx @redwoodjs/agent-ci run --quiet --all --pause-on-failure
```

## Retry

When a step fails, the run pauses automatically. Fix the issue, then retry:

```bash
npx @redwoodjs/agent-ci retry --name <runner-name>
```

To re-run from an earlier step:

```bash
npx @redwoodjs/agent-ci retry --name <runner-name> --from-step <N>
```

Repeat until all jobs pass. Do not push to trigger remote CI when agent-ci can run it locally.

---
> Source: [edmundmiller/dotfiles](https://github.com/edmundmiller/dotfiles) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
