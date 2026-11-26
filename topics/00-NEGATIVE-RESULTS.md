# 00-NEGATIVE-RESULTS

Searches that executed and returned nothing relevant, and searches that could not be executed. A null result is evidence about a query string, not about a concept; access failures are recorded as such and are not counted as absence. Each entry records the query, the source, and what was consulted.

## Findings

Source: arxiv API (export.arxiv.org), 2026-11-26.

all:"subagent" AND all:"memory" AND all:"conflict" | arxiv | 0 results.

all:"CRDT" AND all:LLM AND all:agents | arxiv | only 2 results (CodeCRDT, AgentRoom), both code-workspace not memory.

all:"multi-agent" AND all:"memory" AND all:"conflict resolution" AND all:LLM | arxiv | 4 results, mostly off-target (negotiation, benchmark); only Trust-Aware Traceability relevant.

Queries NOT completed due to HTTP 429 rate limiting (not evidence of absence; rerun): "lost update" with "parallel agents"; "snapshot isolation" AND agents AND LLM; "abandoned" AND "branch" AND agent memory; "shared scratchpad"; branch+merge+rollback agent memory; "agent swarm" state synchronization; "transactional" AND "agent memory"; id_list verification of the top 8 IDs.

Observation: no query surfaced a paper on writes made by an ABANDONED/discarded branch leaking into shared agent memory. [SUBSEQUENTLY CORRECTED: this null result was wrong. arXiv 2606.17182 formalizes the mode as the A3 causal-cascade anomaly and measures it; the terms 'abandoned', 'orphan' and 'speculative' do not occur in that paper. The null result reflected query vocabulary, not absence. See METHOD.md section 3.1.] Git Context Controller, GitOfThoughts, ChronoMem, Zeta-Lite handle branching/rollback but abstracts as summarized do not mention leakage of abandoned-branch writes. Weak absence evidence only (abstract-level, partial query coverage).

### Non-arxiv lane, 2026-11-26 (WebFetch only)

ACCESS FAILURES (not evidence of absence): dblp.org search API (Anubis bot block, both queries); aclanthology.org/search (page returned only help text; search is Google-backed and not scrapable); Semantic Scholar graph API (HTTP 429, 3 queries); DuckDuckGo html (captcha, 2 queries); openreview.net forum pages and api2 /notes?id= (browser challenge; abstracts obtained only via /notes/search?term= snippets); Crossref gave HTTP 429 once, then worked.

OpenReview search "concurrent writes agent memory consistency" (api.openreview.net v1) | 15 hits, all hardware/DB-theory (CheckFence, HyperKV, RECIPE) or irrelevant; nothing on LLM agent memory.

OpenReview search "shared memory multi-agent LLM transaction isolation" (v1) | all hits are RL/transactional-memory/hardware; nothing relevant.

OpenReview search "database perspective LLM agent memory transactional concurrency control" (v2) | only 2 relevant of 20: ICML 2026 Position "Multi-Agent Systems Should Prioritize Concurrency Control" and CoAgent; rest classic TM/DB (HyPer, SIGMOD 2010 partitioned CC). No ICLR/NeurIPS main-track paper on concurrent writes to agent memory surfaced.

OpenReview search "provenance agent memory write attribution rollback" (v2) | surfaced ChronoMem, Collaborative Memory, Write-Back Redundancy (see 06); none about abandoned/forked-branch writes.

CIDR 2026 program (cidrdb.org/cidr2026/program.html) | Agent-related papers: "Please Don't Kill My Vibe: Data Flow Control", "Supporting Our AI Overlords: Agent-First Data Systems" (Berkeley), "Autonomous Data Agent Collaboration", "Deep Research is the New Analytics System". NONE on agent memory, transactions or concurrent memory writes. Vision papers on agent-first data systems exist though; the Berkeley paper may discuss branching/speculation, not read in full (worth a read: it is the DB-community framing).

HotOS 2025 program (sigops.org) | no paper on agent memory/concurrency; only agent security and Guillotine isolation.

Crossref "agentic workloads database transactions branching speculative agents" (proceedings, 2025+) | 12 hits, none on transactional agent state.

Crossref "agent memory database management LLM consistency versioning" | rate-limited, rerun not done; Crossref "multi-agent LLM shared memory write conflict consistency" returned only title-level hits (see 01/03).

VLDB / SIGMOD / USENIX (OSDI/ATC/NSDI/FAST) 2025-26 proceedings: NOT directly searchable via available fetch (dblp blocked). No hit via Crossref or OpenReview. Absence here is WEAK; re-check by browsing dblp conf/vldb/2026, conf/sigmod/2026, conf/usenix 2026 tables of contents manually.

ACL Anthology (ACL/EMNLP/NAACL 2025-26): search unavailable; Crossref returned only Findings of EMNLP 2026 "Agent Memory Distillation" (unrelated) and REALM 2026 "Shared Selective Persistent Memory". No ACL-family paper found on concurrent memory writes. Weak absence.

GitHub letta-ai/letta search (shared block / multi-agent conflict / overwrite) | no issue on lost updates between agents sharing a block beyond #3366 (optimistic locking works, closed). #3388 (persistent core memory poisoning leaks across runs, closed not planned) is state leakage not concurrency.

GitHub cross-repo search for abandoned/cancelled/forked-branch writes polluting persistent memory | 15+12 results; NO issue describes writes from an abandoned, cancelled or rolled-back branch persisting in shared memory. Nearest: CLICS-TH/clics#270 (subagent wrote unapproved memory), promptctl/skillz PR #8 (carries lesson from deleted attempt, by design), trustmybot/plugin#3022 (agents save mistakes as memory). Evidence of absence for the exact abandoned-branch framing; the symptom class (unsanctioned subagent writes) does appear.

Vendor engineering blogs: Anthropic multi-agent research system post mentions "state consistency" only in passing. Letta/Zep/Mem0/LangChain blog pages NOT fetched (no search engine access); absence there is untested.

arXiv API (export.arxiv.org) query: all:survey AND all:"agent memory" (max 30) | 2026 | returned 18 surveys; none has concurrency/consistency/isolation in title or abstract. Only full-text reading found the sparse mentions recorded in 01/03.

arXiv API query: all:"multi-agent" AND all:memory AND all:survey AND all:consistency | returned 5 entries, none about multi-agent memory consistency (geosimulation, hippocampus, embodied security, Code as Agent Harness, healthcare).

arXiv API query: all:"memory" AND all:"LLM agents" AND all:survey sorted by date | 20 entries; relevant ones were only 2603.07670, 2603.11768, 2604.16548, 2606.04990. No survey title/abstract names concurrent writes.

Full-text grep of 10 surveys (2512.13564, 2602.05665, 2602.06052, 2602.19320, 2603.07670, 2603.11768, 2604.16548, 2605.06716, 2606.04990, 2608.06663) for: "lost update", "write conflict", "race condition", "serializab", "isolation level", "CRDT", "eventual consistency", "optimistic" (concurrency sense) | zero hits for lost update / race condition / serializability / isolation level / CRDT in any of them. "eventual consistency" appears once (2512.13564, single-agent offline consolidation). "concurrent writes" appears only in 2603.07670. No survey mentions abandoned/orphaned branch writes.

INCONCLUSIVE (rate-limited, HTTP 429 from export.arxiv.org, NOT evidence of absence): all:"concurrent writes" AND all:"agent memory"; all:"lost update" AND all:agents AND all:memory; all:"multi-agent" AND all:"shared memory" AND all:consistency AND all:LLM; all:"memory consistency" AND all:"multi-agent" AND all:LLM; all:"agent memory" AND all:provenance AND all:branch; all:"agentic memory" AND all:survey AND all:"open problems"; all:"isolation" AND all:"snapshot" AND all:"agent memory". These should be re-run by another lane.

Source: arXiv API (export.arxiv.org), run 2026-11-26. Note: only title/abstract metadata read; no full texts.

QUERY `all:"agent memory" AND (all:"lost update" OR all:"write conflict" OR all:"race condition")` | arXiv API | 0 results. The literal phrases "lost update"/"write conflict"/"race condition" combined with agent memory do not appear in any indexed arXiv paper. (Related work uses other wording: "stale-generation", "conflicting responses", "mixed revisions".)

QUERY `all:"multi-agent" AND all:memory AND (all:"snapshot isolation" OR all:"optimistic concurrency" OR all:linearizability OR all:"eventual consistency")` | arXiv API | 1 result, and it is relevant (2606.17182); no others, so the vocabulary is nearly unused outside that paper.

QUERY `all:"parallel agents" AND all:memory AND (all:speculative OR all:fork OR all:branch)` | arXiv API | 2 results, both irrelevant (speculative decoding; image classification). Nothing on abandoned/forked agent branches writing to shared memory.

QUERY `cat:cs.MA AND all:"shared memory" AND (all:concurrent OR all:conflict OR all:consistency)` | arXiv API | 7 results, essentially all irrelevant (pathfinding, story worlds, decentralized medical QA, a 2004 supercomputer paper); only EvoGit and the provenance-debate paper marginally relevant.

QUERY `all:"memory consistency" AND all:"LLM agents"` | arXiv API | 7 results, mostly irrelevant (belief memory, biometrics, adaptive memory); only the computer-architecture position paper (2603.10062) and MemAudit are relevant.

QUERY `all:"concurrent writes" AND (all:agents OR all:LLM)` | arXiv API | 4 results; only 2606.19616 (grite, coding-agent coordination) relevant; others unrelated.

NOT FOUND in any query: a paper on writes made by an abandoned / superseded / discarded agent branch persisting into shared memory and being attributed or cleaned up. Closest are Zeta-Lite (discard speculative branch, DB-level), ChronoMem (rollback), MemTX (retract belief with cascading repair), GitOfThoughts (pruned branch recorded). None studies leaked abandoned-branch writes as a failure mode.

### Semantic Scholar lane, 2026-11-26 (api.semanticscholar.org, unauthenticated, year>=2024, limit 12, via Python urllib after WebFetch returned HTTP 429). The API was heavily rate-limited, so most queries needed many retries; failures are NOT evidence of absence.

S2 query "agent memory concurrency" | OK, 12 hits. Relevant: 2606.17182, TOKI, PLACEMEM, SuperLocalMemory. Rest were GPU/LLM-serving concurrency (CONCUR, TenonAgent, MAServeBench) or code-test generation. Nothing new beyond the arXiv lane.

S2 query "multi-agent LLM shared memory consistency" | OK, 12 hits. Relevant: SagaLLM, CodeCRDT, Multi-Agent Memory from a Computer Architecture Perspective, AIM. Rest off-target (web search agent, network research reproduction).

S2 query "provenance LLM agent memory" | OK, 12 hits, all provenance-for-trust/poisoning/audit/retrieval. None about writes from an abandoned or discarded branch; none about concurrent writers (verified on abstracts for MemLineage, Agent Zero Memory, 2606.22030, Collaborative Memory, 2606.04990).

S2 query "LLM agent concurrent writes lost update" | FAILED after 10 retries (HTTP 429). Inconclusive.

S2 queries still pending/failed at time of writing (see end-of-file note if later appended): "multi-agent memory conflict"; "agent knowledge base write contention"; "agent memory write skew isolation"; "agent state isolation transactions LLM"; "abandoned branch speculative agent memory writes"; "agent memory versioning rollback".

Observation across S2 lane: the phrases "lost update", "write skew" and "abandoned branch" never appeared in a returned title. Only 2606.17182 uses isolation-anomaly vocabulary for LLM-agent shared state, and it does not mention abandoned-branch writes in its abstract (it mentions "retracted sessions", unresolved).

NOT FOUND: any benchmark measuring lost updates across concurrent LLM agents writing to a shared memory store with real agents (Read Boundaries 2611.19264 measures read-side inconsistency against concurrent writers; 2606.17182 is formal/verified runtimes).
