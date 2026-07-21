# trail-sense

> Use the following scripts to work with the app, but do not modify them:

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/trail-sense/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

Use the following scripts to work with the app, but do not modify them:
- `scripts/build.sh`: build the debug APK
- `scripts/unit-tests.sh [test-filter]`: run unit tests. The optional filter is forwarded to Gradle with `--tests`.
- `scripts/emulator-integration-tests.sh [test-class-or-method-filter] [timeout-seconds]`: run connected Android tests on the emulator with an optional timeout, defaulting to 1800 seconds. Fails if no emulator is connected. Most individual integration tests should finish in 60 to 180 seconds; use the timeout argument for focused runs when practical.
- `scripts/lint.sh`: run Detekt linting

Use the test filters whenever possible.

---
> Source: [kylecorry31/Trail-Sense](https://github.com/kylecorry31/Trail-Sense) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
