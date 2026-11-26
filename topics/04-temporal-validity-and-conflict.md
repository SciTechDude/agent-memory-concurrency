# 04-temporal-validity-and-conflict

Bitemporal memory, fact supersession, contradiction detection, staleness, admission control.

## Findings

_(append below: title | year | venue/source | link | 1-2 line relevance)_
Entries not re-verified against abstracts.
MEMTRACK: Evaluating Long-Term Memory and State Tracking in Multi-Platform Dynamic Agent Environments | 2025 | arXiv 2510.01353 | https://arxiv.org/abs/2510.01353 | Benchmark over Slack/Linear/Git testing resolution of conflicting information.
Rashomon Memory: Argumentation-Driven Retrieval for Multi-Perspective Agent Memory | 2026 | arXiv 2604.03588 | https://arxiv.org/abs/2604.03588 | Keeps conflicting interpretations, resolves at query time.
Mandol: Agglomerative Agent Memory System | 2026 | arXiv 2606.29778 | https://arxiv.org/abs/2606.29778 | KV+vector+graph store with conflict resolution in retrieval.
PLACEMEM | 2026 | arXiv 2607.04089 | https://arxiv.org/abs/2607.04089 | Validity-tracked memory capsules with cascading invalidation.
Governed Shared Memory (supersession) | 2026 | arXiv 2606.24535 | https://arxiv.org/abs/2606.24535 | Supersession of contradictory entries in shared memory.
Trust-Aware Multi-Agent Traceability | 2026 | arXiv 2606.17203 | https://arxiv.org/abs/2606.17203 | Divergence detection and conflict resolution in shared KG.
--- Non-arxiv lane additions ---
Immune Memory: Contradiction Filtering at Write Time for Long-Term LLM Agents | 2026 | Preprints.org 10.24108/preprints-3116872 | https://doi.org/10.24108/preprints-3116872 | Write-time contradiction filtering; title only, single-writer framing presumed.
DISCERN: Preserve at Write, Resolve at Read for Persistent LLM-Agent Memory | 2026 | NeurIPS 2026 workshops (CL4FMAgents, TTCL) | https://openreview.net/forum?id=fT5bqtdEjc | Keep conflicting writes, resolve at read time (same stance as Rashomon Memory and MemSwarm multi-value). Abstract not read.
Failure-Gated Hierarchical Memory: Preventing Memory Pollution via Critic-Guided Write Control | 2026 | MLISE 2026 (IEEE) | https://doi.org/10.1109/mlise70044.2026.11607496 | Write admission gating against pollution; title only.
Structural Write-Path Control for Non-Formation in Agent Persistent Memory | 2026 | FAGEN@ICML 2026 poster | https://openreview.net/forum?id=h2KYjLhzv5 | Write-path control; abstract not read.
mem0 #4956 / #5867 ADD-only extraction surfaces stale/contradictory facts | 2026 | GitHub mem0ai/mem0 | https://github.com/mem0ai/mem0/issues/4956 | Open. v3 removed UPDATE/DELETE, so superseded facts coexist. Production evidence that conflict handling is unsolved; also #5205 near-duplicate preferences not merged, #5352 community workaround for "time-blindness".
Graph-based Agent Memory: Taxonomy, Techniques, and Applications | 2026 (Feb) | arXiv survey 2602.05665 | https://arxiv.org/abs/2602.05665 | Mentions bi-temporal modeling (valid time vs transaction time, Graphiti). Skim of full text found no concurrency/isolation/conflicting-writer discussion (grep for concurren|race|isolation|consisten hit nothing relevant).
Governing Evolving Memory in LLM Agents (SSGM) | 2026 | arXiv 2603.11768 | https://arxiv.org/abs/2603.11768 | Conflict = logical contradiction between new and existing facts (Truth-Maintenance-System style), checked on write; stability-plasticity tradeoff. Contradiction handling, not concurrent-writer handling.
A Survey of Agent Memory in the Second Half | 2026 | arXiv 2602.06052 | https://arxiv.org/abs/2602.06052 | Memory-R1 ADD/UPDATE/DELETE/NOOP and graph-memory "detect edge changes, resolve conflicts" are the conflict-resolution baselines; all are sequential, LLM-judged.

TOKI: Bitemporal Operator Algebra for Contradiction Resolution | 2026 | arXiv 2606.06240 | https://arxiv.org/abs/2606.06240 | Bitemporal dual-row schema; last-writer-wins / evidence-weighted merge / await-confirmation as concurrency-control operators with isolation preconditions.
MemTX | 2026 | arXiv 2607.23929 | https://arxiv.org/abs/2607.23929 | Each record carries evidence, permissions, provenance, validity; retraction cascades to derived records.
MEMOREPAIR: Barrier-First Cascade Repair in Agentic Memory | 2026 | arXiv 2605.07242 | https://arxiv.org/abs/2605.07242 | Cascade-update problem: stale derived memories keep steering actions after source corrected; withdraw-then-republish contract.
DISCERN: Preserve at Write, Resolve at Read | 2026 | arXiv 2611.15729 | https://arxiv.org/abs/2611.15729 | Keeps conflicting facts at write, resolves at read.
The Memory Trust Gap: Reliance on Stale Evidence Across Model Scales | 2026 | arXiv 2609.01852 | https://arxiv.org/abs/2609.01852 | Agents follow stale memory over current evidence.
When Stale Constraints Go Unchecked: Budgeted Verification Failures in Inherited Agent Memory | 2026 | arXiv 2608.25553 | https://arxiv.org/abs/2608.25553 | Agents rarely re-verify superseded constraints.
Navigating Epistemic Parity in LLM Agents (memory vs procedural-skill conflict) | 2026 | arXiv 2610.33128 | https://arxiv.org/abs/2610.33128 | Cross-source conflict resolution benchmark.
Is Agent Memory a Database? (Governed Evolving Memory) | 2026 | arXiv 2605.26252 | https://arxiv.org/abs/2605.26252 | Frames correctness as property of state trajectory; revision/forgetting operators; MemState prototype.
MELD | 2026 | arXiv 2608.16357 | https://arxiv.org/abs/2608.16357 | Five-outcome claim admission (insert/merge/relate/conflict/reject).
PolyMemDB: Polyglot Database System for AI Memory | 2026 | arXiv 2608.25577 | https://arxiv.org/abs/2608.25577 | Probabilistic conflict resolution with provenance.
--- Semantic Scholar lane, 2026-11-26. Abstracts read on arxiv.org/abs. ---
DISCERN (ABSTRACT-VERIFIED, 11 Nov 2026) | 2026 | arXiv 2611.15729 | https://arxiv.org/abs/2611.15729 | Additive bi-temporal provenance graph retains superseded values; read-time zero-LLM tools resolve validity, 4 gated terminal actions. Abstract does not address concurrent writers or locking; contradictions handled by reasoning over history.
TOKI (ABSTRACT-VERIFIED) | 2026 | arXiv 2606.06240 | https://arxiv.org/abs/2606.06240 | Frames contradiction resolution as write-time concurrency control. The one temporal/conflict paper that explicitly crosses into isolation. See 01.
When Does Belief-Based Agent Memory Help? (ABSTRACT-VERIFIED) | 2026 | arXiv 2606.22030 | https://arxiv.org/abs/2606.22030 | Bayesian updating vs last-write-wins; on LoCoMo LWW is nearly as good because the benchmark rarely has contradictory or unequally reliable evidence (so benchmarks understate the conflict problem). Reliability-conditioned and provenance-capped updating help when sources differ.
