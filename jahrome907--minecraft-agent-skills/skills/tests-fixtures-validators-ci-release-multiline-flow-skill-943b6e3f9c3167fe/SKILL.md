---
name: minecraft-ci-release
description: > Use when this capability is needed.
metadata:
  author: Jahrome907
---

# Multiline Flow Fixture

## Required Secrets

- `MODRINTH_TOKEN`

```yaml
name: Matrix Build
on:
  push:
    branches: ["main"]
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        include: [
          { platform: fabric, dir: fabric },
          { platform: neoforge, dir: neoforge }
        ]
    steps:
      - uses: actions/checkout@v4
      - env:
          MODRINTH_TOKEN: ${{ secrets.MODRINTH_TOKEN }}
        run: ./gradlew :${{ matrix.dir }}:build --no-daemon
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
