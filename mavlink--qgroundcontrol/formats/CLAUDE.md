# qgroundcontrol

> Instructions for AI coding agents (Codex, Claude Code, etc.) working on QGroundControl.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/qgroundcontrol/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# AGENTS.md

Instructions for AI coding agents (Codex, Claude Code, etc.) working on QGroundControl.

## Quick References

- [CODING_STYLE.md](CODING_STYLE.md) — Naming, formatting, C++20 features, QML style, logging
- [.github/CONTRIBUTING.md](.github/CONTRIBUTING.md) — Architecture patterns (Fact System, Multi-Vehicle, FirmwarePlugin)
- [tools/README.md](tools/README.md) — Development scripts and tooling
- [test/README.md](test/README.md) — Test framework, base classes, CTest labels, MultiSignalSpy, coverage
- [.github/ci-overview.md](.github/ci-overview.md) — CI workflow/action/script layout and conventions
- [.pre-commit-config.yaml](.pre-commit-config.yaml) — All enforced linters (clang-format, clang-tidy, ruff, pyright, shellcheck, actionlint, zizmor, qmllint, clazy, vehicle-null-check, check-no-qassert, check-no-qtest-ignore-message)

## Golden Rules (enforced — violations fail CI)

These are the non-negotiables. The first four are QGC's core architecture patterns; the rest are
enforced by pre-commit hooks, so ignoring them wastes a build cycle. Full list with code examples:
[.github/CONTRIBUTING.md#architecture-patterns](.github/CONTRIBUTING.md#architecture-patterns) and
[CODING_STYLE.md#common-pitfalls](CODING_STYLE.md#common-pitfalls).

- **Fact System** — ALL vehicle parameters flow through Facts; never create custom parameter storage.
- **Multi-Vehicle** — ALWAYS null-check `activeVehicle()` / `Vehicle*` before dereferencing (`vehicle-null-check`).
- **Firmware Plugin** — use `vehicle->firmwarePlugin()` for firmware-specific behavior, not `if (px4)` branches.
- **QML Integration** — register types with `QML_ELEMENT`/`QML_SINGLETON`/`QML_UNCREATABLE`; expose state via `Q_PROPERTY`.
- **No `Q_ASSERT` in production code** — use defensive checks with early returns (`check-no-qassert`).
- **No `QTest::ignoreMessage`** in tests — use `expectLogMessage`/`ignoreLogMessage` (`check-no-qtest-ignore-message`).
- **No fixed-delay `QTest::qWait(<n>)`** — use `QTRY_*_WITH_TIMEOUT` or `QSignalSpy::wait` (`check-no-fixed-qwait`).

## Critical Files (Read First!)

1. `src/FactSystem/Fact.h` — Parameter system foundation
2. `src/Vehicle/Vehicle.h` — Core vehicle model
3. `src/FirmwarePlugin/FirmwarePlugin.h` — Firmware abstraction

## Code Structure

Key modules (full tree under `src/` — ~33 subdirectories):

```text
src/
├── Vehicle/          # Vehicle state/comms
├── Comms/            # Link layer (serial, UDP, TCP, Bluetooth)
├── FactSystem/       # Parameter management
├── FirmwarePlugin/   # PX4/ArduPilot abstraction
├── AutoPilotPlugins/ # Vehicle setup UI
├── MissionManager/   # Mission planning
├── MAVLink/          # Protocol handling
├── VideoManager/     # Video pipeline (GStreamer)
├── FlyView/          # In-flight UI
├── PlanView/         # Mission planning UI
├── QmlControls/      # Reusable QML components
└── Settings/         # Persistent settings
```

## Build & Test Commands

The `just` recipes are the canonical workflow — see [tools/README.md](tools/README.md) for the full list.
[.github/ci-overview.md](.github/ci-overview.md) documents how CI invokes builds and tests; match CI, don't guess.

```bash
just configure          # CMake configure (pulls submodules first)
just build              # incremental build; leaves ~half the cores free
just test               # ctest, LABELS="Unit|Integration" EXCLUDE="Flaky|Network"
just lint               # fast pre-commit gate (clang-format, ruff, qmllint, ...)
just check              # lint + test (run before declaring done)
just format-fix         # apply clang-format / ruff-format
just info               # print resolved versions (Qt, CMake, GStreamer)
```

- **Build incrementally** — rebuild every few file edits during multi-file C++/Qt work, not just at the end; fix build errors before continuing.
- **Tight test loops** — iterate one test with `ctest -R <name>` (or `--gtest_filter`); only run the full label on the final pass. CI runs `ctest --output-on-failure -L Unit`.
- **Match CI** — before running tests/lint locally, use the same command CI runs ([.github/ci-overview.md](.github/ci-overview.md)), not a local guess.

## Definition of Done

Before considering a change complete:

1. `just build` succeeds.
2. `just lint` (or `pre-commit run --all-files` for the full sweep) passes.
3. Relevant tests pass (`ctest -R <name>` for the touched area; full `-L Unit` on the final pass).
4. Commit message follows Conventional Commits (below).

## Commit & Review Conventions

Commit messages follow **Conventional Commits** — the type drives release automation
(`.releaserc.json` → semantic-release). Use: `feat`, `fix`, `perf`, `revert` (release-triggering);
`docs`, `style`, `chore`, `refactor`, `test`, `build`, `ci` (no release). Example: `fix(Vehicle): guard null activeVehicle in telemetry handler`.

Your output will be reviewed by another AI agent before being accepted. Keep changes focused and
minimal, use clear naming, and leave explanatory commit messages. Avoid unrelated changes,
commented-out code, or ambiguous TODOs.

---

**Key Principle**: Match the style of code you're editing. See [CODING_STYLE.md](CODING_STYLE.md) for conventions and [CODING_STYLE.md#examples](CODING_STYLE.md#examples) for canonical Vehicle/Fact/QML snippets.

---
> Source: [mavlink/qgroundcontrol](https://github.com/mavlink/qgroundcontrol) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
