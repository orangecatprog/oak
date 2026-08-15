# OAK - Non-Goals and Scope Boundaries

> Explicit statement of what OAK is not and the boundaries of its scope.

## Purpose

Record explicitly what OAK is not and the boundaries of its scope, so that design decisions never silently import unstated assumptions.

## Non-goals

OAK is not, and must not become, any of the following:

1. **Not an AI provider or model** — OAK does not implement Models or Providers; it orchestrates them. Concrete implementations belong to their ecosystems (A5, §3).
2. **Not a presentation technology** — the Core does not depend on a TUI or any specific interface. A TUI is one possible presentation (A5, §19).
3. **Not defined by an internal language or architecture** — the programming language, layer structure, and storage mechanism are implementation decisions reserved for the implementation phase (§29).
4. **Not YAML-based by default** — YAML-based Pattern or action definitions are reserved for future development (§28).
5. **Not imposing a single concurrency model** — each Pattern may define whether its interactions are sequential or concurrent (§22).
6. **Not requiring Agent versioning** — out of the initial scope (§8).
7. **Not an interpreter of semantic content** — OAK organizes and exposes the structure of resources; the entity using a resource interprets its semantic content (§17, A5).
8. **Not requiring knowledge of a resource's origin** — OAK works with established conventions without needing to know which system created a compatible resource (§17).
9. **Not requiring a monolithic global configuration** — configuration belongs to the resource or mechanism that requires it (§27).
10. **Not reasoning on behalf of an Agent** — autonomy is the Agent's; no component decides for it (A1).
11. **Not enforcing security through instructions** — security is enforced by the system, independently of the Agent's reasoning (A2, §23).
12. **Not providing editable Sessions** — a Session is a record, not a mechanism for redefining entities (A6, §8).
13. **Not propagating Context implicitly** — only explicitly provided information flows between entities (A4).

## Scope boundaries

### In scope for the design phase (Blocks 2–4)

- Axioms, consistency audit, design principles, non-goals, and exit criteria.
- Architecture: layers, domain contracts, interaction flows, Session and Entry Point model, Plugin contract, security boundaries, observability.
- Resource format and Pattern structure: Markdown with frontmatter, Pattern structure and discovery, resource identity.
- Open decisions (tech stack, TUI framework, session storage) recorded with their resolution criteria.

### Out of scope for the design phase

- Code implementation (Block 5).
- Concrete Model, Provider, Tool, and Guardrail implementations.
- YAML-based formats.

## Relation to other documents

- [axioms.md](./axioms.md) — the foundation these boundaries respect.
- [requirements.md](./requirements.md) — §29 defines what the requirements do not cover.
- [exit-criteria.md](./exit-criteria.md) — the criteria that close the design phase within these boundaries.
