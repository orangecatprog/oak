# OAK - Fundamental Concepts

> Fundamental concepts of OAK - Orange AI Kit.

## OAK

OAK is a kit for creating, managing, connecting, and executing agentic systems through Agents, Skills, Assistants, and other capabilities.

Its main objective is to enable the construction of reusable agentic Patterns through the interaction of different AI entities.

OAK is independent from concrete AI providers and models, allowing the same agentic system to work with different implementations.

## Model

A `Model` is the AI model used by an OAK entity to reason and generate responses.

An entity uses a Model to provide its reasoning and generation capabilities.

An Agent is not permanently coupled to a specific Model.

Changing the Model does not change the identity of the Agent.

## Provider

A `Provider` is an implementation that allows OAK to communicate with a Model.

A Provider represents the mechanism used to access a Model.

The Provider does not define the identity of an Agent.

An Agent can change its Provider without ceasing to be the same Agent.

## Context

A `Context` is the information available to an entity during its interaction or work.

It can include:

- Information provided to the entity.
- Conversation history.
- Information generated during execution.
- Other relevant information available to the entity.

Contexts belong to their respective entities.

An entity does not automatically inherit the complete Context of another entity.

A Subagent maintains a separate Context from its superior Agent.

## Harness

A `Harness` is the environment that allows an AI entity to act in a controlled way.

It provides and controls the operational capabilities available to an entity and participates in its execution cycle.

A Harness contains:

- Tools.
- Guardrails.
- Available entities and interactions.

The Harness defines the operational scope of an entity.

The Harness provides capabilities through Tools and restricts their use through Guardrails.

The Harness is responsible for controlling what an entity can access or use, while the specific restrictions are expressed through Guardrails.

## Guardrail

A `Guardrail` is a restriction that limits the behavior or capabilities of an entity.

Guardrails are part of the Harness.

A Guardrail can restrict:

- Actions an entity can perform.
- Tools an entity can use.
- Resources an entity can access.
- Behavior an entity can maintain.
- Other operational capabilities.

Guardrails are separate from the capabilities provided by Tools.

A Tool provides a capability; a Guardrail restricts how that capability can be used.

## Tool

A `Tool` is an executable capability that an entity can use to perform an action.

Tools are part of the Harness.

The Harness determines which Tools are available to an entity.

If an entity does not have a Tool available through its Harness, it does not possess that operational capability.

A Tool always produces a result for the entity that invokes it, even when the action itself does not produce meaningful data.

## Skill

A `Skill` is a specialized AI capability that provides an Agent with the knowledge or ability required to perform a specific task.

A Skill is not an Agent because it does not maintain its own Context.

A Skill has:

- Model.
- Harness.

A Skill receives the information required from the Agent using it.

The Skill uses that information to provide the Agent with a result.

A Skill is intended to provide a capability to an Agent rather than maintain an independent ongoing interaction.

Skills are therefore typically ephemeral: they are used when their capability is required and do not maintain persistent Context.

## Assistant

An `Assistant` is an AI entity oriented toward thinking, reasoning, and answering rather than performing actions.

An Assistant has:

- Model.
- Context.

An Assistant does not have a Harness.

Therefore, an Assistant can reason and answer, but it cannot perform actions through Tools.

An Agent can interact with an Assistant by providing information and receiving its response.

## Agent

An `Agent` is an autonomous AI entity capable of reasoning, acting, and interacting with other entities.

An Agent has:

- Model.
- Context.
- Harness.

An Agent is defined by its instructions, system prompt, and operational environment.

The Harness determines the capabilities and restrictions available to the Agent.

An Agent is not permanently coupled to a concrete Provider or Model.

An Agent can interact with:

- Other Agents.
- Subagents.
- Skills.
- Assistants.
- Tools.

An Agent decides which available entity to interact with within the boundaries established by its Harness and Guardrails.

## Subagent

A `Subagent` is an Agent subordinated to another Agent.

A Subagent:

- Is an Agent.
- Has its own Model.
- Has its own Context.
- Has its own Harness.
- Can have different capabilities from its superior Agent.
- Receives information explicitly provided by its superior Agent.
- Returns a result to its superior Agent.

A Subagent does not inherit the complete Context of its superior Agent.

The superior Agent may continue working while the Subagent works when its result is not required, but waits for the result when that result is necessary to continue.

The Subagent is responsible for producing the summary returned to its superior Agent.

## Trigger

A `Trigger` is a word or expression associated with an entity.

Triggers help identify or discover entities that may be relevant to a particular interaction.

An entity can have:

- One primary Trigger.
- Multiple secondary Triggers.

Triggers do not directly execute or route entities.

The Agent remains responsible for deciding which available entity to interact with.

Future versions may associate relevance or priority values with Triggers.

## Pattern

A `Pattern` is the organizational structure of an OAK project containing the resources that form an agentic system.

A Pattern is not an independent executable domain entity.

An Agent does not execute a Pattern.

Instead, Agents interact with other entities organized within the Pattern.

A Pattern can contain resources such as:

- Agents.
- Skills.
- Assistants.
- Tools.
- Guardrails.
- Models.
- Providers.

A Pattern provides the organization in which these resources are created, connected, and used.

Patterns can be reused by incorporating their resources into another Pattern.

When a Pattern is incorporated into another Pattern, its resources become part of the destination project.

## Entry Point

An `Entry Point` is the point through which an agentic system is initiated.

Users interact with an agentic system through its Entry Point rather than directly selecting an Agent.

The Entry Point establishes the beginning of an interaction and provides access to the agentic system defined by the loaded Pattern.

The Entry Point can initiate or continue a Session.

## Session

A `Session` represents the continuity of an interaction with an agentic system.

A Session can contain information such as:

- Conversation history.
- Context state.
- Agent interactions.
- Tool results.
- Skill results.
- Subagent results.
- Execution information.

A Session can involve multiple entities during its lifetime.

A Session can be loaded and continued.

Loading a Session does not mean modifying the Agents involved in it.

A Session is therefore a record of an interaction, not a mechanism for redefining the entities that participated in it.

## Agent Interaction

Agents can interact with other entities through different semantic relationships.

The primary Agent-to-Agent interaction forms are:

- Chain.
- Sub.
- Super.

These forms describe relationships between Agents rather than independent domain entities.

### Chain

A `Chain` interaction connects one Agent directly to another Agent.

```text
  _____         _____
 /     \       /     \
|   A   | --> |   B   |
 \_____/       \_____/
```

Agent A provides information to Agent B.

Agent B does not return a response to Agent A as part of the Chain interaction.

Agent B decides what to do with the received information and what information to provide to a subsequent Agent.

A Chain therefore does not automatically propagate complete results or Contexts between Agents.

### Sub

A `Sub` interaction occurs when an Agent requests work from another Agent acting as a Subagent.

```text
     _____
    /     \
   |   A   |
    \_____/
      /
     /
  __$__
 /     \
|   B   |
 \_____/
```

Agent A requests work from Agent B.

Agent B works using its own Context and Harness and returns a result to Agent A.

The Subagent does not inherit the complete Context of Agent A.

### Super

A `Super` interaction represents the return relationship from a Subagent to its superior Agent through a callback.

```text
     _____
    /     \
   |   A   |
    \_____/
       ^
       |
     __~__
    /     \
   |   B   |
    \_____/
```

The Super relationship requires an existing Sub relationship.

The Subagent sends information back to its superior Agent through the callback.

Super is therefore not an independent interaction type; it is the return side of a Sub interaction.

## Agentic Execution

`Agentic Execution` is the process in which OAK coordinates the interaction of Models, Contexts, Harnesses, and entities to perform work.

The Kernel provides the infrastructure required for this execution.

The Agent remains responsible for reasoning and deciding how to interact with the entities available through its Harness.

OAK provides the environment in which those interactions can occur without defining the reasoning itself.

## Resource

A `Resource` is an identifiable element that can participate in an OAK agentic system.

Resources can include:

- Agents.
- Skills.
- Assistants.
- Models.
- Providers.
- Tools.
- Guardrails.

A resource has an identity independent from its human-readable name.

Different resources may have the same name when they originate from different locations or contexts.

## Metadata

`Metadata` is structural information associated with a resource.

OAK can use metadata to organize and relate resources.

Metadata can describe:

- Identity.
- Location.
- Relationships.
- Available operational information.
- Dependencies.
- Other structural information.

Metadata describes the structure of a resource; it does not necessarily represent the semantic content of the resource itself.

## Interoperability

`Interoperability` is the ability of OAK to work with established conventions and systems from the broader AI ecosystem.

OAK can use common patterns and conventions without requiring knowledge of the system that originally created them.

For example, OAK can work with conventions such as `AGENTS.md`.

OAK is responsible for organizing and providing the structure required by the system.

The entity using a resource is responsible for interpreting its semantic content.

OAK therefore does not need to know which external system originally created a compatible resource.

## Plugin

A `Plugin` is an extension that allows additional functionality or integration to be provided to OAK.

Plugins can connect OAK with external systems or provide additional capabilities without making those systems part of the OAK Core.

An external application can use a Plugin to execute or integrate OAK.

Plugins extend OAK through defined interfaces and abstractions rather than becoming part of the conceptual identity of the Core itself.

## Core

The `Core` is the conceptual and operational center of OAK.

It provides the infrastructure required to create, connect, manage, and execute the entities that form an agentic system.

The Core is independent from presentation mechanisms such as a TUI or other user interfaces.

The Core does not define how users interact with OAK visually or through a specific interface.

## Separation of Responsibilities

OAK relies on clear separation of responsibilities between its concepts.

- `Model` provides reasoning and generation.
- `Provider` provides communication with a Model.
- `Context` provides information available to an entity.
- `Harness` defines the operational environment.
- `Tool` provides an executable capability.
- `Guardrail` restricts capabilities and behavior.
- `Skill` provides specialized knowledge or capability to an Agent without maintaining Context.
- `Assistant` reasons and answers without acting.
- `Agent` reasons, acts, and interacts.
- `Subagent` is an Agent subordinated to another Agent.
- `Trigger` helps identify an entity.
- `Pattern` organizes the resources of an agentic system.
- `Entry Point` initiates interaction with the system.
- `Session` preserves interaction continuity.
- `Plugin` extends or integrates OAK.
- `Core` provides the infrastructure in which these concepts operate.
