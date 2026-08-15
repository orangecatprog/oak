# OAK - Open Decisions

> Decisions that remain open and must be resolved before or during implementation.

## Purpose

This register tracks the decisions that are still open. Following the ADR convention, open decisions are not ADRs: ADRs record adopted, portable concepts, while these are OAK-specific choices deferred by [requirements.md](./requirements.md) (§29).

Each entry records the decision, its options, the criteria that will resolve it, and its status. When a decision is made, it is removed from this register and recorded where it belongs (an ADR if portable, or the appropriate design document otherwise).

## Decisions

### D1 · Session storage mechanism

- **Status**: Open — to be resolved in Block 4.
- **Options**: file-based storage, embedded database, other mechanism.
- **Resolution criteria**:
  - Sessions are records, not definitions; they must not be editable (§8, A6).
  - Must preserve the information required to continue an interaction (§8).
  - Must support loading and continuing Sessions (§8).
  - Storage is an External concern; the Core must not depend on the mechanism (§19, ADR 001).

## Related documents

- [exit-criteria.md](./exit-criteria.md) — the design phase requires open decisions to be resolved or explicitly deferred.
- [scope.md](./scope.md) — what is in and out of scope for the design phase.
- [adr/README.md](./adr/README.md) — the ADR convention these decisions follow.
