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

## FM-005 — SPSC ownership violation or overflow
- Affected area/contracts: ARC-DIST, ARC-SIGNAL, ARC-CIRCUIT, ARC-ROUTER; INV-001; exact component contracts pending.
- Trigger/cause: Fan-out shares a buffer, multiple writers appear, or a consumer cannot keep up.
- Symptoms/impact: Data races, lost events, stalled producers, or dropped instructions.
- Detection: Proposed topology validation, saturation tests, sequence checks.
- Prevention/mitigation: Dedicated buffers; capacity and per-stream backpressure rules still require approval; not implemented or verified.
- Recovery: Recovery for gaps/overflow pending stream contracts.
- Verification/tests: Ownership checks and adversarial saturation/fuzz tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.

## FM-006 — Inconsistent cross-stream or SCB ordering
- Affected area/contracts: ARC-SCB, ARC-CIRCUIT, ARC-TRANSLATOR; INV-002, INV-009; exact component contracts pending.
- Trigger/cause: Inputs arrive in different orders or state views mix updates.
- Symptoms/impact: Nondeterministic decisions or orders based on inconsistent/stale state.
- Detection: Proposed deterministic replay and snapshot-version assertions.
- Prevention/mitigation: Single SCB update owner and coherent views proposed; ordering not decided; not implemented or verified.
- Recovery: State resynchronization/replay semantics pending.
- Verification/tests: Schedule permutation, stale-input, and replay tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.

## FM-007 — Timer race or scheduler starvation
- Affected area/contracts: ARC-TIME, ARC-PLANT; INV-009; exact component contracts pending.
- Trigger/cause: Reset/cancel races with expiration, clock changes, or a strategy monopolizes work.
- Symptoms/impact: Duplicate/missed evaluation or delayed processing.
- Detection: Proposed virtual-time tests and timing/health observations.
- Prevention/mitigation: Monotonic deadlines proposed; timer generations, fairness, budgets unresolved; not implemented or verified.
- Recovery: Timer and scheduling recovery pending.
- Verification/tests: Cancel/reset/expiry races, time jumps, and starvation tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.

## FM-008 — Shared-account resource contention
- Affected area/contracts: ARC-PLANT, ARC-SCB, ARC-TRANSLATOR; INV-008; exact component contracts pending.
- Trigger/cause: Strategies allocate against stale balances or reserve the same capital.
- Symptoms/impact: Overcommitment, inconsistent exposure, or rejected orders.
- Detection: Proposed account-level reconciliation and reservation invariant checks.
- Prevention/mitigation: Plant-level allocation coordination proposed; atomic protocol unresolved; not implemented or verified.
- Recovery: Reconcile allocations/orders before permitting new exposure; precise protocol pending.
- Verification/tests: Concurrent allocation and failure/restart tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.

## FM-009 — Duplicate execution or misattributed feedback
- Affected area/contracts: ARC-ROUTER, ARC-SCB; INV-002, INV-003, INV-006, INV-007; exact component contracts pending.
- Trigger/cause: Timeout leaves submission uncertain; retry or demultiplexing is wrong.
- Symptoms/impact: Unintended exposure or another Strategy's state updated.
- Detection: Proposed correlation-ID checks and venue reconciliation.
- Prevention/mitigation: Strategy/instruction identity and idempotency/reconciliation contracts pending; not implemented or verified.
- Recovery: Resolve uncertain external status before retry policy acts; details pending.
- Verification/tests: Timeout-after-acceptance, duplicate/reordered feedback, and restart tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.

## FM-010 — Incompatible signal graph or propagation loop
- Affected area/contracts: ARC-SIGNAL, ARC-CIRCUIT, ARC-STRATEGY; exact component contracts pending.
- Trigger/cause: Configuration connects incompatible semantics or introduces an uncontrolled cycle.
- Symptoms/impact: Invalid decisions, event storms, or nontermination.
- Detection: Proposed schema/topology validation and resource monitoring.
- Prevention/mitigation: Explicit signal semantics; cycle and schema-version policies unresolved; not implemented or verified.
- Recovery: Reject/quarantine invalid assembly; exact lifecycle pending.
- Verification/tests: Malformed configuration, schema fuzzing, and cyclic-graph tests pending; none executed.
- Status: open hypothetical risk, identified during draft design.
- Related change/design: CHG-0002; docs/ARCHITECTURE.md v0.1.
