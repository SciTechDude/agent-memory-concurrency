# Failure Modes, Published Treatments, and Open Defects

This document relates each catalogued failure mode to the publications that address it
and to defect reports that remain open in deployed systems. Nomenclature follows the
literature. Provenance tags are defined in [README.md](README.md#3-provenance-classification).

For several modes a published treatment exists — in certain cases formally verified and
accompanied by measured overheads — while the same mode remains open in a shipped
library. Section 9 summarizes this pattern.

---

## 1. Lost update (read-modify-write against stale state)

Two writers read a value, each determines a subsequent write from what it read, and one
determination is discarded without record.

### Published treatments

- [2606.17182](https://arxiv.org/abs/2606.17182) formalizes the mode as the L0→L1
  refinement of a machine-checked consistency hierarchy, verified in TLA+ and Verus
  (274 proof obligations), with three Rust runtimes implementing pessimistic locking,
  serializable snapshot isolation, and default snapshot isolation. A silent lost update
  in ByteDance deer-flow is reproduced from that project's own regression test.
  Reported overheads: snapshot isolation approximately 8% additional tokens on one
  workload; pessimistic locking 1.6–2.3×. `FULL-TEXT`
- [MemTX 2607.23929](https://arxiv.org/abs/2607.23929) stages writes in
  snapshot-isolated transactions with validate-and-commit. `ABSTRACT-VERIFIED`
- MemSwarm (ICLR 2027 submission) models shared memory as replication with causal
  consistency and CRDT merge, reporting zero lost writes across 23,200 samples relative
  to last-write-wins. Evaluation is single-machine. `title+snippet`
- SVBE ([SSRN 7472480](https://doi.org/10.2139/ssrn.7472480)) reports invariant
  violations in 65.0% of unsafe concurrent runs, with zero violations under all
  protected strategies. Workloads are business-state rather than memory stores.
  `title+snippet`

### Deployed mitigation

- letta applies optimistic locking to memory blocks, returning HTTP 409 to the losing
  writer ([#3366](https://github.com/letta-ai/letta/issues/3366), closed). The losing
  write is rejected rather than merged. The reporting user observed an approximate
  0.01% conflict rate on a periodically updated block.

### Open defects

- [mem0 #6243](https://github.com/mem0ai/mem0/issues/6243): entity-store
  read-modify-write discards `linked_memory_ids`. Labelled `bug / P1-high / accepted`;
  opened 2026-07-11, last activity 2026-08-12.
- [mem0 #7950](https://github.com/mem0ai/mem0/issues/7950): within a single `add()`
  batch, an earlier entity link is overwritten by a later one.
- [langgraph #8115](https://github.com/langchain-ai/langgraph/issues/8115): a race in
  `PregelLoop.put_writes()` produces silent checkpoint data loss. Labelled `external`.
- [cognee #6820](https://github.com/topoteretes/cognee/issues/6820): a concurrent
  rating increment is discarded; the read occurs outside the locked update.
- Approximately ten smaller repositories report this mode independently; see
  [topics/01](topics/01-concurrency-and-consistency.md).

---

## 2. Deduplication TOCTOU (duplicate entries under concurrency)

Two writers evaluate an existence check against the same stale snapshot, both find the
record absent, and both insert.

### Published treatments

- [TOKI 2606.06240](https://arxiv.org/abs/2606.06240) argues that contradiction
  resolution constitutes write-time concurrency control, assigning each merge operator
  an isolation precondition. `ABSTRACT-VERIFIED`
- [2606.17182](https://arxiv.org/abs/2606.17182) treats the phenomenon within the
  phantom class of the same lattice. `FULL-TEXT`

### Open defects

- [mem0 #6515](https://github.com/mem0ai/mem0/issues/6515) (Python SDK) and
  [#6531](https://github.com/mem0ai/mem0/issues/6531) (TypeScript SDK): concurrent
  `add()` calls pass hash-based deduplication against a stale snapshot, producing
  persistent duplicate memories. The proposed remedy acquires a lock within a single
  process and does not address multi-worker deployment. Issue #6515 opened 2026-07-22
  with one comment; #6531 opened 2026-07-23 with none.

---

## 3. Phantom on a predicate (orphan determination)

A deletion is predicated on a condition — that an entity retains exactly one reference
— which a concurrent insertion falsifies between evaluation and execution.

### Published treatments

- [2606.17182](https://arxiv.org/abs/2606.17182) presents this as its
  snapshot-insufficiency observation, parallel to classical write skew, resolved at L1
  and above. `FULL-TEXT`

### Open defects

- [graphiti #2159](https://github.com/getzep/graphiti/issues/2159): `remove_episode`
  executing concurrently with `add_episode` discards the new episode's entity and its
  associated fact. The reporter observed divergence in 19 of 20 iterations on Neo4j; a
  second contributor measured the interval between reference count and deletion at
  approximately 2.7 ms median on FalkorDB. A fix is proposed in PR
  [#2177](https://github.com/getzep/graphiti/pull/2177), open since 2026-11-19.

---

## 4. Stale read and mixed-revision recall

A reader observes a partially applied set of writes and proceeds from a state that was
never committed as a whole.

### Published treatments

- [2611.19264](https://arxiv.org/abs/2611.19264) reports an empirical measurement:
  updates arriving between reads in Hindsight and Cognee produced 199 conflicting
  recalls out of 12,010. A read/write lock is compared against optimistic epoch
  validation. This constitutes the closest available prevalence measurement on
  deployed memory services. `title+snippet`
- [Token Coherence 2603.15183](https://arxiv.org/abs/2603.15183) adapts MESI coherence
  to shared artifacts, with TLA+-verified single-writer safety and bounded staleness.
  `not re-verified`

### Open defects

- [graphiti #2211](https://github.com/getzep/graphiti/pull/2211): `add_episode_bulk`
  resolves edges against the pre-batch graph, so contradictions arising within a batch
  are not detected.

---

## 5. Retraction and causal cascade

A planning or supervising agent withdraws a decision, but writes already derived from
that decision persist and are indistinguishable from writes derived from accepted
decisions.

This mode merits particular attention because it is frequently characterized as
unexplored and is in fact formalized, verified, and measured.

### Published treatments

- [2606.17182](https://arxiv.org/abs/2606.17182) §V-K designates this the A3
  causal-cascade anomaly. Across three model families, supervisors retracted plans at
  rates of 0%, 15.5% and 44.5%; the unguarded baseline corrupted shared state in all
  120 retracted sessions, while the verified L2 runtime prevented corruption in 0 of
  120 (95% CI [0, 2.5%]). `FULL-TEXT`
- [MemTX 2607.23929](https://arxiv.org/abs/2607.23929) provides retraction repair.
  `ABSTRACT-VERIFIED`
- [PLACEMEM 2607.04089](https://arxiv.org/abs/2607.04089) describes versioned memory
  capsules with concurrency-safe cascading invalidation. `ABSTRACT-VERIFIED`
- [ChronoMem 2607.27773](https://arxiv.org/abs/2607.27773) provides per-write snapshots
  and semantic rollback. `title only`

### Open defects

No defect report in this corpus is framed in these terms. The nearest reported symptom
is CLICS-TH/clics#270, in which subagents write unapproved memory twice within a single
gate.

---

## 6. Non-atomic multi-store write

A logical memory write spans two stores — for instance a vector index and a relational
history — without a transaction spanning both, so partial failure leaves inconsistent
state.

### Published treatments

- [SagaLLM 2503.11951](https://arxiv.org/abs/2503.11951) applies the saga pattern with
  compensation, relaxing ACID guarantees. The scope is workflow-level recovery rather
  than memory-write isolation. `ABSTRACT-VERIFIED`
- [Engineering Reliable Commit Gates 2609.10969](https://arxiv.org/abs/2609.10969)
  describes atomic commit-time guards for state-changing agent actions.
  `not re-verified`
- [Zeta-Lite 2609.01818](https://arxiv.org/abs/2609.01818) commits a relational fact and
  its associated vector within a single transaction, and additionally provides
  copy-on-write database branching, forking, merging and rebasing.
  `ABSTRACT-VERIFIED`

### Open defects

- [mem0 #7879](https://github.com/mem0ai/mem0/issues/7879): `add()` persists the vector
  despite failure of the history write, so a subsequent retry duplicates the record.
- [mem0 #7792](https://github.com/mem0ai/mem0/issues/7792): a FAISS update deletes the
  original record before rejecting an invalid vector, so a failed update destroys data.

---

## 7. Ordering violation

Operations intended to be serialized execute out of order, or a check-then-act race
admits a second worker to a region intended to be exclusive.

### Published treatments

- [2606.17182](https://arxiv.org/abs/2606.17182) formalizes tool-effect reordering,
  removed by an L3 commit-order sequencer, and exhibits the anomaly in LangGraph's
  `ToolNode`. `FULL-TEXT`
- CoAgent (CoRR 2606.15376) specifies a pre-determined serialization order with
  order-filtered reads and inverse-tool undo of misordered writes. The shared resources
  considered are version-control trees and documents rather than agent memory.
  `title+snippet`

### Open defects

- [graphiti #2223](https://github.com/getzep/graphiti/issues/2223): multiple queue
  workers start for a single group, causing out-of-order episode processing. The
  one-worker-per-group guarantee is defeated by a check-then-start race.
- [langgraph #8039](https://github.com/langchain-ai/langgraph/issues/8039): write
  ordering is not enforced under `durability=sync`.

---

## 8. Semantic conflict under syntactic convergence

A merge completes without reported conflict and yields a semantically incorrect result.

### Published treatments

- [CodeCRDT 2510.18893](https://arxiv.org/abs/2510.18893) reports 100% convergence and
  zero merge failures across 600 trials alongside semantic conflict rates of 5–10%,
  establishing that CRDT convergence does not entail semantic correctness.
  `ABSTRACT-VERIFIED`
- [AgentRoom 2608.23740](https://arxiv.org/abs/2608.23740) concludes that coordination,
  rather than parallelism or CRDT merge, is the determining design choice.
  `ABSTRACT-VERIFIED`
- [MELD 2608.16357](https://arxiv.org/abs/2608.16357) employs a per-claim status CRDT in
  which conflicts are preserved rather than silently discarded. `not re-verified`

### Open defects

No defect report in this corpus corresponds to this mode. The mode does not by
construction surface as an error condition, which plausibly accounts for its absence
from issue trackers.

---

## 9. Summary of the literature–practice divergence

| Failure mode | Published treatment | Verified | Open defect in a deployed library |
|---|---|---|---|
| 1. Lost update | yes | yes (L0→L1) | mem0, langgraph, cognee |
| 2. Deduplication TOCTOU | yes | partially | mem0 (both SDKs) |
| 3. Predicate phantom | yes | yes | graphiti (fix pending) |
| 4. Stale read | yes, with measurement | no | graphiti |
| 5. Retraction cascade | yes, with measurement | yes (A3) | none reported |
| 6. Non-atomic multi-store | yes | no | mem0 |
| 7. Ordering violation | yes | yes (L3) | graphiti, langgraph |
| 8. Semantic conflict | yes, with measurement | no | none reported |

Of the eight modes catalogued, all have at least one published treatment and four have
an associated open defect in a widely deployed library.

---

## 10. Surveys characterizing the area as open

The following surveys are useful for framing. Their publication dates precede the
majority of the primary literature indexed above, and their characterizations should be
interpreted accordingly.

- [2603.07670](https://arxiv.org/abs/2603.07670) §6.6, §9.6: "consistency under
  concurrent writes — what happens when two agents update shared memory
  simultaneously?" and "distributed memory with merge semantics, hierarchical shared
  memory with per-agent caches — remain wide open." No prior work addressing the
  question is cited. `FULL-TEXT`
- [2602.06052](https://arxiv.org/abs/2602.06052) §4.2.3 surveys only single-writer and
  LLM-adjudicated remedies: Memory-R1 permits a single mutating agent, and WebCoach
  defers writes until an episode completes. `FULL-TEXT`
- [2512.13564](https://arxiv.org/abs/2512.13564) §7.5 identifies write contention in a
  single clause. `FULL-TEXT`
- [2603.10062](https://arxiv.org/abs/2603.10062) is a position paper identifying
  multi-agent memory consistency as the most pressing open challenge.
  `ABSTRACT-VERIFIED`
