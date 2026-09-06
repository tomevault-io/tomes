---
name: solid-floating-ui
description: > Use when this capability is needed.
metadata:
  author: lxsmnsyc
---

Build the thing from the matching recipe. Do not improvise the wiring.

## Pick the recipe

| The user wants                                          | Read                        |
| ------------------------------------------------------- | --------------------------- |
| Hover or focus label on a control                       | `reference/tooltip.md`      |
| Click-triggered panel anchored to a button              | `reference/popover.md`      |
| Centred modal with a backdrop                           | `reference/dialog.md`       |
| Listbox, select or combobox with keyboard navigation    | `reference/select.md`       |
| Dropdown menu, submenus, menu bar                       | `reference/menu.md`         |
| Right-click menu                                        | `reference/context-menu.md` |
| Element that follows the pointer                        | `reference/cursor.md`       |
| Toolbar, tab list or grid with arrow keys, not floating | `reference/composite.md`    |
| Fade or scale the element in and out                    | `reference/transition.md`   |
| A row of tooltips sharing one delay                     | `reference/delay-group.md`  |
| A pointer or arrow on the floating element              | `reference/arrow.md`        |

Read `reference/api.md` first whenever the task is not a straight copy of one
recipe, or when something built from a recipe is not updating.

Combine recipes freely. They share one shape, so a select inside a dialog is
the two files' hooks passed to one `useInteractions`.

## The four rules that break everything when broken

1. **Options are getters.** Anything that changes is `get open() { return open(); }`, never a captured value and never destructured. You never declare what an option depends on.
2. **Return values are getters too.** Keep the object and read through it where the value is used: `floating.placement`, not `const { placement } = floating`.
3. **Accessors in, callbacks out.** Anything the library reads from you takes `() => T`: `items`, `labels`, `scrollElement`, the `arrow` element, a portal `root`, `initialFocus`, `returnFocus`. Anything it produces arrives through a callback: `onElementsChange`, `onLabelsChange`, `onVirtualItemChange`, `onOverflowChange`. There are no ref containers.
4. **Spread the prop getters once.** `{...interactions.getFloatingProps()}` in the markup stays live on its own. Never call it inside a loop; that is what `getItemProps` is for.

## Install

```bash
pnpm add @floating-ui/dom solid-floating-ui
```

`@floating-ui/dom` and `solid-js` are peer dependencies. The package ships JSX
uncompiled through the `solid` export condition, so a Vite project using
`vite-plugin-solid` needs no extra configuration.

## Check the work

- Does every changing option go through a getter?
- Is `useDismiss` present? Almost every floating element needs it.
- Is `useRole` present? It supplies the ARIA wiring the pattern needs.
- Is the element inside `FloatingPortal` when an ancestor clips or stacks it?
- Does an interactive element have `FloatingFocusManager` around it?

---
> Source: [lxsmnsyc/solid-floating-ui](https://github.com/lxsmnsyc/solid-floating-ui) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
