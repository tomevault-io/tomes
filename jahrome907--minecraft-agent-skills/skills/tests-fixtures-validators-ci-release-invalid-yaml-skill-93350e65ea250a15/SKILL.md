---
name: minecraft-ci-release
description: > Use when this capability is needed.
metadata:
  author: Jahrome907
---

# Invalid YAML Fixture

## Secrets

- `GITHUB_TOKEN`

```yaml
name: Broken Workflow
on:
  push:
jobs:
  build:
    runs-on ubuntu-latest
    steps:
      - run: echo "broken"
```

---
> Source: [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
