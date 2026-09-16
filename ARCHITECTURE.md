# Tiger Den Architecture

**Status:** Foundational
**Scope:** Tiger Den only

This document defines the initial architecture for Tiger Den. It is intentionally conservative: the architecture exists to support the map before attempting to build a toolbox, composer, or forge.

## 1. Architectural Principle

Tiger Den is a **computational cartography system**.

> **The world contains the code. Tiger Den contains the map.**

The system therefore treats external software as surveyed terrain. Tiger Den records identities, relationships, evidence, provenance, and locations; it does not attempt to become a universal repository for the implementations it discovers.

The architecture must remain subordinate to the Canon and Law. If evidence shows that an architectural assumption is wrong, the architecture is revised rather than forcing the evidence to fit it.

## 2. System Boundary

Tiger Den has five conceptual layers:

```text
EXTERNAL SOFTWARE CORPUS
        │
        ▼
┌──────────────────────┐
│  DISCOVERY & INTAKE  │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ IDENTITY & ANALYSIS  │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ EVIDENCE & PROVENANCE│
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│      MAP / CATALOG   │
└──────────┬───────────┘
           ▼
┌──────────────────────┐
│ QUERY / PRESENTATION │
└──────────────────────┘
```

These are conceptual boundaries, not yet a prescribed directory tree or implementation technology.

### 2.1 Discovery & Intake

Responsible for locating and defining material to be surveyed.

Inputs may eventually include repositories, release archives, package sources, standards implementations, system software, and other explicitly authorized corpora.

Discovery records **where material came from and what was actually surveyed**. It must not silently expand the corpus.

### 2.2 Identity & Analysis

Responsible for determining what a surveyed artifact appears to contain and identifying candidate computational capabilities.

This layer may use source structure, symbols, APIs, documentation, tests, dependency information, static analysis, dynamic observation, and other evidence. No single signal establishes primitive identity by itself.

The output is initially a set of candidates, not facts.

### 2.3 Evidence & Provenance

Responsible for preserving the chain from claim back to source material and recording the strength and kind of evidence supporting it.

Evidence is a first-class architectural object, not merely a note attached to a result.

### 2.4 Map / Catalog

Responsible for the durable representation of primitive identities, implementations, contracts, properties, relationships, provenance, evidence, and uncertainty.

The map describes the terrain. It does not own the terrain.

### 2.5 Query / Presentation

Responsible for making the map useful to humans and machines.

The presentation layer must not silently strengthen claims. A provisional relationship must remain visibly provisional when presented.

## 3. Core Entities

The initial conceptual data model contains these entities:

### Primitive

An abstract computational capability recognized by Tiger Den.

A Primitive has, where known:

- stable internal identity;
- human-readable description;
- contract;
- meaningful properties and invariants;
- relationships to other primitives;
- evidence supporting its identity;
- confidence/status;
- unresolved questions.

A Primitive is **not** synonymous with a repository, function name, source file, package, or programming language construct.

### Implementation

A concrete realization found in external material.

An Implementation records enough source identity to locate the exact realization examined, including repository/source location and version or commit when available.

One Primitive may have many Implementations.

### Source

The external software artifact from which an Implementation or other evidence was obtained.

Source identity should include the strongest available provenance information, such as project, repository, release, commit, archive identity, or equivalent immutable reference.

### Contract

The meaningful behavioral interface of a capability: inputs, outputs, preconditions, postconditions, invariants, failure behavior, side effects, resource assumptions, and other constraints when known.

A type signature may be part of a Contract but is not necessarily the whole Contract.

### Evidence

A traceable observation or artifact supporting a claim.

Examples include:

- source inspection;
- documentation;
- tests;
- observed execution;
- benchmark measurements;
- dependency or symbol analysis;
- formal or mechanical verification;
- standards conformance evidence.

Evidence must identify what was observed and avoid silently embedding interpretation as fact.

### Relationship

A typed connection between map entities.

Examples may include:

- implements;
- candidate-equivalent-to;
- verified-equivalent-to;
- specializes;
- composes-with;
- depends-on;
- supersedes;
- derived-from.

Relationship types are part of the research model and must not be invented merely to make a graph look complete.

### Property

A characteristic of an Implementation or Primitive, such as determinism, complexity, memory behavior, portability, security-relevant behavior, or resource requirements.

Every property should carry its provenance/status. A property may be observed, measured, declared, derived, tested, or unknown.

## 4. Claim Lifecycle

Tiger Den uses the following progression:

```text
SOURCE MATERIAL
      ↓
  OBSERVATION
      ↓
    CANDIDATE
      ↓
  CHARACTERIZED
      ↓
   RELATED
      ↓
   VERIFIED
      ↓
   CATALOGED
```

A candidate does not become an established Primitive merely because multiple agents agree that it sounds plausible.

The exact promotion criteria are intentionally deferred until empirical work shows what evidence is practical and reliable.

## 5. Evidence Model

Evidence and claim status are separate dimensions.

### Evidence classes

The initial evidence vocabulary is:

- **Raw** — directly captured source material or observation.
- **Derived** — mechanically or analytically produced from raw evidence.
- **Observation** — a factual statement about what was observed.
- **Interpretation** — an explanation or inference drawn from observations.
- **Unknown** — an explicitly unresolved matter.

These classes describe the nature of the record, not whether a conclusion is correct.

### Confidence / status

The initial status vocabulary is:

- **Confirmed** — supported by evidence sufficient for the current verification standard.
- **Strong** — substantial evidence exists, but the highest verification standard has not been met.
- **Provisional** — plausible and supported, but materially unresolved.
- **Unknown** — insufficient evidence to characterize the claim.
- **Refuted** — evidence contradicts the claim.

A record should preserve both dimensions where useful. For example, an observation may be raw evidence while the interpretation derived from it remains provisional.

### Minimum provenance fields

Where applicable, an evidence record should preserve:

- Evidence ID;
- source/project identity;
- source location;
- exact version, commit, release, or archive identity;
- symbol, function, file, section, test, or other locator;
- capture/analysis date;
- evidence class;
- claim supported;
- method used to obtain it;
- limitations;
- confidence/status.

The model must allow missing information to be represented explicitly rather than fabricated.

## 6. Semantic Equivalence

Tiger Den must distinguish several different questions:

1. Do two artifacts look similar?
2. Do they appear to implement the same intended capability?
3. Do their contracts match?
4. Does their observable behavior match within a defined domain?
5. Do their relevant properties and constraints match?

These questions must not collapse into a single similarity score.

A future equivalence engine may use multiple signals, but an automated similarity result is evidence for investigation, not automatic proof of primitive identity.

## 7. Multiple Implementations

The map is many-to-one and one-to-many by design:

```text
                 ┌── Implementation A
                 │
Primitive ───────┼── Implementation B
                 │
                 └── Implementation C
```

Different implementations may legitimately remain separate because of performance, portability, security, licensing, dependencies, environment, resource requirements, or other meaningful differences.

The map therefore canonicalizes **descriptions and relationships**, not necessarily code.

## 8. Corpus Discipline

Every research run must have a defined corpus.

A corpus definition should identify, as appropriate:

- what sources are included;
- what sources are excluded;
- the time/version boundary;
- the discovery method;
- the survey scope;
- known coverage limitations.

Statements about prevalence or redundancy must be qualified by the corpus from which they were measured.

Tiger Den must never imply that a bounded survey is a census of all software unless evidence actually supports that claim.

## 9. Reproducibility

A research result should be reproducible from its recorded source identity and method whenever practical.

Future survey machinery should favor deterministic, inspectable intermediate artifacts. Opaque model output may assist discovery, but important map claims require traceable evidence.

The architecture should permit a future investigator or agent to answer:

> **What did you look at, what did you see, what did you infer, and why did this become part of the map?**

## 10. Storage Direction

The initial project should prefer simple, inspectable representations over premature infrastructure.

The eventual storage format must support:

- stable identifiers;
- structured records;
- provenance;
- evidence;
- typed relationships;
- uncertainty;
- versioning;
- machine access;
- human review.

A specific database, graph engine, serialization format, or directory layout is deliberately **not** frozen by this document. That decision should follow a concrete pilot and the shape of real records produced by it.

## 11. Automation Boundary

Automation is encouraged where it improves repeatability, coverage, or analysis, but it does not receive authority to convert inference into fact.

A future automated pipeline may discover and rank candidates, extract contracts, compare implementations, generate relationships, and run verification. Promotion into stronger catalog status remains governed by evidence and the project's Law.

Any future autonomous synthesis system is outside the current architectural boundary until the map and verification machinery demonstrate that such a system is justified.

## 12. Initial Build Order

The architecture implies this order of work:

```text
1. DEFINE A CONTROLLED CORPUS
          ↓
2. BUILD REPRODUCIBLE DISCOVERY
          ↓
3. CAPTURE RAW EVIDENCE
          ↓
4. PRODUCE CANDIDATE RECORDS
          ↓
5. CHARACTERIZE CONTRACTS / PROPERTIES
          ↓
6. RELATE IMPLEMENTATIONS
          ↓
7. VERIFY SELECTED CLAIMS
          ↓
8. STORE THE MAP
          ↓
9. QUERY / PRESENT THE MAP
```

Only after this foundation produces useful empirical results should Tiger Den commit to larger-scale indexing, semantic composition, gap detection, or synthesis.

## 13. Architectural Guardrails

- The map must not become a code dump.
- A similarity detector must not become an identity oracle.
- A generated description must not become evidence merely because it is well written.
- A single implementation must not silently become the canonical implementation of a primitive.
- Missing provenance must remain missing rather than being guessed.
- Research scope must remain explicit.
- Claims must remain revisable.
- New machinery must earn its place by improving the map.

## 14. Architectural Change Rule

This architecture is foundational but not immutable.

Changes that alter the project's mission, evidence semantics, authority model, or external boundaries require explicit human approval.

Implementation details may evolve as evidence accumulates, provided they remain consistent with the Canon and Law.

> **Build the map before building the machine that acts on the map.**
