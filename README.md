# Development Framework

Development Framework is the umbrella architecture for making software development observable, continuable, transferable, and executable across humans, AI actors, machines, and development systems.

It defines shared principles, responsibilities, boundaries, and contracts. Individual components remain independently implementable and independently replaceable.

## Grand principle

Development should be able to continue when the original person, workstation, AI session, or worker is unavailable.

If the development environment can be reached through the network, another suitable human or actor should be able to understand the current state, assume the necessary responsibility, and continue the work without reconstructing undocumented context.

This requires:

- explicit state and provenance;
- clear responsibility boundaries;
- durable project-owned knowledge;
- replaceable workers and interfaces;
- observable decisions, blockers, and next actions;
- handoff as a normal system capability rather than an exceptional document.

## Component model

### Control Plane

Projects development state and responsibilities into forms appropriate to each actor.

The term has two intentional meanings:

1. a control plane that observes, relates, routes, and controls activity whose execution may happen elsewhere;
2. a common plane on which different responsibilities are projected in role-appropriate forms.

The Control Plane is not synonymous with a web dashboard. A human projection may be Web/Card/Dashboard, while an AI or automated actor may consume CLI, JSON, YAML, API, MCP-style interfaces, or events.

Repository: https://github.com/Period-Inc/Control-Plane

### Development Worker Gateway

Receives executable work, routes it to suitable workers, controls execution, and returns state/results.

Workers are execution capacity, not the canonical owner of project state. They should be replaceable.

### Orchestrate

Provides project-level discovery, status, context, handoff, task, and workstation operations across multiple projects.

### Deploy Kit

Provides standardized deployment execution and deployment-related validation.

### Project Documentation Model

Defines how durable project knowledge is structured, classified, migrated, and fed back into reusable documentation models.

### Mannered Code / Codes

Mannered Code defines how implementation conventions can be described and made reusable. Codes represents selectively adopted organizational implementation practice.

## Shared concepts

### Actor

A concrete human, AI, service, or worker performing activity.

### Role

A responsibility being fulfilled. Initial development roles include Planner, Executor, Evaluator, Reviewer, and Human decision responsibilities.

An Actor and a Role are not the same thing: one actor may perform multiple roles, and one role may be fulfilled by different actors.

### Projection

A role-appropriate semantic view of shared development state.

### Interface

The mechanism through which a projection is exposed: Web, CLI, JSON, YAML, API, MCP, event, or another replaceable mechanism.

Role, Projection, and Interface should remain separable.

## Source-of-truth principle

The Framework should not centralize state merely for convenience.

Code and repository-owned documentation belong to repositories. Provider-native conversations belong to their provider where applicable. Deployment results belong to the deployment system. Other components may project and relate those sources without silently becoming competing canonical stores.

Where normalized state is required, provenance and freshness should remain visible.

## Responsibility flow

A typical flow may be:

Human / Planner
-> Control Plane projection
-> Work definition
-> Development Worker Gateway
-> Executor
-> result/evidence
-> Evaluator
-> Reviewer / Human decision
-> updated project state and projections

This is a responsibility flow, not a requirement that every implementation use the same protocol or process.

## Repository strategy

Development Framework is the definition and integration layer.

Component repositories own their component-specific implementation and detailed specifications. Cross-component principles and contracts belong here; component-specific behavior belongs in the relevant component repository.

## Current components

- Control Plane — https://github.com/Period-Inc/Control-Plane
- Development Worker Gateway
- Orchestrate
- Deploy Kit
- Project Documentation Model
- Mannered Code / Codes

The component list is intentionally extensible.
