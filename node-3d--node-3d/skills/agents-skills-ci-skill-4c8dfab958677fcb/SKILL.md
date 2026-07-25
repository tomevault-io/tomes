---
name: ci
description: Maintain Node3D GitHub Actions and CI infrastructure. Use for workflow files, reusable actions, lint/test/build/publish jobs, platform matrices, native addon CI, CUDA/GPU limitations, prebuilt binary constraints, npm install script safety, cpplint, and keeping package CI consistent across repositories. Use when this capability is needed.
metadata:
  author: node-3d
---

# CI

Use this skill for GitHub Actions and package CI. Node3D CI must account for native addons, platform-specific binaries, direct TypeScript execution, and packages that cannot assume GPU hardware.

## Workflow

1. Compare the target package with similar packages before inventing a workflow.
2. Choose install mode deliberately. Use `npm ci --ignore-scripts` when native postinstall downloads or hardware assumptions would make CI brittle.
3. Separate portable checks from hardware-dependent checks. Lint, tsgo, package build, pure TS tests, and cpplint can often run where native execution cannot.
4. Encode known legacy C++ limitations explicitly and narrowly when a cleanup is out of scope.
5. Keep workflow names, triggers, Node versions, npm commands, and publish patterns consistent across packages.
6. When designing future reusable actions, preserve the standalone package repository model.

## References

- Read [github-actions.md](references/github-actions.md) for current workflow patterns and command choices.
- Read [platform-limits.md](references/platform-limits.md) for native, GPU, CUDA, and platform-specific CI constraints.

---
> Source: [node-3d/node-3d](https://github.com/node-3d/node-3d) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
