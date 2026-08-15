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

## Tech Stack

- **Language**: Go — the Core, Kernel, and TUI.
- **TUI**: Charm (Bubble Tea, Lip Gloss, Bubbles), as an External adapter over the Core ports.
- See [docs/design/tech-stack.md](./docs/design/tech-stack.md) for the decision and its criteria.

## Getting Started

Coming soon — implementation begins in Block 5.

## Contributing

Contributions are welcome. Open an issue or a PR to discuss changes before implementing them.

## License

This project is under the [MIT License](./LICENSE)
