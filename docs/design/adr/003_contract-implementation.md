# ADR 003 · Contract and Implementation

- **Status**: Accepted
- **Date**: 2026-08-15

## Context

OAK must orchestrate entities and capabilities without depending on their concrete implementations (A5, §24). The Core communicates with implementations through defined abstractions (§24), and every concrete technology is replaceable without changing the identity of the entities that use them (A3).

At the same time, each domain entity has a distinct responsibility (P2 · Separation of Responsibilities): the Agent decides, the Harness bounds, the Tool provides a capability, the Guardrail restricts it, the Context holds only explicitly provided information (A4).

The decision must define what a contract is, what an implementation is, and the rules that keep the two separate and replaceable.

## Why contracts and implementations are separate

- **Replaceability** — an implementation that is part of the contract would become part of the identity of the entity using it, contradicting A3. Separation keeps Model, Provider, and Tool changes invisible to the entities.
- **Isolation (P7)** — implementations (including plugins) must interact with OAK through explicit abstractions. A separate contract surface is the boundary through which they do so (§18).
- **Stability** — the contract is the most stable part of the Core; implementations are the most volatile. Mixing them couples the stable to the volatile.
- **Testability** — a contract can be satisfied by a fake implementation, so the Core can be exercised without real providers, models, or storage.
- **Independent evolution** — the Core and external ecosystems evolve separately as long as the contract holds.

## Decision

A **contract** is a domain interface that defines what an entity or capability must provide to OAK. An **implementation** is a concrete adapter that satisfies a contract.

### What a contract is

A contract defines, and only defines:

- **Operations** — the capabilities the entity or capability exposes.
- **Result shapes** — the information produced by an operation (e.g., a Tool always produces a result: useful information, a success status, a code, or an error, per §5).
- **Invariants** — the domain rules that hold for any implementation (e.g., a Skill maintains no persistent Context; a Context is owned by its entity).

A contract never contains behavior, state beyond what it owns, or references to external technology.

### Contract categories

- **Capability contracts** — what an entity can use:
  - **Model** — reasoning and generation.
  - **Provider** — communication with a Model.
  - **Tool** — an executable capability; always returns a result.
  - **Guardrail** — a restriction over capabilities and behavior.
  - **Harness** — the operational environment that provides Tools, Guardrails, and available entities.

- **Entity contracts** — what an entity is and how it participates:
  - **Agent** — reasons, acts, and interacts; has a Model, a Context, and a Harness.
  - **Subagent** — an Agent subordinated to another Agent.
  - **Skill** — a specialized capability; has a Model and a Harness, no Context.
  - **Assistant** — reasons and answers; has a Model and a Context, no Harness.

- **State contract**:
  - **Context** — the information available to an entity; owned by its entity.

### What an implementation is

An implementation satisfies a contract and lives outside the contract:

- Concrete Model and Provider implementations are Infrastructure adapters.
- Concrete Tools and Guardrails are Infrastructure.
- Plugins provide implementations through the exposed abstractions.
- In-memory or persisted Context and Session storage are Infrastructure.

The identity of an entity does not depend on which implementation satisfies its contracts (A3).

### Rules

1. **A contract defines the interface, never the implementation.**
2. **Implementations live in External** (Infrastructure) or are provided by plugins; never inside the contract.
3. **Replaceability** — an implementation can be replaced without changing the identity of the entity using it (A3).
4. **Isolation** — implementations cannot access Core internals beyond what the contract exposes (P7, §18).
5. **Invariants are part of the contract** — e.g., a Tool always returns a result (§5); a Context is owned by its entity (A4); a Skill has no persistent Context (A4).
6. **Capability and restriction stay separate** — a Tool provides a capability; a Guardrail restricts it (A2). Enforcement belongs to the system, never to the Agent's cooperation (§6, §23).
7. **Contracts are the most stable surface of the Core** — they change rarely and with explicit justification, following versioning discipline.

## What this improves

- **Replaceability without identity change** — Model, Provider, and Tool implementations swap without touching entities (A3, §3).
- **Isolation that is mechanical, not conventional** — the contract surface is the only way into the Core (P7, §18).
- **Independent evolution** — Core and ecosystems evolve separately while the contract holds.
- **Testability** — fakes that satisfy contracts replace real infrastructure in Core tests.
- **Verifiable boundary** — the dependency rule is enforced through contracts, giving ADR 001 its mechanical check.
- **Interoperability** — OAK works with established conventions without owning or interpreting them fully (§17), because it only needs the structure a contract declares.

## Consequences

### Positive

- Core stability with volatile infrastructure.
- Providers, models, and tools are swappable (A5).
- Plugins and external systems integrate through a single, explicit surface (§18).
- Domain rules are enforceable as contract invariants.

### Negative

- Contract design has a real cost: interfaces must be designed carefully before implementation.
- Every concrete capability passes through a contract, adding indirection.
- Contract drift is a risk if versioning discipline is not maintained.
- Some invariants are hard to express as type-level contracts and require runtime checks.

## Traceability

- **Axioms**: A2, A3, A4, A5.
- **Principles**: P2, P3, P7.
- **Requirements**: §3, §4, §5, §6, §7, §13, §14, §16, §18, §24, §26.
