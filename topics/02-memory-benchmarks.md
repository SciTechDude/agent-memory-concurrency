# 02-memory-benchmarks

Recall and retrieval benchmarks for agent memory (LoCoMo, LongMemEval, BEAM, MemBench, and others).

## Findings

_(append below: title | year | venue/source | link | 1-2 line relevance)_
MEMTRACK | 2025 | arXiv 2510.01353 | https://arxiv.org/abs/2510.01353 | Memory benchmark with conflicting-info resolution across platforms; single-agent-style, no concurrent-write test.
AgentLeak: Benchmark for Internal-Channel Privacy Leakage in Multi-Agent LLM Systems | 2026 | arXiv 2602.11510 | https://arxiv.org/abs/2602.11510 | Benchmark of leaks via inter-agent messages and shared memory; privacy, not consistency.
Entity-Collision: Stratified Protocol for Attributing Retrieval Lift in Agent Memory | 2026 | arXiv 2605.29630 | https://arxiv.org/abs/2605.29630 | Eval protocol; marginal relevance.
--- Non-arxiv lane additions ---
MEMAUDIT: An Exact Package-Oracle Evaluation Protocol for Budgeted Long-Term LLM Memory Writing | 2026 | NeurIPS 2026 Evaluations & Datasets (poster) | https://openreview.net/forum?id=d7WzgVziwp | Evaluates which facts get WRITTEN under a budget; single-writer. Abstract not read; no sign of concurrency.
AMemGym: Interactive Memory Benchmarking for Assistants in Long-Horizon Conversations | 2026 | ICLR 2026 poster | https://openreview.net/forum?id=sfrVLzsmlf | Recall-style benchmark; single agent.
MemPoison (NeurIPS 2026 E&D poster, https://openreview.net/forum?id=IgiZ5D2F8T), MemLeak (NeurIPS 2026 E&D poster, https://openreview.net/forum?id=ltUE09h18x), OmniMemBench (NeurIPS 2026 E&D poster, https://openreview.net/forum?id=yl7Kom0j0v) | 2026 | OpenReview | https://openreview.net/forum?id=IgiZ5D2F8T | Security/leak/omni-modal memory benchmarks; none surfaced as testing concurrent writers or lost updates (titles/search snippets only).
Does Memory Credit Travel? Paired Factorial Audits of LLM-Agent Memory | 2026 | SSRN 7160321 | https://doi.org/10.2139/ssrn.7160321 | Memory attribution audit; title only.
Observation: no non-arxiv memory benchmark found that has multiple concurrent writers or measures lost updates. The only empirical concurrency evaluation found is the SSRN SVBE paper (business-state workloads) and MemSwarm's own loopback tests; see 01.
Anatomy of Agentic Memory: Taxonomy and Empirical Analysis of Evaluation and System Limitations | 2026 (Feb) | arXiv survey 2602.19320 | https://arxiv.org/abs/2602.19320 | Critiques weak benchmarks, misaligned metrics, backbone sensitivity, maintenance overhead. Text grep: no multi-writer/concurrency benchmark mentioned; "concurrent" appears only as "concurrent systems" caveat. Supports claim that existing benchmarks are single-agent / single-writer.
The Horizon Gap (Planning, Memory, Execution, Training, Evaluation for Long-Horizon LLM Agents) | 2026 (Aug) | arXiv survey 2608.06663 | https://arxiv.org/abs/2608.06663 | ~1,500 papers surveyed. No multi-agent memory consistency discussion found; mentions Git Context Controller (commits/branches/merges of context state) as a context-management analogy.
Ground Truth First: Longitudinal Evaluation Instrument for Agent Memory | 2026 (Jul) | arXiv 2607.21962 | https://arxiv.org/abs/2607.21962 | Listed in search only; abstract-level read. Single-agent longitudinal benchmark; not read in depth.
Memory for Autonomous LLM Agents (2603.07670) | 2026 | https://arxiv.org/abs/2603.07670 | Sec 9.1 notes memory subsystem lacks regression test suites; sec 9.6 names multi-agent governance open. No benchmark for concurrent writes cited.

Read Boundaries in Agent Memory: Consistency, Completeness, and Repair | 2026 | arXiv 2611.19264 | https://arxiv.org/abs/2611.19264 | 600-run + 160-run studies on Cognee/Hindsight measuring conflicting responses under concurrent updates. Only concurrency-oriented measurement of real memory systems found.
Are We Ready For An Agent-Native Memory System? | 2026 | arXiv 2606.24775 | https://arxiv.org/abs/2606.24775 | Data-management evaluation of 12 agent memory systems across 5 workloads; title/summary only, concurrency coverage not verified.
MemDerive: Diagnostic Benchmark for Agent Memory over Evolving Data | 2026 | arXiv 2610.25373 | https://arxiv.org/abs/2610.25373 | Derived-state benchmark with Datalog gold answers; evolving data but no concurrent writers (per summary).
MemForm: Benchmarking Memory Formation Poisoning in LLM Agents | 2026 | arXiv 2610.14431 | https://arxiv.org/abs/2610.14431 | Write-path poisoning benchmark; adversarial, not concurrency.
Ground Truth First: Longitudinal Evaluation Instrument for Agent Memory | 2026 | arXiv 2607.21962 | https://arxiv.org/abs/2607.21962 | Longitudinal fact-script benchmark; single-agent.
MemGym: Long-Horizon Memory Environment for LLM Agents | 2026 | arXiv 2605.20833 | https://arxiv.org/abs/2605.20833 | Memory benchmark across tool use/coding; no concurrency per summary.
