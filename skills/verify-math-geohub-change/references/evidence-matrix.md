# Math GeoHub evidence matrix

This matrix chooses evidence; it does not grant command authorization.

| Changed boundary | Minimum meaningful evidence | Important negative/recovery evidence |
| --- | --- | --- |
| TikZ source/CST/patch | focused unit + no-op/round-trip or property checks | invalid source, opaque overlap, line endings, stale revision |
| GeometryDoc/semantic adapter | unit + fixture parity + adapter integration | ambiguous identity, degraded/opaque capability, basis mismatch |
| Transaction broker/writer | unit + replay/integration + affected UI seam | stale basis, duplicate commit, unauthorized range, dependency impact |
| Agent protocol/run store | reducer/protocol + route integration + replay | malformed output, late event, disconnect, cancellation, terminal CAS |
| Interactive renderer/canvas | geometry/unit + component + host-browser interaction | hit-test edge, drag cancel, stale projection, keyboard alternative |
| Exact compiler/artifact | client tests + compiler tests + isolation/packaging evidence | blocked policy, timeout, duplicate worker, unsafe SVG, private artifact |
| Provider/SSE/API route | parsing/model/stream tests + route integration | oversized input/output, abort, circuit open, unavailable limiter |
| Research gateway/corpus | adapter + normalization + admission + corpus tests | partial source failure, live/unpinned promotion, rights/taint loss |
| Auth/session/console | redirect/form/proxy route tests + browser journey | cross-origin post, open redirect, expired callback, sign-out/cache |
| Landing/Studio UX | component accessibility + browser journey + responsive screenshots | reduced motion, keyboard-only, mobile keyboard, retry/refresh |
| Performance-sensitive path | benchmark or trace with an explicit budget | low-end/degraded mode, queue saturation, long stream, cancellation |
| Deployment/cache | config/static audit + image/package inspection + operational check | private caching, missing generated public assets, runtime mismatch |

## Repository command families

The root package currently exposes `lint`, `test`, `test:compiler`, `build`, and `audit:cdn`; browser checks may use the documented local host flow. Always re-read `package.json` and `AGENTS.md`. Do not run any command family that remains product-owner-controlled.

## Evidence labels

- `pass`: executed against the reported checkout and met the gate.
- `fail`: executed and did not meet the gate.
- `confirmed-by-inspection`: current source/configuration directly proves a structural presence or absence, without a runtime claim.
- `inspected-only`: relevant code/test/artifact was read but not executed.
- `not-run`: required but neither executed nor independently evidenced.
- `blocked`: cannot run because authorization, environment, service, or prerequisite is unavailable.

An old CI result may be supporting context, but it is not a current `pass` for uncommitted changes.
