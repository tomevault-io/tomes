---
name: paper-pdf
description: Create a new academic paper or LaTeX manuscript through a citation-aware drafting and validation DAG; explicit full/PDF requests include artifact compilation. Do not use for repairing an existing manuscript, generic research reports, slides, or plotting. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# meta-paper-write (Meta-Skill)

Draft a long LaTeX manuscript by orchestrating paper-specific skills and
bounded LLM synthesis. The pipeline now leads with explicit experiment
design + placeholder figures/tables + citation provenance audit so the
deliverable can be reviewed for academic rigor, not just length.

DAG (in order):

1. **`paper_collect`** — extracts topic, mode, language, target length,
   audience, and reference count from the same turn without pausing for a
   form. Missing facts are marked as assumptions so first-pass paper
   requests complete inline.
2. **`paper_preferences`** — expand the collected facts into a planning
   contract.
3. **`search_papers`** — sends a clean academic query to Crossref, Brave,
   and Tavily; backend-specific academic filtering stays with each engine.
4. **`refbib`** — `paper-refbib-stub` now extracts ``eprint``/``doi``
   from arXiv/DOI URLs and tags each entry with ``note = {source: <domain>}``
   so downstream gates can classify provenance without re-fetching.
5. **`source_pack`** — curates unique, relevant, verifiable references and
   emits a machine-readable usable count against the integer citation target.
6. **`source_readiness_gate`** — deterministically blocks before experiment
   design or drafting when the curated primary references cannot meet the
   target, reporting a concrete found/required count.
7. **`experiment_design`** — **decides** how many figures and tables the
   paper needs based on RQs, hypotheses, analysis dimensions, and the
   target page budget. Every figure/table is tied to an RQ or analysis
   dimension; no decorative artefacts.
8. **`figure_placeholders`** — render LaTeX ``\fbox{\parbox{...}}``
   placeholder figure environments for each entry in FIGURE_PLAN. Zero
   matplotlib dependency.
9. **`table_placeholders`** — render LaTeX ``\begin{tabular}`` placeholder
   tables for each entry in TABLE_PLAN. Cells contain ``---``/``<TBD>``;
   no fabricated numbers.
10. **`analysis_outline`** — bind every figure/table id to a Discussion
   subsection that names potential findings + threats to validity, and
   covers every ANALYSIS_DIMENSION.
11. **`outline`** — paper outline that ties Method to experiment design
    and Results to the figure/table plan.
12. **`citation_plan`** — assigns concrete cite keys from `refbib` to
    claims; cannot invent keys.
13. **`writing_plan` + section authors** — the explicit FULL_MANUSCRIPT path
    converts the user's page target into section-level `target_words` and
    citation budgets before prose is written; section authors obey that plan.
14. **`final_manuscript_package`** — the lower-latency compact path still
    writes a complete, target-sized MANUSCRIPT_TEX with the
    figure/table/analysis blocks inlined verbatim, plus REFERENCES_BIB
    containing only the entries actually cited.
15. **Sanitize, materialize, and preflight** — persist the manuscript under
    the runtime-owned run directory, then compare language-aware content units
    with TARGET_PAGES. An undersized draft receives one bounded substantive
    expansion; a strict second gate must pass before compilation.
16. **`citation_map`** — strict markdown audit table:
    ``Cite Key | Cited Times | Title | URL/DOI/arXiv | Source Quality``
    with INVALID / UNUSED / WEAK detection. Inlined into the final
    deliverable AND queryable per-run via
    ``opensquilla skills meta runs show``.
17. **Citation and publication gates** — deterministically read the numeric
    `citation_map SUMMARY`; blocks when cited keys are below `CITATION_TARGET`,
    INVALID > 0, a cited source is WEAK, or the sanitized artifact violates
    publication rules. They never trust an LLM verdict or a fixed citation
    count.
18. **Compile probe and bounded page repair** — run the real
    XeLaTeX/BibTeX cycle and count pages with `pypdf`. A measured shortfall gets
    one final substantive expansion and one recompile. The runtime permits only
    the fixed `precompile` and `page-shortfall` repair ids and rejects citation,
    document-boundary, external-input, forced-page, and spacing commands.
19. **Final gates / `compile_pdf` / publish / delivery** — re-run sanitizer,
    length, and publication checks. An unchanged successful probe is reused by
    input fingerprint; a changed manuscript is recompiled once and must meet
    TARGET_PAGES before `publish_artifact` can run.

Removed from the previous version:

- `paper_mode` (llm_classify) — superseded by `paper_collect`
- `experiment` (skill_exec → `paper-experiment-stub`, fake CSV) —
  superseded by `experiment_design` (real plan, not data). The
  bundled `paper-experiment-stub` skill was deleted with this rewrite.
- `plot` (skill_exec → `paper-plot-stub`, matplotlib line chart) —
  superseded by `figure_placeholders` (zero-dependency LaTeX). The
  bundled `paper-plot-stub` skill was deleted with this rewrite.

The default path is COMPACT_SKELETON and ends with a compiled PDF without
section-by-section drafting. Explicit full/PDF/long-form requests use
FULL_MANUSCRIPT. If the topic is missing, `paper_clarify` pauses and asks the
user before generation continues. The compiler refuses to synthesize a degraded
PDF when the manuscript contract is missing.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
