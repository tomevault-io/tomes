---
name: implement-issue
description: > Use when this capability is needed.
metadata:
  author: google
---

# Implement a GitHub issue

Implement GitHub issue **#$ARGUMENTS** (if no number was given, ask for one) by following the
project's shared playbook. Do not reimplement the procedure here — read and follow the
playbook, which is the single source of truth shared with the other AI tools.

## Procedure

1. **Read the playbook** `docs/context/workflow/implement-issue.md` and follow every step:
   fetch & parse the issue, determine scope, load only the relevant `docs/context/{js,php}`
   convention docs (per the map in the playbook), branch off `develop`, implement with
   co-located tests/stories, self-review, and verify.
2. **Fetch the issue**: `gh issue view $ARGUMENTS --json title,body,labels`. Stop and ask the
   user if the issue is missing, empty, or the Implementation Brief is ambiguous.
3. **Self-review** your diff against `docs/context/workflow/review-checklist.md` and fix gaps
   before finishing.
4. **Verify** with the exact commands in the playbook (lint, targeted tests, build).

## Important

- **Local only**: never commit, push, or open a PR unless the user explicitly asks.
- Run only the **specific** test files you touched (`npm -w tests/js run test:js -- <path>`),
  not the whole suite.
- Lint only the files you touched (`npm run lint:js:files -- <path>` / `composer lint --
  <path>`), and if you touched a Storybook story, check just that VRT scenario
  (`./tests/backstop/bin/backstop test --filter="<scenario label>"`) rather than the full
  suite.
- The convention details are in `docs/context/{js,php}/` — read what the issue touches, not
  everything.

---
> Source: [google/site-kit-wp](https://github.com/google/site-kit-wp) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
