---
name: json-schema-builder
description: Dart DSL for building and validating JSON Schemas (Draft 2020-12). Use when: defining schemas with S.object, S.string, S.list, S.integer, S.number, S.boolean, S.nil, S.combined, S.any, Schema, ObjectSchema, StringSchema, ListSchema, NumberSchema, IntegerSchema, BooleanSchema, NullSchema, working with schema validation, ValidationError, SchemaRegistry, or schema composition (allOf, anyOf, oneOf, not, if/then/else). Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# json_schema_builder Package — API Reference

The `json_schema_builder` package (v0.1.3) provides a fluent, type-safe Dart DSL for building, composing, and validating JSON Schemas compliant with **Draft 2020-12**. It is the schema backbone for GenUI catalogue item definitions.

## When to Use

- Defining `dataSchema` for a `CatalogItem`
- Building JSON schemas programmatically (any context)
- Working with `S.object`, `S.string`, `S.list`, or other schema factories
- Composing schemas with `allOf`, `anyOf`, `oneOf`, `not`, `if/then/else`
- Validating data against a schema
- Using `$ref` / `$defs` for schema reuse

---

## DSL Quick Reference

The `Schema` extension type wraps `Map<String, Object?>` and provides factory constructors for all schema types.

```dart
typedef S = Schema;  // Shortcut — use S.object(), S.string(), etc.
```

### Factory Constructors

| Constructor           | Returns         | Purpose                                          |
| --------------------- | --------------- | ------------------------------------------------ |
| `S.string()`          | `StringSchema`  | String with optional constraints                 |
| `S.integer()`         | `IntegerSchema` | Integer with optional range                      |
| `S.number()`          | `NumberSchema`  | Number (int or double) with optional range       |
| `S.boolean()`         | `BooleanSchema` | Boolean value                                    |
| `S.list()`            | `ListSchema`    | Array with item schemas                          |
| `S.object()`          | `ObjectSchema`  | Object with typed properties                     |
| `S.nil()`             | `NullSchema`    | Null value                                       |
| `S.any()`             | `Schema`        | No type constraint                               |
| `S.combined()`        | `Schema`        | Composition (allOf/anyOf/oneOf/not/if-then-else) |
| `S.fromMap(map)`      | `Schema`        | Wrap raw map                                     |
| `S.fromBoolean(bool)` | `Schema`        | `true` = accept all, `false` = reject all        |

---

## Schema Types

### StringSchema

```dart
S.string({
  String? title,
  String? description,
  List<Object?>? enumValues,     // Fixed choices
  Object? constValue,            // Exact match
  int? minLength,
  int? maxLength,
  String? pattern,               // Regex pattern
  String? format,                // 'email', 'date-time', 'date', 'time', 'ipv4', 'ipv6'
})
```

**Examples:**

```dart
S.string(description: 'User email.', format: 'email')
S.string(minLength: 3, maxLength: 20, pattern: r'^[a-z0-9]+$')
S.string(enumValues: ['horizontal', 'vertical'])
```

### ObjectSchema

```dart
S.object({
  String? title,
  String? description,
  Map<String, Schema>? properties,
  Map<String, Schema>? patternProperties,   // Regex-keyed property validation
  List<String>? required,
  Map<String, List<String>>? dependentRequired,
  Object? additionalProperties,             // Schema or bool
  Object? unevaluatedProperties,            // Schema or bool
  Schema? propertyNames,
  int? minProperties,
  int? maxProperties,
})
```

**Example:**

```dart
S.object(
  description: 'User profile.',
  required: ['id', 'email'],
  properties: {
    'id': S.string(minLength: 1),
    'email': S.string(format: 'email'),
    'age': S.integer(minimum: 18),
    'active': S.boolean(),
  },
  additionalProperties: false,
)
```

### ListSchema (Array)

```dart
S.list({
  String? title,
  String? description,
  Schema? items,                 // Schema for all items (after prefixItems)
  List<Schema>? prefixItems,     // Positional schemas (tuple validation)
  Object? unevaluatedItems,      // Schema or bool
  Schema? contains,              // At least one item must match
  int? minContains,
  int? maxContains,
  int? minItems,
  int? maxItems,
  bool? uniqueItems,
})
```

**Example:**

```dart
S.list(
  description: 'Tags list, 1-10 unique strings.',
  items: S.string(),
  uniqueItems: true,
  minItems: 1,
  maxItems: 10,
)
```

### NumberSchema

```dart
S.number({
  String? title,
  String? description,
  num? minimum,              // Inclusive
  num? maximum,              // Inclusive
  num? exclusiveMinimum,     // Exclusive
  num? exclusiveMaximum,     // Exclusive
  num? multipleOf,
})
```

### IntegerSchema

```dart
S.integer({
  String? title,
  String? description,
  int? minimum,
  int? maximum,
  int? exclusiveMinimum,
  int? exclusiveMaximum,
  num? multipleOf,
})
```

### BooleanSchema

```dart
S.boolean({String? title, String? description})
```

### NullSchema

```dart
S.nil({String? title, String? description})
```

---

## Core Schema Methods

| Method     | Signature                                                     | Purpose                      |
| ---------- | ------------------------------------------------------------- | ---------------------------- |
| `validate` | `Future<List<ValidationError>> validate(Object? data, {...})` | Validate data against schema |
| `toJson`   | `String toJson({String? indent})`                             | Convert to JSON string       |
| `value`    | `Map<String, Object?>`                                        | Raw underlying map           |
| `[]`       | `Object? operator [](String key)`                             | Access keyword by name       |

### Metadata Getters

All standard JSON Schema metadata keywords are accessible as properties:

```dart
schema.title         // String?
schema.description   // String?
schema.$comment      // String?
schema.defaultValue  // Object?
schema.examples      // List<Object?>?
schema.deprecated    // bool?
schema.readOnly      // bool?
schema.writeOnly     // bool?
```

---

## GenUI Integration

Schemas define the AI contract for `CatalogItem.dataSchema`. The `description` field in each property acts as a system prompt for the AI — be explicit about constraints.

```dart
final _schema = S.object(
  description: 'A slider for selecting a numeric value.',
  required: ['label', 'value'],
  properties: {
    'label': S.string(description: 'Display label above the slider.'),
    'value': A2uiSchemas.numberReference(
      description: 'State reference for the slider value. Range 0-100.',
    ),
    'min': S.number(description: 'Minimum value. Default 0.'),
    'max': S.number(description: 'Maximum value. Default 100.'),
  },
);
```

> Static display properties use raw `S.*` types. Editable / data-bound properties use `A2uiSchemas.*` references. See the `genui` skill's [data-binding reference](../genui/references/data-binding.md) for the full decision table.

---

## Advanced Topics

For schema composition (`allOf`/`anyOf`/`oneOf`/`not`/`if-then-else`), `$ref`/`$defs`, validation API, and advanced features, see [advanced.md](./references/advanced.md).

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
