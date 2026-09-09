---
name: compile-al-app
description: Compiles a temporary AL project through the workflow-installed public prerelease ALTool and verifies that a fresh app package was emitted. Use when this capability is needed.
metadata:
  author: microsoft
---

Invoke `verify-prerelease-altool`, then run:

```powershell
& .\.github\skills\compile-al-app\Invoke-CompileAlApp.ps1 `
    -ProjectPath <project-folder> `
    -PackageCachePath <project-folder>\.alpackages
```

If `app.json` references platform, application, or dependencies, invoke `download-al-symbols` first.
Preserve compiler diagnostics and the native exit code. Do not invoke `alc.exe` directly.

---
> Source: [microsoft/AL](https://github.com/microsoft/AL) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
