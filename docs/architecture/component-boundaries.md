# Component Boundaries

## Development Framework

Owns:

- shared philosophy;
- shared vocabulary;
- component map;
- cross-component responsibility boundaries;
- cross-component contracts and integration principles.

Does not own every component implementation.

## Control Plane

Owns:

- observation and aggregation of references/state;
- entity relationships;
- role-specific projections;
- human and machine control surfaces;
- decisions/intervention surfaces;
- projection freshness and provenance.

Does not own execution worker internals.

## Development Worker Gateway

Owns:

- accepting executable work;
- worker selection/routing;
- execution lifecycle;
- returning execution state and results.

Does not become the canonical project memory.

## Orchestrate

Owns project-oriented operational capabilities such as discovery, status, context, handoff, tasks, and workstation relationships.

Control Plane may project Orchestrate state/capabilities without duplicating its implementation.

## Deploy Kit

Owns standardized deployment execution and deployment-specific checks.

## Project Documentation Model

Owns the model for durable documentation structure, classification, migration, and reusable knowledge feedback.

## Mannered Code / Codes

Own implementation-convention description methodology and organizationally adopted implementation practice respectively.

## Boundary test

When deciding where a new feature belongs, ask:

1. Is it a framework-wide principle or contract? -> Development Framework.
2. Is it about observing, relating, projecting, or controlling state? -> Control Plane.
3. Is it about dispatching or executing work? -> Development Worker Gateway / worker.
4. Is it a project/repository operational capability? -> Orchestrate or the project repository.
5. Is it deployment execution? -> Deploy Kit.
6. Is it durable documentation modeling? -> PDM.
7. Is it implementation convention modeling/adoption? -> Mannered Code / Codes.
