# ADR 001 · Clean Architecture: Core / External Model

- **Status**: Accepted
- **Date**: 2026-08-15

## Context

OAK must be structured so that:

- The Agent reasons and decides, while the system only orchestrates (A1).
- The system defines and enforces operational limits independently of the Agent's reasoning (A2).
- OAK orchestrates implementations without depending on them; every concrete technology is replaceable (A5).
- The system is decomposed by concern into distinct layers, isolated from each other (P1 · Separation of Concerns).
- OAK exposes a public interface so external systems and presentations can use it without reaching Core internals (§18, §19).
- The Core remains independent of concrete Model, Provider, Tool, and Guardrail implementations (§24).

The decision defines the layer model that satisfies these constraints and the rules that keep the dependencies aligned with them.

## Why clean architecture

Clean architecture organizes the system so that dependencies point **inward**: the most volatile elements (frameworks, providers, UI, storage) depend on the most stable ones (the domain), never the other way around.

This fits OAK because:

- **It realizes the Dependency Rule as an architectural constraint.** OAK's axioms already demand separation; clean architecture turns that separation into a mechanical, verifiable rule: nothing in the Core may reference External.
- **It makes independence an enforced structure, not a convention.** A5 (Technological Independence) requires replaceable implementations. With clean architecture, a Model or Provider is an adapter in External that depends on the Core; replacing it never touches the Core.
- **It isolates plugins architecturally.** P7 (Plugin Isolation) requires plugins to interact through explicit abstractions without unrestricted Core access. Clean architecture places plugins in External, where the boundary itself blocks access to Core internals.
- **It keeps the Core presentation-free and framework-free.** §19 requires the Core not to depend on any presentation. Clean architecture makes the TUI one more External adapter.
- **It enables testability without infrastructure.** The Domain and Application layers can be exercised with no providers, storage, or UI, which matches the requirement that the Core be independent of concrete implementations.

## Decision

OAK is structured in two zones with four layers.

### Core

The Core is the conceptual and operational center of OAK. It contains the Domain and the Application, and it never depends on External.

#### Domain layer

The Domain layer contains the identity of OAK: what the entities are, independent of how they are implemented or presented.

Subparts:

- **Entities** — the domain model of Agent, Subagent, Skill, Assistant, and the other resources they can interact with.
- **Contracts (abstractions)** — the interfaces that define Model, Provider, Context, Harness, Tool, Guardrail, and the interaction surface between entities.
- **Value objects and invariants** — the domain rules such as identity being independent of Model/Provider (A3) and Contexts being owned by their entities (A4).

The Domain layer depends on nothing.

#### Application layer

The Application layer is the Kernel: it coordinates agentic execution using the Domain, without deciding on behalf of any Agent (A1).

Subparts:

- **Orchestration** — the execution cycle of agentic systems: dispatch, coordination, and supervision of entities.
- **Interactions** — the execution of Chain, Sub, and Super relationships between entities.
- **Sessions and Entry Points** — the coordination of Sessions and the handling of Entry Point input, producing a final response and execution information (§9).
- **Ports** — the public interfaces exposed by the Core. Ports are the surface that External consumes and that external systems integrate with (§18, §19).

The Application layer depends only on the Domain layer.

### External

The External zone contains every concrete implementation, interface, and integration. It depends on the Core through its ports and contracts, and never the other way around.

#### Infrastructure layer

The Infrastructure layer provides the adapters that implement the contracts and ports of the Core.

Subparts:

- **Provider adapters** — concrete Model and Provider implementations.
- **Tool and Guardrail implementations** — concrete capabilities and restrictions.
- **Persistence** — the storage mechanism for Sessions and resources.
- **Plugins** — isolated extensions that integrate OAK with external systems through explicit abstractions.

#### Presentation layer

The Presentation layer provides the interfaces through which users manage and use OAK.

Subparts:

- **TUI** — the primary user interface of OAK.
- **Other presentations** — any additional interface built on the same ports.

### Dependency rules

1. **Domain** depends on nothing.
2. **Application** depends only on Domain.
3. **Infrastructure** depends on Core (its ports and contracts).
4. **Presentation** depends on Core (its ports).
5. **Infrastructure and Presentation never depend on each other.**
6. **Nothing inside Core depends on External.**
7. The **public API** of OAK is the set of ports exposed by the Application layer. External systems and presentations integrate through adapters that implement those ports.

## What this improves

- **Technological independence becomes structural.** Replacing a Model, Provider, or storage mechanism touches only Infrastructure, never the Core (A5, §24).
- **Plugin isolation is enforced by the architecture.** Plugins are Infrastructure adapters; the boundary itself prevents unrestricted access to the Core (P7, §18).
- **The Core is presentation-free.** A TUI, a CLI, or an external application are interchangeable adapters over the same ports (§19).
- **Boundaries are verifiable.** The dependency rules can be checked mechanically, which converts an intention (SoC) into an auditable constraint (P1).
- **Testing is decoupled.** Domain and Application can be exercised without providers, storage, or UI, matching the requirement that the Core be independent of concrete implementations.
- **The Agent's autonomy and the system's bounds stay separate.** The Kernel orchestrates (A1) and the boundary enforces limits (A2) without either crossing the other.

## Consequences

### Positive

- Replaceable infrastructure without identity change (A3, A5).
- Multiple presentations and external integrations supported (§18, §19).
- Security enforced at the boundary rather than by cooperation (P7, §23).
- Clear separation between orchestration (Application) and reasoning (the Agent).

### Negative

- Requires discipline: dependency direction must be maintained in every contribution.
- Adds indirection: adapters and ports are an abstraction layer with a cost in structure and verbosity.
- Contributors familiar with hexagonal or layered terminology must map it to the two-zone Core/External naming.
- Persistence and provider specifics are deferred to Infrastructure, which postpones some concrete decisions to the implementation phase.

## Traceability

- **Axioms**: A1, A2, A5.
- **Principles**: P1, P7.
- **Requirements**: §18, §19, §24, §29.
