# ADRs - Architecture Decision Records

> Records of the portable concepts and patterns adopted by OAK.

## Purpose

The ADRs in this directory record the architectural decisions that adopt known, portable concepts. Their purpose is to capture a decision so that the concept can be understood, applied in this project, and transferred to other projects.

## Convention

An ADR in this project is defined as:

> A record of adopting a known, portable concept or pattern, so that it can be used here and applied to another project as-is.

Therefore:

- **A concept is an ADR when it is portable** — clean architecture, screaming architecture, design patterns, test-driven development.
- **OAK-specific architecture is not an ADR** — the identity of OAK (its entities, its interaction forms, its sessions) is documented in [concepts.md](../concepts.md) and the [requirements.md](../requirements.md), not in ADRs.
- **Open decisions are not ADRs** — they are tracked in [open-decisions.md](../open-decisions.md) until resolved.

## Template

Each ADR follows the Nygard format with a traceability section:

- **Title** — `ADR NNN · Name` (file: `nnn_name.md`).
- **Status** — Accepted, Proposed, or Deprecated / Superseded.
- **Date** — the date the decision was recorded.
- **Context** — the situation that requires the decision.
- **Why (optional)** — the reasoning that justifies the decision.
- **Decision** — the adopted concept or pattern and how it is applied.
- **What this improves** — the consequences in favor of the decision.
- **Consequences** — positive and negative consequences.
- **Traceability** — the axioms, principles, requirements, and related ADRs that ground the decision.

## Numbering

- Files are named `nnn_name.md`, with a zero-padded sequential number and a snake-case name.
- Numbers are never reused; a superseded ADR keeps its number and references its replacement.
- The index below is updated when a new ADR is recorded.

## Statuses

- **Proposed** — under consideration.
- **Accepted** — adopted and in force.
- **Deprecated** — replaced; the record is kept for history and references its replacement.

## Index

| ADR | Title | Status |
| --- | --- | --- |
| [001](./001_clean-architecture.md) | Clean Architecture: Core / External Model | Accepted |
| [002](./002_screaming_architecture.md) | Screaming Architecture | Accepted |
| [003](./003_contract-implementation.md) | Contract and Implementation | Accepted |
| [004](./004_design_patterns.md) | Design Patterns | Accepted |
| [005](./005_test-driven-development.md) | Test-Driven Development | Accepted |
