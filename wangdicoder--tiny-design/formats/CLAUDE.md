# tiny-design

> Tiny Design is a React component UI library (80+ components) published as `@tiny-design/react`. It's a pnpm monorepo managed with Turborepo.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/tiny-design/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

## Project Overview

Tiny Design is a React component UI library (80+ components) published as `@tiny-design/react`. It's a pnpm monorepo managed with Turborepo.

## Monorepo Layout

```
packages/react/    → @tiny-design/react (main component library)
packages/tokens/   → @tiny-design/tokens (v2 design tokens and theme runtime)
packages/icons/    → @tiny-design/icons (SVG icon components)
apps/docs/         → documentation site (Vite + MDX)
```

All three publishable packages use **fixed versioning** — they always share the same version number.

## Common Commands

```bash
pnpm install              # Install dependencies
pnpm dev                  # Start docs dev server
pnpm build                # Build all packages (turborepo handles dependency order: tokens → react → docs)
pnpm test                 # Run all tests
pnpm lint                 # ESLint across all packages
pnpm lint:style           # Stylelint for SCSS files
```

### Scoped Commands

```bash
pnpm --filter @tiny-design/react test -- --testPathPattern=button   # Test a single component
pnpm --filter @tiny-design/react test:update                        # Update snapshots
pnpm --filter @tiny-design/react test:coverage                      # Coverage report
```

## Component Structure

Every component in `packages/react/src/` follows this layout:

```
component-name/
├── component-name.tsx       # Implementation (React.forwardRef, function components)
├── types.ts                 # Props interfaces
├── index.tsx                # Barrel export
├── index.md                 # English docs
├── index.zh_CN.md           # Chinese docs
├── style/
│   ├── _index.scss          # Styles (SCSS partial)
│   └── index.tsx            # Style entry point
├── demo/
│   └── basic.tsx            # Usage examples
└── __tests__/
    └── component-name.test.tsx
```

When adding a new component:
1. Create its directory under `packages/react/src/`
2. Export it from `packages/react/src/index.ts`
3. Add a route in `apps/docs/src/routers.tsx`

## Code Conventions

- **TypeScript strict mode** is enabled
- **CSS class prefix**: `ty-` (e.g., `.ty-btn`, `.ty-modal`), customizable via `ConfigProvider`
- **BEM-ish naming**: `ty-component`, `ty-component__element`, `ty-component_modifier`
- **Ref forwarding**: all components use `React.forwardRef`
- **Props pattern**: extend `BaseProps` (style, className, prefixCls) + intrinsic element props
- **Formatting**: Prettier — single quotes, semicolons, 100 char width, 2-space indent
- **Commits**: Conventional Commits — `feat(button): add loading state`, `fix(modal): prevent scroll`
- **Pre-commit hook**: husky + lint-staged auto-fixes SCSS via stylelint

## Testing

- **Framework**: Jest + @testing-library/react + @testing-library/jest-dom
- **Config**: `packages/react/jest.config.js` (ts-jest, jsdom environment)
- Tests live in `__tests__/` within each component directory

## Build Pipeline

The react package build (`packages/react`):
1. `tsdown` — transpiles TS → JS (ESM in `es/`, CJS in `lib/`), generates `.d.ts`
2. `build-styles.js` — compiles component SCSS → CSS via Sass + PostCSS
3. `inject-style-imports.js` — adds CSS imports into JS entry files

## Changesets & Releases

- Use `pnpm changeset` to create a changeset file in `.changeset/`
- On merge to `master`, CI creates a "Version Packages" PR
- Merging that PR publishes to npm and deploys the docs site
- `@tiny-design/docs` is excluded from npm publishing

## Key Dependencies

- React 18.2+, TypeScript 5.4
- Popper.js (`@popperjs/core`) for positioning (tooltips, dropdowns, popovers)
- `react-transition-group` for animations
- `classnames` for conditional class construction
- Node.js >= 22, pnpm 10.x

---
> Source: [wangdicoder/tiny-design](https://github.com/wangdicoder/tiny-design) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
