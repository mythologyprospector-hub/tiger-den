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

## Pilot 001 — Discovery Pass Notes

The first pinned-source discovery pass has now begun against the immutable references recorded in `corpus/manifest.json`. Search results from repository default branches are not being treated as evidence for pinned historical sources; source-level observations are being taken from the pinned commits themselves.

### zlib v1.3.2

The pinned `zlib.h` explicitly defines a stream-oriented compression/decompression interface and documents its buffer, progress, error, format, and initialization contracts.

Observed candidate capability areas:

- streaming compression via `deflate()`;
- streaming decompression via `inflate()`;
- one-step in-memory compression/decompression;
- Adler-32 and CRC-32 integrity calculations;
- raw DEFLATE, zlib-wrapped DEFLATE, and gzip-wrapped DEFLATE handling;
- compression configuration through level, window, memory, and strategy parameters;
- preset dictionary support.

Important observation: these are candidate capability areas, not yet asserted primitive identities. The header itself demonstrates that "compression" contains materially different contracts and operating modes.

The pinned header also states that the decoder checks compressed-data consistency and is intended not to crash on corrupted input. This is evidence of a documented behavioral property, not yet an independently verified property.

### Zstandard v1.5.7

The pinned `lib/zstd.h` explicitly describes:

- simple single-step compression/decompression;
- reusable compression contexts;
- streaming compression;
- dictionary-based compression;
- frame-content-size inspection;
- compressed-frame boundary discovery;
- configurable compression levels, including negative levels and high-memory levels.

The source-level implementation also contains distinct compression/decompression machinery, including match-state structures and decompression window/dictionary handling.

Important distinction: zlib and Zstandard overlap at the broad capability level but their documented contracts and format/algorithm constraints differ. No equivalence claim is made merely from both being compression libraries.

**Provenance/legal note:** the pinned Zstandard header states that the source is licensed under both the BSD-style license in `LICENSE` and GPLv2 in `COPYING`, with the user selecting one of those licenses. The corpus manifest's license field currently records BSD-3-Clause from `LICENSE`; that is incomplete as a description of the licensing notice and should be reconciled before the manifest is treated as final legal metadata.

### LibYAML 0.2.5

Pinned scanner/parser/emitter source provides a particularly clear layered pipeline:

```
input stream → tokens → parser events → serialized output
```

Observed candidate capability areas include:

- lexical scanning/tokenization into YAML tokens;
- syntactic parsing from tokens into events;
- event-based representation of YAML structures;
- emission/serialization of events into YAML output.

These are useful candidates because the source documentation exposes the boundaries between layers instead of requiring Tiger Den to infer them solely from names.

### SQLite 3.53.4

The pinned `src/tokenize.c` contains a character-classification table and `sqlite3GetToken()`, whose documented role is to determine token length and token type.

Observed candidate capability area:

- SQL lexical tokenization / token classification.

This is deliberately treated as a low-level candidate inside a much larger system. The existence of reusable computational machinery inside a project does not make the surrounding application architecture a primitive.

### Current Research State

At this checkpoint:

- corpus identities are pinned;
- empirical discovery has begun;
- raw source observations have been captured;
- candidate capability areas are emerging;
- primitive identity has not yet been declared for these observations;
- cross-project equivalence has not been declared;
- provenance and licensing details remain part of the research record;
- the map's persistent record format is still intentionally unfrozen.

The next research step is to extract candidate records with explicit separation between observation, interpretation, and primitive identity, without prematurely freezing a storage schema.

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


## Pilot 001 — Preliminary Candidate Extraction

Candidate extraction is now separated from primitive declaration.

The current observations support the following **candidate capability families** for further characterization:

**Compression/decompression.** zlib and Zstandard both expose externally meaningful compression and decompression operations, but their contracts, stream formats, tuning parameters, framing, and auxiliary capabilities differ. The correct current relationship is **overlapping capability domain / separate implementations under investigation**, not "same primitive" and not "different primitives" as a settled fact.

**Integrity checksums.** zlib exposes Adler-32 and CRC-32 operations as distinct documented interfaces. These are sufficiently concrete to proceed as separate candidate capabilities for contract characterization. No claim is yet made that either is a final primitive record.

**Lexical tokenization.** LibYAML's scanner and SQLite's tokenizer both expose a recognizable transformation from input characters/bytes toward typed lexical units. Their language grammars, token contracts, state requirements, and output representations differ substantially. This makes them useful cross-domain candidates for testing whether Tiger Den can recognize a common computational shape without incorrectly declaring semantic equivalence.

**Syntactic parsing.** LibYAML's parser consumes tokens and produces parser events. This is a candidate parsing capability with an unusually explicit source-level contract and therefore a strong target for characterization.

**Serialization/emission.** LibYAML's emitter converts parser events into YAML output under documented buffering and output rules. It is a candidate serialization/emission capability, but its YAML-specific contract must remain attached to the candidate rather than being generalized prematurely into a universal "serializer" primitive.

**Format/frame inspection.** Zstandard exposes operations for determining frame content size and locating the compressed size of a frame. These are candidates for characterization as metadata/format-inspection operations rather than being folded into the compression operation merely because they live in the same library.

**Dictionary-assisted compression.** Both the zlib and Zstandard evidence show dictionary-related compression interfaces. This is a promising comparison target, but the dictionaries, format semantics, initialization requirements, and implementation behavior must be characterized before any relationship is asserted.

### Classification discipline

These candidate families are deliberately at different levels of abstraction. That is useful terrain rather than a defect.

The next characterization pass should test each candidate against a common set of questions:

1. What are the inputs and outputs?
2. What preconditions and postconditions are documented?
3. What failures are part of the contract?
4. What state is required across calls?
5. What side effects or resource requirements matter?
6. What observable properties distinguish this candidate from nearby capabilities?
7. Which claims are directly observed, which are derived from source evidence, and which remain interpretation?
8. What exact source locator makes the evidence reproducible?

No candidate is promoted to an established primitive by naming similarity, API similarity, or co-location in a library.

## Current Research State

At this checkpoint:

- corpus identities are pinned;
- empirical discovery has begun;
- raw source observations have been captured;
- candidate capability families have been extracted;
- primitive identity has not yet been declared for these observations;
- cross-project equivalence has not been declared;
- provenance and licensing details remain part of the research record;
- the map's persistent record format is still intentionally unfrozen.

The next research step is characterization of selected candidates against their explicit contracts and observable behavior, without prematurely freezing a storage schema.


## Pilot 001 — Contract Characterization Pass

A first characterization pass was performed against pinned source files. This pass records what the source establishes about candidate contracts; it does not promote candidates to final primitive identities.

### Characterized candidate: zlib streaming decompression

**Observation:** `inflate()` accepts a mutable stream state containing input/output pointers and available byte counts, processes as much input/output as possible, and is intended to be called repeatedly until stream completion or error.

**Inputs:** compressed input bytes plus caller-managed output space and stream state; the caller must maintain the `next_*` and `avail_*` fields as buffers are consumed/refilled.

**Outputs:** decompressed bytes in caller-provided output storage; updated stream position/count state; a return status describing progress, completion, or failure.

**State requirement:** yes. The documented operation is explicitly stream-stateful across calls.

**Failure contract:** documented statuses distinguish malformed/corrupt input, inconsistent stream state, memory exhaustion, missing dictionary, and lack of progress/output space.

**Format scope:** zlib and gzip wrapped DEFLATE are supported by the documented interface, with raw DEFLATE also available through the initialization interface.

**Interpretation:** this is stronger evidence for a distinct *streaming decompression capability* than for a generic decompression primitive. Buffer protocol, stream state, framing, checksums, and error semantics are part of the contract and must not be discarded during normalization.

**Status:** candidate characterized; not promoted.

### Characterized candidate: Zstandard frame content-size inspection

**Observation:** `ZSTD_getFrameContentSize()` examines the beginning of a Zstandard frame and returns either a known decompressed content size, an explicit unknown sentinel, or an error sentinel.

**Inputs:** pointer to frame bytes and available byte count; the source requires enough bytes for the frame header.

**Outputs:** a size value with distinct meanings for known size, unknown size, and malformed/insufficient input.

**State requirement:** none is documented for this operation.

**Failure/uncertainty contract:** unknown content size is deliberately different from an error. The source also warns that an untrusted source can contain an incorrect or intentionally modified size and that callers must enforce their own authorized limits.

**Interpretation:** this is evidence for a format-metadata inspection capability separate from decompression itself. It also demonstrates that "returns a number" is insufficient to describe a contract; sentinel meanings and trust boundaries matter.

**Status:** candidate characterized; not promoted.

### Characterized candidate: LibYAML lexical scanning

**Observation:** `src/scanner.c` explicitly defines scanning as transforming an input stream into a sequence of typed tokens. The source enumerates stream/document boundaries, collection delimiters, keys/values, aliases, anchors, tags, and scalar tokens.

**Inputs:** YAML input stream handled by the scanner state.

**Outputs:** ordered typed token sequence consumed by the parser.

**State requirement:** yes. The scanner maintains parsing/scanning state while recognizing YAML constructs, including indentation and simple-key handling.

**Failure/uncertainty contract:** the source describes scanner-specific complexity and the broader library has explicit error machinery; exact error cases require a deeper API-level characterization before making a generalized robustness claim.

**Interpretation:** this is a well-bounded lexical-analysis candidate whose output contract is materially richer than "split text into words." YAML token types, stream structure, indentation semantics, anchors, tags, and scalar styles are part of the observed contract.

**Status:** candidate characterized; not promoted.

### Characterized candidate: LibYAML syntactic parsing

**Observation:** `src/parser.c` publishes a grammar mapping token sequences into parser events and exposes `yaml_parser_parse()` as the public entry point. The grammar distinguishes implicit/explicit documents, block/flow collections, mappings, sequences, aliases, properties, and scalars.

**Inputs:** scanner-produced token stream through parser state.

**Outputs:** ordered YAML parsing events.

**State requirement:** yes. The parser maintains a token queue and state machine while producing events.

**Contract distinction:** the event stream is not simply a generic AST. It is a YAML-specific event representation whose structure follows the documented grammar.

**Interpretation:** this provides strong evidence for a parsing capability with a precisely observable boundary. Generalizing it to a universal parser primitive would require preserving the language grammar and output representation as part of the contract.

**Status:** candidate characterized; not promoted.

### Characterized candidate: SQLite lexical tokenization

**Observation:** `src/tokenize.c` defines character classes and `sqlite3GetToken()` logic for splitting SQL input into tokens. The implementation handles operators, comments, quoted strings/identifiers, numeric forms, identifiers, variables, and illegal characters. The source explicitly states that the lookup-table classification is chosen for speed.

**Inputs:** SQL input characters/bytes at the current scan position.

**Outputs:** token type plus token length, allowing the caller to advance through the input.

**State requirement:** the core token operation is position-based and does not require a general parser state object merely to classify the next token; broader SQLite tokenization behavior also depends on surrounding compilation configuration and generated keyword data.

**Observable property:** the source documents an intentional performance mechanism: character classification through a lookup table rather than direct switching on character values.

**Interpretation:** this is a strong candidate for a lexical token-recognition operation, but its SQL-specific token vocabulary and SQLite compatibility behavior must remain explicit.

**Status:** candidate characterized; not promoted.

### Cross-candidate finding

The characterization pass exposes a useful pattern for Tiger Den: candidates can share a computational shape without sharing a primitive contract. LibYAML scanning and SQLite tokenization both recognize lexical units, yet their token vocabularies, grammar assumptions, state models, and outputs differ. Likewise, zlib and Zstandard both compress/decompress data, while their framing and operational contracts differ.

The map therefore needs to preserve both **capability shape** and **contract-specific identity**. A future relationship record may say that two implementations occupy an overlapping capability domain without asserting semantic equivalence.

## Current Research State

At this checkpoint:

- corpus identities are pinned;
- discovery and preliminary candidate extraction are complete for the current pass;
- selected candidates have been contract-characterized from pinned source;
- no candidate has been promoted to an established primitive solely from source naming or broad functional similarity;
- cross-project equivalence remains unasserted;
- licensing/provenance reconciliation remains open for Zstandard;
- persistent map serialization remains intentionally unfrozen.
