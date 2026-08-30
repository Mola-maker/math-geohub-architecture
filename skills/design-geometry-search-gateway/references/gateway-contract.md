# Gateway contract

## Illustrative channel contract

```ts
type SearchChannel = {
  id: string;
  origin: URL;
  allowedEndpoints: readonly string[];
  accessMode: 'live-search' | 'registry-only' | 'restricted-opt-in';
  rightsPosture: 'cleared' | 'review-required' | 'restricted';
  usage: {
    display: 'allowed' | 'blocked' | 'review-required';
    evaluation: 'allowed' | 'blocked' | 'review-required';
    commercial: 'allowed' | 'blocked' | 'review-required';
    training: 'allowed' | 'blocked' | 'review-required';
  };
  restrictedOptInAuthority?: string;
  queryPrivacy: 'public-upstream' | 'contracted-private' | 'local-only';
  normalizationVersion: string;
  pinning: 'immutable-revision' | 'unpinned-live-viewer' | 'none';
  budgets: {
    maxRequests: number;
    maxResponseBytes: number;
    attemptTimeoutMs: number;
  };
  search(query: BoundedQuery, signal: AbortSignal): Promise<ChannelResult>;
};

type ChannelResult =
  | { status: 'ok'; records: LiveReference[] }
  | { status: 'empty' }
  | { status: 'timeout' | 'quota' | 'transport' | 'invalid-payload' | 'rights-blocked'; detail?: string };
```

Names are illustrative. Preserve existing project types when they already own the concept.

## Source review matrix

| Field | Required question |
| --- | --- |
| Identity | Is the source ID stable and owned in one registry? |
| Upstream | Which exact origin/endpoints/configurations are allowed? |
| Rights | Are code, dataset, and original statement/image rights separate? |
| Revision | Is evidence immutable, pinned, or explicitly live/unpinned? |
| Normalization | Which version transformed the payload? |
| Digest | What exact bytes/fields does the digest cover? |
| Taint | Does external taint survive every projection and admission? |
| Admission | Is this display-only, research-only, evaluation, training, or redistribution? |
| Onboarding | Who may enable live use, with which decision artifact and rollback? |
| Privacy | Which query/identity fields leave the service and under what contract? |
| Cache | Key, TTL, stale/negative policy, visibility, and invalidation? |
| Budget | Query, rows, bytes, requests, concurrency, timeout, retries? |
| Abort | Who owns upstream cancellation and shared single-flight work? |
| Failure | Can callers distinguish timeout, quota, invalid data, rights, and infrastructure? |
| Observability | Per-source latency, bytes, cache state, disposition, and degraded reason? |
| Corpus | What immutable receipt and duplicate/leakage checks are required? |

## State transition

```text
live external payload
  -> bounded normalized live snapshot
  -> read-only reference with null/unpinned revision and external taint
  -> trusted offline pin/download/manifest/rights review
  -> immutable admission receipt for explicitly allowed lanes
  -> read-only corpus registration
```

No route, model call, cache write, or user click may skip a transition.

## Receipt choice

For an in-process capability, record issuer object identity, process lifetime, bound digests, and restart invalidation. For a durable signed receipt, record issuer/verifier keys, canonical payload, expiry, nonce/replay store, revocation, and persistence boundary. In either case bind source, source item, immutable content, task, rights decision, allowed lanes, and admission-policy version.
