# Tiger Den Development Notes

This document records implementation and research notes that do not belong in the project's Canon or Law.

## Current Foundation

Tiger Den began as an idea for an ultimate collection of reusable "code Legos." The project has since been deliberately narrowed to a more defensible mission: map the computational primitives that already exist in the world's software rather than attempting to store all of their implementations.

The central distinction is:

> **The world contains the code. Tiger Den contains the map.**

## Initial Design Direction

The first engineering phase should be discovery rather than synthesis.

The system should eventually be able to:

1. survey a defined software corpus;
2. identify candidate reusable components;
3. normalize their descriptions and interfaces;
4. compare candidates at the contract and behavioral level;
5. cluster potentially equivalent implementations;
6. preserve meaningful distinctions;
7. record source locations and provenance;
8. attach evidence and confidence to claims;
9. expose relationships between primitives and implementations;
10. provide a machine-readable map that can be queried and extended.

No claim is made yet about how many primitives exist. Measuring that question is part of the research.

## Working Vocabulary

**Primitive** — an identifiable computational capability with a meaningful contract and behavior.

**Implementation** — a concrete realization of a primitive in an existing software artifact.

**Material** — an implementation regarded as useful evidence or an exemplar of a primitive, together with its relevant properties and provenance.

**Map** — the structured body of identities, locations, contracts, relationships, evidence, and provenance maintained by Tiger Den.

**Corpus** — the explicitly defined collection of software being surveyed for a given research operation.

**Exemplar** — an implementation selected because it provides useful evidence or preserves a meaningful property of a primitive. Exemplar does not mean universally best.

## Research Posture

The project should begin with small, controlled corpora. Early machinery should favor transparent measurements and inspectable intermediate artifacts over opaque claims of comprehensive understanding.

The first useful milestone is not a giant catalog. It is a demonstrably reproducible survey pipeline that can take a known corpus and produce useful candidate primitive records.

## Open Questions

These questions are intentionally unresolved until evidence or experimentation provides an answer:

- What is the minimum useful definition of a primitive?
- Which properties can be derived automatically and which require tests or human review?
- How should semantic equivalence be represented?
- How should multiple valid implementations of one primitive be related?
- What corpus is appropriate for the first empirical survey?
- What evidence threshold promotes a candidate into the established map?
- Which data formats best support both humans and future agents?
- How should the map represent uncertainty and competing classifications?

These are research questions, not invitations to guess.
