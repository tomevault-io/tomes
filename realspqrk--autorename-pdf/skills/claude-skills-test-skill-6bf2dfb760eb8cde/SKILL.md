---
name: test
description: Run the test suite with coverage report. Use when tests need to be executed or verified. Use when this capability is needed.
metadata:
  author: realspqrk
---

# Run Tests

Run the project test suite using pytest.

## Steps

1. Activate the venv before running any commands:

```bash
source venv/Scripts/activate
```

2. Run tests with coverage:

```bash
python -m pytest tests/ -v --tb=short --cov=. --cov-report=term-missing
```

3. If an argument is provided (e.g., `test_document_processing`), run only that test file:

```bash
python -m pytest tests/test_<argument>.py -v --tb=short
```

4. Report results to the user:
   - Number of tests passed/failed/skipped
   - Coverage percentage for key modules
   - If failures: show the failing test name and assertion error

## If Tests Fail

- Read the failing test to understand what's expected
- Read the source module being tested
- Identify the root cause and suggest a fix
- Do NOT modify tests to make them pass unless the test itself is wrong

---
> Source: [realspqrk/autorename-pdf](https://github.com/realspqrk/autorename-pdf) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-04 -->
