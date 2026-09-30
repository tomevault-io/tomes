---
name: validate-charts
description: Run the repository's cross-platform chart validation before review or release. Use when this capability is needed.
metadata:
  author: gurgen-k-y
---

# Validate charts

Run:

```shell
./gradlew \
  :charts:desktopTest \
  :charts:compileKotlinIosSimulatorArm64 \
  :example:compileKotlinDesktop \
  :example:wasmJsBrowserDistribution \
  :androidApp:assembleDebug \
  :charts:dokkaGenerate \
  :charts:publishToMavenLocal
```

Then run `git diff --check` and inspect the Maven Local POM/module metadata. Do not publish remotely.

---
> Source: [gurgen-k-y/compose-multiplatform-charts](https://github.com/gurgen-k-y/compose-multiplatform-charts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-27 -->
