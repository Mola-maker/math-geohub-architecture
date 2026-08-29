# Dual-render pipeline contract

## Example compile job

```ts
type ExactJobRequest = {
  documentId: string;
  epoch: number;
  revision: number;
  source: string;
  sourceDigest: string;
  profile: string;
  visibility: 'public' | 'private';
};

type ExactJobStatus = {
  jobId: string;
  status: 'queued' | 'running' | 'succeeded' | 'failed' | 'blocked';
  attempt: number;
  artifactUrl?: string;
  attestation?: ExactAttestation;
  diagnostic?: Diagnostic;
};
```

## Example attestation

```ts
type ExactAttestation = {
  submittedSourceDigest: string;
  executedSourceDigest: string;
  wrapperDigest?: string;
  engineDigest: string;
  libraryBundleDigest: string;
  driver: string;
  fontBundleDigest?: string;
  securityProfileDigest: string;
  artifactDigest: string;
};
```

Keep wrapper and source identities separate. A wrapper may establish a standalone document without changing the user-authored bytes.

## Cache and visibility matrix

| Surface | Recommended policy |
| --- | --- |
| Fingerprinted application assets | public, long-lived, immutable |
| Public content-addressed exact artifact | public, immutable when product policy permits |
| Private exact artifact | authenticated access; no public CDN namespace |
| Job and polling API | no-store; rate limited |
| HTML or mutable entry document | short cache or revalidation |
| Deterministic compiler failure | short negative cache |
| Infrastructure/transient failure | retry policy, normally no negative cache |

## Worker invariants

- Validate input size, encoding, profile allowlist, and declared digest.
- Create one unique temporary directory per attempt.
- Run with no network, no shell escape, limited filesystem access, and pinned dependencies.
- Enforce wall time, CPU, memory, process, and output bounds.
- Verify output structure, remove or reject active content, and compute artifact digest.
- Publish the terminal result only when the lease and attempt fence still match.
- Delete or quarantine partial output from rejected/expired attempts.

## Review questions

- Can exact work occur during pointer move, animation frame, or synchronous request rendering?
- Can a stale exact result replace current interactive state?
- Is the submitted source modified before execution without a visible transaction?
- Are wrapper, compiler, library, driver, fonts, and policy identities attested separately?
- Can two worker attempts both publish terminal output?
- Can a private artifact be inferred or fetched from a public content address?
- Are unsupported interactive features shown as exact-only rather than editable?
- Does generated SVG/HTML/PDF cross an active-content safety boundary?
- Are queue saturation and compiler absence distinct from invalid source?
- Does the product measure each lane against its own latency and fidelity budget?
