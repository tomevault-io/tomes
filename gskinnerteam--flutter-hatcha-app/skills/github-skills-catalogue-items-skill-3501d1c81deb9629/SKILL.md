---
name: catalogue-items
description: Project file conventions for GenUI catalogue items. Use when: adding a new widget to the catalogue, following the 5-step file convention, naming CatalogItem files, writing example data, using leaf/container/three-tier/factory patterns, working with ChildrenResolver, atomic components, nested GenUI controllers, or module sizing. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# Creating GenUI Catalogue Items

This skill guides you through creating catalogue items — the bridge between AI-generated JSON and themed Flutter widgets.

## When to Use

- Adding a new widget type to the GenUI catalogue
- Following the 5-step file convention for catalogue item files
- Writing example data (leaf vs container export rules)
- Using leaf, container, three-tier, or factory patterns
- Working with `ChildrenResolver` for container items
- Creating atomic components or nested GenUI controllers
- Module sizing with `AppModuleCard`

> **Package API**: For `CatalogItem`, `CatalogItemContext`, `DataModel`, `DataContext`, `A2uiSchemas` reference types, and the data binding pattern, see the `genui` skill. For building schemas with `S.object`, `S.string`, etc., see the `json-schema-builder` skill.

## Pre-requisites

Before creating a catalogue item, review the reference examples for advanced topics (DataModel updates, dataBinding, nested controllers, ChildrenResolver shapes, three-tier pattern).

---

## 1. File Structure (5-Step Convention)

Every catalogue item file MUST contain these 5 sections **in this exact order**:

```dart
// 1. _name — PascalCase, matches CatalogItem.name
final _name = 'MyWidget';

// 2. _schema — JSON schema defining the AI contract
final _schema = S.object(
  description: '...',
  properties: { /* ... */ },
  required: ['...'],
);

// 3. Extension type — Private, type-safe data accessor
extension type _MyWidgetData.fromMap(Map<String, Object?> _json) {
  String get label => _json['label'] as String;
}

// 4. Example data — Stringified JSON for dev/debug previews
final myWidgetExampleData = '''
"$_name": {
  "label": "Hello"
}
''';

// 5. CatalogItem — The public export wiring everything together
final myWidget = CatalogItem(
  name: _name,
  dataSchema: _schema,
  exampleData: [
    () => '[{"id":"root","component":{$myWidgetExampleData}}]',
  ],
  widgetBuilder: (itemContext) {
    final data = _MyWidgetData.fromMap(itemContext.data as Map<String, Object?>);
    return Text(data.label);
  },
);
```

### Naming Conventions

| Element        | Convention                             | Example                 |
| -------------- | -------------------------------------- | ----------------------- |
| `_name`        | Private, PascalCase string             | `'MeterGauge'`          |
| `_schema`      | Private `final`                        | `_schema`               |
| Extension type | Private, `_` prefix + `Data` suffix    | `_MeterGaugeData`       |
| Example data   | Public, lowerCamelCase + `ExampleData` | `meterGaugeExampleData` |
| CatalogItem    | Public, lowerCamelCase                 | `meterGauge`            |

### Example Data Rules

- Always a stringified JSON array with `"id": "root"` as the root component
- Use `$_name` or `${_name}` to reference the catalogue item name
- Reference other items' example data via their exported names

**Container items** (those with `componentArrayReference` or `componentReference`): Do NOT export example data as a public constant. Keep it inline within `CatalogItem.exampleData` to prevent other items from importing full component trees.

**Leaf items** (no children): Export example data as a public constant so container items can reference it.

See [leaf example](./references/leaf-example.md) and [container example](./references/container-example.md) for complete templates.

---

## 2. Widget Patterns

> For `CatalogItem` constructor API, `CatalogItemContext` properties, and data binding patterns, see the `genui` skill's [catalog-api.md](../genui/references/catalog-api.md) and [data-binding.md](../genui/references/data-binding.md).
> For schema types (`S.object`, `S.string`, etc.) and the `A2uiSchemas` vs `S.*` decision, see the `genui` skill's [data-binding.md](../genui/references/data-binding.md) and the `json-schema-builder` skill.

### Schema Description Best Practices

The `description` **is the system prompt for the AI**. Be explicit:

- **Bad**: `"A list of labels."`
- **Good**: `"Ordinal text array (e.g., [\"\$\", \"\$\$\"]). Length 2-6. Each label max 5 characters."`

Include constraints (min/max counts, value ranges, expected formats).

### Leaf Widget Pattern

No children — return a widget directly from `widgetBuilder`. Export example data as a public constant.

See [leaf example](./references/leaf-example.md).

### Container Widget Pattern

Uses `componentArrayReference` or `componentReference` for children. Use `ChildrenResolver` to handle all child reference shapes (static lists, data bindings, templates).

```dart
import 'package:hatcha/design_system/widgets/children_resolver.dart';

widgetBuilder: (context) {
  final data = _MyContainerData.fromMap(context.data as Map<String, Object?>);

  return ChildrenResolver(
    childrenData: data.childIds,      // The raw childIds value from JSON
    dataContext: context.dataContext,
    buildChild: context.buildChild,
    builder: (children) {
      if (children.isEmpty) return const SizedBox.shrink();
      return Column(children: children);
    },
  );
},
```

Keep example data inline (not exported) for container items. See [container example](./references/container-example.md).

### Interactive Widget Pattern

Form widgets exist in separate subdirectories per context:

| Variant     | Directory                       | Purpose                                   |
| ----------- | ------------------------------- | ----------------------------------------- |
| Interactive | `guest_invite/` or `interview/` | User fills out forms, writes to DataModel |

---

## 3. Registering & Advanced Patterns

### Registering a Catalogue Item

After creating the file, add the item to the appropriate `Catalog` list. Items are gathered in catalogue aggregation files (e.g., `interview_input_catalogue_item.dart`) and passed to the `Catalog` constructor.

### Factory-Pattern Catalogue Items

When a catalogue item needs injected context (e.g. `eventId`, `moduleId`) not available in a static export, use a factory function:

```dart
CatalogItem moduleCard(String eventId, String moduleId) {
  return CatalogItem(
    name: _name,
    dataSchema: _schema,
    widgetBuilder: (itemContext) {
      return _ModuleCardWidget(eventId: eventId, moduleId: moduleId, ...);
    },
  );
}
```

Register factory items inside the controller's `catalog` getter (not as a static top-level constant):

```dart
@override
Catalog get catalog => Catalog([
  moduleCard(eventId, moduleId), // factory — receives injected context
  keyValueGrid,                  // static items
]);
```

---

## 4. Nested GenUI Controller Pattern

Some catalogue items create their own **internal GenUI controller** for complex nested UI. The item instantiates a controller with a mini-catalogue and its own system prompt.

```dart
class _MyWidgetState extends State<_MyWidget> {
  late final GenUiController _internalController;
  String? _surfaceId;

  @override
  void initState() {
    super.initState();
    _internalController = $genUi.getController(
      MyInternalController(data: widget.data),
    )..addEventHandlers(
        key: this,
        onSurfaceAdded: (data) {
          if (!mounted) return;
          setState(() => _surfaceId = data.surfaceId);
        },
        onSurfaceRemoved: (data) {
          if (!mounted) return;
          if (_surfaceId == data.surfaceId) setState(() => _surfaceId = null);
        },
      );
    _surfaceId = _internalController.activeSurfaceId;
    if (_internalController.activeSurfaceId == null &&
        !_internalController.isProcessing.value) {
      _internalController.sendMessage('initial_data: ${widget.data}');
    }
  }

  @override
  void dispose() {
    _internalController.removeEventHandlers(this);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AppGenUiSurface(controller: _internalController, surfaceId: _surfaceId);
  }
}
```

Use when: the item needs to orchestrate multiple dynamic child components, requires its own system prompt, or needs complete isolation from the parent UI tree.

---

## 5. Atomic Components Pattern

For space-constrained layouts (compact cards, dense displays), use atomic components with minimal properties and preset styling via `context.styles`.

**Available atomic components** (`lib/design_system/catalogue_items/atomic/`):

- `Text` — `content` + `weight` (light/normal/medium), uses `caption` (12px)
- `Header` — `content`, uses `body2` (14px)
- `Column` — `childIds` + `spacing` (none/tight/normal/loose)
- `Row` — `childIds` + `spacing` (none/tight/normal/loose)
- `MiniChecklist` — `header`, `items[]` with `label` + optional `subitems`, `selectedValues` state ref

**Spacing presets**: none=0, tight=4px, normal=8px, loose=16px

Use when: space-constrained cards (~250×294px), information-dense layouts, controllers needing ≤5 components. Limit depth to 3 levels (Column → Row → Text).

---

## 6. Module Sizing (AppModuleCard)

`AppModuleCard` (`lib/design_system/widgets/app_module_card.dart`) is the standard container for dashboard modules and charts.

- **Width**: `double.infinity`
- **Height**: Content-driven (no fixed constraint)
- **`AppModuleCard.cardHeight`**: Legacy constant (`300.0`) for charts that self-constrain via `ConstrainedBox`

```dart
// Charts: self-constrain height
ConstrainedBox(
  constraints: BoxConstraints(maxHeight: AppModuleCard.cardHeight),
  child: YourChartWidget(...),
);

// Content cards: no height constraint
AppModuleCard(title: data.title, child: YourContentWidget(...));
```

### Styling

Access styles ONLY via `context.styles` and `context.colors` (BuildContext extensions). Never hardcode colors or text styles.

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
