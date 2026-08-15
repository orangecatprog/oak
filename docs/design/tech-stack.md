# OAK - Tech Stack

> The concrete technologies adopted by OAK, and the criteria that resolved them.

## Purpose

This document records the resolved technology decisions of OAK. Following the ADR convention, these decisions are OAK-specific — they apply to this project but are not portable concepts — so they are recorded here instead of in [adr/](./adr/README.md). When a decision recorded here is made, it is removed from [open-decisions.md](./open-decisions.md).

## Decisions

### D1 · Programming language — Go

- **Status**: Decided.
- **Date**: 2026-08-15.
- **Options considered**: Rust, Go, TypeScript/Node, Python.
- **Resolution criteria**: the criteria defined for D1 in [open-decisions.md](./open-decisions.md).

**Decision:** OAK is implemented in Go.

Go resolves the D1 criteria as follows:

- **Cross-platform distribution as a single artifact (§25)** — Go produces static binaries with trivial cross-compilation (`GOOS`/`GOARCH`), covering Windows, Linux, macOS, WSL, and server environments from a single codebase.
- **Mature TUI ecosystem for the presentation layer** — the Go TUI ecosystem is the reference for interactive terminal applications, with Charm (Bubble Tea, Lip Gloss, Bubbles) actively maintained and cross-platform.
- **Core/External boundary and plugin isolation (P7, §18)** — Go's static typing enforces the contract surface (ADR 003). OAK does not rely on in-process dynamic plugin loading; plugins are isolated as separate processes or WebAssembly modules (Wazero), which reinforces P7 rather than relying on cooperation.
- **Fit with the agent/LLM ecosystem (§17)** — OAK communicates with Providers through abstractions over HTTP and URL (§3, README), so the Core does not depend on language-native AI SDKs. The relative immaturity of Go LLM SDKs is mitigated by the Provider contract, not by the language.
- **Team familiarity and long-term maintainability** — Go's simplicity, static typing, and built-in concurrency primitives (goroutines) fit the orchestration of concurrent Agent interactions (§22).

### D2 · TUI framework — Charm (Bubble Tea)

- **Status**: Decided.
- **Date**: 2026-08-15.
- **Options considered**: depends on D1.
- **Resolution criteria**: the criteria defined for D2 in [open-decisions.md](./open-decisions.md).

**Decision:** the presentation layer uses Charm — **Bubble Tea** (reactive UI), **Lip Gloss** (styling), and **Bubbles** (components).

The TUI is an External adapter (ADR 001, §19): it depends on the Core only through its ports, never the other way around. Bubble Tea supports the views required to manage the agent schema (agents, interactions, sessions) while remaining independent of the Core.

## Considerations and mitigations

- **LLM SDK ecosystem gap** — language-native AI SDKs are less mature in Go than in TypeScript/Python. Mitigated by the Provider contract (§3, §24): OAK communicates with Models and Providers through abstractions over HTTP and URL, keeping the Core independent of concrete SDKs (A5).
- **No in-process dynamic plugin loading** — Go's `plugin` mechanism is platform-restricted and unreliable. Mitigated by design: plugins are isolated as separate processes or WebAssembly modules, which enforces the plugin isolation required by P7 and §18.
- **Deferred decisions** — the session storage mechanism (D3) remains open and is tracked in [open-decisions.md](./open-decisions.md).

## Traceability

- **Axioms**: A3, A5, A7.
- **Principles**: P1, P6, P7.
- **Requirements**: §3, §17, §18, §19, §22, §24, §25.
- **ADRs**: 001 (Core / External), 003 (Contract and Implementation).

## Relation to other documents

- [open-decisions.md](./open-decisions.md) — the register from which these decisions were removed once resolved.
- [adr/README.md](./adr/README.md) — the convention this document follows: OAK-specific decisions are not ADRs.
- [requirements.md](./requirements.md) — §29 leaves the language out of the requirements scope; §25 defines the platform constraint these decisions satisfy.
- [exit-criteria.md](./exit-criteria.md) — criterion 7 requires open decisions to be recorded as decided or explicitly deferred.
