---
name: xyne-spaces
description: Log the user into Xyne Claw. Use when this capability is needed.
metadata:
  author: juspay
---

Call the `claw_login` MCP tool.

Show the returned verification URL and user code, and tell the user to open the URL and approve the login with that code.

Poll `claw_whoami` until it reports that the user is logged in, then display the current Xyne Claw identity.

---
> Source: [juspay/xyne-spaces](https://github.com/juspay/xyne-spaces) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
