---
name: verify-python
description: Verify changes to the code2prompt Python bindings. Use when this capability is needed.
metadata:
  author: mufeedvh
---

# Verify Python

From `crates/code2prompt-python`:

```bash
uv sync
uv run pytest --quiet
```

Keep Python a thin adapter over the core. Preserve public Python names and types unless
intentionally changed. Report the Python version and failed checks explicitly.

---
> Source: [mufeedvh/code2prompt](https://github.com/mufeedvh/code2prompt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
