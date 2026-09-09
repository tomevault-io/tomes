---
name: create-al-project
description: Creates the smallest temporary AL project needed to reproduce a public issue without VS Code.
metadata:
  author: microsoft
---

1. Invoke `verify-prerelease-altool`.
2. Create the project under `$env:RUNNER_TEMP`, never inside the repository checkout.
3. Write `app.json` with a new GUID, name, publisher, version, target, runtime, and the smallest ID
   range needed by the report.
4. Add `platform`, `application`, and dependencies only when the scenario needs them.
5. Add only the AL source and analyzer settings required by the reported steps.
6. If symbol references exist, invoke `download-al-symbols`.
7. Compile with `compile-al-app`.

Do not launch VS Code or invoke `AL: Go!`.

---
> Source: [microsoft/AL](https://github.com/microsoft/AL) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
