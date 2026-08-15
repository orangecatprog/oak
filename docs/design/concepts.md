# OAK - Concepts

> Fundamental concepts of OAK

## OAK (metadefinition)

OAK is a kit to create, manage, connect and execute agent systems by agents, skills, assistants and other capacities.

Its main objective is allow the construction of reusable agentic patterns by the interaction of different AI entities.

## Model

A `model` is the LLM used by an entity of OAK to provide razoning reasons and generation.

An agent is not linked permanently to a concrete model.

### Provider

A `provider` is the implementation that allows OAK to comunicate with a model.

The provider doesn't defines the identity of the agent.

## Context

The `context` is the available information for an entity during its interaction or work.

It can include information provided to the agent and the historial of the conversation (with human or other entity).

## Harness

The `harness` is the environment that allows an AI act of controlled form.

Provides and controls the operative capacities of an entity and participes in his execution cycle.

A harness contains tools and guardrails.

The harness enables the available capacities, while the guardrails sets its restrictions.

The tools and the restrictions (guardrails) of access to resouces are part of the operative ambit controller by the harness, mantaining the specific responsability of the restrictions in the guardrails.

### Guardrail

A `guardrail` is a restriction that limits the behavior or the capacities of an entity.

The guardrails takes part of the harness and can limit:

- The actions that an entity can do
- The tools that can use

- The behavour that can mantain

The guardrails are a separated responsability to the capacities proportioned by the tools.

### Tool

A `tool` is a executable capacity that an entity can use to do an action.

The tools takes part of the harness.

The harness sets what tools are available for the entity.

An entity that hasn't any tool hasn't that capacity no matters other restrictions setted by its guardrails

## Skill

A `skill` is an specialized AI that provides a concrete capacitity, but it isn't an agent, because it hasn't context.

A skill has:

- Model
- Harness

The skills aren't persistent: They are used to a concrete capacity and after, they dissapear.

## Assistant

An `assistant` is an AI oriented to think, iterate, and answer, but not to perform actions over the codebase.

An assistant has:

- Model
- Context

An assistant hasn't harness.

So an assistant can razonate and answer, but no act by tools.

## Agent

An `Agent` is a autonom entity that can razonate, act and interact with other entities.

An agent is defined by:

- Its instructions
- Its system prompt
- Its harness

An agent uses a `Model`, but it doesn't depends of a concrete provider. The model and the provider can change without the agent ceasing to be the same agent.

An agent can interact with other agents, skills, assistants and tools.

### Subagent

A `subagent` is an agent subordinated to other agent.

A subagent:

- Is an agent.
- Can have different capacities than the agent that solicites it.
- Mantains a separated context.
- Returns the result by a abstract.

A subagent don't heredate the complete context of the super agent (the agent that solicites the subagent).

## Agent Interaction

The agents can interact by different way.

### Chain

An `Chain` interaction connects directly two agents.

```plaintext
  _____         _____
 /     \       /     \
|   A   | --> |   B   |
 \_____/       \_____/

```

The first agent provides information to the next agent, but the next agent doesn't return information to the first agent.

### Sub

A `Sub` interaction allows an agent solicites work to other agent like subagent.

```plaintext
     _____
    /     \
   |   A   |
    \_____/
      / 
     /
  __$__
 / sub \
|   B   |
 \_____/

```

### Super

A `super` interaction allows a subagent returns information to the super agent by a callback.

```plaintext
     _____
    /super\
   |   A   |
    \_____/
       $ 
       |
     __~__
    / sub \
   |   B   |
    \_____/
```

This interaction ways doesn't convert a chain, sub or super to independent entity of the domain
