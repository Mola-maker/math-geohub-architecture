# Math GeoHub journey matrix

## Core journeys

| Journey | States to verify |
| --- | --- |
| `/` landing -> `/math` | meaningful first content, scroll/keyboard/reduced-motion navigation, language/music controls, gateway activation, deep link |
| `/` landing -> `/tikz` | same landing checks plus Studio launch and back/close behavior |
| `/math` | client load, GeoGebra load/retry, provider/model catalog, prompt/stream, construction/repair/rollback, reset/export, close/reopen, refresh |
| `/tikz` | provider/model catalog, source/canvas/inspector sync, agent proposal/commit, stream/cancel/replay, stale projection, exact preview, close/reopen, deep-link selection |
| `/auth/login` -> callback/confirm -> `/console` | GitHub/email choice, validation, sent status, callback expiry/reuse, safe `next`, session cookie, failure recovery |
| `/console` -> Studios -> sign-out | authenticated load, profile fallback, empty/recent work truth, same-origin navigation, session expiry, sign-out/no-store |

## Persistence questions

For each Studio state explicitly state what survives:

- dialog close/reopen;
- route change;
- refresh;
- tab/browser restart;
- auth redirect;
- session expiry;
- network interruption.

Distinguish preferences, chat/run events, source/document, semantic projections, exact artifacts, and dashboard snapshots.

For recovery evidence also record principal/account state, storage scope, snapshot schema/revision/hash, last acknowledged write, recovery source, conflict outcome, lost-item count, browser/version, network condition, and restore duration.

## Viewports and input

Use representative widths around 1440, 1024, 820, 640, 560, 440, and 375 CSS pixels, plus a mobile virtual keyboard. Exact sizes may change with the product; test breakpoints and the spaces between them.

At each state verify reachability of:

- global navigation and close/back;
- canvas and direct-manipulation controls;
- source editor and panels;
- composer/model controls;
- status, error, retry, and cancellation controls;
- dialog focus and restored focus;
- touch targets, safe areas, zoom, and screen-reader announcements;
- horizontal/vertical scrolling without trapped content.

## Evidence packet

Record route, viewport, input mode, reduced-motion/language state, starting data/session state, action sequence, expected result, observed result, screenshot or trace reference, source revision/run/artifact basis where relevant, and residual uncertainty.
