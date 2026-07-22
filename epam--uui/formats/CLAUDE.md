# uui

> **UUI** (EPAM Unified UI) is a React-based components and accelerators library built by EPAM Systems. This is a monorepo managed with **Lerna** and **Yarn Workspaces**, containing multiple packages for themeable components, headless core components, and styled theme packages.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/uui/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# UUI Project - Agent Guidelines

## 1) Project Overview

**UUI** (EPAM Unified UI) is a React-based components and accelerators library built by EPAM Systems. This is a monorepo managed with **Lerna** and **Yarn Workspaces**, containing multiple packages for themeable components, headless core components, and styled theme packages.

### Architecture

- **Monorepo structure**: Multiple packages managed with Lerna and Yarn Workspaces
- **Local development**: Entire repository built by Create React App (CRA) with watch mode
- **Production builds**: Each workspace built separately using individual build processes

### Key Packages

- `@epam/uui` — Ready-to-use, themeable components (**new components go here**)
- `@epam/uui-components` — Legacy package with logic-only components (no visual styles)
- `@epam/uui-core` — Core interfaces, types, services, data sources, hooks, and utilities
- `@epam/loveship`, `@epam/electric`, `@epam/promo` — Styled theme packages
- `@epam/uui-editor` — Slate.js-based Rich Text Editor
- `@epam/uui-timeline` — Gantt-chart like interfaces
- `@epam/assets` — Icons set, built-in themes and fonts
- `@epam/uui-test-utils` — Helpers for unit tests
- `@epam/uui-docs` — Utilities for docs site (DocBuilder, demo data, Property Explorer contexts). Needed when working on documentation
- `@epam/uui-build` — Build scripts, linting config, npm scripts
- `@epam/uui-db` — Client-side relational state cache
- `templates/` — Project templates (CRA, Next.js, Vite)
- `next-demo/` — Next.js demo apps for integration testing

## 2) Development Environment

### Requirements

- **Node.js**: >= 18.x
- **Package Manager**: Yarn
- **Git**: Fork-and-Pull workflow

### Setup Instructions

1. Clone the repository:
   ```bash
   git clone git@github.com:epam/UUI.git
   ```

2. Install dependencies:
   ```bash
   yarn
   cd ./server
   yarn
   cd ..
   ```

3. Build server and start development app:
   ```bash
   yarn build-server
   yarn start
   ```
   This opens uui.epam.com locally in watch mode.

### Workspace Commands

- `yarn start` — Run development app (opens documentation site)
- `yarn start-server` — Start Node.js server for docs site
- `yarn watch-server` — Start server in watch mode

## 3) Build & Test Commands

### Build Commands

- `yarn build` — Build all packages
- `yarn build-dev` — Build app for development
- `yarn build-modules` — Build all workspace modules
- `yarn build-server` — Build Node.js server

### Test Commands

**Unit Tests:**
- `yarn test` — Run all unit tests
- `yarn test-watch` — Run tests in watch mode
- `yarn test-update` — Update test snapshots
- `yarn test-report` — Generate test coverage report (saves to `.reports/unit-tests`)
- `yarn test-typecheck` — TypeScript type checking

**E2E Tests:**
- `yarn test-e2e` — Run E2E tests (Playwright)
- `yarn test-e2e-chromium` — Run E2E tests in Chromium only
- `yarn test-e2e-update` — Update E2E screenshots
- `yarn test-e2e-open-report` — Open E2E test report

**Note for Windows users:** If encountering test errors, use reduced worker count:
```bash
yarn test --maxWorkers=2 --testTimeout=10000
```
You can increase `maxWorkers` up to 4 if needed.

### Validation Commands

- `yarn eslint` — Run ESLint
- `yarn eslint-fix` — Run ESLint with auto-fix
- `yarn stylelint` — Run Stylelint
- `yarn stylelint-fix` — Run Stylelint with auto-fix
- `yarn track-bundle-size` — Check if bundle sizes exceed baseline (PR quality check)
- `yarn track-bundle-size-override` — Override baseline with current sizes (use only if sizes are expected to increase)

### Other Commands

- `yarn generate-components-api` — Generate Property Explorer data and API references
- `yarn generate-theme-tokens` — Generate theme CSS variables from Figma JSON
- `yarn process-icons` — Update icons from Figma (place icons in `icons-source` folder first)

## 4) Code Style & Conventions

### Component Architecture

- **New components** must be created in `uui/components/`, **not** `uui-components/`
- See [.cursor/skills/components/SKILL.md](.cursor/skills/components/SKILL.md) for `withMods`, `forwardRef`, styling patterns, and examples

### Linting & Formatting

- ESLint configuration: extends `uui-build/linting/eslintrc.base.js`
- Stylelint for CSS/SCSS/LESS files
- Pre-commit hooks via Husky and lint-staged

### TypeScript

- TypeScript 5.4.2 (enforced via resolutions)
- Type checking: `yarn test-typecheck`
- Project uses strict TypeScript configuration

### File Organization

- Test files: `__tests__/**/*.test.{js,ts,tsx}` pattern
- Components: `uui/components/` for new components
- Documentation: `app/src/docs/` for documentation site
- Preview configs: `app/src/docs/explorerConfigs` for Property Explorer

## 5) Testing Guidelines

- Add unit tests for bug fixes and new functionality
- Update snapshots when UI changes: `yarn test-update`
- Run full test suite before committing: `yarn test`
- Consider E2E/screenshot tests for UI changes
- See [.cursor/skills/unit-testing/SKILL.md](.cursor/skills/unit-testing/SKILL.md) for test patterns and `@epam/uui-test-utils` usage
- See [.cursor/skills/e2e-testing/SKILL.md](.cursor/skills/e2e-testing/SKILL.md) for Playwright screenshot and E2E tests

## 6) Security Considerations

- Be cautious with `dangerouslySetInnerHTML` — sanitize content before rendering
- Never commit API keys, tokens, or credentials
- Sensitive areas: `server/` folder (API endpoints), authentication logic

## 7) PR/Commit Guidelines

- Create branches from `develop` (not `main`): `fix/123-description`, `feature/456-description`
- Include GitHub issue number in branch name when applicable
- Add entry to `changelog.md` for every change (see [.cursor/skills/pr-contributing/SKILL.md](.cursor/skills/pr-contributing/SKILL.md) for format)
- Target `develop` branch for PRs
- See [.cursor/skills/pr-contributing/SKILL.md](.cursor/skills/pr-contributing/SKILL.md) for full PR checklist, commit messages, and quality gates

## Resources

- **Skills** (in `.cursor/skills/`): components, documentation, e2e-testing, unit-testing, pr-contributing, themes, release-workflow, github-issue-workflow, **data-sources**, **services-context**
- **Documentation**: https://uui.epam.com
- **Contributing Guide**: [CONTRIBUTING.md](CONTRIBUTING.md)
- **Developer Guides**: See [dev-docs/](dev-docs/) folder:
  - [dev-docs/overview.md](dev-docs/overview.md) — Project overview and monorepo layout
  - [dev-docs/dev-workflows.md](dev-docs/dev-workflows.md) — Local development workflows
  - [dev-docs/uui-documentation.md](dev-docs/uui-documentation.md) — Editing documentation
  - [dev-docs/e2e-tests.md](dev-docs/e2e-tests.md) — E2E and screenshot testing
  - [dev-docs/release-workflow.md](dev-docs/release-workflow.md) — Release workflow (maintainers)

---
> Source: [epam/UUI](https://github.com/epam/UUI) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
