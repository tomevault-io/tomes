---
name: theming
description: Theme system for the Hatcha app. Use when: working with colors, typography, spacing, dark/light mode, design tokens, AppStyle, context.styles, $theme, $palette, AppColors, AppText, or any styling. Covers all design token tables, palette system, file structure, and customization patterns. Use when this capability is needed.
metadata:
  author: gskinnerTeam
---

# Theme System Guide

**NOTE**: This system is not in a complete state — it has been stubbed in.

The app uses a centralized theme system with design tokens accessible via `context.styles` (BuildContext extension) and `$theme` / `$palette` from `service_locator.dart`.

## When to Use

- Styling any widget (colors, typography, spacing, corners, shadows)
- Adding new design tokens
- Working with dark/light mode or palette switching
- Understanding the responsive scaling system

---

## Quick Reference

```dart
// Via BuildContext extension (preferred)
context.styles.colors.primaryA1     // Palette colors
context.styles.text.h1              // Typography
context.styles.insets.md            // Spacing
context.styles.corners.lg           // Border radius
context.styles.shadows.card         // Shadows
context.styles.times.fast           // Animation durations

// Shorthand extensions
context.colors                      // = context.styles.colors
context.textStyles                  // = context.styles.text

// Globals (service_locator.dart)
$theme.toggleTheme()                // Toggle dark/light
$theme.isDarkMode                   // Check current mode
$palette.setPalette(palette)        // Switch color palette
```

---

## File Structure

```
lib/
├── service_locator.dart                    # $theme, $palette accessors + updateAppStyle()
├── core/logic/
│   ├── theme_controller.dart               # Dark/light mode controller
│   └── palette_controller.dart             # Swappable color palette controller
└── design_system/
    ├── styles/
    │   ├── styles.dart                     # AppStyle, AppText, AppInsets + AppStyleContext extension
    │   ├── colours.dart                    # AppColors, AppColorPalette tokens (light/dark)
    │   └── color_utils.dart                # Color manipulation utilities
    └── widgets/
        └── app_scaffold.dart               # AppStyleScope provider wrapper
```

---

## Accessing Styles

### `AppStyleContext` Extension (preferred)

Defined in `styles.dart`, provides three getters on `BuildContext`:

```dart
extension AppStyleContext on BuildContext {
  AppStyle get styles => AppStyleScope.of(this);
  AppColors get colors => styles.colors;
  AppText get textStyles => styles.text;
}
```

`AppStyleScope` is an `InheritedWidget` set up in `app_scaffold.dart` that provides `AppStyle` to all descendants.

> **`$styles` is deprecated.** Always use `context.styles` instead.

---

## Colors (`context.colors`)

### Background

| Token       | Light       | Dark              | Use Case                 |
| ----------- | ----------- | ----------------- | ------------------------ |
| `surface`   | White       | Black (#000000)   | Main surface             |
| `container` | Light grey  | 5% white opacity  | Containers, subtle depth |
| `highlight` | Medium grey | 30% white opacity | Highlighted areas        |

### Text

| Token           | Use Case                                   |
| --------------- | ------------------------------------------ |
| `textPrimary`   | Primary text content                       |
| `textSecondary` | Body text, secondary content (50% opacity) |
| `textTertiary`  | Tertiary/muted text                        |

### Raised (Elevated Surfaces)

| Token          | Use Case                 |
| -------------- | ------------------------ |
| `raisedStrong` | Strong elevation         |
| `raisedMedium` | Medium elevation (cards) |
| `raisedFaint`  | Subtle elevation         |

### Inset (Recessed Areas)

| Token         | Use Case                 |
| ------------- | ------------------------ |
| `insetStrong` | Deep inset (30% black)   |
| `insetMedium` | Medium inset (20% black) |
| `insetFaint`  | Subtle inset (10% black) |

### Stroke (Borders & Dividers)

| Token          | Use Case                      |
| -------------- | ----------------------------- |
| `stkPrimary`   | Primary borders, strong lines |
| `stkSecondary` | Standard borders              |
| `stkTertiary`  | Subtle dividers, separators   |

### Status

| Token       | Use Case                          |
| ----------- | --------------------------------- |
| `success`   | Success messages, completed steps |
| `attention` | Warnings, cautions, pending items |
| `critical`  | Errors, destructive actions       |

---

## Palette System (`$palette` / `context.colors`)

Colors are **not hardcoded** — they come from a swappable `AppColorPalette`. This enables per-event theming and brand switching.

### `AppColorPalette` (4 swappable tokens)

| Token          | Default                   | Description         |
| -------------- | ------------------------- | ------------------- |
| `primaryA1`    | `#FFE5C07B` (gold)        | Primary theme color |
| `supportA2`    | `#FF5E4A26` (dark brown)  | Support accent      |
| `complementB1` | `#FF8A7BFF` (purple)      | Complement color    |
| `supportB2`    | `#FF2B2452` (dark purple) | Support secondary   |

### Factory Constructors

| Factory                            | Description                      |
| ---------------------------------- | -------------------------------- |
| `AppColorPalette.defaultPalette()` | Gold/warm brand (home/event hub) |
| `AppColorPalette.noTheme()`        | Grayscale baseline               |
| `AppColorPalette.eventDefault()`   | Event context (same as default)  |

### `PaletteController` (`$palette`)

A `ChangeNotifier` that manages palette switching:

```dart
$palette.setPalette(AppColorPalette palette)  // Set custom palette
$palette.setDefaultPalette()                   // Gold/warm brand
$palette.setNoThemePalette()                   // Grayscale
$palette.setEventPalette()                     // Event default
$palette.currentPalette                        // Get current palette
```

### Palette → AppColors Integration

Palette tokens are directly accessible via `context.colors`:

```dart
context.colors.primaryA1       // e.g., #FFE5C07B
context.colors.supportA2       // e.g., #FF5E4A26
context.colors.complementB1    // e.g., #FF8A7BFF
context.colors.supportB2       // e.g., #FF2B2452
```

Derived gradients:

```dart
context.colors.graphSpectrumGradient  // [supportA2, primaryA1, complementB1, supportB2]
context.colors.rsvpHandleGradient     // [primaryA1, supportA2]
```

### Theme-Scoped Palette Changes

Use `EventThemeBuilder` widget to apply a palette to a widget subtree. `updateAppStyle()` in `service_locator.dart` accepts an optional `palette` parameter to rebuild `AppStyle` with new colors.

---

## Typography (`context.textStyles`)

Display text uses **EB Garamond**; body/UI text uses **Lato**. All styles scale responsively.

| Token          | Size | Weight        | Font        | Use Case            |
| -------------- | ---- | ------------- | ----------- | ------------------- |
| `displayLarge` | 45px | Regular (400) | EB Garamond | Hero text           |
| `h1`           | 32px | Medium (500)  | EB Garamond | Page titles         |
| `h2`           | 24px | Medium (500)  | Lato        | Section headers     |
| `body1`        | 16px | Medium (500)  | Lato        | Primary body text   |
| `body1Light`   | 16px | Light (300)   | Lato        | Secondary body text |
| `body2`        | 14px | Medium (500)  | Lato        | Small body text     |
| `caption`      | 12px | Medium (500)  | Lato        | Captions, labels    |
| `captionLight` | 12px | Regular (400) | Lato        | Light captions      |
| `btn`          | 14px | Medium (500)  | Lato        | Button text         |

Apply color with `copyWith`:

```dart
Text('Error', style: context.textStyles.body1.copyWith(color: context.colors.critical))
```

---

## Spacing (`context.styles.insets`)

Values scale responsively based on device size.

| Token    | Base Value | Description            |
| -------- | ---------- | ---------------------- |
| `xxs`    | 4px        | Micro spacing          |
| `xs`     | 8px        | Tight spacing          |
| `sm`     | 12px       | Compact spacing        |
| `md`     | 16px       | Standard spacing       |
| `lg`     | 24px       | Comfortable spacing    |
| `xl`     | 32px       | Section spacing        |
| `xxl`    | 40px       | Large section spacing  |
| `offset` | 80px       | Special offset layouts |

---

## Corners (`context.styles.corners`)

| Token  | Value | Use Case                 |
| ------ | ----- | ------------------------ |
| `sm`   | 4px   | Subtle rounding          |
| `md`   | 8px   | Standard cards           |
| `lg`   | 16px  | Prominent elements       |
| `xl`   | 24px  | Modals, sheets           |
| `full` | 999px | Pills, circular elements |

---

## Shadows (`context.styles.shadows`)

| Token            | Type              | Description             |
| ---------------- | ----------------- | ----------------------- |
| `textSoft`       | `List<Shadow>`    | Subtle text depth       |
| `text`           | `List<Shadow>`    | Standard text shadow    |
| `textStrong`     | `List<Shadow>`    | High contrast text      |
| `cardSoft`       | `List<BoxShadow>` | Subtle card elevation   |
| `card`           | `List<BoxShadow>` | Standard card elevation |
| `cardStrong`     | `List<BoxShadow>` | High elevation (modals) |
| `insetHighlight` | `List<BoxShadow>` | Inner highlight effect  |

---

## Animation Timings (`context.styles.times`)

| Token            | Duration | Use Case             |
| ---------------- | -------- | -------------------- |
| `fast`           | 300ms    | Micro-interactions   |
| `med`            | 600ms    | Standard transitions |
| `slow`           | 900ms    | Emphasis             |
| `extraSlow`      | 1300ms   | Dramatic effect      |
| `pageTransition` | 200ms    | Page transitions     |

---

## Sizes (`context.styles.sizes`)

| Token              | Value   | Description            |
| ------------------ | ------- | ---------------------- |
| `maxContentWidth1` | 800px   | Large containers       |
| `maxContentWidth2` | 600px   | Medium containers      |
| `maxContentWidth3` | 500px   | Small containers       |
| `minAppSize`       | 380×650 | Minimum app constraint |

---

## Dark/Light Mode

```dart
$theme.toggleTheme()              // Toggle
$theme.setThemeMode(ThemeMode.dark)  // Force dark
$theme.setThemeMode(ThemeMode.light) // Force light
$theme.isDarkMode                 // Check
```

How it works: `ThemeController` (ChangeNotifier in GetIt) → `AppScaffold` watches it → `AppStyle` recreated with `isDark` flag → all tokens auto-switch.

---

## Customization

### Adding colors

Edit `lib/design_system/styles/colours.dart`:

```dart
Color get brandTertiary => isDark ? const Color(0xFF...) : const Color(0xFF...);
```

### Adding text styles

Edit `AppText` in `styles.dart`:

```dart
late final TextStyle myCustomStyle = _createFont(font, sizePx: 18, heightPx: 24, spacingPc: 2, weight: FontWeight.w600);
```

### Adding spacing

Edit `AppInsets` in `styles.dart`:

```dart
late final double custom = 40 * _scale;
```

---

## Rules

- Access styles ONLY via `context.styles`, `context.colors`, `context.textStyles` — never use `$styles` (deprecated) or hardcode colors
- Extend styles with `copyWith` — don't create `TextStyle()` from scratch (loses font family and scaling)
- Use the spacing scale consistently — don't use arbitrary pixel values
- Use semantic token names — `context.colors.critical` not `Color(0xFFE01F1B)`
- Use palette tokens for brand/accent colors — `context.colors.primaryA1` not hardcoded hex

---
> Source: [gskinnerTeam/flutter-hatcha-app](https://github.com/gskinnerTeam/flutter-hatcha-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
