---
name: audit-math-geohub-ux
description: Audit or improve Math GeoHub user journeys across the animated MathHub landing page, Math Studio, TikZ Studio, authentication, and console, with evidence for accessibility, recovery, responsive behavior, performance, and truthful revision state. Use for UX acceptance or implementation planning; do not use for purely visual styling critique or generic frontend code review.
---

# Audit Math GeoHub UX

Judge whether a user can enter, understand, act, recover, and trust the product. Visual polish is secondary to a complete, accessible, responsive, and truthful journey.

## Trace journeys as state machines

Cover the affected path from entry to exit. For each transition record trigger, loading, success, empty, failure, retry, cancellation, close/back, refresh, session expiry, and durable recovery. The core journey inventory is in [references/journey-matrix.md](references/journey-matrix.md).

Do not infer a browser journey from isolated components. Inspect current source and tests, then use permitted host-browser checks when they materially improve evidence. Follow `verify-math-geohub-change` for command authorization and reporting.

## Accessibility gate

- Prefer native buttons, links, inputs, dialogs, and headings.
- Verify logical Tab order, visible focus, focus trap, focus restoration, scoped Escape handling, and editor shortcut isolation.
- Give icon-only actions names and canvas operations keyboard alternatives.
- Use status announcements for loading/progress and alerts for actionable failures without flooding streamed updates.
- Do not hide visually active content from assistive technology with `aria-hidden`.
- Verify language changes, labels, mathematical content, revision/currentness, and error recovery are understandable without color or motion.
- Exercise reduced-motion and keyboard-only flows, not just inspect CSS declarations.

## Recovery and truth gate

Force catalog/runtime/provider failure, stream interruption, cancellation, stale revision, stale exact artifact, edited or expired proposal, refresh, route change, and auth expiry when relevant.

Create failure and auth-expiry states only in local or approved staging environments with disposable test accounts and recoverable data. Do not manipulate production sessions, user storage, or live work to manufacture evidence.

The UI must distinguish:

- interactive projection available vs exact rendering pending/unavailable;
- proposal vs committed document change;
- current vs stale revision/artifact;
- retryable transport failure vs invalid user source;
- persisted preference vs persisted document/work;
- canceled work vs failed infrastructure.

Never report success before the source revision and required projection/attestation basis match. Do not silently discard unsaved work or imply document recovery when only model preference survives.

Define "work" before designing persistence: unsent prompt draft, chat/run events, committed GeoGebra commands, authoritative document/source, semantic revision, UI preferences, exact artifacts, and interrupted runs have different owners and survival rules. For every durable item specify principal/account binding, storage scope, versioned snapshot schema, atomic write/recovery point, corruption/migration behavior, quota/private-mode fallback, multi-tab conflicts, retention/deletion, anonymous-to-account adoption, and different-account rejection. Never import one account's local work into another account without explicit consent and server-side ownership checks where server persistence exists.

## Responsive and performance gate

Verify canvas, source editor, inspector, composer, status/error surfaces, dialogs, and primary actions at representative desktop, tablet, narrow mobile, and virtual-keyboard states. Avoid hard minimum heights or fixed overlays that make controls unreachable.

Define measurable budgets for landing meaningful content, Studio open-to-interactive, GeoGebra readiness, pointer/drag response, streamed rendering, exact-preview handoff, and recovery. Measure interactive and exact lanes separately. Check low-end and reduced-motion behavior before adding blur, animation, observers, or eager heavyweight runtimes.

For autosave/recovery include serialization frequency, snapshot bytes, main-thread blocking, compaction, write acknowledgement, and restore-to-interactive latency. Accessibility checks must cover autosave/restore announcements, conflict choices, restored focus, touch targets, safe areas, zoom, virtual keyboards, and an alternative to canvas-only meaning.

## Evidence gate

Classify each claim as supported by focused test, browser scenario, measurement artifact, documented manual check, `confirmed-by-inspection`, inspection only, or unverified. Use `confirmed-by-inspection` only when current source structurally proves presence or absence; it still does not claim runtime behavior. Existing test names are leads; re-read current tests and do not imply they ran.

Prioritize findings by journey blockage, false-success/data-loss risk, accessibility exclusion, unrecoverable failure, mobile reachability, and measured performance cost. A cosmetic inconsistency is lower priority unless it hides state or blocks comprehension.

## Deliver

Return:

1. affected journey/state map;
2. prioritized findings with exact location, trigger, user impact, and evidence;
3. keyboard/screen-reader/reduced-motion results;
4. recovery and persistence matrix;
5. responsive viewport and performance evidence;
6. smallest implementation slices with acceptance scenarios;
7. unverified claims and owner-controlled gates still required.

Use the claim ledger from `verify-math-geohub-change` as the single final-status record. This skill contributes journey findings and scenarios; the verification skill owns `pass/fail/not-run/blocked` status.
