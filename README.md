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

**Block 2**: Foundation — *current*

- [x] Define the project concepts
- [x] Define the project requirements
- [ ] Define and document the axioms
  - [ ] Define the validity criteria of an axiom
  - [ ] Extract candidate axioms from concepts and requirements
  - [ ] Validate and reduce to a minimal set
  - [ ] Document the axioms ([axioms.md](./docs/design/axioms.md))
- [ ] Audit consistency: map requirements and concepts to their grounding axioms
  - [ ] Map each requirements section (§1–§29) to its grounding axioms
  - [ ] Review [concepts.md](./docs/design/concepts.md) against the axioms
  - [ ] Record and resolve inconsistencies
- [ ] Derive the design principles (derivation tree)
  - [ ] Derive Separation of Concerns from the axioms
  - [ ] Derive Separation of Responsibilities from the axioms
  - [ ] Derive interaction semantics (Chain/Sub/Super) from the axioms
  - [ ] Document the derivation tree
- [ ] Define non-goals and scope boundaries
  - [ ] Enumerate what OAK is not (§29 scope)
  - [ ] Document the scope boundaries
- [ ] Define the exit criteria for the design phase
  - [ ] Define acceptance criteria to close the design phase
  - [ ] Document the criteria

## Getting Started

Coming soon — this section will be filled once the tech stack is decided.

## Contributing

Contributions are welcome. Open an issue or a PR to discuss changes before implementing them.

## License

This project is under the [MIT License](./LICENSE)
