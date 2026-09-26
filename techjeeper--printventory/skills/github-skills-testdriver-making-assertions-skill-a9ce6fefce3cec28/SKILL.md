---
name: testdrivermaking-assertions
description: Verify application state with AI-powered assertions Use when this capability is needed.
metadata:
  author: TechJeeper
---
<!-- Generated from making-assertions.mdx. DO NOT EDIT. -->

## Making Assertions

Use AI-powered assertions to verify application state:

```javascript
// Verify visibility
await testdriver.assert('login page is displayed');
await testdriver.assert('submit button is visible');
await testdriver.assert('loading spinner is not visible');

// Verify content
await testdriver.assert('page title is "Welcome"');
await testdriver.assert('success message says "Account created"');
await testdriver.assert('error message contains "Invalid email"');

// Verify state
await testdriver.assert('checkbox is checked');
await testdriver.assert('dropdown shows "United States"');
await testdriver.assert('button is disabled');

// Verify visual appearance
await testdriver.assert('submit button is blue');
await testdriver.assert('form has red border');
```

<Info>Assertions are not cached and always re-evaluated to ensure accuracy.</Info>

---
> Source: [TechJeeper/Printventory](https://github.com/TechJeeper/Printventory) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
