---
name: minecraft-agent-skills
description: - run: echo path/to/workflows Use when this capability is needed.
metadata:
  author: Jahrome907
---
# CI Release Fixture

## Required Secrets

- `MODRINTH_TOKEN`

```yaml
name: Broken Build
on:
  push:
    branches: ["main"]
steps:
  - run: echo path/to/workflows
  - env:
      CURSEFORGE_TOKEN: ${{ secrets.CURSEFORGE_TOKEN }}
    run: echo release
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
