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
