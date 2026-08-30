---
name: evolve-math-geohub
description: Review, plan, or implement Math GeoHub architecture and reuse changes across the Next.js host, MathHub landing app, Math Studio, TikZ Studio, providers, and compiler service. Use when a change may duplicate an owner, widen a protocol, split a large module, add a studio/provider/capability, or migrate generated or deprecated surfaces; use the narrower canvas, agent-write, or dual-render skills when only those contracts are changing.
---

# Evolve Math GeoHub

Keep each concept under one owner while preserving the product's established truth and deployment boundaries. Do not infer architecture from file size alone: prove mixed ownership, schema drift, or broad change amplification before proposing a split.

## Establish current authority

1. Read the closest `AGENTS.md`, the live entrypoint, its owner modules, affected tests, and current specs or research notes.
2. Record branch, HEAD, dirty files, generated areas, and work owned by others. Preserve unrelated changes.
3. Trace the requested behavior as `entrypoint -> domain owner -> boundary adapter -> side effects -> evidence seam`.
4. Name the canonical source for every concept touched. Treat docs as intended architecture and code as implemented architecture; report drift instead of silently choosing one.

Read [references/project-map.md](references/project-map.md) when locating owners or choosing between Math Studio, TikZ Studio, shared geometry, provider, auth, gateway, compiler, and landing surfaces.

Before planning a new provider or large extraction, capture the decisions that change the architecture. For a provider include identity, protocol adapter, allowed origin/catalog, credential owner, model normalization, vision/tool/reasoning capabilities, browser-visible label, default precedence, health, and failover policy. For a module extraction include responsibility clusters, state owner, dependency direction, target API, consumer cutover order, and rollback.

## Make reuse an ownership decision

For every apparent duplicate, decide whether it is:

- one concept accidentally redefined;
- deliberate translation across a trust or process boundary;
- defense in depth that needs a shared policy/version contract;
- generated output whose source lives elsewhere;
- a compatibility lane with an explicit removal condition;
- coincidental similarity that should stay local.

Use the new-variant test: if the owner adds one valid provider, construction kind, widget, capability, or failure state, which passive consumers must also change? A passive router or serializer that must redefine the owner's variants is a drift hotspot.

Prefer reusing an existing deep module, protocol, registry, or adapter. Add an abstraction only when it hides real external complexity or proven variation; a one-adapter interface is hypothetical unless tests or another runtime already form the second adapter. Read [references/reuse-review.md](references/reuse-review.md) for the decision matrix and known investigation hotspots.

## Preserve project boundaries

- `mathhub/` is the only landing frontend; `public/mathhub/` is generated output.
- TikZ source and immutable revision remain authoring truth. GeometryDoc, scenes, dashboards, render primitives, exact artifacts, and AI context are projections.
- GeoGebra live command snapshots are observations unless a specific broker contract grants write authority.
- Browser-facing code may choose safe model/provider identifiers but never owns credentials, origin policy, or transport health.
- ECS owns dynamic APIs, LLM relay, job control, and untrusted compilation. CDN and edge previews do not define production runtime behavior.
- Generated PGF registries, compiler profiles, protocol limits, schema versions, and sanitization policy identifiers are compatibility contracts, not convenient constants to copy.

Use the sibling skills for their owning concerns:

- `build-semantic-canvas`: persisted truth, semantic projection, source ownership, and brokered document writes.
- `guard-agentic-canvas-writes`: model intent, authority receipts, run events, and post-commit truth.
- `design-dual-render-pipeline`: interactive/exact rendering and compiler artifact lifecycle.
- `design-geometry-search-gateway`: production search/admission gateways.
- `audit-math-geohub-ux`: user journeys and browser-visible quality.
- `verify-math-geohub-change`: authorization-aware evidence plan and final verification status.

When several concerns apply, keep this skill as the architecture integrator and ask each owning skill for its contract or evidence packet. Do not restate a sibling's full protocol as a second authority.

## Plan migration vertically

Define one concept-owned slice with current callers, target owner, compatibility need, removal condition, rollback, and claim-matched evidence. Preserve behavior while moving ownership; time-bounded compatibility adapters are allowed when callers cannot migrate atomically, but every forwarding module, `v2` twin, duplicate enum, or parallel source tree needs an owner and retirement gate.

For implementation, keep route handlers as bounded transport adapters and move reusable policy to the domain owner. Recheck consumers after each contract change; do not introduce broad re-exports that hide the new owner.

## Deliver

Return or record:

1. current architecture and authority map;
2. verified duplication/coupling findings plus rejected false positives;
3. reuse/consolidate/translate/keep-local decisions;
4. smallest dependency-ordered migration slices;
5. preserved behavior, deferred work, removal conditions, and rollback;
6. evidence required through `verify-math-geohub-change`.

The evidence section must repeat the closest repository command-authorization rule. Never let a generic migration plan imply permission to run owner-controlled tests, builds, compilers, or containers.
