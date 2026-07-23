---
name: docker-test
description: Build the Docker image as :local and run the full Bats test suite Use when this capability is needed.
metadata:
  author: rojopolis
---

Run the full test cycle for the spellcheck action:

1. Build the local Docker image:
   ```bash
   docker build -t jonasbn/github-action-spellcheck:local .
   ```

2. Run all Bats tests against the local image:
   ```bash
   bats test/test.bats
   ```

3. Report which tests passed or failed. If the Docker build failed, show the build error before proceeding.

To run a single test by name, use:
```bash
bats --filter "<test name>" test/test.bats
```

---
> Source: [rojopolis/spellcheck-github-actions](https://github.com/rojopolis/spellcheck-github-actions) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
