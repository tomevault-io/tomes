---
name: lean-parsing-completeness
description: Use when proving parsing completeness theorems — that a parsing function returns .ok when given well-formed input, or that spec-level success implies native success. Also use when proving position bounds, eliminator lemmas, or chaining monadic parsing steps in Except/Option.
metadata:
  author: kim-em
---

# Parsing Completeness Proof Patterns

Two flavours:
1. **Spec ⟹ native**: spec returns `some (result, rest)`, prove native returns `.ok (result', state')` with result/state correspondence.
2. **Native ⟹ properties** (eliminator lemmas): native returns `.ok`, prove bounds/invariants about the result.

Both share the same core technique. Note: tightening native rejection (rejecting inputs the spec accepts) makes flavour-1 `*_complete` theorems false — fix by tightening the **spec**, not the native decoder.

## Core technique: destructuring `h : f data pos = .ok (r, p)`

1. Unfold ONE function: `simp only [parseFunction, bind, Except.bind] at h`.
2. Eliminate guard error branches:
```lean
by_cases h1 : guard_condition
· rw [if_pos h1] at h; ...
· rw [if_neg h1] at h; exact nomatch h  -- error branch impossible
```
3. Case-split on intermediate `.ok`/`.error` results:
```lean
cases hstep : intermediateCall with
| error e => simp only [hstep] at h; exact nomatch h
| ok v => rw [hstep] at h; dsimp only [Bind.bind, Except.bind] at h
```
4. Extract from the final pure: `simp only [pure, Pure.pure, Except.pure] at h; obtain ⟨rfl, rfl⟩ := h`.
5. Close with `rfl`, `exact ⟨rfl, rfl⟩`, or chain bounds with `omega`.

Always use explicit case splits (not `<;>`): different branches need different closers (`rfl` vs `simp_all` vs `exact nomatch h`).

## Sentinel/guard elimination: `nomatch` not `simp`

`exact nomatch h` closes an impossible error branch (`h : throw _ = .ok _`). Prefer it over `simp` — faster, robust, clear intent.

## After `rw [hstep] at h`, always `dsimp only`

`rw` leaves `match (.ok v) with ...` unreduced. Follow with `dsimp only [Bind.bind, Except.bind] at h` to collapse it.

## Unfold one function at a time

If `parseA` calls `parseB` calls `parseC`, unfold only `parseA`, then case-split on the `parseB` call. `simp only [parseA, parseB, parseC]` explodes the term.

## Common sub-patterns

- **`PUnit.unit` artifacts** (side-effect-free binds): `simp only [pure, Pure.pure, Except.pure] at h`.
- **`getElem!` with bounds**: `simp only [getElem!_def] at h; split at h` — one branch has the element, the other contradicts the guard.
- **`BEq` → `Prop`**: `simp only [beq_iff_eq] at h` (or `bne_iff_ne` for the negative).
- **Format discriminant dispatch** (e.g. 2-bit sizeFormat): nested `by_cases h : fmt == 0 / == 1 / == 2`, each with `rw [if_pos]`/`rw [if_neg]`; the final case (== 3) closes via `omega`.

## Chaining position bounds

Compose `_le_size` and `_pos_ge` lemmas from each step, then `omega`:
```lean
have h1_le := step1_le_size hstep1   -- pos₁ ≤ data.size
have h2_le := step2_le_size hstep2
have h1_ge := step1_pos_ge hstep1    -- pos₁ ≥ pos + k₁
have h2_ge := step2_pos_ge hstep2
omega
```

## WF-recursive parsers

Use `f.induct` for structural induction:
```lean
induction fuel using parseLoop.induct generalizing acc
```

## Visibility

Completeness proofs in `Zip/Spec/` reference `Zip/Native/` functions. Those must NOT be `private` — use no modifier (public) or `protected`. Check early: `grep -n 'private def targetFunction'`.

## Eliminator Lemma Pattern

Factor a duplicated case-analysis chain into one reusable eliminator that extracts all useful facts from parse success; downstream theorems consume it instead of re-analyzing:
```lean
theorem parseX_ok_elim (h : parseX data pos = .ok (result, pos')) :
    pos' ≥ pos + minSize ∧ pos' ≤ data.size ∧ result.field ∈ validRange := by ...

theorem parseY_complete (h : parseY data pos = .ok ...) : ... := by
  have ⟨hge, hle, hvalid⟩ := parseX_ok_elim hX
  ...
```

## Field characterization via struct projection

Prove a parsed struct's fields equal expressions over input bytes. After `unfold`/`unfold_except` and `split at h`:
- Success branches give `h : {field1 := ..., ...} = result ∧ pos+k = afterPos`; `obtain ⟨rfl, rfl⟩ := h`.
- Simple projection (`hdr.blockSize = raw >>> 3`): close with `rfl`.
- Conjunction over match branches (`(typeVal=0 → .raw) ∧ ...`): use `simp_all` (it needs the `heq✝ : matchDiscrim = N` hypothesis to kill impossible implications).
```lean
theorem parseBlockHeader_blockType_eq ... := by
  unfold Zip.Native.parseBlockHeader at h
  unfold_except
  split at h
  · exact nomatch h          -- guard failure
  · split at h
    · obtain ⟨rfl, rfl⟩ := h; simp_all  -- typeVal = 0
    · obtain ⟨rfl, rfl⟩ := h; simp_all  -- typeVal = 1
    · obtain ⟨rfl, rfl⟩ := h; simp_all  -- typeVal = 2
    · exact nomatch h                     -- reserved type
```

## Existential goals: `match hresult` not `simp only`

When the goal has existentials (`∃ x y z, f = .ok (x,y,z)`), do NOT unfold `f` in the goal — `simp only [f, bind, ...]` explodes distributing under `∃`. Match on the result instead:
```lean
match hresult : parseFunction data pos with
| .ok (a, b, c) => exact ⟨a, b, c, rfl⟩
| .error _ =>
  exfalso
  simp only [parseFunction, bind, Except.bind, ...] at hresult
```

## Helper definitions: avoid `let`

`let` bindings in a helper become opaque `have` terms after `unfold`, blocking `split` from finding the `if`. Inline conditions directly:
```lean
-- Good: split sees the if after `unfold rawSize at hsize; split at hsize`
def rawSize (data : ByteArray) (pos : Nat) : Nat :=
  if ((data[pos]! >>> 2 &&& 3).toNat == 0) then 1 + ... else ...
```
Use `contradiction` to drop branches conflicting with an outer split context. When `split at h` meets `if cond` and the context already has `h✝ : cond = true`, it auto-resolves — no second split needed.

## Goal-side vs hypothesis-side guard elimination

Constructing an existential `.ok` works on the **goal**; the `split at h` patterns above do not transfer. Goal-side:
```lean
simp only [hguard_false, ↓reduceIte]  -- eliminate known-false guard
split                                   -- case-split if/match in goal
· rename_i hbad; exact absurd hbad (by omega)  -- error case
· split
  · rename_i hbad; exact absurd hbad (by ...)
  · apply ih; ...
```
Differences: use `split` (not `split at h`); omit `dsimp only [letFun]` (no-op on goal); close impossible branches with `absurd` + contradiction (not `nomatch`).

## Composed completeness (single block): 6-step recipe

Prove a high-level op succeeds given only raw-byte preconditions. Preconditions are `data[off]!` expressions (usable without running the parser); field characterization theorems bridge raw bytes ↔ struct fields.
```lean
theorem composed_completeness (data : ByteArray) (off : Nat)
    (hsize : data.size ≥ off + minBytes) (htypeVal : rawByteExpr = expectedValue)
    (hlastBit : ...) (hpayload : data.size ≥ off + headerSize + payloadSize) :
    ∃ result pos', topLevelFunction data off ... = .ok (result, pos') := by
  -- 1. Guard satisfiable, e.g. typeVal ≠ 3 (reserved)
  have htypeNe3 : rawTypeExpr ≠ 3 := by rw [htypeVal]; decide
  -- 2. Sub-parser completeness
  obtain ⟨hdr, afterHdr, hparse⟩ := parseFunction_succeeds data off hsize htypeNe3
  -- 3. Field characterizations
  have htype := (parseFunction_blockType_eq ... hparse).1 htypeVal
  have hpos_eq := parseFunction_pos_eq ... hparse
  -- 4. High-level constraints from raw-byte hyps (decide closes typeVal implications)
  have hlast : hdr.lastBlock = true := by rw [hlast_eq, hlastBit]; decide
  -- 5. Sub-operation completeness (payload size flows through hpos_eq)
  have hpayload' : data.size ≥ afterHdr + neededBytes := by rw [hpos_eq]; omega
  obtain ⟨block, afterBlock, hraw⟩ := subOperation_succeeds data afterHdr ... hpayload'
  -- 6. Close via composition lemma
  exact ⟨_, _, composition_lemma ... hparse hbs htype hraw hlast⟩
```
Prerequisites: `parseFunction_succeeds`, `parseFunction_fieldName_eq` (each field), `subOperation_succeeds`, `composition_lemma`. Concrete: `Zip/Spec/Zstd.lean` `decompressBlocksWF_succeeds_single_raw`/`_single_rle`.

## Two-block composed completeness

Extends the single-block recipe to two consecutive blocks (first non-last, second last). Key addition: **position threading** — the second block's offset depends on the first's output position. Introduce explicit `off2` with `hoff2 : off2 = off + 3 + blockSize1.toNat`, then `subst`:
```lean
obtain ⟨hdr1, afterHdr1, hparse1⟩ := parseBlockHeader_succeeds ...
have hpos1_eq := parseBlockHeader_pos_eq ... hparse1
obtain ⟨block1, afterBlock1, hraw1⟩ := decompressRawBlock_succeeds ...
have hAfterBlock1_eq := decompressRawBlock_pos_eq ... hraw1
have hoff2_eq : off2 = afterBlock1 := by rw [hoff2, hpos1_eq]; omega
subst hoff2_eq   -- rewrites every off2 hyp to afterBlock1; eliminates the later var
-- block 2 via single-block recipe, then:
exact ⟨_, _, raw_step ... hparse1 hraw1 hlast1_false (single_raw ... hparse2 ...)⟩
```
Position formulas: `off + 3 + blockSize` (raw), `off + 4` (RLE), variable (compressed). For N blocks, use induction on the WF recursion instead (see `lean-content-preservation`).

## Multi-level composition chain

Each level wraps the previous:
```
decompressBlocksWF_succeeds_*  →  decompressFrame_succeeds_*  →  decompressZstd_succeeds_*
```
- **Frame level**: wraps block completeness with frame-header parsing + dict/checksum/size checks. Block hypotheses are universally quantified over `(hdr, afterHdr)` from `parseFrameHeader`, so byte-level conditions can depend on the (format-varying) header size.
- **API level**: the "frame fills data" condition is a quantified hypothesis `hterm : ∀ content pos', decompressFrame ... = .ok (content, pos') → pos' ≥ data.size`, cleaner than computing the exact end position.

## Cross-references

- **lean-monad-proofs**: general `Except`/`Option` bind unfolding
- **lean-zstd-patterns** / **lean-zstd-spec-pattern**: Zstd parsing impl + spec structure
- **lean-wf-recursion** / **lean-fuel-induction**: recursive parser unfolding

---
> Source: [kim-em/lean-zip](https://github.com/kim-em/lean-zip) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
