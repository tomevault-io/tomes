---
name: bonsai
description: Use when working with the art of keeping your AI stack small and shaped on purpose. Use when building AI features, selecting models, designing extraction/RAG/agent pipelines, or about to reach for a frontier LLM (GPT-5, Claude Opus, Gemini Pro). Enforces a smallest-tool-first ladder (regex, spaCy NER, small LLM, frontier) and challenges JSON-everywhere, RAG-everywhere, browser-automation-everywhere defaults. Use whenever the user mentions token cost, latency, model sizing, structured output, RAG, or agent architecture.
metadata:
  author: NehmeAILabs
---

Keep the AI stack small and shaped on purpose. A bonsai isn't a stunted tree — it's a tree shaped with intent. Stop at the first rung that holds, always.

## Task ladder

Climb until one works, then stop:

1. Regex / rules / lookup tables — $0, <1ms. Most extraction dies here.
2. Structured/tabular data → XGBoost, random forest, logistic regression. Often beats LLMs.
3. Search/retrieval → BM25 first. Add vector search only if needed.
4. External knowledge → <100 pages, stuff in context. Larger, then consider RAG.
5. Simple LLM task (classify, extract, summarize) → small model, 1B-8B. Test first.
6. Frontier model — but measure first. You usually don't need it.

For extraction specifically: regex → spaCy NER → small LLM (1B-4B) → medium (8B-12B) → frontier. Reaching frontier for pure extraction is a red flag. See [patterns/extraction.md](patterns/extraction.md).

## Model sizing

- 70-80% accuracy: 1B-4B (drafts, triage).
- 85-95%: 4B-12B (production).
- 95%+: fine-tune a small model — don't scale up. Frontier rarely buys more than 5% on simple tasks; that 5% costs 50x.

Output tokens drive latency and cost. Yes/no → tiny model + constrained decoding. Category label → 1B + constrained decoding. Short extraction → delimiters or grammar-constrained. Paragraph → 4B-8B. Long generation → maybe bigger.

## Structured output

**The JSON tax.** JSON has overhead. For simple extraction:

```
# JSON output (35 tokens)
{"name": "John Smith", "company": "Acme Corp", "title": "CTO", "status": "lead"}

# Delimiter output (11 tokens)
John Smith::Acme Corp::CTO::lead
```

3x fewer tokens, 3x faster, 3x cheaper. JSON's verbosity is a recurring token cost you pay on every request.

Preference order: **constrained decoding > delimiters > JSON.** Constrained decoding (GBNF, Outlines, xgrammar) forces valid output at the sampler level — zero parse failures, no retries, the JSON-vs-delimiter tradeoff disappears. Use it when you control inference (local model, or an API that exposes it). Delimiters for simple flat extraction when you can't constrain. JSON only for nested structures, optional fields, or API contracts.

## RAG

Context windows are 2M-10M tokens. <100 pages → stuff in context, skip RAG. RAG adds chunking, embeddings, vector DBs, reranking — all for docs that fit in one prompt. RAG earns its keep only for: millions of docs, frequently changing content, cost at scale (8-80x cheaper per query for large static corpora).

## Agents

Agent decision: no real-time web → stuff context, no agent. API or public URL → search API + fetch + HTML→MD + LLM synthesis. UI interaction (login walls, dynamic forms, actions) → browser automation.

- Browser automation is overkill for reading public content. 10x slower, 10x costlier, more brittle. Use only for login walls, dynamic forms, actions, JS-only SPAs with no API.
- Skip the framework. Native LLM tool use over LangChain/LlamaIndex. See [patterns/agents.md](patterns/agents.md).
- 2-3 tools = best accuracy. 10+ = poor. Specialized agents with few tools beat one agent with many.
- Hard limits: `MAX_ITERATIONS = 10`, `MAX_TOOL_CALLS = 20`. Hitting the limit means the task is too hard or tools are wrong.
- Plan with 12B+, execute with 4B.
- Default to single agent. Add agents only for parallel subtasks, distinct domains, or adversarial verification.
- `requests.get(url, timeout=10)` — a timeoutless fetch hangs the agent forever.
- Verify outputs: FlashCheck against sources, per-step, or human checkpoint for high-stakes.

## Cascade

Smallest model → verify → escalate on failure. Verifier: format validation, classifier, or FlashCheck. See [examples/cascade.py](examples/cascade.py).

## Anti-patterns to push back on

- "We use GPT-5 for everything" — a $50K/month bill, not a flex.
- "Small models aren't accurate enough" — did you test, with the right prompt, on your actual data?
- "We'll optimize later" — you'll optimize never. Start right-sized.
- "JSON output is industry standard" — for simple extraction it's industry waste.
- "We need RAG for our documents" — for small doc sets, no you don't.
- Browser automation for research — use search + fetch + HTML→MD + synthesis.
- Frontier models for simple extraction — burning money.
- Not testing regex first — most extraction is one regex away.

## Reference files

- [patterns/extraction.md](patterns/extraction.md) — extraction ladder with code
- [patterns/agents.md](patterns/agents.md) — agent architecture with code
- [examples/cascade.py](examples/cascade.py) — working cascade example

---
> Source: [NehmeAILabs/llm-sanity-checks](https://github.com/NehmeAILabs/llm-sanity-checks) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
