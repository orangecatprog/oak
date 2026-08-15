# OAK - Axioms

> Foundational axioms of OAK - Orange AI Kit.

## Purpose

An axiom is the irreducible foundation of OAK. Every principle, requirement, and design decision of the project must derive from these axioms, directly or indirectly, or at minimum must not contradict them.

This document defines what an axiom is, the criteria that validate it, and the seven axioms that form the axiom set of OAK.

## Definition and statement hierarchy

An axiom in OAK is:

> A foundational statement accepted without justification, from which all principles, requirements, and design decisions derive, directly or indirectly. It is not a choice or a goal; it is the basis that justifies the choices and the goals.

Every statement of the project must be classifiable in this hierarchy, and the direction of justification never forms cycles: it always terminates in axioms.

```plaintext
Axiom       → accepted, requires no justification
Principle   → derived from axioms
Requirement → derived obligation
Decision    → justified choice
```

## Validity criteria

**Per axiom (individual):**

- **C1 · Irreducible** — cannot be justified by means of another axiom in the set.
  *Test: "can I derive this from another axiom?" → if yes, it is not an axiom; it is another kind of statement (principle, requirement, or decision).*
- **C2 · Foundational** — concrete decisions derive from it.
  *Test: "if I remove it, do decisions remain ungrounded?" → if not, it is decorative.*
- **C3 · Essential** — negating it contradicts the nature of the project.
  *Test: "if I negate it, does OAK cease to be OAK?" → if not, it is not essential.*
- **C4 · Precise** — unambiguous, applicable, and auditable statement.
  *Test: "can two people disagree on what it implies?" → if yes, restate it.*

**Of the set (set-level):**

- **C5 · Consistency** — no axiom contradicts another.
- **C6 · Completeness** — every requirement and decision is traceable to at least one axiom.
- **C7 · Parsimony** — minimal set, without surplus or overlap.

## The axioms of OAK

The following seven statements form the axiom set of OAK. Each was extracted from [concepts.md](./concepts.md) and [requirements.md](./requirements.md) and validated against the criteria C1–C7.

### A1 · Autonomy

The Agent is solely responsible for its reasoning. It decides which entity to interact with and which actions to perform. No other component reasons on its behalf.

Provenance:

- [concepts.md](./concepts.md): Agent; Trigger; Agentic Execution.
- [requirements.md](./requirements.md): §2.1, §15.

### A2 · Bounded Operation

The system defines and enforces the operational limits of an entity, independently of the entity's reasoning.

Provenance:

- [concepts.md](./concepts.md): Harness; Guardrail; Tool.
- [requirements.md](./requirements.md): §2.1, §2.2, §4, §5, §6, §16, §18, §22, §23.

### A3 · Identity

An entity's identity is defined by what it is, not by the technology it uses.

Provenance:

- [concepts.md](./concepts.md): Model; Provider; Resource.
- [requirements.md](./requirements.md): §2.1, §3, §26.

### A4 · Explicit Information

Information flows between entities only when explicitly provided; nothing is inherited implicitly.

Provenance:

- [concepts.md](./concepts.md): Context; Skill; Subagent; Chain; Sub; Super.
- [requirements.md](./requirements.md): §2.2, §2.3, §7, §12, §13, §14.

### A5 · Technological Independence

OAK orchestrates implementations without depending on them; every concrete technology is replaceable.

Provenance:

- [concepts.md](./concepts.md): Interoperability; Plugin; Core.
- [requirements.md](./requirements.md): §3, §11, §17, §18, §19, §22, §24, §25, §27, §28, §29.

### A6 · Organization Is Not Behavior

Structure organizes; it is not executed and does not redefine behavior.

Provenance:

- [concepts.md](./concepts.md): Pattern; Session; Entry Point.
- [requirements.md](./requirements.md): §1, §8, §9, §10, §11, §16, §27, §28.

### A7 · Accountability

The system must be able to account for what occurs during its execution.

Provenance:

- [concepts.md](./concepts.md): Session.
- [requirements.md](./requirements.md): §8, §20, §21.

## Statements considered and not proposed

- "A Tool always produces a result for the entity that invokes it" — a contract requirement on Tools, grounded in A2 rather than a foundation.
- "Users interact with a system through its Entry Point rather than directly selecting an Agent" — an interaction requirement (§9), grounded in A6.
- "A Skill is ephemeral and maintains no persistent Context" — a consequence of A4.
- "Sessions are not directly editable" — a consequence of A6.
- "Agent versioning is not required" — a scope decision (§8), not a foundation.

## Validation

### Individual criteria (C1–C4)

| Axiom | C1 · Irreducible | C2 · Foundational | C3 · Essential | C4 · Precise |
| --- | --- | --- | --- | --- |
| A1 · Autonomy | Passes | Passes | Passes | Passes |
| A2 · Bounded Operation | Passes | Passes | Passes | Passes |
| A3 · Identity | Passes | Passes | Passes | Passes |
| A4 · Explicit Information | Passes | Passes | Passes | Passes |
| A5 · Technological Independence | Passes | Passes | Passes | Passes |
| A6 · Organization Is Not Behavior | Passes | Passes | Passes | Passes |
| A7 · Accountability | Passes | Passes | Passes | Passes |

Notable checks:

- **C1 · Irreducible** — no axiom can be justified through another axiom of the set. A3 and A5 share their origin in technology but address distinct concerns: A3 defines the semantic identity of an entity, A5 defines the architectural decoupling of OAK.
- **C3 · Essential** — negating A3 or A6 directly contradicts explicit statements of [concepts.md](./concepts.md) ("An Agent is not permanently coupled to a specific Model"; "An Agent does not execute a Pattern"). Negating A7 contradicts §20 of [requirements.md](./requirements.md).

### Set criteria

- **C5 · Consistency** — no axiom contradicts another. The pairs with the highest tension (A1/A2, A3/A5, A6/A7) are complementary, not contradictory:
  - A1 and A2: the Agent decides; the system enforces the limits of that decision.
  - A3 and A5: technology neither defines an entity's identity nor binds OAK.
  - A6 and A7: structure does not behave, but the system can still account for what happened.
- **C7 · Parsimony** — no reduction was required: removing any axiom leaves requirements ungrounded, and no pair can be merged without losing meaning. The minimal set is 7.
- **C6 · Completeness** — every requirements section §1–§29 is traceable to at least one axiom. The detailed traceability table is produced by the consistency audit task.

## Relation to other documents

- [concepts.md](./concepts.md) — the conceptual model that these axioms underpin.
- [requirements.md](./requirements.md) — the obligations derived from these axioms.
- Next tasks of the design phase: derive the design principles (derivation tree) from these axioms, and produce the detailed consistency audit.
