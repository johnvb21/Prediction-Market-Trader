# Failure-mode register

Track possible and observed failures as work proceeds. All initial entries below are hypothetical risks; none is an observed product incident or a verified mitigation. Architecture, component contracts, and tests have not yet been specified or approved.

## FM-001 — Unlogged edits
- Affected area/contracts: repository workflow; AGENTS.md change-logging rule.
- Trigger/cause: edits committed without a corresponding log entry, or interrupted multi-step work.
- Symptoms/impact: files and recorded state disagree; audit trail is incomplete.
- Detection: compare commit diffs and affected paths with change-log entries.
- Prevention/mitigation: same-commit log updates and review; policy only, automated enforcement not implemented.
- Recovery: append a correction describing the missing changes and evidence; preserve original entries.
- Verification/tests: documentation review only; automated check unspecified.
- Status: open; workflow requirement recorded.
- Related change: CHG-0001.

## FM-002 — Unspecified or unapproved behavior
- Affected area/contracts: overall architecture and every component; contract IDs pending.
- Trigger/cause: implementation precedes approved contracts or specifications change without renewed approval.
- Symptoms/impact: ambiguous behavior and tests that validate unintended behavior.
- Detection: review approval references and contract/test/code traceability.
- Prevention/mitigation: existing architecture approval and tests-first gates; enforcement not yet verified.
- Recovery: stop affected implementation, document deviations, obtain approval, then update tests before code.
- Verification/tests: pending approved architecture and contract suite.
- Status: open.
- Related change: CHG-0001.

## FM-003 — Upstream integration faults
- Affected area/contracts: planned Kalshi and Polymarket adapters; contract IDs pending.
- Trigger/cause: malformed, stale, partial, duplicated, reordered, or unavailable data; timeouts or rate limits.
- Symptoms/impact: incorrect market state, inconsistent positions, or misleading valuations.
- Detection: proposed schema/freshness checks and reconciliation; exact guarantees pending design.
- Prevention/mitigation: proposed boundary validation, bounded retry, and explicit unavailable/stale state; not implemented or approved.
- Recovery: proposed resynchronization and reconciliation; exact recovery semantics pending approval.
- Verification/tests: required adversarial/fuzz campaigns and fault injection; not yet written or run.
- Status: open hypothetical risk; no adapters implemented.
- Related change: CHG-0001.

## FM-004 — Incorrect cross-venue interpretation or accounting
- Affected area/contracts: planned normalized market model and ledger; contract IDs pending.
- Trigger/cause: conflating resolution rules, currencies, price units, fees, fills, or settlement semantics.
- Symptoms/impact: false market equivalence, incorrect exposure, cost basis, or P&L.
- Detection: proposed venue-specific fixtures, ledger reconciliation, and accounting invariants.
- Prevention/mitigation: preserve venue metadata and separate contracts; exact normalization/accounting contracts pending approval.
- Recovery: proposed replay/reconciliation from preserved source transactions; design pending.
- Verification/tests: boundary, property, integration, and settlement tests pending approved contracts.
- Status: open hypothetical risk; no ledger implemented.
- Related change: CHG-0001.
