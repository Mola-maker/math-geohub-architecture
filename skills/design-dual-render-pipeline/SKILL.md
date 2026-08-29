---
name: design-dual-render-pipeline
description: Design or audit a visual editor that needs both responsive interaction and an authoritative high-fidelity renderer or compiler. Use for SVG/canvas previews paired with TeX, CAD, browser, server, GPU, PDF, video, or other exact output; do not use when one renderer satisfies both interaction latency and fidelity requirements.
---

# Design a dual-render pipeline

Treat interactive and exact output as separate, revision-bound projections of the same persisted document. Do not force the exact renderer into the pointer loop, and do not present the interactive renderer as authoritative fidelity when it implements only a semantic subset.

## Define the two contracts

**Interactive lane**

- Optimized for selection, hit testing, dragging, tool previews, and immediate feedback.
- May render a semantically understood subset or approximation.
- Must declare unsupported, opaque, or degraded regions.
- Updates within the frame budget without compilation, network, hashing, rasterization, or pixel diff in the pointer-move loop.

**Exact lane**

- Executes or compiles the persisted source under a pinned engine/profile.
- Runs asynchronously, cancelably, and outside the UI frame loop.
- Produces an immutable artifact plus provenance/attestation.
- May reject a source or profile, but must not silently sanitize or rewrite user content and then call it exact.

An exact artifact verifies rendering fidelity, not semantic truth. An interactive projection verifies manipulable meaning, not byte-exact output.

## Bind every result to source identity

Carry at least document ID, epoch where applicable, revision, submitted source digest, renderer/compiler profile, and adapter/kernel basis. The exact lane should additionally attest engine image/build, library bundle, driver/backend, fonts/assets, security profile, executed source digest, and wrapper digest when a wrapper is used.

Display a result as current only when every required basis field matches. A late artifact from an old revision is a historical preview; it must not overwrite the current canvas or clear current diagnostics.

## Keep source transformation visible

For a true exact lane, submitted and executed source digests should match. If the runtime needs a document wrapper, record it separately. If migration or sanitization changes user source, first expose that as a reviewable authoring transaction; do not hide it inside the compiler.

Policy rejection should identify the blocked command/family/profile. Legal but unavailable capabilities should return a profile diagnostic rather than being removed.

## Isolate untrusted execution

When exact rendering runs user-authored or generated code:

- isolate it from the web/API process;
- disable network and shell escape by default;
- use immutable cached dependencies and pinned profiles;
- constrain filesystem, CPU, memory, process count, wall time, and output size;
- use a fresh job directory;
- validate and sanitize output artifacts as untrusted active content;
- keep compiler credentials and provider keys server-side;
- distinguish blocked-by-policy from compile failure and infrastructure failure.

Do not put an untrusted compiler in an edge request or browser frame loop merely to reduce deployment components.

## Design the asynchronous job lifecycle

- Derive an idempotency/cache key from executed source identity, profile, visibility, and immutable runtime digests.
- Deduplicate active and terminal jobs for the same key.
- Bound the queue and return explicit backpressure such as 429 plus retry guidance.
- Give running jobs leases/heartbeats and fence completion by attempt number.
- Requeue expired work atomically and prevent an old attempt from overwriting a newer result.
- Content-address successful artifacts and cache deterministic failures briefly.
- Cancel or ignore polling/results for superseded revisions.
- Never place private artifacts in a public CDN namespace.

## Compare lanes without conflating them

Visual or structural differential checks may explain why lanes differ, but they cannot let one lane rewrite the other. Classify differences as:

- expected approximation;
- unsupported interactive semantics;
- profile/library mismatch;
- stale artifact;
- actual renderer defect;
- unsafe or invalid output.

Use capability metadata and typed diagnostics to decide which surface can be edited and which can only be viewed exactly.

## Set independent budgets

Specify budgets for pointer-to-preview latency, semantic reproject time, exact metadata cache hits, exact cache misses, queue depth, and hard timeout. Degrade interaction predictably when solver or projection work exceeds its budget; do not block the canvas waiting for exact output.

## Deliver an actionable pipeline

For a design or review, provide:

1. lane ownership and truth claims;
2. basis and attestation fields;
3. async job, cancellation, retry, and fencing states;
4. isolation and artifact-safety boundary;
5. cache/visibility matrix;
6. stale-result behavior and differential diagnostics;
7. independent performance and availability targets.

Read [references/pipeline-contract.md](references/pipeline-contract.md) for example job schemas, attestation, cache policy, and review questions. Read the provenance reference from the sibling `build-semantic-canvas` skill only when source attribution is requested.
