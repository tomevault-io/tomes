# elps

> This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/elps/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ELPS is an embedded Lisp interpreter implemented in Go. It is a Lisp-1 dialect designed to be embedded within Go applications. Module: `github.com/luthersystems/elps`.

## Build and Test Commands

| Command | Description |
|---------|-------------|
| `make` | Build the `./elps` binary |
| `make test` | Run all tests (Go tests + example lisp files) |
| `make go-test` | Run Go tests only: `go test -cover ./...` |
| `go test ./lisp/...` | Run tests for a specific package |
| `go test -run TestName ./lisp/` | Run a single test |
| `make static-checks` | Run golangci-lint with gosec |
| `make repl` | Build and launch the REPL |
| `./elps run file.lisp` | Run a lisp file |
| `./elps doc <query>` | Show function/package documentation |
| `./elps doc -m` | Check for missing docstrings (used in CI) |
| `./elps doc --guide` | Print the full language reference |
| `./elps doc --debug-guide` | Print the debugging guide |
| `./elps doc --lsp-guide` | Print the Language Server Protocol guide |
| `./elps lsp --stdio` | Start the LSP server (stdio transport) |
| `./elps lsp --port 7998` | Start the LSP server (TCP transport) |
| `./elps lint file.lisp` | Run static analysis on a lisp file |
| `./elps fmt file.lisp` | Format a lisp file |
| `make release-notes` | Preview release notes (commits, PRs, CI status since last tag) |
| `make release VERSION=v1.X.0` | Create a tagged GitHub release (must be on main, CI must pass) |

## Architecture

### Core Packages

- **`lisp/`** — The interpreter core. Contains `LVal` (lisp values), `LEnv` (environment/evaluator), builtins, special operators, macros, package system, call stack, error handling, and Go interop.
- **`parser/`** — Lexer (`lexer/`), tokens (`token/`), and two parser implementations: `rdparser/` (recursive descent, primary) and `regexparser/` (regex-based, alternative).
- **`lisp/lisplib/`** — Standard library packages loaded by `LoadLibrary()`: time, help, golang, math, string, base64, json, regexp, testing, schema.
- **`cmd/`** — Cobra CLI commands: `run`, `repl`, `doc`, `lint`, `fmt`, `lsp`.
- **`repl/`** — Interactive REPL using readline.
- **`elpstest/`** — Test framework (`Runner`) for executing lisp-based test files as Go subtests.
- **`elpsutil/`** — Helpers for building embedded packages in Go (`Function()`, `PackageLoader()`, etc.).
- **`lsp/`** — Language Server Protocol server built on `tliron/glsp`. Provides diagnostics, hover, go-to-definition, references, completion, document symbols, and rename. Embeddable via `lsp.WithEnv()` / `lsp.WithRegistry()` options.
- **`lisp/x/profiler/`** — Experimental profiling (callgrind, OpenCensus, OpenTelemetry).

### Key Types (lisp/)

- **`LVal`** — The universal value type. Everything in ELPS is an LVal: ints, floats, strings, symbols, lists, functions, errors, sorted-maps, arrays, native Go values, tagged values.
- **`LEnv`** — Environment/evaluator. Handles eval, scoping, function calls, tail recursion optimization, macro expansion, and package management. Tree-structured (parent/child scopes).
- **`Runtime`** — Shared state across the env tree: package registry, call stack, reader, library, profiler.
- **`LBuiltin`** — Function signature for Go-implemented builtins: `func(env *LEnv, args *LVal) *LVal`.

### Embedding Pattern

Standard setup for embedding ELPS in Go:
```go
env := lisp.NewEnv(nil)
env.Runtime.Reader = parser.NewReader()
env.Runtime.Library = &lisp.RelativeFileSystemLibrary{}
rc := lisp.InitializeUserEnv(env)
rc = lisplib.LoadLibrary(env)
rc = env.InPackage(lisp.String(lisp.DefaultUserPackage))
```

### Test Infrastructure

Tests exist in two forms:
1. **Go unit tests** — Standard `_test.go` files using `testify/assert`.
2. **Lisp test files** — `.lisp` files executed via `elpstest.Runner`, which loads them and runs as Go subtests. The `libtesting` stdlib package provides `test`, `test-let`, `assert=`, `assert-equal`, `assert-nil`, etc.

Go test suites typically use `elpstest.TestSuite` with `TestSequence` entries that define `{expression, expected-result, expected-output}` triples.

### Language Key Points

- **Lisp-1**: Single namespace for functions and variables.
- **Booleans**: `true` and `false` are symbols. `()` (nil) is falsey; everything else is truthy.
- **Function args**: Support required, optional (`&optional`), variadic (`&rest`), and keyword (`&key`) arguments.
- **Packages**: Namespaced with `in-package`, `use-package`, `export`. Qualified symbols use `:` (e.g., `lisp:set`). Keywords start with `:`.
- **Error handling**: Condition-based with stack traces. `handler-bind` and `ignore-errors`.
- **Tail recursion**: Optimized via stack frame analysis.

### Error Propagation Convention

Functions return `*LVal`. Errors are LVal values with type `LError`. Check with `v.Type == lisp.LError` or use the `GoError()` helper. Errors propagate up the call chain — most code returns errors immediately rather than using Go's `error` interface.

## Additional Packages

- **`formatter/`** — Source code formatter. Uses annotated AST with `LVal.Meta *SourceMeta`. Parser `preserveFormat` mode collects comments, brackets, newlines.
- **`analysis/`** — Semantic analysis: scope building, symbol resolution, reference counting. `prescan()` uses a two-phase approach (definitions first, exports second) so `(export 'name)` before `(defun name ...)` works correctly.
- **`lint/`** — Static analysis modeled after `go vet`. Each check is an `Analyzer` with a `Run func(pass *Pass) error`. Uses `Walk()`/`WalkSExprs()` for AST traversal, plus custom walkers for context-sensitive checks.
- **`diagnostic/`** — Rust-style annotated source snippets for error and lint output. Zero dependencies on `lisp/`.

## Development Workflow

### Adding New Builtins or Special Operators

When adding a new builtin function, special operator, or macro:

1. **Add the implementation** in `lisp/builtins.go`, `lisp/op.go`, or `lisp/macro.go`.
2. **Include a docstring** in the definition. All builtins must have documentation — CI runs `elps doc -m` to enforce this.
3. **Add a linter check** if the new form has structural requirements (e.g., `rethrow-context` checks that `rethrow` is only used inside `handler-bind`). Add the analyzer to `lint/analyzers.go` and register it in `DefaultAnalyzers()` in `lint/lint.go`.
4. **Update `docs/lang.md`** if the feature is user-facing. This file is embedded in the binary and served via `elps doc --guide`.
5. **Write tests**: Go unit tests in `_test.go` files and/or lisp test files via `elpstest.Runner`.
6. **Verify**: Run `make test && make static-checks` before committing.

### Linter Development

- Each analyzer is an `*Analyzer` struct in `lint/analyzers.go` with `Name`, `Doc`, and `Run` fields.
- Use `WalkSExprs()` for simple checks that inspect each s-expression independently.
- Use custom recursive walkers with depth/context tracking for checks that depend on enclosing forms (see `walkRethrowContext` for an example).
- Register new analyzers in `DefaultAnalyzers()` and update the analyzer count in `TestDefaultAnalyzers`.
- Support `; nolint:analyzer-name` suppression via trailing comments — this is handled automatically by `filterSuppressed()`.
- Every diagnostic now includes a `; nolint:` suppression hint in its notes.

### `set` vs `set!` Semantics

- **`set` creates or overwrites** bindings — it is the only way to create new top-level bindings.
- **`set!` only mutates** existing bindings — it errors if the symbol is not already bound.
- The `set-usage` linter flags repeated `set` on the same symbol, not every `set`.

## Skills

Prescriptive workflows live in `.claude/skills/`. **Before starting a task, read the matching skill file and follow its workflow exactly.** Match tasks to skills by description:

| Skill File | When to Use |
|------------|-------------|
| `implement/SKILL.md` | Any code change — builtins, ops, macros, parser, formatter, CLI, bug fixes, docs |
| `add-linter-check/SKILL.md` | New lint analyzer — prescriptive 3-file-touch workflow |
| `add-stdlib-package/SKILL.md` | New stdlib package — create, wire, test |
| `verify/SKILL.md` | CI gate — build, test, golangci-lint, fmt, lint, doc checks |
| `pr/SKILL.md` | Ship — verify, push, create PR with summary and test plan |
| `pickup-issue/SKILL.md` | Full lifecycle — issue to branch to implementation to PR |
| `benchmark/SKILL.md` | Performance — before/after benchstat comparison |
| `audit/SKILL.md` | Systematic codebase audit — bugs, security, perf, tests, docs, quality |
| `release/SKILL.md` | Create a tagged GitHub release with auto-generated notes from merged PRs |

Multiple skills can chain: e.g., a GitHub issue triggers `pickup-issue`, which uses `implement` for the code change, `verify` before committing, and `pr` to ship.

## GitHub Tooling

Use `gh` for GitHub-hosted resources in this repository's workflows:
- issues: `gh issue view`, `gh issue list`, `gh issue comment`
- pull requests: `gh pr view`, `gh pr checks`, `gh pr create`
- repo metadata and API queries: `gh repo view`, `gh api`

Do not use generic web-scraping/search tooling for normal GitHub issue or PR retrieval when the GitHub CLI can provide the data directly.

---
> Source: [luthersystems/elps](https://github.com/luthersystems/elps) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
