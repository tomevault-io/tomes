---
name: vite-plus
description: Vite+ unified toolchain (vp CLI) usage for this project, wrapping Vite, Rolldown, Vitest, tsdown, Oxlint, Oxfmt, and Vite Task. Use when running install/build/test/check/format/lint, working with the `vp` CLI, or validating changes in this repo. Use when this capability is needed.
metadata:
  author: victorgarciaesgi
---

<!--VITE PLUS START-->

# Using Vite+, the Unified Toolchain for the Web

This project is using Vite+, a unified toolchain built on top of Vite, Rolldown, Vitest, tsdown, Oxlint, Oxfmt, and Vite Task. Vite+ wraps runtime management, package management, and frontend tooling in a single global CLI called `vp`. Vite+ is distinct from Vite, and it invokes Vite through `vp dev` and `vp build`. Run `vp help` to print a list of commands and `vp <command> --help` for information about a specific command.

Docs are local at `node_modules/vite-plus/docs` or online at https://viteplus.dev/guide/.

## Review Checklist

- [ ] Run `vp install` after pulling remote changes and before getting started.
- [ ] Run `vp check` and `vp test` to format, lint, type check and test changes.
- [ ] Check if there are `vite.config.ts` tasks or `package.json` scripts necessary for validation, run via `vp run <script>`.

<!--VITE PLUS END-->

---
> Source: [victorgarciaesgi/regle](https://github.com/victorgarciaesgi/regle) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
