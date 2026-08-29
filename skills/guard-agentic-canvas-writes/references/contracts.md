# Guarded agent write contracts

The names below are illustrative. Keep the user's domain vocabulary and existing protocol where possible.

## Model decision

```ts
type AgentDecision =
  | { kind: 'answer'; text: string }
  | { kind: 'clarify'; question: string }
  | { kind: 'act'; intent: SemanticIntent }
  | { kind: 'verify'; claim: SemanticClaim };
```

The model-facing intent should contain semantic references and desired outcomes, not source authority fields.

## Host mutation envelope

```ts
type MutationEnvelope = {
  schema: 'mutation/v1';
  origin: 'agent' | 'code' | 'canvas' | 'inspector' | 'solver';
  basis: {
    documentId: string;
    epoch: number;
    revision: number;
    sourceHash: string;
    semanticHash: string;
    adapterSetDigest: string;
  };
  authorization: {
    ownerId: string;
    sourceRanges: SourceRange[];
    capabilityId: string;
  };
  operation: ResolvedOperation;
  idempotencyKey: string;
};
```

This envelope is host-authored after resolving the model intent. Do not ask the model to copy these fields from context.

## Permission receipt

```ts
type PermissionReceipt = {
  runId: string;
  basisDigest: string;
  operationDigest: string;
  impactDigest: string;
  outcome: 'allow-once' | 'reject' | 'cancel';
  expiresAt: string;
};
```

Any unknown outcome is non-authorizing. If the current impact differs from the receipt, request permission again.

## Commit observation

```ts
type CommitObservation = {
  status: 'committed' | 'rejected';
  oldBasis: DocumentBasis;
  newBasis?: DocumentBasis;
  transactionDigest?: string;
  diagnostics: Diagnostic[];
  verification: {
    semanticCurrent: boolean;
    exactCurrent?: boolean;
  };
};
```

The final response must be derived from this observation, not from the proposed intent.

## Threat and failure checklist

- Prompt injection in retrieved examples attempts to grant write authority.
- A stale model action targets revision N after code or canvas moved to N+1.
- A label or display name ambiguously resolves to more than one semantic entity.
- The model supplies a source range or binding copied from an earlier observation.
- A deletion has dependent or cross-scope impact not shown during approval.
- A preview transaction differs from the transaction recomputed at commit.
- A retry emits both a read-tool call and a write action in one turn.
- The UI reports success on proposal publication, before commit.
- A crash records two terminal outcomes or replays a write twice.
- Post-commit semantic projection fails or points to a different source digest.

Fail closed at the narrowest boundary and preserve the current document unchanged.
