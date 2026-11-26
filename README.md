# Agent Memory Under Concurrency: An Index of Research and Open Defects

A curated index of published research and open production defect reports concerning
the correctness of shared memory in multi-agent large language model systems when two
or more agents write concurrently.

## 1. Motivation

Memory systems for LLM agents are extensively evaluated for retrieval quality. A
registry of such benchmarks is maintained separately
([memory-bench-registry](https://github.com/Fengzdadi/memory-bench-registry)). By
contrast, the question of whether these systems remain *correct* under concurrent
writes has received comparatively little systematic evaluation, despite a cluster of
relevant publications appearing since mid-2025 and a substantial number of
corresponding defect reports in deployed libraries.

This index records both bodies of evidence and relates them to one another. Three
observations motivate its construction.

**1.1 Terminological divergence.** The subject area has developed at least three
distinct naming conventions — classical database terminology, formal-methods
terminology, and practitioner terminology — which do not consistently cross-reference
one another. A literature search conducted in one convention may return null results
for a concept that is well covered in another. Section 2 provides a mapping.

**1.2 Divergence between literature and practice.** Several failure modes catalogued
here have published fixes, in some cases formally verified and with measured overheads,
while the same failure modes remain open in shipped libraries. [MATRIX.md](MATRIX.md)
presents this pairing by failure mode.

**1.3 Asymmetry of negative evidence.** A null search result is evidence about a query
string, not about a concept. [topics/00-NEGATIVE-RESULTS.md](topics/00-NEGATIVE-RESULTS.md)
therefore distinguishes searches that executed and returned nothing relevant from
searches that could not be executed. Several venues were not reachable by the methods
used; those gaps are recorded as access failures rather than counted as absence.

## 2. Terminological mapping

| Practitioner formulation | Corresponding term in the literature |
|---|---|
| abandoned or orphaned write | retraction; causal cascade; compensating action |
| stale read | stale-generation; mixed-revision recall; split-view |
| duplicate entry | hash-dedup TOCTOU; phantom |
| contradictory records | supersession; bitemporal validity; belief-drift skew |
| overwritten update | lost update; write skew; last-write-wins |
| undoing an incorrect write | compensation; saga; semantic rollback |

The terms *abandoned*, *orphan*, *speculative* and *rollback* do not occur in
[2606.17182](https://arxiv.org/abs/2606.17182), the work that most directly formalizes
writes derived from a withdrawn decision. That work designates the phenomenon a
*causal-cascade* anomaly and the affected executions *retracted sessions*. A search
restricted to the practitioner formulation returns no result for this paper.

## 3. Provenance classification

Each entry carries a tag indicating the strength of its sourcing.

| Tag | Definition |
|---|---|
| `FULL-TEXT` | The relevant section of the full text was consulted. |
| `ABSTRACT-VERIFIED` | The abstract was read at the primary source. |
| `title+snippet` | Title and a search-result excerpt were consulted; the abstract was not. |
| `title only` | The record surfaced in a search; no abstract or excerpt was read. |
| `not re-verified` | The record originates from a summarizing tool and has not been confirmed against the primary source. To be treated as a lead rather than a citation. |

All 90 arxiv identifiers appearing in this corpus were submitted to the arxiv API and
resolved, with title and submission date confirmed. Records that could not be verified
are labelled accordingly.

## 4. Inclusion and exclusion criteria

**Included.** Concurrent writes to shared agent memory; isolation and consistency
models for agent state; lost updates, phantoms, write skew and stale reads in agent
memory; retraction and compensation mechanisms; provenance insofar as it bears on
correcting or withdrawing writes; defect reports in deployed systems demonstrating any
of the foregoing.

**Excluded.** Retrieval and recall benchmarks, which are covered by the registry cited
in Section 1; prompt-construction techniques; memory architectures advancing no
concurrency claim.

## 5. Repository structure

| Path | Contents |
|---|---|
| [MATRIX.md](MATRIX.md) | Failure mode, published treatments, and open defect reports, cross-referenced |
| [METHOD.md](METHOD.md) | Construction method, coverage limitations, outstanding verification tasks |
| [topics/](topics/) | Source corpus organized by subject area |
| [topics/00-NEGATIVE-RESULTS.md](topics/00-NEGATIVE-RESULTS.md) | Null results and access failures, distinguished |

## 6. Limitations

Coverage is uneven and the unevenness is documented rather than concealed. Arxiv and
GitHub are well covered. OpenReview and Crossref are partially covered. The ACL
Anthology, dblp, and the proceedings of VLDB, SIGMOD and the USENIX conferences were
not directly searchable by the methods used; absence of records from those venues
should be given little weight. Several surveys relied upon for framing predate the
majority of the primary literature indexed here by several months, and their
characterizations of the area as unexplored should be read with that in mind.

## 7. Contributing

Additions and corrections are welcome. Contributions of the following kinds are
particularly useful:

1. Publications not represented here, especially from the venues identified as
   under-covered in Section 6.
2. Defect reports in any agent framework or memory library demonstrating a catalogued
   failure mode.
3. Corrections to provenance tags. A mislabelled tag is treated as a defect in this
   index.
4. Manually verified tables of contents for venues listed as unsearchable.

Contributions should state the provenance tag and identify what was in fact consulted.

## 8. License

Index content is released under CC-BY-4.0. Cited publications and defect reports remain
the property of their respective authors.
