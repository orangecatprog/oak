# ADR 005 · Test-Driven Development

- **Status**: Accepted
- **Date**: 2026-08-15

## Context

This project records ADRs to adopt portable concepts that can be used here and transferred to other projects. Test-Driven Development is exactly that kind of concept: a development practice applicable to any project, independent of its technology.

OAK's architecture provides the conditions that make TDD effective:

- The dependency rule of [ADR 001](./001_clean-architecture.md) isolates layers so each can be tested without the others.
- The contracts of [ADR 003](./003_contract-implementation.md) allow fake implementations to satisfy capabilities.
- The domain vocabulary of [concepts.md](../concepts.md) lets tests read as domain scenarios rather than technical plumbing.

## Why test-driven development

- **Testability is decided by the structure.** Whether a layer can be tested in isolation is determined by the dependency rule and the contracts, not by a test framework.
- **Requirements become executable.** Each requirement (§1–§29) is expressed as a failing test first, then satisfied by design, making the consistency audit mechanically verifiable.
- **Design proceeds incrementally.** Red-green-refactor adds each capability through its observable behavior.
- **Feedback is fast and deterministic.** The Core is tested against contracts, without networks, providers, or storage.

## Decision

OAK adopts test-driven development as its development practice: each capability begins with a failing test (red), continues with the minimal behavior that makes it pass (green), and ends with refactoring under the safety of the tests.

### Testing strategy by layer

- **Domain layer** — unit tests on entities, contracts, and invariants. No I/O, no external dependencies.
- **Application layer (Kernel)** — behavior tests of orchestration and interaction scenarios (Chain, Sub, Super), using fake implementations that satisfy the contracts of [ADR 003](./003_contract-implementation.md).
- **External layer** — minimal integration tests with real adapters; the Core's behavior is already covered by contract tests.

### Coverage of requirements

- Every requirement §1–§29 has executable coverage at the appropriate layer, or an explicit deferral when it is out of the initial scope.
- Contract invariants are tested through their fakes (e.g., a Tool always returns a result; a Skill maintains no persistent Context; a Context is owned by its entity).

## What this improves

- **Verifiable traceability** — tests are the executable form of the requirements audit.
- **Boundary enforcement** — if a layer cannot be tested in isolation, the dependency rule has been violated; tests police [ADR 001](./001_clean-architecture.md) mechanically.
- **Safe evolution** — infrastructure, providers, and UI can change without re-verifying the Core manually.
- **Deterministic quality** — Core behavior is verified without relying on external services.

## Consequences

### Positive

- The Core is assured independently of its infrastructure (A5).
- Requirements become executable specifications.
- Refactoring of External layers is safe and cheap.

### Negative

- Contract design discipline is required: fakes must faithfully mirror the contracts they satisfy.
- Up-front time cost: every capability begins with a failing test.
- Integration coverage is limited by design; real provider and storage behavior must be validated separately.

## Traceability

- **Axioms**: A5.
- **Principles**: P1, P2, P7.
- **Requirements**: §20, §24.
- **ADRs**: 001, 003.
