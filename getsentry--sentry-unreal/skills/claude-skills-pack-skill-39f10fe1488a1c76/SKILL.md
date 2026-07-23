---
name: pack
description: Package plugin and update file snapshot Use when this capability is needed.
metadata:
  author: getsentry
---

Package the Sentry plugin and update the file snapshot. Use this after adding or removing files under `plugin-dev/`.

1. Run the packaging script:

```bash
pwsh ./scripts/packaging/pack.ps1
```

2. Update the snapshot to accept the new file listing:

```bash
pwsh ./scripts/packaging/test-contents.ps1 accept
```

---
> Source: [getsentry/sentry-unreal](https://github.com/getsentry/sentry-unreal) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
