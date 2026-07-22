---
name: minecraft-ci-release
description: > Use when this capability is needed.
metadata:
  author: Jahrome907
---

# Warning Fixture

## Secrets

- `MODRINTH_TOKEN`

```yaml
name: Warn Only
on:
  workflow_dispatch:
jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - run: echo "ok"
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
