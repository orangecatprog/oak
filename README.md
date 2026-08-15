# OAK - Orangecat Ai Kit

> Crea tus agentes, enlázalos y crea patrones agénticos

![Status](https://img.shields.io/badge/status-design%20phase-orange)

> [!NOTE]
> This project is in design phase, that means that it's being actively designed.

## Overview

OAK is a kit for developing and connecting agents, enabling reusable agent patterns.

### Purpose

OAK is designed to be easy to use, with an intuitive TUI with different views to manage your agent schema.

### Providers

You can add AI providers with a basic plugin or a URL.
You can create your own LLM plugins — for example, a plugin that runs each question to the AI through a defined number of iterations.

### Example

An example is the **Orchestrator-Workers** pattern, where a coordinator agent (`orchestrator agent`) delegates subtasks to specialized worker agents (`worker agents`).

## Roadmap

**Block 2**: Foundation — *done*

- [x] Define the project concepts
- [x] Define the project requirements
- [x] Define and document the axioms
  - [x] Define the validity criteria of an axiom
  - [x] Extract candidate axioms from concepts and requirements
  - [x] Validate and reduce to a minimal set
  - [x] Document the axioms ([axioms.md](./docs/design/axioms.md))
- [x] Audit consistency: map requirements and concepts to their grounding axioms
  - [x] Map each requirements section (§1–§29) to its grounding axioms
  - [x] Review [concepts.md](./docs/design/concepts.md) against the axioms
  - [x] Record and resolve inconsistencies
- [x] Derive the design principles (derivation tree)
  - [x] Derive Separation of Concerns from the axioms
  - [x] Derive Separation of Responsibilities from the axioms
  - [x] Derive interaction semantics (Chain/Sub/Super) from the axioms
  - [x] Document the derivation tree
- [x] Define non-goals and scope boundaries
  - [x] Enumerate what OAK is not (§29 scope)
  - [x] Document the scope boundaries
- [x] Define the exit criteria for the design phase
  - [x] Define acceptance criteria to close the design phase
  - [x] Document the criteria

**Block 3**: Architecture — *current*

- [ ] Write the architecture document (layers, domain contracts, interactions)
  - [ ] Define the architectural layers and their dependency rules
  - [ ] Define the domain contracts of the entities
  - [ ] Define the interaction flows (Chain/Sub/Super) and the concurrency extension point
  - [ ] Define the Session and Entry Point model
  - [ ] Document the Plugin contract and the security boundaries
  - [ ] Record open decisions (tech stack, TUI, storage) with resolution criteria

## Getting Started

Coming soon — this section will be filled once the tech stack is decided.

## Contributing

Contributions are welcome. Open an issue or a PR to discuss changes before implementing them.

## License

This project is under the [MIT License](./LICENSE)
