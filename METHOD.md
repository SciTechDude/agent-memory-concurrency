# Construction Method and Coverage Limitations

## 1. Search procedure

The corpus was assembled on 2026-11-26 using five concurrent search procedures, each
assigned a distinct source:

| Lane | Source | Approach |
|---|---|---|
| A | arxiv API | Queries on concurrency, isolation and consistency terminology |
| B | arxiv API | Queries on multi-agent coordination over shared state |
| C | Semantic Scholar API | Broad queries, 2025–2026 restricted |
| D | arxiv | Survey papers, read in full text, with attention to stated open problems |
| E | OpenReview, Crossref, CIDR, HotOS, GitHub | Non-arxiv venues and defect trackers |

Approximately 45 publications were judged directly relevant. Lane D read ten surveys in
full text. Lane E additionally catalogued defect reports across six agent-memory and
agent-framework libraries.

## 2. Verification performed

All 90 arxiv identifiers occurring in the corpus were submitted to the arxiv API and
resolved; titles and submission dates were confirmed against the returned records. Three
further identifier-like strings were examined and found to be fragments of IEEE DOI
numbers rather than arxiv identifiers; they are not treated as citations.

Where the full text of a publication was consulted, the relevant section is identified
in [MATRIX.md](MATRIX.md). Where only an abstract or a search excerpt was consulted,
the entry is tagged accordingly. No entry is presented as more strongly sourced than it
is.

## 3. Methodological limitations

### 3.1 Terminological bias

The query vocabulary was specified centrally and applied across all five lanes. The
lanes therefore varied by *source* but not by *terminology*. Because the subject area
exhibits the terminological divergence described in
[README.md](README.md#2-terminological-mapping), source diversity does not confer
independence on a conclusion that depends on terminology coverage.

This limitation was material. Four of the five lanes independently returned a null
result on one specific question, and that null result was subsequently shown to be
incorrect: the relevant publication uses a naming convention absent from the query set.
Agreement among concurrent search procedures that share a query vocabulary should not
be interpreted as corroboration.

### 3.2 Absence of citation-graph traversal

The procedure consisted of keyword queries. No lane traversed reference lists or
forward citations. The publication identified in §3.1 is cited by a publication the
lanes had already retrieved, and would have been reached in a single citation step.
Keyword retrieval is lexical; citation traversal is semantic. Future extension of this
index should prioritize the latter.

### 3.3 Rate limiting

Concurrent querying of shared APIs by multiple lanes induced rate limiting. The arxiv
API returned HTTP 429 to three lanes, and the Semantic Scholar API throttled one lane
such that retries required approximately five minutes each; that lane completed three
of eight planned queries. Queries that did not execute are recorded in
[topics/00-NEGATIVE-RESULTS.md](topics/00-NEGATIVE-RESULTS.md) as access failures and
are not counted as null results.

### 3.4 Survey recency

Lane D read ten surveys in full text and found no treatment of concurrent writes. The
surveys consulted were published between December 2025 and August 2026, whereas the
majority of the primary literature indexed here was published between June and
September 2026. The lane's null result is therefore attributable to corpus recency
rather than to absence, and the surveys' own characterizations of the area as
unexplored should be read as statements about the period preceding their publication.

### 3.5 Unreachable venues

The following could not be searched directly by the methods available: dblp (bot
blocking), the ACL Anthology (search function not programmatically accessible), and the
proceedings of VLDB, SIGMOD and the USENIX conferences. OpenReview forum pages were
accessible only through search-result excerpts. Absence of records from these venues
carries little evidential weight.

## 4. Outstanding verification tasks

1. Manual inspection of dblp tables of contents for VLDB 2026, SIGMOD 2026 and the
   USENIX 2026 conferences.
2. Full-text reading of entries presently tagged `title only` or `not re-verified`.
3. Re-execution of the queries recorded as access failures in
   [topics/00-NEGATIVE-RESULTS.md](topics/00-NEGATIVE-RESULTS.md).
4. Citation-graph traversal, forward and backward, from the publications identified as
   most central in [MATRIX.md](MATRIX.md).
5. Full-text reading of the CIDR 2026 agent-first data systems papers, which approach
   the subject from a database-systems perspective not otherwise represented here.

## 5. Reproducibility

The search procedures were executed by LLM-based agents operating against public APIs,
with results recorded by source lane in [topics/](topics/). Provenance tags distinguish
records confirmed against primary sources from records originating in tool-generated
summaries. The distinction is preserved rather than flattened, so that any reader may
determine which claims rest on direct inspection.
