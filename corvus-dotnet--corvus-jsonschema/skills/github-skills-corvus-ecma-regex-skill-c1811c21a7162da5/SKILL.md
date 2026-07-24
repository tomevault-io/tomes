---
name: corvus-ecma-regex
description: > Use when this capability is needed.
metadata:
  author: corvus-dotnet
---

# ECMAScript Regex Translation

## Entry Point API

The translator is in `src/Corvus.Text.Json.CodeGeneration/EcmaRegexTranslator.cs`:

```csharp
// Translate an ECMAScript /u mode pattern to .NET
string dotnetPattern = EcmaRegexTranslator.Translate(@"\d+\.\d+");

// Non-throwing variant with span output
OperationStatus status = EcmaRegexTranslator.TryTranslate(
    ecmaPattern, buffer, out int charsWritten);

// Safe fallback — returns original pattern if translation fails
string pattern = EcmaRegexTranslator.TranslateOrFallback(ecmaPattern);
```

## Translation Examples

| ECMAScript Pattern | .NET Translation | Reason |
|---|---|---|
| `.` | `[^\n\r\u2028\u2029]` | Dot excludes specific line terminators |
| `\d` | `[0-9]` | ASCII digits only |
| `\u{1F600}` | `(?:\uD83D\uDE00)` | Supplementary char → surrogate pair |
| `(a)\1` | `(a)(?(1)\1)` | Backreference wrapped in conditional |
| `[a\D]` | `(?:[a]\|[^0-9])` | Negated shorthand in class uses alternation |

## Why Translation Is Needed

JSON Schema's `pattern` keyword uses ECMAScript regex semantics (ECMA 262 `/u` mode).
.NET's `System.Text.RegularExpressions` has different semantics for several constructs.
The translator converts ECMAScript patterns to equivalent .NET patterns.

## Key Translation Rules

### Character Class Shorthands

| ECMAScript | .NET Translation | Reason |
|-----------|------------------|--------|
| `\d` | `[0-9]` | .NET `\d` matches Unicode digits; ECMAScript only ASCII |
| `\w` | `[a-zA-Z0-9_]` | .NET `\w` matches Unicode word chars |
| `\s` | Explicit ECMAScript whitespace set | Different whitespace sets |
| `.` | `[^\n\r\u2028\u2029]` | ECMAScript excludes 4 line terminators |

### Word Boundaries

`\b` → explicit lookaround assertions using ASCII word characters only (ECMAScript definition).

### Supplementary Code Points

`\u{XXXXX}` (code points above U+FFFF) → `(?:\uHHHH\uLLLL)` surrogate pair in .NET.

### Backreferences

ECMAScript treats non-participating groups as always-matching. Translated to:
`(?(N)\N)` — .NET conditional syntax that checks if group N participated.

### Unicode Property Escapes

`\p{Script=Latin}` → expanded character class ranges (34 BMP + 5 supplementary ranges).

Binary properties like `\p{Emoji}` → equivalent .NET character class unions.

## Performance Characteristics

The translator is **zero-allocation** using:
- `ref struct` translator type
- `stackalloc` for small intermediate buffers
- `ArrayPool<char>` for larger buffers

The translated regex pattern is then compiled using `RegexOptions.Compiled` for
repeated use in validation.

## Regex Pattern Classification (at code-gen time)

Before translating, the code generator classifies patterns:

| Classification | Example | Optimization |
|----------------|---------|-------------|
| `Noop` | `.*`, `^.*$` | Skip validation entirely |
| `NonEmpty` | `.+` | Simple length > 0 check |
| `Prefix` | `^foo` | `StartsWith("foo")` |
| `Range` | `[a-z]` | Inline character range check |
| `FullRegex` | Everything else | Full compiled regex |

## Cross-References
- For the evaluator that uses translated patterns, see `corvus-standalone-evaluator`
- For the keyword that drives pattern validation, see `corvus-keywords-and-validation`
- Full reference: `docs/EcmaRegexTranslator.md`, `docs/EcmaRegexTranslations.md`

---
> Source: [corvus-dotnet/Corvus.JsonSchema](https://github.com/corvus-dotnet/Corvus.JsonSchema) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
