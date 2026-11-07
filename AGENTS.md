# Mandatory repository workflow

These rules apply to every proposed change and every contributor, including coding agents.

## 1. Design from the top

Before implementation, specify the overall architecture and decompose it into components. Define responsibilities, boundaries, interfaces, dependencies, data flow, state ownership, and interactions.

Specify exact behavioral contracts for the architecture as a whole, every component, and every affected operation. Assign stable contract identifiers. Include:
- Preconditions and postconditions expressed as Hoare triples: `{P} operation {Q}`.
- Invariants, including cross-component and system-wide invariants.
- Inputs, outputs, types, units, valid ranges, and boundary behavior.
- State transitions, permitted side effects, and failure behavior.
- Any applicable concurrency, ordering, idempotency, persistence, and recovery guarantees.

Explicitly identify assumptions and unresolved questions. Do not silently fill gaps during implementation.

## 2. Approval is mandatory

The repository owner must explicitly approve the overall architecture and all component contract specifications before any implementation begins. Approval must identify the specification revision or commit it covers; record that reference.

A changed architecture or contract requires renewed approval before dependent implementation proceeds. Silence, elapsed time, or approval of an earlier revision is not approval of a new revision.

## 3. Tests first

Test cases are the first executable artifacts: write them before production code, scaffolding, stubs, or implementation changes. Architecture and contract specifications necessarily precede the tests so the tests can enforce the approved behavior.

Tests must enforce every specified behavioral contract and invariant at component and overall architecture levels. Cover normal behavior, boundaries, invalid inputs, failures, and applicable state transitions and component interactions. Use property-based tests where needed to check invariants across input or state spaces.

Maintain traceability from every contract/invariant identifier to its enforcing tests. If a guarantee cannot be tested directly, document the limitation and proposed verification method in the specification and obtain explicit approval before implementation. Do not claim finite tests constitute formal proof.

Run the tests before implementation and record the expected failures or inability to run due to missing implementation. Then implement only the approved behavior and run the complete relevant contract suite. Do not weaken tests or alter contracts merely to accommodate implementation.

## 4. Document the code's exact contracts

All code must document the exact contract it satisfies. Identify the approved contract IDs and their specification revision, and state the applicable preconditions, postconditions, invariants, side effects, and failure behavior in the code documentation. This includes test code and supporting executable code.

Maintain architecture-to-component-to-operation-to-test-to-code traceability. Code without corresponding approved contracts is not ready for implementation or acceptance.

## 5. Adversarial testing for integrated components

Every newly integrated component, including third-party dependencies and venue adapters, must undergo adversarial testing at its actual integration boundary before acceptance. Changes to an existing integration must repeat and extend these tests for the affected behavior.

Specify the adversarial test plan with the component contracts and obtain owner approval before implementation. Write adversarial tests and fuzz harnesses before production integration code, under the tests-first rule.

Required coverage:
- Fuzz interface inputs and serialized data, including malformed, truncated, oversized, unexpected, and boundary values. Use stateful or sequence fuzzing for stateful interfaces.
- Assert approved contracts and invariants after accepted inputs, rejected inputs, and failures; verify no unauthorized side effects or corrupted state.
- Inject applicable dependency faults: timeouts, disconnects, partial responses, stale data, duplicates, reordered messages, rate limits, and invalid upstream responses.
- Exercise applicable concurrency, retry, cancellation, restart, and recovery behavior.
- Check resource bounds and failure containment against explicit approved limits.

Document applicability for each fault category; omissions require an explicit rationale and owner approval. Fuzz testing is mandatory for every new integration, not replaced by ordinary example tests.

Make failures reproducible: record seeds, execution budgets, tool versions, and relevant configuration; minimize failing inputs and retain them as regression cases. Define a bounded CI fuzz run and a longer pre-acceptance campaign in the approved plan. Run against isolated environments and synthetic data, without live financial side effects.

Acceptance requires recorded adversarial test results, completion of the approved fuzzing budgets, and no unresolved contract or invariant violations. A passing fuzz campaign is evidence, not proof of correctness.

## 6. Completion criteria

A change is complete only when approved specifications, tests, implementation, and code documentation agree, every contract and invariant has verification coverage, and all required checks, including the approved adversarial and fuzz testing campaigns, pass.

Recording this repository policy is not approval of any product architecture, component specification, or implementation.
