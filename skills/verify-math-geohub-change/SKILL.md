---
name: verify-math-geohub-change
description: Select, authorize, execute, and report evidence for Math GeoHub changes across source transactions, semantics, agents, rendering, compiler isolation, gateways, auth, and user journeys. Use before completion claims or when planning tests and browser checks; this skill must honor the repository rule that product-owner-controlled test, build, lint, typecheck, compiler, and Docker commands cannot run without explicit reauthorization.
---

# Verify a Math GeoHub change

Match proof to the claim and affected boundary. A file diff, model statement, proposal card, or old passing run is not current verification.

## Read authorization before commands

Read the closest `AGENTS.md` every time. In the current project, automated tests, build, lint, typecheck, compiler, and Docker execution belong to the product owner unless they explicitly reauthorize Codex. Do not interpret a request to create or review code as permission to run those commands.

Host-browser interaction checks are allowed under the current project rules. They do not substitute for unrun unit, integration, compiler, isolation, or deployment checks. If authorization changes, record its exact scope and run only the allowed commands.

## Build a claim ledger

For each material claim record:

- behavior or invariant being claimed;
- boundary and authoritative owner;
- positive, negative, stale, cancellation, recovery, and abuse cases that matter;
- cheapest trustworthy proof seam;
- whether evidence may be inspected, browser-checked, or command-executed;
- current result: `pass`, `fail`, `confirmed-by-inspection`, `inspected-only`, `not-run`, or `blocked`.

Read [references/evidence-matrix.md](references/evidence-matrix.md) to choose proportional evidence. Use existing incident and regression tests before proposing new coverage.

## Verify current basis

- Pin the checkout, relevant dirty files, and exact changed surface.
- Inspect current tests and contracts before adding or recommending tests.
- For source mutations, prove untouched bytes and unsupported regions survive, the current revision commits once, and projection basis converges.
- For agent work, distinguish answer, unapplied candidate, commit, verification, cancellation, and infrastructure failure.
- For async work, prove late or superseded results cannot become current.
- For gateways, prove bounds, abort propagation, partial failure, cache identity, taint, and admission behavior.
- For UX, trace loading, success, failure, retry, close, refresh, and authentication states with browser-visible evidence.

Do not call an exact artifact current from URL or timestamp alone. Do not call a browser flow correct because component tests exist. Do not call a test pass current unless it ran against the checkout being reported.

Use `confirmed-by-inspection` only for a structural fact directly established by current source or configuration, such as the absence of any persistence write path. It cannot establish timing, browser behavior, integration success, or production operation.

## Execute only authorized evidence

Before each command family, confirm authorization remains in scope. Prefer the narrowest test or browser scenario that proves the claim, then expand only for affected consumers. Stop on a failing prerequisite; do not bury it under broader commands.

When commands are not authorized:

1. inspect relevant test cases, configs, and prior artifacts;
2. perform permitted read-only and host-browser checks;
3. provide the exact command plan to the product owner;
4. report every unrun gate as unrun, not presumed pass.

## Report truthfully

Return:

1. checkout and changed surface;
2. claim/evidence ledger;
3. commands and browser scenarios actually run, with results;
4. inspected-only evidence;
5. required but unrun or blocked gates and authorization reason;
6. residual risk and the next smallest gate that can change confidence.

When another skill contributes an audit, merge its scenarios and findings into this one ledger; do not maintain competing final-status tables.

Use `verified` only for claims supported by current evidence. Otherwise use `implementation complete; verification pending`, `partially verified`, or `blocked on owner-controlled gate` as appropriate.
