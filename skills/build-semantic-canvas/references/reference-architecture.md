# Semantic canvas reference architecture

Use this reference as a design aid, not as a requirement to copy names or technologies.

## State and data flow

```text
Code / structured document     Agent intent     Canvas / inspector gesture
             \                    |                    /
              +---------------- transaction broker ---+
                               |
                    minimal authoring transaction
                               |
                    immutable document revision
                               |
                lossless parse + semantic projection
                         /                  \
             interactive renderer       exact renderer
```

## Example basis

```ts
type DocumentBasis = {
  documentId: string;
  documentEpoch: number;
  revision: number;
  sourceHash: string;
  semanticHash?: string;
  adapterSetDigest?: string;
};
```

Use an epoch when the same logical document ID can be replaced or reset. Use independent hashes for source, semantics, and renderer output; they answer different questions.

## Example semantic projection

```ts
type SemanticDocument = {
  schema: 'semantic-document/v1';
  basis: DocumentBasis;
  syntax: {
    roots: SyntaxNodeRef[];
    opaqueRegions: OpaqueRegion[];
  };
  semantics: {
    entities: Record<string, Entity>;
    relations: Relation[];
    constraints: Constraint[];
    graph: TypedDependencyGraph;
  };
  sourceMap: SourceBindingMap;
  diagnostics: Diagnostic[];
};
```

The semantic document is a projection, not a database record to edit directly.

## Review checklist

- Can every persisted byte or node be reconstructed after a no-op round trip?
- Are unsupported constructs preserved as opaque rather than misparsed?
- Does every writable semantic entity have a source owner and reversible writer?
- Can an old canvas gesture overwrite a newer code edit?
- Does delete compute dependency and ownership impact before commit?
- Is transient selection or preview state excluded from semantic identity?
- Can a renderer result be mistaken for semantic or source truth?
- Are stale projections and artifacts visibly labeled and non-writable?
- Can every mutation be traced from origin to document transaction and new projection?

## Migration sequence

1. Inventory current state stores and choose persisted truth.
2. Add immutable revision and digest to all projections.
3. Preserve unknown syntax/content and make unsupported regions read-only.
4. Introduce stable semantic IDs and source bindings.
5. Route one low-risk mutation through the broker end to end.
6. Move remaining code, canvas, inspector, solver, and agent writes behind the same boundary.
7. Consolidate dependency closure and typed failures.
8. Add renderer attestation and stale-result handling.

Prefer vertical slices that produce an observable, reversible user action. Avoid a flag-day rewrite of parser, renderer, UI, and agent protocol at once.
