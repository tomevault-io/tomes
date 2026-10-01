---
name: code-quality
description: > Use when this capability is needed.
metadata:
  author: QuantConnect
---
# QuantConnect Algorithm Code Quality
Apply these rules to `main.py` and custom data classes. The goal is compiling code that does not hide real failures.
## Imports
Use AlgorithmImports for LEAN APIs and common algorithm types. Do not add redundant imports for datetime, timedelta, date, pandas, numpy, or math. Put required standard library imports before AlgorithmImports, separated by one blank line.
## Subscription Variables
Store the Security returned by add_data, add_equity, or add_crypto. Pass that Security directly anywhere a Symbol is expected; do not store or use .symbol.
```python
# Bad
self._custom_symbol = self.add_data(MyData, "TICKER").symbol
data[self._custom_btc.symbol]
# Good
self._custom_btc = self.add_data(MyData, "TICKER")
if self._custom_btc not in data:
    return
bar = data[self._custom_btc]
```
Use x in data and x not in data, not data.contains_key(x).
## Comments
Follow PEP 8: block comments start with # , use complete sentences, start sentences with capitals, and end sentences with periods. Inline comments are rare, separated from code by at least two spaces, and start with # .
```python
# Bad
# add equity
x = price*quantity #calculate value
# Good
# Add the equity subscription.
x = price * quantity  # Calculate the order value.
```
## Multi-Line Boolean Expressions
Put and/or at the end of each continued line.
```python
# Bad
if (
    close > ema_fast
    and open_ > ema_fast
    and rsi > 50):
    return
# Good
if (close > ema_fast and
    open_ > ema_fast and
    rsi > 50):
    return
```
## Blank Lines
Use two blank lines before top-level classes, one blank line before methods inside classes, and no blank lines inside method bodies.
## Error Handling
Do not wrap algorithm logic in `try / except` blocks. Exceptions reveal invalid state, missing data, and incorrect assumptions; catch-all handlers make bugs invisible.
```python
# Bad
try:
    self.set_holdings(self._spy, target_weight)
except Exception:
    pass
# Good
if target_weight:
    self.set_holdings(self._spy, target_weight)
```
## Checklist
1. Standard library imports precede AlgorithmImports.
2. Stored subscription variables are Security objects, not .symbol values.
3. Comments follow language-specific rules.
4. Multi-line boolean expressions follow language-specific continuation style.
5. Blank lines match language rules.
6. Algorithm code has no `try / except`; it uses explicit guards for expected conditions.

---
> Source: [QuantConnect/Documentation](https://github.com/QuantConnect/Documentation) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
