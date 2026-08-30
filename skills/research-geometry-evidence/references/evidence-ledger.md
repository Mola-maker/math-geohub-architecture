# Evidence ledger

## Research decision packet

```text
question:
decision_owner:
target_repository_and_commit:
current_date:
version_or_time_boundary:
stopping_rule:
queries_and_channels:
results_reviewed:
pages_fetched:
deduplication_and_exclusions:
unavailable_lanes:
supersession_or_correction_checks:
```

## Claim record

```text
claim_id:
claim:
decision_impact:
status: verified-current | verified-historical | cited-unchecked | inferred | contradicted | open
date_or_version:
local_integration_point:
evidence_ids:
counter_evidence_ids:
confidence_and_reason:
next_check:
```

## Source record

```text
evidence_id:
channel:
title:
canonical_url:
source_kind: specification | source | test | release | paper | dataset-card | issue | practitioner | secondary
authors_or_owner:
published_or_commit_date:
version_or_commit_sha:
retrieved_at:
direct_support:
quality_signals:
rights_or_license:
source_material_rights:
taint: untrusted-external-reference
admission: research-reference-only
limitations:
```

Mark missing values `not found`. Distinguish an explicitly absent fact from a fact not found within the search budget.

## Technology candidate

Add: current gap, user value, smallest reusable unit, target owner, dependency surface, privacy/security effects, latency/scale effects, maintenance evidence, license compatibility, integration cost, reversibility, proof question, success threshold, stop condition, and `adopt | adapt | build | reject`.

## Research-to-product handoff

The ledger may inform a proposal or source-catalog entry. It cannot issue an admission receipt. Product ingestion separately requires immutable bytes/revision, normalization identity, digests, rights evidence, taint retention, trusted review, lane decisions, and corpus duplicate/leakage checks.

Enabling a live channel requires an independent onboarding decision. Admitting exact upstream material requires a trusted artifact/rights receipt. An independently authored local fixture derived only from abstract relations is a separate provenance path and must never be labeled as upstream corpus admission.
