# ADR 004 · Design Patterns: Adoption of Reusable Patterns

- **Status**: Accepted
- **Date**: 2026-08-15

## Context

OAK must implement its architecture using well-known, portable design patterns. An ADR records the adoption of a concept so that it can be transferred to another project and used there; classic design patterns are exactly that kind of portable concept.

The patterns OAK adopts must serve its structural requirements, not decorate them:

- Independence from concrete implementations (A5, §24), expressed by contracts separated from implementations ([ADR 003](./003_contract-implementation.md)).
- Layers and boundaries that isolate the Core ([ADR 001](./001_clean-architecture.md)).
- Observable execution (A7, §20).

## Why reusable design patterns

- **Recognizability** — a classic pattern is understood by any reader without project-specific documentation.
- **Portability** — a pattern is a concept that can be taken, applied to another project, and used as-is, which is the purpose of an ADR in this project.
- **Purposeful adoption** — each pattern is chosen because it serves one of OAK's requirements; no pattern is decorative.

## Decision

OAK adopts the following classic design patterns, each applied where it serves a structural requirement.

### Factory

- **Purpose**: create entities and contracts without coupling to concrete implementations.
- **Application**: the creation of Agents, Skills, Assistants, and their Models, Providers, and Tools goes through factories, so the Core never names a concrete implementation (A5, §24; [ADR 003](./003_contract-implementation.md)).
- **Layer**: Domain and Application.

### Adapter

- **Purpose**: satisfy a contract (port) with a concrete implementation.
- **Application**: Infrastructure adapters implement the contracts of the Core — Providers, Tools, storage — so replaceable implementations live in External ([ADR 001](./001_clean-architecture.md), [ADR 003](./003_contract-implementation.md)).
- **Layer**: External (Infrastructure).

### Strategy

- **Purpose**: provide replaceable behaviors behind a stable interface.
- **Application**: interchangeable behaviors such as Model and Provider selection, error handling strategies per Pattern (§21), and concurrency strategies (§22).
- **Layer**: Application and External.

### Observer

- **Purpose**: notify interested parties about events without coupling them.
- **Application**: execution events for observability (A7, §20) — interactions, Tool and Skill usage, Subagent results, errors, timing.
- **Layer**: Application (event surface) and External (subscribers).

### Builder

- **Purpose**: construct complex entities with optional parts.
- **Application**: assembling an Agent from its Model, Context, and Harness (likewise a Subagent or a Skill) with explicit parts, preserving identity (A3).
- **Layer**: Domain and Application.

### Facade

- **Purpose**: expose a simplified surface over a subsystem.
- **Application**: the public API / ports that external systems and presentations use (§18, §19), hiding Core internals ([ADR 001](./001_clean-architecture.md)).
- **Layer**: Application (ports).

### Patterns not adopted

- **Singleton** — OAK has no global state; resource identity is per-resource, not process-global (A3, §26).
- **Chain of Responsibility** — the OAK "Chain" interaction (Agent A provides information to Agent B) is domain semantics, not the Chain of Responsibility pattern. Adopting the pattern would conflate the two; the domain interaction remains defined in [concepts.md](../concepts.md).

## What this improves

- **Recognizability** — the design is readable through a common, transferable vocabulary.
- **Portability** — each adopted pattern can be taken to another project and used there, which is the purpose of these ADRs.
- **Purposefulness** — every pattern maps to a structural requirement, so nothing is adopted for its own sake.
- **Consistency** — patterns reinforce the layers and contracts of [ADR 001](./001_clean-architecture.md) and [ADR 003](./003_contract-implementation.md).

## Consequences

### Positive

- A familiar design vocabulary, shared across projects.
- Patterns serve the axioms (A5, A7) instead of driving them.
- Clear homes for typical implementation tasks (creation, adaptation, replacement, notification).

### Negative

- The pattern set must be revalidated as the architecture evolves.
- Misuse risk: a pattern must only be applied where it serves a requirement.
- Not every classic pattern applies; unadopted patterns must be deliberately excluded to keep the design honest.

## Traceability

- **Axioms**: A5, A7.
- **Principles**: P1, P2, P7.
- **Requirements**: §18, §19, §20, §21, §22, §24.
- **ADRs**: 001, 003.
