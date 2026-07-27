---
name: figma-import
description: Translates Figma designs into production-ready Flutter code. Use when: importing, implementing, or building UI from a Figma design, link, or node; user mentions 'implement design', 'generate code', 'implement component', provides Figma URLs, or asks to build widgets matching Figma specs. Covers the full workflow: URL parsing, MCP context fetching, design tokens, layout, icons, placeholders, component mapping, and validation. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# Figma Import & Implement Guide

## When to Use

- Importing or implementing UI from a Figma design, link, or node
- Building Flutter widgets from Figma component specifications
- Extracting design tokens from Figma variables
- Mapping Figma components to Flutter widgets
- User says "implement design", "generate code", "implement component", or provides a Figma URL

### Skill Boundaries

- Use this skill when the deliverable is **Flutter code** in the user's repository.
- If the user asks to **create/edit/delete nodes inside Figma** itself, switch to [figma-use](../figma-use/SKILL.md).

---

## Required Workflow

**Follow these steps in order. Do not skip steps.**

### Step 1: Parse the Figma URL

Extract `fileKey` and `nodeId` from the URL:

| URL Format                                          | fileKey          | nodeId               |
| --------------------------------------------------- | ---------------- | -------------------- |
| `figma.com/design/:fileKey/:name?node-id=X-Y`       | `:fileKey`       | `X-Y` → `X:Y`        |
| `figma.com/file/:fileKey/:name?node-id=X-Y`         | `:fileKey`       | `X-Y` → `X:Y`        |
| `figma.com/design/:fileKey/branch/:branchKey/:name` | use `:branchKey` | from `node-id` param |

Always convert `nodeId` hyphens to colons: `1234-5678` → `1234:5678`.

### Step 2: Fetch Design Context

Run `get_design_context` with the extracted file key and node ID.

This provides structured data including layout properties, typography, color values, design tokens, component structure, variants, spacing, and padding.

**If the response is too large or truncated:**

1. Run `get_metadata(fileKey, nodeId)` to get the high-level node map
2. Identify specific child nodes from the metadata
3. Fetch individual child nodes with `get_design_context(fileKey, childNodeId)`

### Step 3: Capture Visual Reference

Run `get_screenshot` with the same file key and node ID. This screenshot is the **source of truth** for visual validation. Keep it accessible throughout implementation.

### Step 4: Download Required Assets

Download any assets (images, icons, SVGs) returned by the Figma MCP server.

- If the MCP server returns a `localhost` source for an image or SVG, **use that source directly** — do not modify the URL
- Do NOT import or add new icon packages — all assets should come from the Figma payload
- Do NOT use placeholders if a `localhost` source is provided

### Step 5: Translate to Flutter

Translate the Figma output into Flutter code following the project conventions below. Treat the MCP output as a representation of design intent, not final code. Reuse existing widgets, design tokens, and patterns.

---

## Design Tokens

Use Figma variables and named text styles to match existing design tokens in `lib/design_system/styles/styles.dart` and `lib/design_system/styles/colours.dart`. Access tokens via BuildContext extensions:

```dart
context.styles.insets.md        // Spacing (xxs, xs, sm, md, lg, xl, xxl, offset)
context.styles.corners.lg       // Border radius
context.styles.shadows.card     // Shadows
context.styles.times.fast       // Animation durations

context.colors.primaryA1        // Palette colors (AppColors)
context.textStyles.body1        // Typography (AppText)
```

Assume tokens are not used 100% consistently in the design file — attempt to match raw values to tokens as appropriate. When a Figma value conflicts with an existing token, prefer the existing token if the difference is minor (e.g. 1–2px, near-identical color).

Use `get_variable_defs` via the Figma MCP server when encountering a new potential token.

### Colors

Color tokens live in `AppColors` / `AppColorPalette` (`lib/design_system/styles/colours.dart`).

Create local one-off opacity variations using `.withValues(alpha:)` if a close match does not exist as a token. Use multiples of 0.05 for alpha values. If an opacity variation repeats, ask if a new token should be added.

### Text Styles

Text style tokens live in `AppText` (`lib/design_system/styles/styles.dart`):
`displayLarge`, `displayMedium`, `h1`, `h2`, `body1`, `body1Light`, `body2`, `body2Light`, `caption`, `captionLight`, `btn`

Use `copyWith` to create local one-off variants. These can change style attributes like color, weight, and decorations, but **not** font family, size, or layout metrics (line height, letter-spacing). Ask before creating new text styles.

---

## Naming

Use names in Figma as a guide, but not a rule. They may not always be up to date, accurate, or semantic. Views should be named with a `View` suffix. Other widgets should use clear semantic names.

---

## Widgets

Default to `StatelessWidget`.

---

## Layout

Figma layout only provides a hint for implementation and may be incorrect or outdated. Use appropriate Flutter widgets to create responsive layouts based on context and design.

### Spacing

Extract padding and item spacing from Figma auto-layout properties. Match values to existing `context.styles.insets` tokens (xxs=4, xs=8, sm=12, md=16, lg=24, xl=32, xxl=40, offset=80) when possible. Use inline `const` values for one-off spacing that doesn't warrant a token.

### Dimensions

**Always** call `get_metadata` on nodes whose pixel size matters (dividers, spacing/padding, icons, indicators, fixed-height containers). Do NOT guess dimensions from screenshots or derive them from `get_design_context` CSS percentages — these are unreliable. Instance child node IDs (e.g. `I2:266;2:264`) are not valid for `get_metadata` — use the source component's child node ID (the part after the `;`, e.g. `2:264`) instead.

---

## Animation / Transitions

Unless explicitly specified, don't implement animations.

---

## Interaction / Functionality

Unless explicitly specified, don't implement interactions or specific functionality. Add an appropriate TODO instead. Also add a `debugPrint` call for mouse interactions, logging the widget name and interaction type:

```dart
onTap: () {
  debugPrint('SubmitButton tapped');
  // TODO: implement submit action
},
```

---

## Icons

The project uses a dual icon system:

1. **Material `Icons.*`** — for common UI icons (add, search, edit, delete, settings, etc.)
2. **`AppIcons` enum** (`lib/design_system/app_icons.dart`) — for branded/custom SVG icons mapped to `assets/images/_common/icons/`

Prefer `AppIcons` when a matching branded icon exists. Otherwise use `Icons.*` (Material). Never use raw `IconData` values. If no suitable match exists, use `Icons.square` as a placeholder and add a TODO with the Figma icon name.

---

## Images

Ask if the image should be exported (default to `assets/images/`), or a `Placeholder` used.

---

## Placeholders

Figma placeholder visuals (grey boxes with or without X patterns, named "placeholder" or similar) represent missing assets — do not replicate their appearance. Use:

- `Icons.square` — for items with names containing "icon", or smaller items
- `Placeholder()` — for items with names containing "image", "photo", etc., or larger items

---

## Components

When importing Figma components, consider making reusable public widgets, especially if a component is used more than once. Ask for clarification if unsure.

---

## Effects

- **Drop shadows** (`shadow-[*]`, non-inset) → `BoxShadow` in `BoxDecoration`
- **Backdrop blur** (`backdrop-blur-*`) → `BackdropFilter` + `ImageFilter.blur`
- **Opacity** (`opacity-*`) → `.withValues(alpha:)` or `Opacity` widget
- **Gradients** (`linear-gradient`, `radial-gradient`) → `LinearGradient` / `RadialGradient`

If you believe an effect is trivial, confirm with the user before omitting it.

---

## Completion Checklist

Before considering an implementation complete, validate the final UI against the Figma screenshot from Step 3.

### Visual Parity

- [ ] Layout matches (spacing, alignment, sizing)
- [ ] Typography matches (font, size, weight, line height)
- [ ] Colors match exactly
- [ ] Interactive states work as designed (hover, active, disabled)
- [ ] Responsive behavior follows Figma constraints
- [ ] Assets render correctly

### Effects Translation

Scan the generated code for these CSS patterns from `get_design_context` and verify each has a Flutter equivalent:

- `shadow-[*]` (non-inset) → `BoxShadow` in `BoxDecoration`
- `backdrop-blur-*` → `BackdropFilter` + `ImageFilter.blur`
- `opacity-*` → `.withValues(alpha:)` or `Opacity` widget
- Gradients (`linear-gradient`, `radial-gradient`) → `LinearGradient` / `RadialGradient`

### Design System Integration

- [ ] Existing project widgets reused where possible
- [ ] Design tokens used instead of hardcoded values
- [ ] Any deviations from Figma documented in code comments

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
