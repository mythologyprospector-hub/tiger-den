# Tiger Den Research Protocol

**Status:** Foundational research protocol
**Scope:** Tiger Den only

This document defines how Tiger Den begins empirical work without prematurely claiming a universal map.

## 1. First Empirical Mission

The first mission is:

> **Find the Materials.**

Tiger Den will test its mapping method on a small, explicitly bounded software corpus before attempting broad discovery.

The objective is not to maximize the number of records. The objective is to demonstrate that Tiger Den can reproducibly move from existing software to useful, traceable primitive records.

## 2. Controlled Corpus

Every survey must begin with an explicit corpus definition.

The first corpus should be:

- small enough to inspect and reproduce;
- publicly accessible;
- version-pinned;
- legally suitable for analysis;
- diverse enough to contain repeated computational capabilities;
- familiar enough that results can be sanity-checked;
- bounded enough that coverage can be stated honestly.

The initial corpus selection is intentionally not frozen by this document. It is a research decision to be made from concrete candidate corpora and documented before surveying begins.

A corpus record should state:

- included projects;
- excluded projects or categories when relevant;
- exact releases, commits, or archive identities;
- languages and platforms represented;
- discovery method;
- survey date;
- scope boundaries;
- known coverage limitations.

## 3. Survey Pipeline

The first reproducible pipeline should follow:

```text
DEFINED CORPUS
      ↓
DISCOVERY
      ↓
RAW EVIDENCE
      ↓
CANDIDATE EXTRACTION
      ↓
CHARACTERIZATION
      ↓
RELATION ANALYSIS
      ↓
SELECTED VERIFICATION
      ↓
CATALOG RECORDS
```

Each stage should leave inspectable evidence for the next stage.

## 4. Candidate Discovery

Candidate discovery may use multiple signals, including:

- source structure;
- function and symbol information;
- APIs and interfaces;
- documentation;
- tests;
- dependency information;
- static analysis;
- dynamic observation where appropriate.

Discovery produces candidates. It does not establish primitive identity.

## 5. Characterization

For each useful candidate, the survey should attempt to determine:

- what capability it provides;
- its meaningful inputs and outputs;
- preconditions and postconditions where known;
- failure behavior;
- side effects;
- important invariants;
- resource assumptions;
- relevant properties;
- implementation-specific limitations;
- exact source provenance.

Unknown fields remain explicitly unknown.

## 6. Relationship Analysis

Potential relationships between candidates should be recorded separately from primitive identity.

Examples include:

- possible equivalence;
- implementation of;
- specialization of;
- dependency on;
- composition with;
- derived from.

A relationship must carry evidence and status appropriate to its strength.

Similarity is a discovery signal, not proof of equivalence.

## 7. Verification Sampling

The first survey should select a manageable subset of interesting claims for deeper verification.

Verification may include:

- source-level comparison;
- test comparison;
- controlled execution;
- differential testing;
- property testing;
- standards or specification comparison;
- benchmark measurement where performance is part of the claim.

Verification depth should be recorded rather than implied.

## 8. Expected Research Outputs

The first mission should produce at least:

1. a pinned corpus definition;
2. reproducible discovery results;
3. raw or otherwise traceable evidence;
4. candidate primitive records;
5. characterized implementation records;
6. selected relationship records;
7. verification results for selected claims;
8. a small machine-readable map suitable for inspection;
9. a record of unresolved questions and failures.

The pipeline itself is a research result. A failed or inconclusive experiment is useful if its limitations are documented.

## 9. Success Criteria

The first mission succeeds if an independent investigator can follow the recorded evidence and answer:

- What software was surveyed?
- Which material was examined?
- What was directly observed?
- What was derived or inferred?
- Why was a candidate considered a possible primitive?
- Why was a relationship proposed?
- What was actually verified?
- What remains unknown?

Success does **not** require demonstrating that Tiger Den has found most or all existing primitives.

## 10. Research Discipline

The following rules apply throughout the mission:

- Do not silently enlarge the corpus.
- Do not treat generated text as evidence.
- Do not collapse distinct implementations without evidence.
- Do not promote provisional claims merely to make the map look complete.
- Do not report bounded measurements as universal facts.
- Preserve enough provenance to reproduce important findings.
- Record failures and negative results when they affect interpretation.

## 11. After the Pilot

Only after the pilot is complete should Tiger Den decide, based on observed record shape and research needs, whether it requires:

- a particular serialization format;
- a database or graph store;
- larger-scale indexing;
- automated semantic comparison;
- additional verification machinery;
- broader corpus ingestion.

The pilot determines what machinery is justified.

> **Measure the terrain before building the surveying machine.**
