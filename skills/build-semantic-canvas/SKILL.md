---
name: build-semantic-canvas
description: Design or refactor an interactive visual editor so source, semantic state, canvas interactions, and renderers remain consistent. Use for geometry, diagram, CAD, whiteboard, scene, graph, or code-backed canvas architecture; do not use for a purely decorative canvas with no persistent structured document.
---

# Build a semantic canvas

Design the editor around explicit truth boundaries. Preserve the user's chosen source format and product constraints; apply these principles to the existing stack instead of requiring TikZ, CodeMirror, or Math GeoHub components.

## Establish the truth model

Name each state store and classify it before proposing components:

1. **Persisted authoring truth**: the bytes or structured document that survives reload and collaboration.
2. **Syntax projection**: a lossless or best-available parse tied to one immutable document revision.
3. **Semantic projection**: typed entities, relations, constraints, ownership, and dependencies derived from the authoring truth.
4. **Interaction state**: selection, hover, active tool, drag preview, viewport, and transient solver state.
5. **Rendering truth**: one or more visual artifacts, each labeled with the source and profile that produced it.

Do not let a derived scene, React state tree, renderer cache, or agent conversation become a second writable canonical document. If the product truly needs multiple writable formats, define an explicit synchronization or CRDT contract rather than calling both of them "the source of truth."

## Grade capabilities by lane

Avoid a single `supported` flag. Evaluate each feature independently:

- **Preservation**: can unknown or unsupported content round-trip unchanged?
- **Inventory**: is the upstream surface catalogued with version and provenance?
- **Semantics**: can the system derive stable meaning without guessing?
- **Interaction**: is there a reversible writer for safe direct manipulation?
- **Exact execution**: can a pinned runtime reproduce the authoritative artifact?

A feature may be preserved and rendered exactly while remaining opaque and read-only. Keep that state visible in capability metadata and diagnostics.

## Build the projection boundary

- Prefer a lossless CST or equivalent source index when byte preservation matters.
- Give semantic entities stable IDs independent of offsets, parser node identity, array position, labels, and renderer IDs.
- Record source bindings and ownership so a semantic change can be lowered to the smallest valid edit.
- Preserve unsupported regions as opaque nodes with exact source slices and conservative effect metadata.
- Tie every projection to a basis containing at least document identity, epoch if documents can be replaced, immutable revision, and source digest.
- Make the semantic projection fully reconstructable from persisted truth plus versioned adapters/plugins.

When a parse is invalid, emit a typed invalid projection. A last-valid projection may remain visible only as explicitly stale and read-only.

## Route all writes through one transaction boundary

Code edits, canvas gestures, inspector changes, solver outputs, and agent proposals should converge at one broker or transaction coordinator. The broker must:

- compare the proposal basis to the current document;
- resolve source ownership and the writable capability again on current state;
- reject opaque-region overlap and namespace collisions;
- lower the semantic operation to a minimal document transaction;
- apply the document transaction atomically;
- reparse and reproject the committed revision;
- return the new basis and diagnostics.

Pointer movement should update previews only. Finish or pointer-up submits one transaction. Derived objects are edited by changing writable upstream drivers through a constraint solver, not by freezing the rendered coordinate into the source.

## Model dependencies once

Use a typed dependency graph for invalidation, delete impact, agent context, solver components, and conflict diagnostics. Distinguish at least definition, read, style, scope, constraint, and unknown-effect edges when the domain needs them. Reusing one graph prevents each subsystem from inventing a subtly different closure.

## Specify failure semantics

Prefer typed, recoverable failures such as `stale-basis`, `source-conflict`, `opaque-barrier`, `read-only-capability`, `namespace-conflict`, `degenerate-geometry`, and `unsupported-semantics`. A failure must not:

- present old geometry as current;
- silently rewrite or drop unknown source;
- mutate a derived projection in place;
- convert an unsupported semantic form into a guessed literal;
- claim success before a current-basis projection exists.

## Deliver an actionable architecture

For a design request, return:

1. the truth/state inventory;
2. the data-flow and mutation path;
3. the revision and identity basis;
4. the capability-lane matrix;
5. opaque and invalid-state behavior;
6. incremental migration slices that preserve current user workflows;
7. acceptance checks proportional to the affected boundary.

Read [references/reference-architecture.md](references/reference-architecture.md) when concrete schemas, a migration sequence, or an architecture review checklist would help. Read [references/math-geohub-provenance.md](references/math-geohub-provenance.md) only when the user asks where the principles came from or needs source citations.
