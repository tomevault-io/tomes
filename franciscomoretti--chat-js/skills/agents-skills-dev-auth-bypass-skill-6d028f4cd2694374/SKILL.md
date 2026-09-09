---
name: dev-auth-bypass
description: Authenticate a browser against a local ChatJS app without OAuth. Use for development login, local auth bypass, authenticated browser or Playwright testing, and the /api/dev-login route. Use when this capability is needed.
metadata:
  author: FranciscoMoretti
---

# Dev Auth Bypass

- Given the app URL, navigate the browser to `<app-url>/api/dev-login`.
- Use browser navigation rather than `curl` so the browser receives the session
  cookie.
- Expect the route to create the local dev user and session, then redirect to
  the app.
- Use this route only in development. It returns `404` otherwise.

---
> Source: [FranciscoMoretti/chat-js](https://github.com/FranciscoMoretti/chat-js) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-09 -->
