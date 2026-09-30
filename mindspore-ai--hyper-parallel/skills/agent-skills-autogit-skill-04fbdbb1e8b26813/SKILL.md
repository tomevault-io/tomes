---
name: autogit
description: > Use when this capability is needed.
metadata:
  author: mindspore-ai
---

# AutoGit

Safe GitCode fork workflow. Principle: **never overwrite without explicit
request; always back up before danger**.

Load `.agent/rules/code-style.md` before generate/modify/commit.
Announce: `Running AutoGit `<command>` …`

## When to Activate

| Intent | Command |
|---|---|
| 提交 / push | `commit` |
| 创建 PR | `pr` |
| PR 状态 | `status` |
| squash | `squash` |
| lint only | `check` |
| slash | `/commit`, `/create-pr`, `/test`, `/gen-commit-msg` |

## Tool Requirements

- Python 3.8+ (`yaml`), `git` with `origin` + `upstream`, `GITCODE_TOKEN`
- `pylint`, `markdownlint` (auto-install on first `check` if missing)

## Execution

```bash
python3 {skill_dir}/scripts/autogit.py <command> [options]
```

Quick command table + full flags: [references/commands.md](references/commands.md).

## Core flow (standard)

```text
feature branch → autogit commit … → autogit pr → (review) pr --to #N → optional squash
```

Pipelines (commit vs PR gates), lint hook ownership, interactive UT/ST and
content-preview rules: **read [references/pipelines.md](references/pipelines.md)
before running `pr` or non-tty `commit`.**

AI orchestration + anti-patterns: [references/orchestration.md](references/orchestration.md).

## Hard rules

- Show user commit msg / PR title / body before re-invoke with `-m`/`--title`/`--body`
- Ask UT/ST one at a time; never `--ut skip --st skip` unless user chose skip
- No silent force-push; squash/rebase create `backup/<timestamp>`
- No AI attribution trailers in commits
- STOP and ask before: force-push shared branches, delete others' remote branches, squash/amend others' PRs

## Error quick fix

| Error | Fix |
|-------|-----|
| Token not found | `export GITCODE_TOKEN=<token>` |
| No upstream | `git remote add upstream <URL>` |
| Uncommitted changes | `autogit commit` first |
| Push rejected | `git pull --rebase origin <branch>` |

## References

- [references/commands.md](references/commands.md)
- [references/pipelines.md](references/pipelines.md)
- [references/orchestration.md](references/orchestration.md)
- [references/examples.md](references/examples.md)

---
> Source: [mindspore-ai/hyper-parallel](https://github.com/mindspore-ai/hyper-parallel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
