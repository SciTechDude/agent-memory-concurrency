# 05-graph-and-kv-stores

Graph memory, GraphRAG, knowledge graphs and KV stores used as agent memory.

## Findings

_(append below: title | year | venue/source | link | 1-2 line relevance)_
Zeta-Lite: Concurrent, Branchable In-Browser SQL Database for Agentic Memory | 2026 | arXiv 2609.01818 | https://arxiv.org/abs/2609.01818 | SQL store with snapshot-isolated transactions, conflict detection, copy-on-write branching purpose-built for agent memory. Not re-verified.
Mandol | 2026 | arXiv 2606.29778 | https://arxiv.org/abs/2606.29778 | Unified KV/vector/graph agent memory; concurrency tested only for performance.
Trust-Aware Multi-Agent Traceability | 2026 | arXiv 2606.17203 | https://arxiv.org/abs/2606.17203 | Shared KG with consistency protocol.
(KV-cache sharing papers PolyKV 2604.24971, Agent Memory Below the Prompt 2603.04428 are inference KV caches, NOT memory stores: irrelevant to the question.)
--- Non-arxiv lane additions: store-level concurrency bugs in shipped graph/KV/vector memory libraries (GitHub issue titles/snippets only) ---
graphiti #2159 (remove vs add episode loses fact on Neo4j, not FalkorDB), #2223 (multi-worker race), #2211 (bulk edge resolution vs pre-batch graph), #1840 (FalkorDB shared driver mutation) | 2026 | GitHub getzep/graphiti | https://github.com/getzep/graphiti/issues/2159 | Temporal KG memory has several open concurrency defects; backend-dependent behaviour (Neo4j vs FalkorDB). See 01.
mem0 #6243 entity-store read-modify-write drops linked_memory_ids; #7599 batch ops note local Qdrant is not thread-safe; #4892 Qdrant HNSW concurrent-write corruption (referenced from #6515, not fetched) | 2026 | GitHub mem0ai/mem0 | https://github.com/mem0ai/mem0/issues/6243 | Vector/entity stores underneath memory libs lack concurrency control; app-level RMW on entity links is unprotected.
cognee #6820 / #6559 | 2026 | GitHub topoteretes/cognee | https://github.com/topoteretes/cognee/issues/6820 | Counter RMW lost update; cross-dataset delete vs add on shared file.
langgraph store/checkpoint: #8115 put_writes race, #9234 SqliteSaver.list() holds lock across yields, #9558 SqliteStore refresh_ttl batch bug | 2026 | GitHub langchain-ai/langgraph | https://github.com/langchain-ai/langgraph/issues/8115 | Official BaseStore/checkpointer implementations have open concurrency/consistency bugs.
Zeta-Lite-like systems not found outside arxiv: no VLDB/SIGMOD/CIDR 2026 program entry on agent memory stores with snapshot isolation (see 00).
Graph-based Agent Memory: Taxonomy, Techniques, and Applications | 2026 (Feb) | arXiv survey 2602.05665 | https://arxiv.org/abs/2602.05665 | Graph-memory lifecycle survey. Full-text grep for concurrency/transaction/isolation/CRDT/optimistic found nothing; "transaction" only as bi-temporal transaction time and journal names.
Graph-Based Personalized Memory for LLM Agents | 2026 (Sep) | arXiv survey 2609.08599 | https://arxiv.org/abs/2609.08599 | Seen in search results only (abstract-level), not read; lists open challenges, unverified for concurrency.

Zeta-Lite: Concurrent, Branchable In-Browser SQL Database for Agentic Memory | 2026 | arXiv 2609.01818 | https://arxiv.org/abs/2609.01818 | MVCC engine, SI conflict detection, CoW branching; graph queries mentioned as engine capability.
Is Agent Memory a Database? | 2026 | arXiv 2605.26252 | https://arxiv.org/abs/2605.26252 | MemState prototype on property-graph backend; record-level DB ops argued insufficient.
Oracle Agent Memory as an Enterprise Memory Substrate | 2026 | arXiv 2607.13157 | https://arxiv.org/abs/2607.13157 | Database-native agent memory on Oracle DB; transactional properties inherited from the DB, not analyzed here (summary only).
Mandol: Agglomerative Agent Memory (KV + vector + graph) | 2026 | arXiv 2606.29778 | https://arxiv.org/abs/2606.29778 | Unified store; cross-database latency focus.
MemoriesDB: Temporal-Semantic-Relational Database for Agent Memory | 2025 | arXiv 2511.06179 | https://arxiv.org/abs/2511.06179 | PostgreSQL/pgvector design.
FluctlightDB: A Memory Model of Data for AI Agents | 2026 | arXiv 2608.12365 | https://arxiv.org/abs/2608.12365 | Embedded engine with write/cue-read semantics.
Supporting Our AI Overlords: Redesigning Data Systems to be Agent-First | 2025 | arXiv 2509.00997 | https://arxiv.org/abs/2509.00997 | Vision paper on agent-first data systems incl. speculative agentic workloads.
MemForest: Write-Efficient Agent Memory | 2026 | arXiv 2605.23986 | https://arxiv.org/abs/2605.23986 | Write path efficiency; no concurrency per summary.
