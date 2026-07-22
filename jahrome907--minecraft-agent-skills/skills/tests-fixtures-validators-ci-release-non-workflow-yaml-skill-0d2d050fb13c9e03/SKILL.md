---
name: minecraft-agent-skills
description: uses: gradle/actions/setup-gradle@v3 Use when this capability is needed.
metadata:
  author: Jahrome907
---
# CI Release Fixture

## Required Secrets

- `MODRINTH_TOKEN`

```yaml
# In all workflow jobs:
- name: Setup Gradle
  uses: gradle/actions/setup-gradle@v3
  with:
    cache-read-only: ${{ github.event_name == 'pull_request' }}
```

```yaml
name: Build
on:
  push:
    branches: ["main"]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo ok
      - env:
          MODRINTH_TOKEN: ${{ secrets.MODRINTH_TOKEN }}
        run: echo release
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
