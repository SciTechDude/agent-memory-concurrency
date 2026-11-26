# 03-multi-agent-shared-state

Multi-agent coordination over shared state, blackboard architectures, shared scratchpads, subagent fan-out.

## Findings

Source lane: arxiv API, multi-agent over shared state. Entries not re-verified against abstracts (see 01 note). 2026 IDs.

| Title / item | Year | Venue / source | Link | Relevance & provenance |
|---|---|---|---|---|
| Governed Shared Memory for Multi-Agent LLM Systems | 2026 | arXiv 2606.24535 | https://arxiv.org/abs/2606.24535 | Formalizes shared-memory failure modes; multi-tenant memory service with scoped retrieval, supersession, provenance. Very close to question; read full text. |
| Verified Detection and Prevention of Concurrency Anomalies in Multi-Agent LLM Systems | 2026 | arXiv 2606.17182 | https://arxiv.org/abs/2606.17182 | Concurrency anomalies in shared memory/vector stores/tool registries with isolation hierarchy. See 01. |
| Token Coherence (MESI for multi-agent LLM) | 2026 | arXiv 2603.15183 | https://arxiv.org/abs/2603.15183 | Cache-coherence for shared artifacts. See 01. |
| PatchBoard | 2026 | arXiv 2605.29313 | https://arxiv.org/abs/2605.29313 | Transactional JSON-Patch mutations on shared state. See 01. |
| CodeCRDT | 2025 | arXiv 2510.18893 | https://arxiv.org/abs/2510.18893 | CRDT shared state for concurrent code agents. See 01. |
| AgentRoom | 2026 | arXiv 2608.23740 | https://arxiv.org/abs/2608.23740 | CRDT-backed shared workspace, file claiming. See 01. |
| SAFEFLOW | 2025 | arXiv 2506.07564 | https://arxiv.org/abs/2506.07564 | Transactional agent protocol with provenance. See 01. |
| Collaborative Memory: Multi-User Memory Sharing in LLM Agents with Dynamic Access Control | 2025 | arXiv 2505.18279 | https://arxiv.org/abs/2505.18279 | Private/shared tiers, immutable provenance attributes, access policies. Isolation by access control, not write concurrency. |
| MAPLE-Guard | 2026 | arXiv 2608.00426 | https://arxiv.org/abs/2608.00426 | Gates memory writes and private-to-shared promotion against poisoning; adjacent to quarantine of bad writes. |
| AIM: Privacy-Aware Interoperable Memory Framework for Multi-Agent Multi-User LLM Systems | 2026 | arXiv 2609.12320 | https://arxiv.org/abs/2609.12320 | Private vs public memory with index-level access control. |
| tap: A File-Based Protocol for Heterogeneous LLM Agent Collaboration | 2026 | arXiv 2606.14445 | https://arxiv.org/abs/2606.14445 | Git worktree isolation between Claude and Codex agents; isolation by filesystem, not memory semantics. |
| Exploring Advanced LLM Multi-Agent Systems Based on Blackboard Architecture | 2025 | arXiv 2507.01701 | https://arxiv.org/abs/2507.01701 | Blackboard LLM agents; no concurrency control discussed. |
| Terrarium: Revisiting the Blackboard for Multi-Agent Safety, Privacy, and Security Studies | 2025 | arXiv 2510.14312 | https://arxiv.org/abs/2510.14312 | Blackboard testbed for poisoning/malicious agents; security not consistency. |
| Scaling Multi-Agent Intelligence with Substrate-Centric Coordination (ScaleMAS) | 2026 | arXiv 2610.16120 | https://arxiv.org/abs/2610.16120 | Shared store of linked messages with citations; persistence and provenance-by-reference. |
| Trust-Aware Multi-Agent Traceability: Confidence-Calibrated KGs | 2026 | arXiv 2606.17203 | https://arxiv.org/abs/2606.17203 | Shared KG with consistency protocol, divergence detection, conflict resolution. |
| When Do Institutions Beat Intelligence? | 2026 | arXiv 2608.11357 | https://arxiv.org/abs/2608.11357 | Stale/distorted shared state and claim provenance as collective failures. |
| MemGraphRAG | 2026 | arXiv 2606.00610 | https://arxiv.org/abs/2606.00610 | Agents resolve logical conflicts via shared memory while building KGs. |
| Mining the Design Space of Multi-Agent Workflows | 2026 | arXiv 2610.31709 | https://arxiv.org/abs/2610.31709 | Finds persistent shared document outperforms debate; empirical support for shared state. |
| Long Context Scaling: Divide and Conquer via Multi-Agent Question-driven Collaboration | 2025 | arXiv 2505.20625 | https://arxiv.org/abs/2505.20625 | Agents update a centralized shared memory to keep knowledge consistent. |
| Code as Agent Harness | 2026 | arXiv 2605.18747 | https://arxiv.org/abs/2605.18747 | Survey; lists consistent shared state across agents as open challenge. |

### Non-arxiv lane additions (see 01 for full production-bug list)

| Title / item | Year | Venue / source | Link | Relevance & provenance |
|---|---|---|---|---|
| MemSwarm | 2027 (under review) | ICLR 2027 submission | https://openreview.net/forum?id=GI31Uxmkpn | Causal consistency + CRDT multi-value shared memory for agent teams; most direct non-arxiv competitor. See 01. |
| Position: Multi-Agent Systems Should Prioritize Concurrency Control | 2026 | ICML 2026 Position | https://openreview.net/forum?id=nfYEDaDzv9 | Frames MAS failures as concurrency anomalies on shared state. See 01. |
| CoAgent | 2026 | CoRR 2606.15376 | https://openreview.net/forum?id=VqAXwx2WSB | Serializable-in-fixed-order concurrency control with undo for parallel agents on shared resources. See 01. |
| Intrinsic Memory Agents: Heterogeneous Multi-Agent LLM Systems through Structured Contextual Memory | 2026 | ICLR 2026 (rejected) | https://openreview.net/forum?id=UbSUxAK3BI | Per-agent structured memory in multi-agent LLMs; abstract not read (OpenReview challenge page). Likely no concurrency treatment; verify. |
| Shared Selective Persistent Memory for Agentic LLM Systems | 2026 | REALM 2026 workshop (ACL-affiliated) | https://doi.org/10.18653/2026.realm-1.1 | Shared persistent memory across agents; title/metadata only, abstract not read. Check for concurrency handling. |
| Memory Fabric for Conversational AI Agents: Shared and Persistent Memory Across Users | 2025 | TechRxiv preprint | https://doi.org/10.36227/techrxiv.176523350.08289935/v1 | Shared memory across users; title only. |
| A Governed Shared-Kernel Architecture for Persistent, Auditable Multi-Agent Societies Beyond the LLM Session | 2026 | Research Square preprint | https://doi.org/10.21203/rs.3.rs-10847583/v1 | Shared kernel + governance/audit; title only. |
| nanocoai/nanoclaw #4475 "Agent group sessions share transcripts, notes and memory read-write" | 2026 | GitHub | https://github.com/nanocoai/nanoclaw/issues/4475 | Practitioner report of unisolated shared memory across sessions; proposes per-session isolation. |
| mem0 #3998 / #3645 / #4126 per-agent memory isolation when agents share one userId | 2025-26 | GitHub mem0ai/mem0 | https://github.com/mem0ai/mem0/issues/3998 | Multi-agent writers under one user_id bleed memories and dedup against each other's adds. Isolation here = namespace scoping, not transaction isolation. |
| Anthropic, "How we built our multi-agent research system" | 2025 | Anthropic Engineering blog | https://www.anthropic.com/engineering/multi-agent-research-system | Only says async subagents add "state consistency" challenges; subagents write to external stores and pass references. No treatment of concurrent memory writes or lost updates. |
| Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers | 2026 (Mar) | arXiv survey 2603.07670 | https://arxiv.org/abs/2603.07670 | Sec 9.6 names it open: "Multi-agent systems raise questions that single-agent memory never encounters: access control over shared stores, consensus protocols for concurrent writes, and knowledge transfer mechanisms... distributed memory with merge semantics, hierarchical shared memory with per-agent caches—remain wide open." Sec 6.6: "Two challenges dominate: shared vs. private memory boundaries... and consistency under concurrent writes". Also says "Database-style access control lists, adapted for natural language records, are a natural but unexplored solution." Surveys confirm the gap; no citations to prior solutions. |
| A Survey of Agent Memory in the Second Half | 2026 | arXiv 2602.06052 (TMLR) | https://arxiv.org/abs/2602.06052 | Sec 4.2 taxonomy of multi-agent memory: private-only, shared-workspace, hybrid, orchestrated. Sec 4.2.3 "Memory Isolation and Conflicts" (write control vs feedback-loop consistency). Cited systems: Memory-R1 (single mutator), WebCoach (write at episode end), EvoMem (constraint memory + verifier), Agents Thinking Fast and Slow (stale-read bug: Talker "can read an outdated belief state before the Reasoner updates it"), MetaGPT shared pool, Candidate Bus. Worth chasing these primaries. |
| Memory in the Age of AI Agents | 2025 | arXiv 2512.13564 | https://arxiv.org/abs/2512.13564 | Sec 7.5: shared memory evolution isolated -> centralized (vector store/blackboard/MetaGPT docs) -> "memory clutter, write contention, and the lack of role- or permission-aware access control". Write contention named as a challenge, one clause. |
| From Storage to Experience | 2026 | arXiv 2605.06716 | https://arxiv.org/abs/2605.06716 | "Distributed Shared Memory" future direction; frames as communication/consensus, not write isolation. |
| MIRIX / Topology Matters (Liu et al. 2025a) / Rezazadeh 2025 (multi-tenant ACL memory) | 2025 | cited in SSGM survey tables 2603.11768 | https://arxiv.org/abs/2603.11768 | Pointers: multi-agent memory work in the governance survey focuses on leakage and access control (Provenance & ACLs), not concurrent-write correctness. |

| Title / item | Year | Venue / source | Link | Relevance & provenance |
|---|---|---|---|---|
| Verified Detection and Prevention of Concurrency Anomalies in Multi-Agent LLM Systems | 2026 | arXiv 2606.17182 | https://arxiv.org/abs/2606.17182 | Formal anomaly taxonomy for multi-agent shared memory/vector index/tool registry state. See 01. |
| MemTX: Transactional Belief Commit for Stateful Agent Memory | 2026 | arXiv 2607.23929 | https://arxiv.org/abs/2607.23929 | Explicit shared-memory multi-agent framing ("one agent's write becomes another agent's premise"). See 01. |
| Before the Pull Request: Mining Multi-Agent Coordination | 2026 | arXiv 2606.19616 | https://arxiv.org/abs/2606.19616 | Concurrent coding agents collide on shared work; append-only signed log (grite) prevents silent write loss. |
| EvoGit: Decentralized Code Evolution via Git-Based Multi-Agent Collaboration | 2025 | arXiv 2506.02049 | https://arxiv.org/abs/2506.02049 | Agents coordinate via git version graph; git as shared state with branches. |
| Multi-Agent Transactive Memory | 2026 | arXiv 2606.19911 | https://arxiv.org/abs/2606.19911 | Shared trajectory repository for agents; no write-conflict treatment per summary. |
| Governed Collaborative Memory as Artificial Selection in LLM-Based MAS | 2026 | arXiv 2605.04264 | https://arxiv.org/abs/2605.04264 | Viewpoint: governance of which memories become shared state; provenance + version lineage; abstract has no concurrency/isolation. |
| MELD: Merging Knowledge Across Distributed Agentic Memories | 2026 | arXiv 2608.16357 | https://arxiv.org/abs/2608.16357 | CRDT-style status merge across agent memories. |
| SagaLLM | 2025 | arXiv 2503.11951 | https://arxiv.org/abs/2503.11951 | Transactional guarantees for multi-agent planning. See 01. |
| Multi-Agent Memory from a Computer Architecture Perspective | 2026 | arXiv 2603.10062 | https://arxiv.org/abs/2603.10062 | Position paper naming consistency as open problem. |
| SuperLocalMemory: Privacy-Preserving Multi-Agent Memory with Bayesian Trust Defense | 2026 | arXiv 2603.02240 | https://arxiv.org/abs/2603.02240 | Agent isolation (access) + trust scoring; isolation here means privacy, not transaction isolation. |
| AIM: Privacy-Aware Interoperable Memory for Multi-Agent Multi-User LLM Systems | 2026 | arXiv 2609.12320 | https://arxiv.org/abs/2609.12320 | Private/shared memory access control; not concurrency. |
| Surfacing Disagreement Beats Resolving It (provenance-weighted memory, multi-agent debate) | 2026 | arXiv 2611.22461 | https://arxiv.org/abs/2611.22461 | Shared debate memory keeping contradictions visible. |

### Semantic Scholar lane, 2026-11-26 (queries "agent memory concurrency", "multi-agent LLM shared memory consistency"). Abstracts read on arxiv.org/abs unless noted.

| Title / item | Year | Venue / source | Link | Relevance & provenance |
|---|---|---|---|---|
| Verified Detection and Prevention of Concurrency Anomalies in Multi-Agent LLM Systems | 2026 | arXiv 2606.17182 | https://arxiv.org/abs/2606.17182 | Top S2 hit for "agent memory concurrency"; abstract-verified. Reproduces a lost update in deer-flow and tool reordering in LangGraph ToolNode. See 01. |
| SagaLLM | 2025 | PVLDB / arXiv 2503.11951 | https://arxiv.org/abs/2503.11951 | Saga transactions plus persistent memory and compensation for multi-agent planning. See 01. |
| CodeCRDT | 2025 | arXiv 2510.18893 | https://arxiv.org/abs/2510.18893 | CRDT shared state; semantic conflict 5-10% despite 100% convergence. See 01. |
| AIM: Privacy-Aware Interoperable Memory Framework for Multi-Agent Multi-User LLM Systems (ABSTRACT-VERIFIED, 11 Sep 2026) | 2026 | arXiv 2609.12320 | https://arxiv.org/abs/2609.12320 | Private/public labels, index-level access control, MUMBench. Abstract says nothing on concurrency or provenance. |
| Modeling Response Consistency in Multi-Agent LLM Systems: Shared vs Separate Context | 2025 | arXiv 2504.07303 | https://arxiv.org/abs/2504.07303 | S2 hit, title only. "Consistency" here is likely response consistency, not store consistency; probably not relevant. |
| Multi-Agent Tool Sharing (LMIAT 2026) | 2026 | doi 10.1109/lmiat70705.2026.11682229 | (see 01) | Independently surfaced by S2; tool access, not memory. |
| RCR-Router: Role-Aware Context Routing for Multi-Agent LLM Systems with Structured Memory | 2025 | arXiv (no id in S2) | (no link) | S2 hit, title only; routing of context, not write consistency. |
