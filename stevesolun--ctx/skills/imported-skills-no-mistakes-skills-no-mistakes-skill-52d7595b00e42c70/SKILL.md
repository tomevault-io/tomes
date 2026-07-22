---
name: no-mistakes
description: > Use when this capability is needed.
metadata:
  author: stevesolun
---

# no-mistakes

`no-mistakes` is a local git gate. It validates committed branch changes before
they reach upstream and reports decision points in machine-readable TOON.

## Preconditions

- Work is committed.
- Current branch is a feature branch, not the default branch.
- The repository has been initialized with `no-mistakes init`.
- The intent is explicit: what the user wanted to accomplish, not only a diff
  summary.

## Run

```sh
no-mistakes axi run --intent "<what the user set out to accomplish>"
```

Use the user's exact objective as the intent, enriched with material decisions
and constraints learned during the work.

## Decision Loop

If output contains a `gate:` object, inspect each finding:

- `auto-fix`: make the mechanical fix, then respond with `fix`.
- `no-op`: approve or continue when nothing needs changing.
- `ask-user`: stop and relay the finding to the user before responding.

Useful commands:

```sh
no-mistakes axi respond --action approve
no-mistakes axi respond --action fix --findings <id1,id2> --instructions "<guidance>"
no-mistakes axi respond --action skip
no-mistakes axi status
no-mistakes axi logs --step <name> --full
no-mistakes axi abort
```

## Output Contract

- `checks-passed`: CI is green and the PR is ready for human review/merge.
- `passed`: the gate completed.
- `failed` or `cancelled`: inspect output and fix the reported issue.

Do not silently approve `ask-user` findings unless the user explicitly gave
standing consent such as `--yes`.

---
> Source: [stevesolun/ctx](https://github.com/stevesolun/ctx) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
