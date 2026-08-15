# OAK - Requirements

> Requirements for OAK - Orange AI Kit.

## 1. Purpose

OAK must provide a framework for creating, organizing, managing, connecting, and executing agentic systems.

OAK must enable the construction of reusable agentic patterns through the interaction of Agents, Skills, Assistants, Tools, and other resources.

OAK must not require users to create every component from scratch. It must be able to reuse and work with established conventions and patterns from the broader AI ecosystem.

## 2. Agentic Entities

OAK must support the following fundamental entities:

- Agents.
- Skills.
- Assistants.

Each entity must have clearly separated responsibilities.

### 2.1 Agents

OAK must support autonomous Agents capable of:

- Reasoning.
- Acting through their Harness.
- Interacting with other entities.
- Interacting with other Agents.
- Requesting work from Subagents.
- Selecting available entities to interact with.

An Agent must have:

- A Model.
- A Context.
- A Harness.

An Agent must not be permanently coupled to a specific Model or Provider.

Changing the Model or Provider must not change the identity of the Agent.

### 2.2 Skills

OAK must support Skills as specialized AI capabilities used by Agents.

A Skill must provide an Agent with the knowledge or capability required to perform a specific task.

A Skill must have:

- A Model.
- A Harness.

A Skill must not have its own Context.

A Skill may receive input from an Agent and must return a result.

Skills should be usable as ephemeral capabilities without requiring persistent independent state.

### 2.3 Assistants

OAK must support Assistants as AI entities intended for reasoning and answering without performing actions.

An Assistant must have:

- A Model.
- A Context.

An Assistant must not have a Harness.

An Assistant must not execute Tools or perform actions through a Harness.

An Agent must be able to provide information to an Assistant and receive its response.

## 3. Models and Providers

OAK must abstract Models from their concrete implementations.

OAK must support changing the Model used by an entity without requiring the entity itself to be recreated.

OAK must abstract communication with Models through Providers.

An Agent must not depend on the identity of a specific Provider.

The Core must remain independent of concrete Model and Provider implementations.

## 4. Harness

OAK must provide a Harness for entities that can perform actions.

A Harness must define the operational environment available to an entity.

A Harness must contain or manage:

- Tools.
- Guardrails.
- Available entities and interactions.

The Harness must determine what an entity can access or use.

An Agent must be able to interact with entities exposed through its Harness.

An Agent must be able to decide which available entity to interact with, provided that the interaction is permitted by its Harness and Guardrails.

## 5. Tools

OAK must support executable Tools as capabilities available through a Harness.

A Tool must always return a result to the entity that invoked it.

The result may contain:

- Useful information.
- A success status.
- A code.
- An error.
- Other execution information.

A Tool may perform an action without producing meaningful data, but it must still return a result.

## 6. Guardrails

OAK must support Guardrails as restrictions over the behavior and capabilities of entities.

Guardrails must be able to restrict:

- Actions.
- Tool usage.
- Resource access.
- Behavior.
- Other operational capabilities.

Guardrails must be separate from the capabilities provided by Tools.

Security restrictions must not depend exclusively on Agent reasoning.

## 7. Context

OAK must support Context as information available to an entity during its work.

Contexts must be independently associated with their respective entities.

A Subagent must maintain a separate Context from its superior Agent.

An entity receiving information from another entity must not automatically receive the sender's complete Context.

In Agent interactions, the receiving Agent must be able to use:

- Its own Context.
- Information explicitly provided by the other Agent.

The Harness and Guardrails may further restrict what information is available.

## 8. Sessions

OAK must support persistent Sessions for interactions initiated through Entry Points.

A Session must belong to the system or Entry Point being executed rather than to an individual Agent.

A Session may involve multiple Agents and other entities.

A Session must preserve the information required to continue an interaction, including:

- Conversation history.
- Relevant Context state.
- Agent interactions.
- Tool results.
- Skill results.
- Subagent results.
- Entry Point information.
- Execution information.

OAK must allow Sessions to be loaded and continued.

A Session must not be directly editable.

Modifying a Session directly must not be used as a mechanism for modifying Agents or their behavior.

Agent versioning is not required by the initial OAK requirements.

## 9. Entry Points

OAK must provide Entry Points as the standard way to initiate interaction with an agentic system.

Users must interact with a system through its Entry Point rather than directly selecting an Agent for execution.

An Entry Point must accept textual user input.

An Entry Point must provide a consistent interaction model regardless of the internal Pattern.

An Entry Point must provide:

- A final response.
- Information about the work performed by the system.

OAK must support inspecting execution information associated with an Entry Point.

## 10. Patterns

A Pattern must represent the organization of an agentic system within an OAK project.

A Pattern is not an independent executable domain entity.

An Agent must not execute a Pattern.

Agents must instead interact with other entities according to the organization established by the Pattern.

A Pattern must be able to contain and organize resources such as:

- Agents.
- Skills.
- Assistants.
- Tools.
- Guardrails.
- Models.
- Providers.
- Other Pattern resources.

OAK must provide a recommended structure for Patterns without requiring a rigid directory structure.

Patterns must be reusable.

A Pattern must be loadable before its resources can be executed.

OAK must support:

- Automatic Pattern discovery.
- Explicit Pattern loading.

A Pattern may incorporate another Pattern by importing it into the destination project.

Imported Pattern resources must become part of the destination project and must be freely modifiable.

## 11. Pattern Projects and Target Codebases

OAK must distinguish between:

- The project where a Pattern and its resources are created.
- The codebase where the agentic system operates.

A Pattern must be executable against a different target codebase from the project in which the Pattern was created.

The target codebase does not need to be an OAK Pattern project.

The Pattern must be loaded before it can operate against a target codebase.

OAK must therefore support agentic systems defined independently from the codebases on which they operate.

## 12. Agent Interactions

OAK must support multiple semantic forms of Agent interaction.

### 12.1 Chain

A Chain must allow one Agent to provide information directly to another Agent.

The receiving Agent must not be required to return a response to the sending Agent as part of the Chain interaction.

The receiving Agent must decide what information to use and what information to provide to a subsequent Agent.

A Chain must not automatically pass an Agent's complete result or Context to the next Agent.

### 12.2 Sub

A Sub interaction must allow an Agent to request work from another Agent acting as a Subagent.

The Subagent must:

- Be an Agent.
- Have a separate Context.
- Receive the information explicitly provided by its superior Agent.
- Perform its assigned work.
- Produce a summary of its result.
- Return that summary to its superior Agent.

A Subagent must not inherit the complete Context of its superior Agent.

A superior Agent must wait for a Subagent result when that result is required for its continued work.

A superior Agent must be able to continue working without waiting when the Subagent result is not required.

### 12.3 Super

A Super interaction must allow a Subagent to return information to its superior Agent through a callback.

A Super interaction must require an existing Sub relationship.

A Super interaction must not exist independently from a Sub interaction.

The information sent through the callback constitutes the response from the Subagent to its superior Agent.

## 13. Agent Interaction with Skills

An Agent must be able to invoke Skills available through its Harness.

A Skill must receive the information necessary to perform its task.

A Skill must not maintain a Context of its own.

A Skill must always return a result to the Agent that invoked it.

## 14. Agent Interaction with Assistants

An Agent must be able to provide information to an Assistant.

The Assistant must reason using its own Model and Context.

The Assistant must return a response to the Agent.

The Assistant must not perform actions through Tools.

## 15. Triggers

OAK must support Triggers associated with entities.

A Trigger must be a word or expression associated with an entity.

An entity must support:

- One primary Trigger.
- Multiple secondary Triggers.

Future versions may associate relevance or priority information with secondary Triggers.

Triggers must assist with entity discovery and identification.

Triggers must not independently determine which entity is executed.

The Agent receiving a request must remain responsible for deciding which available entity to interact with.

## 16. Entity Discovery

OAK must support dynamic discovery of resources.

Resources must not require registration in a single global configuration.

OAK must be able to discover structural information about resources, including:

- Identity.
- Location.
- Relationships.
- Available capabilities or operational information.
- Dependencies.

An Agent must be able to access entities exposed through its Harness.

The Harness must be able to expose entities directly and provide mechanisms for discovering or consulting additional entities available within its scope.

## 17. Interoperability

OAK must prioritize interoperability with existing AI ecosystems.

OAK must be able to use established conventions and patterns where they are compatible with OAK.

OAK must not require existing resources to be recreated from scratch.

OAK must not require knowledge of the system that originally created a compatible resource.

OAK may use common conventions such as `AGENTS.md` without requiring knowledge of whether the file originated from OpenCode, another AI system, or another ecosystem.

OAK must primarily organize and expose the structure of resources.

The entity using a resource is responsible for interpreting its semantic content.

OAK may interpret structural metadata required to organize resources without becoming responsible for interpreting their complete semantic content.

## 18. Plugins

OAK must support plugins as an extension mechanism.

Plugins must be able to provide integrations and extend OAK without requiring changes to the Core for every external ecosystem.

Plugins may provide:

- External system integrations.
- Support for external formats.
- Resource discovery mechanisms.
- Integration mechanisms.
- Kernel extensions exposed through defined abstractions.
- Additional OAK capabilities.
- Integration with external applications.

Plugins must not be required for creating Models, Providers, Tools, or Guardrails directly, as these resources must be manageable through OAK itself.

Plugins must be isolated from the Core.

Plugins must interact with OAK through explicit abstractions and exposed capabilities rather than direct access to internal Core implementation details.

OAK must prevent plugins from obtaining unrestricted access to the Core.

External systems must be able to integrate OAK through appropriate extension mechanisms.

OAK must expose a public interface that allows external systems to use OAK.

External integrations may provide mechanisms such as plugins that allow systems such as OpenCode to execute OAK.

OAK must not need to interpret or take ownership of resources belonging to the external system performing the integration.

## 19. Presentation

OAK must separate its core capabilities from presentation concerns.

OAK must not require its Core to depend on a specific presentation interface.

OAK must provide interfaces through which users can manage and use OAK.

The specific presentation technologies and their architectural organization are not defined by these requirements.

## 20. Observability

OAK must provide observability over agentic execution.

Users must be able to inspect, where supported:

- Active Agents.
- Agent-to-Agent interactions.
- Tool usage.
- Skill usage.
- Subagent creation and execution.
- Returned results.
- Errors.
- Execution time.
- Logs.
- Other relevant execution information.

Detailed execution logs may be introduced progressively.

Future versions must be able to provide detailed logs for Subagent execution.

## 21. Error Handling

OAK must support error handling throughout agentic execution.

Errors must be able to:

- Be propagated.
- Be handled by another Agent.
- Be stored in the Session.
- Allow execution to continue when appropriate.

Error handling behavior must be able to depend on:

- The type of error.
- The current agentic system.
- The Pattern.
- The context in which the error occurred.

OAK must not impose a single error recovery strategy for every agentic system.

## 22. Concurrency

OAK must not impose a single concurrency model on Patterns.

A Pattern must be able to define whether Agent interactions are:

- Sequential.
- Concurrent.

The initial requirements do not prescribe the implementation of concurrency.

## 23. Security

Security must be a fundamental requirement of OAK.

OAK must provide security mechanisms independently from Agent Guardrails.

Core security must protect, where applicable:

- The Kernel.
- Sessions.
- Resources.
- Plugins.
- External integrations.
- Access boundaries.

Guardrails must remain responsible for restricting the operational behavior and capabilities of AI entities.

Security must not rely exclusively on an Agent correctly following its instructions.

## 24. Abstraction and Technology Independence

OAK must remain independent from concrete implementations of its fundamental entities and capabilities.

The Core must communicate with implementations through defined abstractions.

OAK must not require the Core to depend directly on a specific:

- Model.
- Provider.
- Tool implementation.
- Guardrail implementation.
- External system.
- Technology.

Concrete implementations must be replaceable without changing the conceptual identity of the entities that use them.

## 25. Platform Support

OAK must be designed to operate across platforms.

The system must support, where technically applicable:

- Windows.
- Linux.
- macOS.
- WSL.
- Server environments.

Platform-specific implementations must not alter the fundamental conceptual model of OAK.

## 26. Resource Identity

OAK must allow multiple resources to have the same name when they originate from different locations or sources.

Resource names must not be required to be globally unique.

The identity of a resource must be distinguishable independently of its human-readable name.

## 27. Configuration

OAK must avoid requiring a monolithic global configuration for all resources.

Resources must be manageable independently.

Configuration should belong to the resource or mechanism that requires it rather than being forced into a single global configuration structure.

## 28. Future Compatibility

OAK must be designed so that future extensions can be introduced without invalidating the fundamental conceptual model.

Future capabilities may include:

- Additional resource formats.
- Additional integrations.
- More advanced logging.
- More advanced Trigger relevance.
- Additional Pattern mechanisms.
- Additional execution mechanisms.

YAML-based Pattern or action definitions are not required by the current OAK model and are reserved for future development.

## 29. Scope of These Requirements

These requirements define what OAK must provide and support.

They do not define:

- The internal architecture.
- The exact layer structure.
- The programming language.
- The implementation of the Kernel.
- The implementation of the TUI.
- The implementation of plugins.
- The exact resource file structure.
- The YAML format.
- The internal storage mechanism.
- The concrete Model or Provider implementations.

Those decisions belong to the architecture and implementation phases of OAK.
