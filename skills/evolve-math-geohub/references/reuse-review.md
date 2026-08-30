# Reuse and drift review

## Decision matrix

| Evidence | Decision |
| --- | --- |
| Same concept and same lifecycle repeated in several owners | Consolidate under the real owner |
| Same data expressed across browser/server, host/worker, or trusted/untrusted boundary | Keep translation explicit; share schema or policy identity where safe |
| Same safety check in two processes | Keep defense in depth; version the rule and prove parity |
| Similar code with different domain meaning or change cadence | Keep local |
| Generated file repeats source declarations | Change the generator/source, never the output |
| Temporary old/new implementation | Require migration owner, consumer list, removal condition, and deadline/release gate |
| Interface has one implementation and no external complexity | Avoid speculative abstraction |

## Investigation signals

Signals are not findings until callers and owners prove a problem:

- route or component imports many domain layers;
- the same union/enum/limit/error mapping appears in passive consumers;
- adding one variant requires edits across unrelated modules;
- old and `v2` trees both parse or render the same protocol;
- client and service implement the same sanitization or attestation rule without a policy version;
- catalog, codec, validator, writer, prompt, and tests each enumerate the same construction kinds;
- a generated artifact is edited manually;
- a large broker mixes canonical authority with action-specific decoding and policy.

Current high-signal places to inspect include `components/math-studio.tsx`, `components/tikz-studio.tsx`, `app/api/tikz/route.ts`, `lib/tikz/transactions/broker.ts`, the TikZ authoring catalog/codec/IR trio, provider-facing API routes, and compiler/client SVG policy. Re-evaluate them from current code rather than assuming they remain problematic.

## Recommendation fields

For each surviving finding record:

- concept and current owner;
- duplicate/consumer locations;
- concrete change that currently amplifies;
- counter-evidence checked;
- reuse decision and why;
- migration slice and compatibility need;
- removal condition;
- proof seam and rollback.

For provider changes also record protocol adapter, allowed origins/catalog, credential owner, safe model normalization, capability matrix, browser-visible/server-only fields, default/failover policy, and transport-health semantics.

For module extraction also record responsibility clusters, state owner, dependency direction, target API, extraction order, consumer cutover, affected dirty/concurrent files, compatibility duration, and release/deadline removal gate.

For route consolidation separate reusable domain/provider policy from transport parsing, request bounds, auth/rate policy, error/status mapping, and deliberate defense-in-depth.
