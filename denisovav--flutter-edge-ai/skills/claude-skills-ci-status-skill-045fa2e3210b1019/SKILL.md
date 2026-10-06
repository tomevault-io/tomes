---
name: ci-status
description: Check CI status for current branch or PR, show failed job logs Use when this capability is needed.
metadata:
  author: DenisovAV
---

# CI Status Check

## Steps

1. Determine target:
   - If argument is a PR number, use that
   - Otherwise, find PR for current branch: `gh pr list --head $(git branch --show-current) --json number -q '.[0].number'`
   - If no PR found, check latest workflow runs: `gh run list --branch $(git branch --show-current) --limit 3`

2. Show check status:
   ```bash
   gh pr checks <PR_NUMBER>
   ```

3. If any checks failed, show failed logs:
   ```bash
   gh run view <RUN_ID> --log-failed 2>&1 | tail -80
   ```

4. Summarize:
   - Which jobs passed/failed/pending
   - For failures: root cause from logs (error message, not full log)
   - Suggest fix if obvious

---
> Source: [DenisovAV/flutter_edge_ai](https://github.com/DenisovAV/flutter_edge_ai) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
