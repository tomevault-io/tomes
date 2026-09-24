---
name: bench-compare
description: Comparison criteria (e.g. performance,api-design,scalability) Use when this capability is needed.
metadata:
  author: afx-team
---

# Benchmark & Compare

Compare multiple agent memory projects across key dimensions.

## Instructions

1. For each project in `${projects}`:
   - Search for benchmarks, performance reports, and comparisons
   - Analyze the architecture and API design
   - Check community feedback (GitHub issues, discussions, Reddit, HN)
2. Compare across these default criteria (override with `${criteria}` if provided):
   - **Memory Types**: What types of memory are supported
   - **Retrieval Strategy**: How memories are retrieved (vector, graph, hybrid)
   - **Scalability**: How it handles large memory stores
   - **API Design**: Ease of integration
   - **Ecosystem**: Integrations with LLM frameworks
   - **Performance**: Latency, throughput if data available
   - **Community**: Stars, contributors, activity
3. Output a comparison matrix (markdown table)
4. Provide a recommendation summary with trade-offs

---
> Source: [afx-team/hebb-mind](https://github.com/afx-team/hebb-mind) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
