# content-scope-scripts

> Generates TypeScript types from JSON Schema files. Used by `injected/` and `special-pages/` workspaces.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/content-scope-scripts/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Types Generator

Generates TypeScript types from JSON Schema files. Used by `injected/` and `special-pages/` workspaces.

## Structure

```
build-types.mjs     # Main entry — buildTypes(config)
json-schema.mjs     # Schema → TypeScript conversion logic
json-schema-fs.mjs  # File system utilities for schema resolution
unit-test/          # Unit tests
```

## Usage

```javascript
import { buildTypes } from "../types-generator/build-types.mjs";

const config = {
    "featureName": {
        "schema": "path/to/schema.json",
        "types": "path/to/output/types.d.ts",
        "kind": "settings"  // or "messages"
    }
};

buildTypes(config);  // writes directly to disk
```

Two mapping kinds:
- **`SettingsKind`** — schemas representing feature settings → TypeScript types
- **`MessagesKind`** — messaging schemas → TypeScript types integrated with `@duckduckgo/messaging`

## Rules

- **Never manually edit generated `.ts` files** — they are overwritten on each run
- The script **fails fast** — errors are not caught, to ensure visibility during type generation
- Platform-specific exclusions can be specified per mapping entry

## Testing

```shell
# Run from types-generator/ directory
npm test
```

---
> Source: [duckduckgo/content-scope-scripts](https://github.com/duckduckgo/content-scope-scripts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
