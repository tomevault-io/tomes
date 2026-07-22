---
name: minecraft-agent-skills
description: runs-on: ubuntu-latest
metadata:
  author: Jahrome907
---
# CI Release Fixture

## Required Secrets

- `MODRINTH_TOKEN`
- `CURSEFORGE_TOKEN`

```yaml
name: Build
on:
  push:
    branches: ["main"]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo ok
      - env:
          MODRINTH_TOKEN: ${{ secrets.MODRINTH_TOKEN }}
          CURSEFORGE_TOKEN: ${{ secrets.CURSEFORGE_TOKEN }}
        run: echo release
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
