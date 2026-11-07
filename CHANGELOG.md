# Change log

Entries are append-only. Git commits provide exact diffs; this log records intent, state transitions, approvals, and evidence. This file tracks development changes; runtime audit-log behavior requires separate approved contracts.

## CHG-0001 — 2026-11-07T21:07:05Z — Codex acting on owner instruction

- Reason/authorization: owner requires all edits to be logged and possible failure modes documented continuously.
- Affected paths: `AGENTS.md`, `CHANGELOG.md` (including this entry), `docs/FAILURE_MODES.md`.
- Before: architecture/contract approval, tests-first, code-contract documentation, adversarial testing, and fuzzing policies existed; no dedicated change log or failure-mode register.
- After: mandatory logging and continuous failure-mode tracking rules established; both tracking files initialized.
- Approval: direct owner instruction in this chat for this policy/documentation change. Product architecture and component contracts remain unapproved.
- Verification: reviewed policy and register for required fields and consistency with existing gates; documentation-only change, no executable tests applicable. Publication is evidenced by the containing Git commit.
- Related failure modes: FM-001 through FM-004.
- Product state: planning only; no product implementation or integrations. Earlier commits are the authoritative history before logging began; this entry does not reconstruct missing historical records.

## CHG-0002 — 2026-11-07T21:30:46Z — Codex acting on owner instruction

- Reason/authorization: owner requested recording the initial structure discussed in chat.
- Affected paths: `docs/ARCHITECTURE.md`, `docs/FAILURE_MODES.md`, `CHANGELOG.md` (including this entry).
- Before: architecture existed only in discussion; risk register covered FM-001 through FM-004.
- After: draft v0.1 captures Plant/Strategy containers, SCB, SPSC topology, signal/circuit composition, timing, translator, and Router; FM-005 through FM-010 added.
- Approval: permission to record a draft only. No complete architecture/component contract approval or implementation authorization inferred. Scheduling semantics explicitly deferred.
- Verification: reviewed against discussion and AGENTS.md; checked component/invariant/failure-mode references, deferred decisions, and no executable changes. Documentation-only; executable tests/fuzzing not applicable to this recording step. Publication evidenced by containing commit.
- Related failure modes: FM-002 through FM-010; all remain open, with proposed mitigations unverified.
- Follow-up: refine unresolved decisions, exact Hoare contracts, and test plans before approval and tests-first implementation.
