---
name: farmfe-guide
description: > Use when this capability is needed.
metadata:
  author: farm-fe
---

# Farm Build Tool — Agent Guide

Farm is an extremely fast Vite-compatible web build tool written in Rust.  
Official site: https://farmfe.org | Package: `@farmfe/core` | Repo: `farm-fe/farm`

---

## Reference Index

Detailed documentation is split into focused reference files under `references/`:

| File | Contents |
|------|----------|
| [`references/config.md`](references/config.md) | Config file setup, shared options, all `compilation.*` options, all `server.*` options |
| [`references/cli.md`](references/cli.md) | CLI commands (`start`, `build`, `watch`, `preview`, `clean`) and all flags |
| [`references/plugins.md`](references/plugins.md) | Using plugins (Rust, JS, Vite/Rollup, SWC, Runtime) + official plugins table |
| [`references/features.md`](references/features.md) | Quick start, CSS, TypeScript/JSX, env vars, assets, library mode, SSR, HMR, lazy compilation, persistent cache |
| [`references/javascript-api.md`](references/javascript-api.md) | `@farmfe/core` JS API — `start/build/watch/preview/clean`, `Compiler`, `Server`, `loadEnv` |
| [`references/js-plugin-api.md`](references/js-plugin-api.md) | Writing JS plugins — all hooks, `filters` structure, code examples |
| [`references/writing-plugins.md`](references/writing-plugins.md) | **Authoring custom plugins** — scaffolding, JS plugin structure, Rust plugin structure, hooks, publishing |
| [`references/recipes.md`](references/recipes.md) | Common patterns, framework quick-configs (React/Vue/Svelte/Electron), troubleshooting |

---

## Quick Orientation

### Create a Project

```bash
pnpm create farm@latest
# or with a template:
pnpm create farm my-app --template react
```

Templates: `vanilla`, `react`, `vue3`, `vue2`, `svelte`, `solid`, `preact`, `lit`, `nestjs`, `tauri`, `electron`.

### Minimal Config

```ts title="farm.config.ts"
import { defineConfig } from '@farmfe/core';

export default defineConfig({
  plugins: ['@farmfe/plugin-react'],  // Rust plugin by package name
  compilation: {
    input:  { index: './index.html' },
    output: { targetEnv: 'browser-es2017' },
  },
  server: { port: 9000 },
});
```

### Key Rules

- Config file: `farm.config.ts|js|mjs` — do **not** use `__dirname`/`__filename`; use `import.meta.url`.
- Rust plugins → `plugins: ['package-name']` or `['package-name', optionsObject]`.
- Vite/Rollup plugins → `vitePlugins: [plugin()]`, **not** `plugins`.
- JS plugin hooks **must** declare `filters` (regex arrays) for performance.
- `resolve.symlinks: true` is required when using pnpm.
- `targetEnv: 'library'` enables library mode with `format: ['esm', 'cjs']` array support.

### Dev/Prod Defaults

| Option | Development | Production |
|--------|:-----------:|:----------:|
| `lazyCompilation` | ✅ enabled | ❌ disabled |
| `persistentCache` | ✅ enabled | ✅ enabled |
| `minify` | ❌ disabled | ✅ enabled |
| `treeShaking` | ❌ disabled | ✅ enabled |
| `presetEnv` | ❌ disabled | ✅ enabled |
| `css.transformToScript` | ✅ enabled | ❌ disabled |

---
> Source: [farm-fe/farm](https://github.com/farm-fe/farm) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
