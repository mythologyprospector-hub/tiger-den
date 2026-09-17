# Tiger Den First Corpus Pilot

**Status:** Foundational research plan
**Scope:** Tiger Den only

This document defines the first bounded corpus experiment required by the Research Protocol. It is deliberately small. The purpose is to test Tiger Den's mapping method, not to make a claim about the software universe.

## 1. Pilot Objective

The pilot asks a narrow empirical question:

> Can Tiger Den take a small, version-pinned body of existing software, identify repeated computational capabilities, distinguish implementations from abstract primitives, and preserve enough evidence to explain every important classification?

The pilot is successful if the answer can be demonstrated with inspectable records. The number of primitives discovered is secondary.

## 2. Corpus Selection Criteria

The first corpus must satisfy all of these requirements:

- public and independently inspectable;
- version-pinnable to immutable source identities;
- legally suitable for analysis and redistribution of metadata;
- small enough for a complete pilot survey;
- mature enough to provide meaningful implementations rather than toy examples;
- overlapping enough in functionality to test relationship analysis;
- sufficiently varied in implementation context to expose meaningful distinctions;
- documented and tested well enough to support verification;
- reproducible by another investigator.

## 3. Proposed Pilot Shape

The initial corpus should contain **three to five mature open-source projects** selected to create intentional overlap in computational capabilities while avoiding a corpus so large that the evidence chain becomes opaque.

The preferred capability families for the first pass are:

- parsing and tokenization;
- hashing and checksums;
- encoding/decoding and serialization;
- compression or decompression;
- searching, sorting, or other fundamental data operations;
- memory/data-structure primitives.

The exact projects and immutable versions are to be recorded in the corpus manifest before analysis begins.

## 4. Why This Shape

A first corpus made from only one project could demonstrate extraction but could not adequately test cross-project primitive identity.

A huge corpus would make it difficult to determine whether a failure came from the mapping model or from scale.

Three to five mature projects provide a useful middle ground: enough terrain for repeated capabilities and meaningful distinctions, while retaining a tractable evidence surface.

## 5. Required Corpus Manifest

Before surveying begins, create a machine-readable manifest containing at least:

- corpus identifier;
- project name;
- canonical project location;
- exact commit, release, or archive identity;
- license identifier and source location;
- languages/platforms represented;
- inclusion rationale;
- exclusions or relevant scope limits;
- survey date;
- discovery method;
- known coverage limitations.

No project enters the empirical corpus merely because it is convenient to analyze.

## 6. Pilot Survey Boundary

The first survey should concentrate on **discoverable, externally meaningful computational capabilities**, rather than attempting to classify every helper function.

A candidate is worth carrying forward when there is enough evidence to describe a capability independently of its local function name or source-file organization.

The pilot should deliberately include negative cases:

- functions that look similar but serve different contracts;
- functions with the same purpose but materially different constraints;
- wrappers that should not become separate primitives;
- project-specific machinery that does not generalize;
- candidates for which evidence is insufficient.

These cases are essential for testing whether Tiger Den can avoid false deduplication.

## 7. First Record Set

The pilot should initially produce three linked record classes:

### Source Records

What exact external material was examined.

### Implementation Records

What concrete capability-bearing artifacts were found in that material.

### Primitive Candidate Records

What abstract computational capability the evidence suggests may exist independently of a particular implementation.

Relationships between these records should be explicit rather than encoded indirectly in prose.

## 8. Verification Target

After candidate extraction, select a small number of cross-project relationships for deeper verification.

Selection should favor relationships that test the difficult cases rather than merely confirming obvious matches.

At least one verification target should attempt to distinguish:

- genuinely equivalent capability;
- similar implementation with a materially different contract;
- insufficient evidence.

## 9. Decision Gate

The corpus is considered pinned only when the manifest records the exact source identities and scope boundaries.

After pinning, changing the corpus requires a new documented research decision rather than silently replacing the terrain underneath an existing result.

## 10. What We Are Not Doing Yet

The pilot does **not** attempt to:

- crawl GitHub universally;
- create a global software census;
- build a graph database;
- assign a universal similarity score;
- synthesize missing code;
- declare a final periodic table of computation;
- choose one canonical implementation for every capability.

Those are downstream questions. The pilot exists to determine whether the map can be built faithfully in the first place.

> **Start with a small patch of real terrain. Prove the map works. Then widen the horizon.**
