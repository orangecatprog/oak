# OAK - Design Principles

> Principles derived from the axioms of [axioms.md](./axioms.md).

## Method

A principle is a design statement derived from one or more axioms. Each principle cites the axioms that ground it, and the derivation tree shows the whole structure. No principle may contradict an axiom, and every principle must trace back to at least one axiom.

## Derivation tree

```text
P1 · Separation of Concerns        A1 + A2 + A5
P2 · Separation of Responsibilities A1 + A2 + A4
P3 · Identity Model                 A3
P4 · Interaction Semantics          A4 + A6
P5 · Organization Principle         A6
P6 · Accountability                 A7
P7 · Plugin Isolation               A2 + A5
```

## Principles

### P1 · Separation of Concerns (A1 + A2 + A5)

The system is decomposed by concern into distinct layers, each responsible for one concern and isolated from the others:

- **Kernel** — orchestrates agentic execution without deciding on behalf of an Agent (A1).
- **Domain contracts** — define the abstractions between OAK and implementations (A5).
- **Plugins** — extension, isolated and bounded (A2, A5).
- **Presentation** — external, depends only on public interfaces (A5).

Consequence: no layer reasons on behalf of an Agent, no layer binds OAK to a concrete technology, and boundaries are defined and enforced by the system.

### P2 · Separation of Responsibilities (A1 + A2 + A4)

Each domain entity has a distinct responsibility:

- **Agent** — decides, acts, and interacts (A1).
- **Harness** — defines the operational scope (A2).
- **Tool** — provides a capability (A2).
- **Guardrail** — restricts a capability (A2).
- **Context** — holds only explicitly provided information (A4).
- **Skill** — provides a specialized capability without persistent Context (A2, A4).
- **Assistant** — reasons without acting (A1, A2).
- **Subagent** — works with its own Context and returns a result (A1, A4).

Consequence: no entity combines responsibilities that another axiom separates (no Tool–Guardrail fusion, no Skill with Context).

### P3 · Identity Model (A3)

An entity's identity is independent of its Model and Provider. A resource's identity is distinguishable from its human-readable name, and multiple resources may share the same name.

Consequence: changing a Model or Provider does not change the entity; identity is never tied to technology.

### P4 · Interaction Semantics (A4 + A6)

Agent interactions are explicit transfers, never implicit propagation:

- **Chain** — an Agent provides information to another Agent; no automatic return and no automatic Context propagation.
- **Sub** — an Agent delegates work to a Subagent; the Subagent works with its own Context and returns a summary.
- **Super** — the Subagent returns information to its superior Agent through a callback; it requires a prior Sub relationship.

Consequence: the interaction model is derived from the axioms, not chosen independently.

### P5 · Organization Principle (A6)

Patterns organize resources; Sessions record interactions. Neither executes nor redefines behavior.

Consequence: loading a Session does not modify Agents; importing a Pattern makes its resources part of the destination project; a Session is a record, not a definition.

### P6 · Accountability (A7)

Execution must be observable and auditable: interactions, Tool and Skill usage, Subagent creation and results, errors, and timing.

Consequence: observability and error handling are requirements derived from an axiom, not optional additions.

### P7 · Plugin Isolation (A2 + A5)

Plugins extend OAK through explicit abstractions without unrestricted access to the Core.

Consequence: plugins interact through exposed interfaces; security is enforced by the system, not by plugin cooperation or by an Agent following instructions.

## Principle traceability

| Principle | Grounding axioms |
| --- | --- |
| P1 · Separation of Concerns | A1, A2, A5 |
| P2 · Separation of Responsibilities | A1, A2, A4 |
| P3 · Identity Model | A3 |
| P4 · Interaction Semantics | A4, A6 |
| P5 · Organization Principle | A6 |
| P6 · Accountability | A7 |
| P7 · Plugin Isolation | A2, A5 |

## Relation to other documents

- [axioms.md](./axioms.md) — the source of these principles.
- [requirements.md](./requirements.md) — the obligations these principles support.
- [audit.md](./audit.md) — the consistency audit that grounds requirements and concepts in axioms.
