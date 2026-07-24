---
name: corvus-keywords-and-validation
description: > Use when this capability is needed.
metadata:
  author: corvus-dotnet
---

# Keywords and Validation Handlers

## Keyword Architecture

Keywords are **stateless singletons** implementing `IKeyword` plus behavioral marker interfaces.

### IKeyword Interface

Every keyword implements:
- `Keyword` property — the JSON property name (e.g., `"type"`, `"maxLength"`)
- Behavioral marker interfaces that declare how the keyword participates in schema processing

### Behavioural Marker Interface Categories (25+)

1. **Schema structure** — type shape: `ISubschemaTypeBuilderKeyword`, `ILocalSubschemaRegistrationKeyword`, `IPropertySubchemaProviderKeyword`
2. **Validation** — runtime checks: `IObjectPropertyValidationKeyword`, `IValueKindValidationKeyword`, `INumericValidationKeyword`, `IStringValidationKeyword`, `IArrayValidationKeyword`
3. **Annotation & documentation** — `IAnnotationProducingKeyword`, `IShortDocumentationProviderKeyword`, `ILongDocumentationProviderKeyword`, `IDefaultValueProviderKeyword`, `IExamplesProviderKeyword`, `INonStructuralKeyword`, `IDeprecatedKeyword`
4. **References & identity** — `IRefKeyword`, `IDynamicRefKeyword`, `IIdKeyword`, `IAnchorKeyword`, `ISchemaKeyword`

## Vocabularies

Vocabularies are modular sets of keywords (introduced formally in Draft 2019-09):
- **Core** — `$id`, `$schema`, `$ref`, `$defs`
- **Applicator** — `allOf`, `anyOf`, `oneOf`, `if/then/else`, `properties`, `items`
- **Validation** — `type`, `minimum`, `maximum`, `pattern`, `required`
- **MetaData** — `title`, `description`, `default`, `examples`
- **Format** — `format` keyword (annotation in 2019-09+, assertion in earlier drafts)
- **Content** — `contentEncoding`, `contentMediaType`, `contentSchema`
- **Unevaluated** — `unevaluatedProperties`, `unevaluatedItems` (2019-09+)

## Validation Handler Priorities

Handlers execute in strict priority order (defined in `ValidationPriorities` static class in `src-v4/Corvus.Json.CodeGeneration/.../Validation/ValidationPriorities.cs`, shared by both V4 and V5):

| Priority | Name | Value | Purpose |
|----------|------|-------|---------|
| First | `First` | 0 | Must run before everything |
| CoreType | `CoreType` | 1,000 | Basic type checking (`type` keyword) |
| Default | `Default` | ~2.1 billion (`uint.MaxValue / 2`) | Standard validation (min/max, pattern, etc.) |
| Composition | `Composition` | Default + 1,000 | `allOf`, `anyOf`, `oneOf`, `not` |
| AfterComposition | `AfterComposition` | Composition + 1,000 | Keywords that depend on composition results (arrays, objects) |
| Last | `Last` | `uint.MaxValue` | Final cleanup, unevaluated properties/items |

The large gap between CoreType (1,000) and Default (~2.1B) leaves room for future priorities without redefining existing values.

## Draft-Specific Keyword Variations

Keywords change behavior across JSON Schema drafts:

| Keyword | Draft 4 | Draft 6+ |
|---------|---------|----------|
| `exclusiveMaximum` | Boolean modifier on `maximum` | Standalone number |
| `exclusiveMinimum` | Boolean modifier on `minimum` | Standalone number |
| `items` | Single schema or array | Single schema only in 2020-12 (`prefixItems` for array) |
| `additionalItems` | Used with array `items` | Removed in 2020-12 |
| `$ref` | Replaces all siblings | Coexists with siblings in 2019-09+ |

## Custom Keyword Extension Points (8)

The code generation engine exposes extension points at different phases:

1. **Schema discovery** — register custom schema locations
2. **Type declaration building** — modify type declarations during construction
3. **Type reduction** — control how trivial subschemas are collapsed
4. **Validation handler registration** — add custom validation code emitters
5. **Property handler** — customize how object properties are processed
6. **Array handler** — customize array item processing
7. **Format handler** — add custom format validators
8. **Composition handler** — customize allOf/anyOf/oneOf/not processing

## How Handlers and Keywords Fit Together

Validation handlers are **stateless singletons** registered with the `CSharpLanguageProvider`. Each handler declares which keyword marker interface it handles and optionally registers child handlers for sub-concerns.

### Handler registration

Handlers are registered in `CSharpLanguageProvider.CreateDefaultCSharpLanguageProvider()` (`src/Corvus.Text.Json.CodeGeneration/CSharpLanguageProvider.cs`):

```csharp
languageProvider.RegisterValidationHandlers(
    TypeValidationHandler.Instance,
    FormatValidationHandler.Instance,
    NumberValidationHandler.Instance,
    StringValidationHandler.Instance,
    ConstValidationHandler.Instance,
    CompositionAllOfValidationHandler.Instance,
    CompositionAnyOfValidationHandler.Instance,
    CompositionOneOfValidationHandler.Instance,
    CompositionNotValidationHandler.Instance,
    TernaryIfValidationHandler.Instance,
    ObjectValidationHandler.Instance,
    ArrayValidationHandler.Instance);
```

### Handler structure

Each handler extends `KeywordValidationHandlerBase` and implements three things:

```csharp
// From StringValidationHandler.cs
internal sealed class StringValidationHandler
    : TypeSensitiveKeywordValidationHandlerBase, IStringKeywordValidationHandler
{
    public static StringValidationHandler Instance { get; } = CreateDefault();

    // 1. Priority — controls execution order
    public override uint ValidationHandlerPriority => ValidationPriorities.Default;

    // 2. Keyword matching — dispatches on marker interfaces
    public override bool HandlesKeyword(IKeyword keyword)
    {
        return keyword is IStringValidationKeyword;
    }

    // 3. Child handlers for sub-concerns
    private static StringValidationHandler CreateDefault()
    {
        var result = new StringValidationHandler();
        result.RegisterChildHandlers(
            StringRegularExpressionValidationHandler.Instance,
            StringLengthValidationHandler.Instance);
        return result;
    }
}
```

### Execution flow

During code generation, `typeDeclaration.OrderedValidationHandlers()` retrieves handlers from the provider and sorts by `ValidationHandlerPriority`. Each handler emits setup code and validation code into the generated `Evaluate()` method in priority order.

## TypeDeclaration

The central data structure representing a resolved JSON Schema as a C# type:
- Holds the schema keywords, their values, and resolved references
- Tracks the type's place in the inheritance/composition hierarchy
- Type reduction collapses trivial subschemas for leaner generated code

## Common Pitfalls

- **Draft awareness**: Always check which draft(s) your keyword applies to. A keyword may have different semantics or not exist in certain drafts.
- **Priority order**: Putting a handler at the wrong priority can cause it to run before its dependencies are resolved.
- **Stateless keywords**: Keywords must be stateless singletons. State lives in `TypeDeclaration`.

## Cross-References
- For code generation, see `corvus-codegen`
- For the standalone evaluator's internal architecture, see `corvus-standalone-evaluator`
- For annotation flow, see `corvus-standalone-evaluator` (annotation pipeline section)
- Full guide: `docs/AddingKeywords.md`, `docs/ValidationHandlerGuide.md`

---
> Source: [corvus-dotnet/Corvus.JsonSchema](https://github.com/corvus-dotnet/Corvus.JsonSchema) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
