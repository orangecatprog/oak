# OAK - Consistency Audit

> Audit of [concepts.md](./concepts.md) and [requirements.md](./requirements.md) against the axioms of [axioms.md](./axioms.md).

## Purpose

Verify that every concept and every requirement is grounded in at least one axiom (C6 · Completeness), and that no statement contradicts the axiom set (C5 · Consistency). Record and resolve any inconsistencies found.

## Method

For each requirements section §1–§29, identify the axioms that ground it. For each concept of [concepts.md](./concepts.md), identify the axioms that ground it. Review the resulting coverage and the consistency of every pair.

## Requirements traceability (§1–§29)

| Requirements section | Grounding axioms |
| --- | --- |
| §1 Purpose | A5, A6 |
| §2 Agentic Entities | A2, A4 |
| §2.1 Agents | A1, A2, A3 |
| §2.2 Skills | A2, A4 |
| §2.3 Assistants | A2, A4 |
| §3 Models and Providers | A3, A5 |
| §4 Harness | A2 |
| §5 Tools | A2 |
| §6 Guardrails | A2 |
| §7 Context | A4 |
| §8 Sessions | A6, A7 |
| §9 Entry Points | A6 |
| §10 Patterns | A6 |
| §11 Pattern Projects and Target Codebases | A5, A6 |
| §12 Agent Interactions | A4 |
| §12.1 Chain | A4 |
| §12.2 Sub | A4 |
| §12.3 Super | A4 |
| §13 Agent Interaction with Skills | A4 |
| §14 Agent Interaction with Assistants | A4 |
| §15 Triggers | A1 |
| §16 Entity Discovery | A2, A6 |
| §17 Interoperability | A5 |
| §18 Plugins | A2, A5 |
| §19 Presentation | A5 |
| §20 Observability | A7 |
| §21 Error Handling | A7 |
| §22 Concurrency | A2, A5 |
| §23 Security | A2 |
| §24 Abstraction and Technology Independence | A5 |
| §25 Platform Support | A5 |
| §26 Resource Identity | A3 |
| §27 Configuration | A5, A6 |
| §28 Future Compatibility | A5, A6 |
| §29 Scope of These Requirements | A5 |

## Concepts grounding

| Concept | Grounding axioms |
| --- | --- |
| OAK | A5, A6 |
| Model | A3, A5 |
| Provider | A3, A5 |
| Context | A4 |
| Harness | A2 |
| Guardrail | A2 |
| Tool | A2 |
| Skill | A2, A4 |
| Assistant | A1, A2, A4 |
| Agent | A1, A2, A3, A4 |
| Subagent | A1, A4 |
| Trigger | A1 |
| Pattern | A6 |
| Entry Point | A6 |
| Session | A6, A7 |
| Agent Interaction | A4 |
| Chain | A4 |
| Sub | A4 |
| Super | A4 |
| Agentic Execution | A1, A7 |
| Resource | A3 |
| Metadata | A3, A6 |
| Interoperability | A5 |
| Plugin | A2, A5 |
| Core | A5 |
| Separation of Responsibilities | A1, A2, A4 |

## Notes and resolutions

1. **"Complete Context" phrasing** — §7, §12.1 (Chain), and the Context concept use "does not automatically inherit the complete Context". Read literally, this could suggest implicit partial inheritance. A4 forbids implicit inheritance of any kind: information flows only when explicitly provided. Resolution: the axioms prevail; a receiving entity receives only what is explicitly provided. Recommendation: rephrase the requirements to "does not automatically inherit Context" to remove the ambiguity.

2. **§6 weaker than A2** — "Security restrictions must not depend exclusively on Agent reasoning" is weaker than A2 ("independently of the entity's reasoning"). Resolution: A2 prevails; security enforcement never depends on the Agent's reasoning. Recommendation: rephrase §6 to "must not depend on Agent reasoning".

3. **§22 concurrency** — no axiom mandates a default concurrency model. A Pattern defining whether interactions are sequential or concurrent is consistent with A2 (the system defines operational behavior) and A5 (no imposed implementation). No change required; recorded for traceability.

4. **§8 sessions non-editable** — "must not be directly editable" is a consequence of A6 and does not contradict A7: the system can account for what occurred without allowing redefinition. No change required.

## Conclusion

All requirements sections and all concepts are grounded in at least one axiom. No contradiction requires changing the axiom set. Two phrasings in [requirements.md](./requirements.md) are weaker than their grounding axioms; the resolutions and recommendations are recorded above.
