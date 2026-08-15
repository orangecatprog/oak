# ADR 002 · Screaming Architecture: Prioritizing Domain over Technical Concepts

- **Status**: Accepted
- **Date**: 2026-08-15

## Context

The architecture of OAK must reveal what OAK is: a kit for creating, managing, connecting, and executing agentic systems. If the structure is organized around technical concepts (controllers, services, repositories, framework names), reading the architecture says nothing about the domain it serves.

OAK is defined by its domain model — Agents, Subagents, Skills, Assistants, Harnesses, Contexts, Tools, Guardrails, Patterns, Sessions — and by the interactions between them ([concepts.md](../concepts.md)). The identity of the system is domain, not technology (A5, P3).

The architecture must therefore prioritize the business logic and the domain over technical concepts: the domain is the reason the system exists, and the structure should say so first.

## Why screaming architecture

Screaming architecture is the practice of organizing the architecture around the domain and use cases it serves, so that the structure itself "screams" the purpose of the system. A healthcare system should read like a healthcare system; an agentic kit should read like an agentic kit.

This fits OAK because:

- **It makes the domain the organizing principle.** OAK's identity is its domain model and its agentic interactions. Structuring by domain makes the architecture communicate that identity directly.
- **It reinforces technological independence (A5).** If the Core is organized around domain concepts, no framework or technology can reshape it. Technology lives in External, subordinate to the domain.
- **It aligns structure with Separation of Responsibilities (P2).** Responsibilities are defined by what each entity is and does, not by the technical layer it happens to occupy.
- **It keeps the Core presentation-free and implementation-free (§19, §24).** The presence of a TUI, concrete providers, or a storage mechanism is invisible in the Core's structure because those are technical concerns of External.
- **It gives the repository a stable vocabulary.** Domain terms change slowly; technical terms change with every framework upgrade.

## Decision

The Core is organized by the domain, not by technical archetypes.

### Structure expresses the domain

The Core structure is derived from the domain model of [concepts.md](../concepts.md):

- **Entities** are named and organized by their domain identity: Agent, Subagent, Skill, Assistant.
- **Contracts** are organized by what they abstract: Model, Provider, Context, Harness, Tool, Guardrail.
- **Capabilities** are organized by what they do for the agentic system: orchestration, interactions (Chain, Sub, Super), Sessions, Entry Points.
- **Interactions** are first-class domain concepts, not scattered across technical layers.

### Technical concerns are subordinate

Technical concerns never drive the Core structure:

- No Core organization by controller, service, repository, or framework archetype.
- No Core naming derived from a technology, framework, or vendor.
- Persistence, concrete providers, and UI details are External concerns; their presence is invisible in the Core.

### The vocabulary is the domain vocabulary

- Names in the Core come from [concepts.md](../concepts.md).
- When a technical name is unavoidable, it is a port or an adapter in External, clearly subordinate to the domain it serves.

## What this improves

- **Discoverability** — reading the structure reveals what OAK does: agents, interactions, harnesses, sessions — not what it is built with.
- **Stability** — domain vocabulary is stable; framework names are not. A structure that depends on the first survives the second.
- **Lock-in resistance** — the Core cannot be dominated by a technology it does not mention (A5).
- **Responsibility clarity** — entities keep the responsibilities the axioms assign them (P2), unclouded by technical archetypes.
- **Coherent evolution** — new capabilities enter the structure as domain concepts first, technical implementation later.
- **Test framing** — tests read as domain scenarios ("an Agent delegates to a Subagent and receives its summary"), not as technical plumbing.

## Consequences

### Positive

- The architecture communicates intent at a glance.
- Technology changes do not reshape the Core.
- A single, shared vocabulary across all design documents (concepts, axioms, ADRs).

### Negative

- Requires naming discipline: resisting conventional technical archetypes in every contribution.
- Requires a shared and maintained domain vocabulary, with [concepts.md](../concepts.md) as its source of truth.
- Technical concerns still need names and a home; they must remain subordinate in External without leaking into Core naming.

## Traceability

- **Axioms**: A1, A3, A5.
- **Principles**: P2, P3.
- **Requirements**: §19, §24, §29.
