---
name: cppjs-runtime-api
description: Use this skill the moment the user asks about cpp.js runtime/build configuration, C++ binding rules, or build troubleshooting — phrases like "what options does initCppJs accept", "how do I enable OPFS / persistent storage in cpp.js", "useWorker", "is cppjs multithread", "runtime: mt vs st", "COOP COEP for cpp.js", "what fields go in cppjs.config.js", "cppjs.build.js hooks", "what shape is state / target in build hooks", "cpp.js binding rules / can I use raw pointers", "writing a C++ wrapper for cpp.js", "manual SWIG .i file in cpp.js", "cppjs override mechanism for emccFlags / cmake / env", "cppjs build error / linker error / out of memory", "cppjs performance defaults / tunable flags", "do I need m.delete in cpp.js", "TypeScript types for cpp.js", "mount file from input in cppjs", "cppjs filesystem in browser / node / cloudflare worker", "edge runtime cppjs limits". Pull the matching reference doc into context before answering.
metadata:
  author: bugra9
---

# cppjs-runtime-api

Answer cpp.js runtime / config questions from the canonical reference docs, never from training-data guesses. The reference covers four surfaces; pick the one matching the question.

## Routing table

| User asks about | Load this doc | MCP topic |
|-----------------|---------------|-----------|
| `initCppJs(opts)` parameters, return shape, Module helpers | `docs/api/init.md` | `init` |
| `cppjs.config.js` fields (consumer, build-time) | `docs/api/cppjs-config.md` | `config` |
| `cppjs.build.js` hooks (package author, build-time) | `docs/api/cppjs-build.md` | `build` |
| OPFS, memfs, persistence, file mounting, `m.FS` | `docs/api/filesystem.md` | `filesystem` |
| `runtime: 'st' \| 'mt'`, `useWorker`, COOP/COEP, edge limits | `docs/api/threading.md` | `threading` |
| C++ binding rules (no pointers, C++11+, wrapper pattern) | `docs/api/cpp-binding-rules.md` | `binding-rules` |
| Manual SWIG `.i` escape hatch | `docs/api/swig-escape.md` | `swig` |
| `state` / `target` shapes for build hooks; 20 built-in target inventory | `docs/api/build-state.md` | `state` |
| Catalog of override mechanisms (filter → targetSpecs → build hooks → extensions) | `docs/api/overrides.md` | `overrides` |
| Common errors mapped to fixes; tribal-knowledge gotchas | `docs/api/troubleshooting.md` | `troubleshooting` |
| Default Emscripten / CMake flags + safe-override guide | `docs/api/performance.md` | `performance` |
| Memory / object lifecycle in JS (none needed) + TypeScript notes | `docs/api/lifecycle-and-types.md` | `lifecycle` |
| Where to start | `docs/api/README.md` (decision tree) | `index` |

GitHub mirrors of all docs:

- `https://github.com/bugra9/cpp.js/blob/main/docs/api/<file>.md`

## How to use

1. **Identify the surface** the question lives in (runtime vs build-time, consumer vs package author, fs vs threading vs binding rules).
2. **Pull the matching doc** into context. Three ways:
   - **MCP**: call `cppjs_get_api_reference({ topic: 'init' })` (or any topic from the table above).
   - **Inside the monorepo**: Read the file directly.
   - **Outside the monorepo**: WebFetch the GitHub URL.
3. **Answer from the doc**, with concrete examples. Don't paraphrase if the doc has the exact snippet.
4. **Surface the load-bearing constraint.** Most questions have a hidden constraint that bites users later — name it explicitly:
   - OPFS persistence → requires `useWorker: true`
   - `runtime: 'mt'` in production → requires COOP/COEP headers
   - Edge runtimes → no `useWorker`, no `mt`, no OPFS
   - `paths.native` is an array, not a string
   - C++ side: no raw pointers, C++11+ minimum, write a wrapper if upstream lib uses unbindable types
   - Defaults: `-O3`, `-msimd128`, `-sALLOW_MEMORY_GROWTH=1`, etc. — don't override speculatively
5. **`cppjs.config.js` is build-time only.** Putting `useWorker: true` in it does nothing — that's a runtime option for `initCppJs(opts)`. Catch this confusion early.
6. **Reach for the least invasive override.** When a default doesn't fit, the order is: target filter → `targetSpecs[].specs.*` → `cppjs.config.js env / functions` → `cppjs.build.js` hooks → `extensions[]` → `~/.cppjs.json`. See `overrides.md`.

## The 5 most-asked questions (and the 1-line answer for each)

> Use these to short-circuit obvious cases. Always offer to load the full doc for nuance.

1. **"How do I get persistent storage in browser?"**
   → `useWorker: true`, then write to `/opfs/<appName>/`. See `filesystem.md`.

2. **"How do I make cpp.js multithreaded?"**
   → `target.runtime: 'mt'` in `cppjs.config.js` + COOP/COEP headers in production. See `threading.md`.

3. **"What does `useWorker` actually do?"**
   → Spawns the Wasm module in a Web Worker; everything becomes async via Comlink. Required for OPFS, optional for parallelism (separate from `runtime: 'mt'`). See `init.md` + `threading.md`.

4. **"Can I use cpp.js on Cloudflare Workers?"**
   → Yes, but only `runtime: 'st'` + memory fs. No `useWorker`, no OPFS, no `mt` — edge runtimes don't expose the Worker API. See `threading.md` "Edge runtime limits".

5. **"What fields go in `cppjs.config.js`?"**
   → `general.name`, `dependencies[]`, `paths.{config, project, native[], output, …}`, `target.runtime`, `export.{type, libName[]}`. See `cppjs-config.md` for the full shape with defaults.

## Don't

- Don't answer cpp.js API questions from training-data assumptions. The API has evolved; load the current doc.
- Don't conflate `cppjs.config.js` (build-time) with `initCppJs(opts)` (runtime). Different surfaces, different fields.
- Don't conflate `useWorker: true` with `runtime: 'mt'`. They're orthogonal axes (see the matrix in `threading.md`).
- Don't suggest writing `cppjs.build.js` to a consumer — that file is package-author-only.
- Don't omit the COOP/COEP heads-up when the user is shipping a `mt` build to production. It's the #1 reason `mt` "works in dev, fails in prod".

## Reference

Full index: https://github.com/bugra9/cpp.js/blob/main/docs/api/README.md

---
> Source: [bugra9/cpp.js](https://github.com/bugra9/cpp.js) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
