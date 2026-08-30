# Math GeoHub owner map

Use this as a discovery index. Re-read live files before relying on details because the project evolves quickly.

| Surface | Primary owner | Boundary to preserve |
| --- | --- | --- |
| Public landing | `mathhub/src/` | Builds into generated `public/mathhub/`; same-origin links `/math` and `/tikz` |
| Next routes and transport | `app/` | Parse/bound/authenticate/serialize; domain policy belongs under `lib/` |
| Math Studio shell | `components/math-studio.tsx`, `components/math-studio-route.tsx` | UI orchestration over GeoGebra and shared geometry contracts |
| GeoGebra domain | `lib/math/`, `lib/geometry/` | Live runtime observations and brokered commands; do not create a second geometry truth |
| TikZ Studio shell | `components/tikz-studio.tsx`, `components/tikz/` | UI orchestration over document, semantic, render, agent, and exact lanes |
| TikZ source/revision | `lib/tikz/document/` | Authoritative bytes, revision, source access, transaction metadata |
| Syntax/capabilities | `lib/tikz/subset/`, `lib/tikz/syntax/`, `lib/tikz/analyze/` | Preserve unknown source; distinguish parse, semantics, interaction, and exact execution |
| Semantic/authoring | `lib/tikz/ir/`, `semantics/`, `authoring/` | Stable IDs, dependencies, construction schemas, writer artifacts |
| Mutation authority | `lib/tikz/transactions/` | Current-basis authorization and atomic source transaction |
| Interactive rendering | `lib/tikz/render/` | Responsive projection, hit testing, selection, previews |
| Agent runtime | `lib/tikz/agent/` | Protocol, bounded context, checkpoints, replay, widgets, run store |
| Exact rendering | `lib/tikz/exact/`, `app/api/tikz/render/`, `services/tikz-compiler/` | Async isolated compilation, attestation, artifact safety |
| Research/problem data | `lib/tikz/problems/`, `app/api/tikz/problems/` | Live tainted reference -> trusted admission -> read-only corpus |
| Providers/streaming | `lib/provider/`, `lib/llm/` | Server-only credentials, safe IDs, catalog/cache/health, bounded SSE |
| Request safety | `lib/http/`, `lib/rate-limit.ts`, `lib/client-ip.ts` | Size, byte, timeout, abuse, and production failure policy |
| Auth/session | `app/auth/`, `lib/auth/`, `lib/supabase/`, `proxy.ts` | Same-origin mutations, safe redirects, HttpOnly session, no-store |
| Authenticated console | `app/console/` | Read-only workspace projection and same-origin Studio navigation |
| Production deployment | `deploy/ecs/`, root `Dockerfile`, `services/tikz-compiler/` | ECS dynamic runtime, Nginx/load balancer, object storage/CDN split |

## Authority order

1. Current user request and explicit authorization.
2. Closest applicable `AGENTS.md`.
3. Live source, configuration, schemas, tests, and generated-source declarations.
4. Current specs/ADRs/research notes, with disagreements called out.
5. Generic sibling skills and external best practices.

Do not invent a new canonical contract merely because a generic pattern uses different names.

