---
name: angular-best-practices-ngrx
description: > Use with the core `angular-best-practices` skill. Use when this capability is needed.
metadata:
  author: alfredoperez
---
# Angular Ngrx Best Practices

> Use with the core `angular-best-practices` skill.

---

## 1. NgRx State Management

**Impact: HIGH** (Global state)

### 1.1 Keep Reducers Pure

**Impact: HIGH** (Predictable state, testable, time-travel debugging)

Reducers must be pure functions: no side effects, no HTTP calls, no subscriptions. Only compute new state from action and current state. Move side effects to Effects.

**Example:**

```typescript
on(UsersActions.load, state => ({ ...state, loading: true }));
// HTTP call goes in UsersEffects
```

### 1.2 Use Feature Selectors

**Impact: MEDIUM** (Memoized selection, better performance)

Use `createFeatureSelector` and `createSelector` for memoized state selection. Selectors only recompute when their inputs change.

**Example:**

```typescript
const selectCounterState = createFeatureSelector<CounterState>('counter');
export const selectCount = createSelector(selectCounterState, s => s.count);
```

---

---
> Converted and distributed by [TomeVault](https://tomevault.io/claim/alfredoperez) — claim your Tome and manage your conversions.
<!-- tomevault:4.0:skill_md:2026-04-11 -->
