---
name: design-geometry-search-gateway
description: Design, implement, or audit Math GeoHub production gateways for geometry-problem sources, provider/model discovery, or other multi-source research APIs. Use when adding a search channel, changing fan-out, cache, timeout, abort, rate-limit, auth, provenance, rights, failure, or corpus-admission behavior; do not use for offline literature research or ordinary application routes with no external-source trust boundary.
---

# Design a geometry search gateway

Keep live retrieval, trusted admission, and evaluation consumption as separate states. A gateway may return useful partial evidence without granting source, semantic, or write authority.

## Map the boundary

Trace:

`caller -> route policy -> channel registry -> remote attempts -> normalization -> live reference projection -> optional trusted admission -> read-only corpus`

For each stage name the owner, input/output schema, trust state, resource budget, cache identity, abort owner, failure states, and observability. Read [references/gateway-contract.md](references/gateway-contract.md) for a source-adapter contract and review matrix.

## Register channels behind one contract

Each channel should declare source identity, upstream origin, access mode, rights posture, supported query/configuration, normalization version, revision/pinning capability, byte/request/time budgets, cache policy, and failure mapping. Keep source-specific parsing inside the adapter and fan-out/fan-in policy in the orchestrator.

Before enabling a channel, require a project-owned onboarding decision distinct from research completion and corpus admission. It must bind the source/catalog entry, allowed origins/endpoints, display/reference/commercial/training decisions, restricted opt-in authority, revision policy, credential and query-privacy exposure, budgets, and rollback. If the catalog requires an immutable revision, fail closed when only a mutable live endpoint is available.

Adding one channel should not require passive routes, UI widgets, caches, and corpus code to redefine a source union independently. Use a registry or generated contract when the source set is intentionally extensible.

## Bound all work

Set explicit limits for query length, rows, records, statement/asset metadata, per-response bytes, aggregate bytes, request count, concurrency, per-attempt time, whole-search time, cache entries, stale window, observation payload, and retries.

- Compose caller cancellation with gateway timeout without letting one canceled waiter abort shared single-flight work for other callers.
- Abort remote reads and release timers/readers on timeout or disconnect.
- Treat positive, negative, and stale caches separately; never let a live content hash masquerade as a pinned upstream revision.
- Return partial success with per-source status when useful channels succeed; do not hide a total outage behind an empty result.

## Preserve provenance and taint

A live record needs source and dataset URLs, provider/config/split/row identity, retrieval time, normalization identity, content digest and scope, revision state, rights evidence, solution provenance, asset verification state, external taint, and `search-reference-only` admission.

Fetched text, URLs, captions, proofs, and metadata remain untrusted strings. They cannot be parsed as tool instructions, mutation envelopes, permissions, or semantic facts. Public/agent observations should expose bounded previews and omit solution bodies unless an explicit trusted workflow requires them.

## Separate admission from search

Search is read-only. Batch ingestion belongs in a trusted offline/admin process that pins immutable revisions and bytes, validates manifests/assets/digests, records rights and lane decisions, retains taint, and issues an unforgeable receipt. Corpus registration must reject live/unpinned/writable references and bind manifest, task, split, leakage group, and content identities.

Define the receipt mechanism rather than relying on the adjective "unforgeable": state whether it is an in-process capability or signed durable record, who verifies it, what identities it binds, its expiry and replay protection, and how persistence/restart affects validity.

Use the sibling `research-geometry-evidence` skill for human research. Its ledger is input evidence, not an admission receipt.

## Keep gateway policies distinct

- Authentication identifies a caller; it does not replace rate, byte, timeout, taint, or admission checks.
- Rate-limit infrastructure failure is not ordinary quota exhaustion; expose a distinct service-unavailable condition when policy requires fail-closed behavior.
- Transport health means the origin is reachable, not that a model/source is correct or licensed.
- Provider/model discovery validates safe identifiers and capabilities; browser code never receives credentials or arbitrary upstream URLs.
- Private, user-specific, job, auth, and degraded responses must not enter public CDN caches.

## Deliver

Provide:

1. data-flow and trust-state map;
2. per-channel registry matrix;
3. resource, abort, cache, partial-success, and failure policy;
4. provenance/rights/taint schema;
5. search-to-admission boundary and corpus rejection rules;
6. rate/auth/provider/transport responsibilities;
7. observable tests and rollout/rollback plan.
