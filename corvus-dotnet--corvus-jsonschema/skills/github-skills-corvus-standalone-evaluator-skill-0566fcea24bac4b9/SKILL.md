---
name: corvus-standalone-evaluator
description: > Use when this capability is needed.
metadata:
  author: corvus-dotnet
---

# Standalone Schema Evaluator

## Overview

The standalone evaluator validates JSON against a schema and optionally collects
annotations — without generating full C# types. Useful for validation-only scenarios
or when you need annotation data (e.g., `readOnly`, `writeOnly`, `deprecated`).

## Generating Evaluator Code

### Via Source Generator

```csharp
[JsonSchemaTypeGenerator("schema.json", EmitEvaluator = true)]
public partial struct MySchema;
```

### Via CLI

```powershell
corvusjson jsonschema schema.json --codeGenerationMode SchemaEvaluationOnly --outputPath ./Evaluator
# Or for both types and evaluator:
corvusjson jsonschema schema.json --codeGenerationMode Both --outputPath ./Output
```

### Using the Generated Evaluator

The generated evaluator exposes a static `Evaluate<T>()` method. Pass any `IJsonElement<T>` value:

```csharp
using var doc = ParsedJsonDocument<JsonElement>.Parse("""{"name": "Alice", "age": 30}""");

// Simple validation — returns true if the instance is valid
bool isValid = MySchemaEvaluator.Evaluate(doc.RootElement);

// With annotation collection
var collector = new JsonSchemaResultsCollector();
bool isValid2 = MySchemaEvaluator.Evaluate(doc.RootElement, collector);
// collector now contains validation results and annotations
```

## Two-Pass Architecture

### Pass 1: Schema Discovery
Traverses the schema tree and builds a `SubschemaInfo` map:
- Assigns a unique identifier to each subschema
- Records which keywords are present
- Determines property patterns, required properties, composition structure

### Pass 2: Code Emission
Generates evaluation methods using the `SubschemaInfo` map:
- One method per subschema
- Methods chain together via composition keywords (allOf, anyOf, oneOf, not)

## Property Matchers

For schemas with named properties:
- **≤3 properties**: Sequential `if/else if` chain
- **≥4 properties**: Hash map for O(1) dispatch

Property matching uses UTF-8 byte-level comparison for zero-allocation matching.

## Required Property Tracking

Required properties tracked with `Span<uint>` bitmasks, stack-allocated:

```csharp
Span<uint> requiredBits = stackalloc uint[bitCount];
// Each required property sets its bit when encountered
// After processing, check all bits are set
```

## Regex Pattern Classification

Regex patterns are classified at code-generation time for optimal dispatch:

| Classification | When | Generated code |
|----------------|------|----------------|
| `Noop` | Pattern matches everything (e.g., `.*`) | Skip validation entirely |
| `NonEmpty` | Pattern requires non-empty string | Simple length check |
| `Prefix` | Pattern is a literal prefix | `StartsWith()` check |
| `Range` | Character range pattern | Inline range check |
| `FullRegex` | General pattern | Compiled `Regex` instance |

## Annotation Pipeline

### Collecting Annotations

```csharp
bool isValid = element.EvaluateSchema(collector);
// collector receives annotations during validation
```

**`Verbose` mode** is required for annotation collection.

### How Annotations Flow

- `IAnnotationProducingKeyword` keywords (like `readOnly`, `writeOnly`, `deprecated`)
  emit annotations during validation
- Annotations use the **IgnoredKeyword path divergence** pattern:
  `IgnoredKeyword` appends to the evaluation path only (not the instance path)
- `JsonSchemaAnnotationProducer.IsAnnotation()` distinguishes annotations from
  validation results

### Composition Behavior

| Keyword | Semantics |
|---------|-----------|
| `allOf` | AND — all subschemas must validate |
| `anyOf` | At least one subschema must validate |
| `oneOf` | Exactly one subschema must validate |
| `not` | Subschema must NOT validate |

Annotations from failed subschemas are discarded. In `anyOf`/`oneOf`,
only annotations from validating subschemas are collected.

## Discriminator Fast Paths

When a composition has a discriminator property (common in OpenAPI), the evaluator
generates an optimized fast path that checks the discriminator value first and
directly dispatches to the matching subschema, avoiding evaluation of all branches.

## Common Pitfalls

- **Missing Verbose mode**: Annotations are only collected in `Verbose` mode. Default mode skips annotation processing.
- **Unreduced types**: The evaluator uses unreduced type declarations to preserve the full schema structure. This differs from full type generation, which reduces trivial subschemas.
- **Path confusion**: The evaluation path and instance path are different concepts. Annotations append to evaluation path only.

## Cross-References
- For annotation system details, see `docs/AnnotationSystem.md`
- For evaluator internals, see `docs/StandaloneEvaluatorInternals.md`
- For the keyword system, see `corvus-keywords-and-validation`
- For code generation, see `corvus-codegen`

---
> Source: [corvus-dotnet/Corvus.JsonSchema](https://github.com/corvus-dotnet/Corvus.JsonSchema) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
