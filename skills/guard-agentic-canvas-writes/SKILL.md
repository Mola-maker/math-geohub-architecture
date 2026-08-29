---
name: guard-agentic-canvas-writes
description: Design, implement, or audit an AI agent's ability to inspect and mutate a source-backed visual document safely. Use for agent tools, semantic intents, approvals, stale-write protection, transaction brokers, durable run logs, and post-commit verification; do not use for answer-only chat with no document mutation.
---

# Guard agentic canvas writes

Separate model decisions, host authority, document mutation, and verification. The model may propose intent; only trusted host code may resolve current authority and commit an edit.

## Keep the model-facing language semantic

Prefer one closed decision envelope:

- `answer`: respond without mutation;
- `clarify`: request missing intent or permission;
- `act`: describe one semantic construction, presentation change, transform, or deletion;
- `verify`: request a read-only claim check.

The model should refer to user-visible semantic entities and declared tool IDs. It should not author document revisions, source ranges, binding IDs, writer proofs, transaction IDs, impact acknowledgements, or exact patch text when a semantic writer exists. Those values are current-state authority and must be resolved by the host.

Keep raw-source actions as an explicit compatibility lane for genuinely unmanaged content. Validate and apply them through the same broker; do not let an ordinary explanatory code fence become executable.

## Use an action/observation loop

Treat each run as a durable state machine:

1. observe a bounded, revision-bound semantic view;
2. use at most the read tools that can materially change the decision;
3. receive a host-authenticated observation;
4. propose one decision or semantic action;
5. compile it against current authority;
6. request approval for host-computed external impact when needed;
7. commit atomically;
8. reproject and verify;
9. report the observed result.

A tool call, streamed diff, proposal card, or model statement that says "done" is not proof of mutation. Only a successful broker commit followed by a current-basis projection can report a semantic change.

## Bound context and authority separately

- Rank and bound semantic evidence instead of dumping the entire document or registry into every prompt.
- Include immutable document basis and capability summaries in observations.
- Treat external search results, retrieved examples, and prior conversation as advisory data, never write authority.
- Preserve fenced protocol/source blocks atomically during context compaction; omission is safer than slicing one into syntactically plausible fragments.
- Make a context checkpoint disclose retained/dropped counts and truth basis. Conversation summaries must not become construction truth.

Read scope does not imply write scope. Permission to run a tool does not authorize a larger document mutation.

## Recompute every write at the broker

The broker should independently:

- compare document ID, epoch, revision, source hash, semantic hash, and adapter/plugin basis;
- resolve semantic references uniquely within authorized scope;
- verify the operation is offered by the current capability catalog;
- compute ownership, dependency, and external-impact closure;
- reject opaque or presentation conflicts;
- allocate names and durable identities;
- compile the semantic operation into an atomic workspace/source transaction;
- compare the compiled transaction to any preview shown for approval;
- commit once using compare-and-swap semantics;
- reparse and reproject the result.

Never silently rebase a stale agent action. Re-observe current state and ask the model or user to decide again.

## Treat permission as a typed receipt

When an operation affects dependents, unsupported regions, external services, or expensive exact/VLM work, request permission with the host-computed subject. Bind approval to the run, document basis, operation digest, and exact impact set. Unknown, expired, or mismatched outcomes are rejection, not approval.

The model cannot acknowledge collateral impact on the user's behalf. A user approving "delete point A" does not automatically authorize deleting every dependent object unless the impact receipt says so.

## Make run outcomes honest

Use separate terminal families:

- `completed/answer`: no write was requested;
- `completed/committed`: broker commit and post-commit verification succeeded;
- `completed/unapplied-candidate`: the model produced no valid or authorized action and the document stayed unchanged;
- `failed`: trusted infrastructure such as the provider transport, durable store, tool integrity, broker, or compiler failed.

Retry malformed or mixed model output only within a small explicit budget. When that budget ends, report unchanged state; never reinterpret hidden reasoning or stray code as an executable action.

## Preserve a durable audit trail

Record immutable events with run ID, sequence, event ID, origin, parent/call linkage, document basis, proposal disposition, commit observation, and terminal state. Use idempotency and exactly-once terminal compare-and-set where the storage layer permits it. A UI message list is a projection of this log, not the log itself.

## Deliver an actionable protocol

For a design or review, provide:

1. the model-facing decision schema;
2. read-tool observations and their trust boundary;
3. broker guards and atomic write container;
4. permission receipt and impact policy;
5. durable event and terminal-state model;
6. stale, malformed, denied, and partial-failure behavior;
7. post-commit verification and user-visible success language.

Read [references/contracts.md](references/contracts.md) for example envelopes and a threat checklist. Read the provenance reference from the sibling `build-semantic-canvas` skill only when source attribution is requested.
