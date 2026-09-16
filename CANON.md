# Tiger Den Canon

**Status:** Foundational
**Scope:** Tiger Den only

## 1. Purpose

Tiger Den is a map of existing computational knowledge.

Its purpose is to discover, identify, characterize, relate, and locate reusable computational primitives that already exist in the world's software corpus.

Tiger Den is not intended to contain the world's code. The implementations remain where they already live; Tiger Den records what has been discovered about them and where they can be found.

## 2. The Central Idea

> **Find the Legos humanity already made. Just the primitives.**

The project treats the world's existing software as a surveyable landscape. Repeated implementations are evidence of potentially reusable underlying capabilities, but textual similarity alone does not establish primitive identity.

## 3. What Tiger Den Is

Tiger Den is:

- a computational atlas;
- a catalog of candidate and established primitives;
- a provenance and evidence record;
- a semantic relationship map;
- a research instrument for measuring software redundancy and reuse potential.

## 4. What Tiger Den Is Not

Tiger Den is not:

- a mirror of GitHub;
- a package manager;
- a universal code archive;
- a replacement for existing implementations;
- a claim that every implementation of a capability should be reduced to one implementation;
- an autonomous code-generation system by default.

Synthesis may become useful later, but discovery and verification come first.

## 5. Primitive Identity

A primitive is an identifiable computational capability with a meaningful contract and observable or documented behavior. Names, syntax, programming language, repository, API spelling, and implementation style are evidence about a candidate; they are not sufficient by themselves to establish identity.

Two implementations may represent the same primitive while differing substantially in source code. Conversely, similar source code may represent different primitives when contracts, invariants, or behavior differ.

## 6. Evidence Before Assertion

Tiger Den must distinguish what is known from what is inferred.

A catalog record should preserve, where available:

- source location;
- exact version or commit;
- implementation identity;
- contract;
- observed behavior;
- declared properties;
- tests or other verification evidence;
- relationships to other records;
- known limitations;
- confidence and unresolved questions.

Unknown is a valid result.

## 7. Provenance Is Part of the Map

A primitive without trustworthy provenance is an incomplete map entry. Claims must remain traceable to the material from which they were derived.

Tiger Den must not silently mix observations from different source versions when that distinction could change the claim.

## 8. Canonicalization

The project seeks canonical **descriptions of primitives**, not necessarily canonical implementations.

Multiple implementations may legitimately coexist because they can differ in performance, portability, resource requirements, security properties, dependencies, licensing, environment, or other meaningful characteristics.

## 9. Research Discipline

The project proceeds from observation toward increasingly strong claims:

```text
DISCOVER
   ↓
IDENTIFY
   ↓
CHARACTERIZE
   ↓
RELATE
   ↓
VERIFY
   ↓
CATALOG
```

Automation may accelerate these steps, but automation does not turn an unverified inference into fact.

## 10. The Long-Term Vision

The long-term objective is a machine-readable map from which a builder can discover the computational materials already available to humanity and understand how those materials relate and compose.

The map comes first.

The toolbox, composition machinery, and any future forge come later and must be justified by evidence gathered through the map.
