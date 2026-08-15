# OAK - Exit Criteria for the Design Phase

> Acceptance criteria to close the design phase and begin implementation.

## Purpose

Define the criteria that must be met before the design phase is considered complete and implementation (Block 5) can begin.

## Criteria

1. **Axioms defined and validated** — [axioms.md](./axioms.md) documents the axiom set with its validity criteria and its validation. *Status: done.*
2. **Consistency audit complete** — every requirement §1–§29 and every concept of [concepts.md](./concepts.md) is grounded in at least one axiom; inconsistencies are recorded and resolved in [audit.md](./audit.md). *Status: done.*
3. **Design principles derived** — [principles.md](./principles.md) derives the design principles from the axioms, each traceable to its grounding axioms. *Status: done.*
4. **Non-goals documented** — [scope.md](./scope.md) records what OAK is not and the boundaries of its scope. *Status: done.*
5. **Architecture documented** — the architecture document defines layers, domain contracts, interaction flows, the Session and Entry Point model, and the Plugin contract, consistent with the axioms, principles, and requirements.
6. **Resource format and Pattern structure specified** — the resource format (Markdown with frontmatter) and the Pattern structure and discovery are defined, consistent with §10, §11, §26, and §27.
7. **Open decisions resolved or explicitly deferred** — the tech stack, TUI framework, and session storage are recorded either as decided or as explicitly deferred with the criteria that will resolve them.
8. **Traceability holds** — every architecture decision cites its grounding chain: axiom → principle → requirement → decision.
9. **Requirements coverage** — the architecture addresses all §1–§29, or records an explicit deferral for those outside its scope.
10. **Cross-platform consideration** — §25 (Windows, Linux, macOS, WSL, server environments) is considered in the architecture without altering the conceptual model.

## How to verify

- Each referenced document exists and has been reviewed.
- The traceability tables are complete: no requirement or concept is left ungrounded.
- A final review pass confirms each criterion and records the result in the [CHANGELOG.md](../../CHANGELOG.md).

## Relation to other documents

- [axioms.md](./axioms.md), [principles.md](./principles.md), [audit.md](./audit.md), and [scope.md](./scope.md) — the foundation of the design phase.
- [requirements.md](./requirements.md) — the obligations the design must satisfy.
