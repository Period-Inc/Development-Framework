# Control Plane in the Framework

Control Plane is a first-class Development Framework component.

Its central abstraction is not a dashboard but a projection plane.

The same underlying development reality can be projected differently according to responsibility:

- Human -> cards, boards, timelines, decisions, alerts;
- Planner -> objectives, constraints, context, dependencies;
- Executor -> executable work and acceptance criteria;
- Evaluator -> outputs, evidence, tests, expected outcomes;
- Reviewer -> intent, findings, disagreements, exceptions, provenance;
- Automation -> structured state and events.

Interfaces are replaceable. A Planner projection might currently be JSON/YAML/CLI and later be delivered through another protocol without redefining the Planner role.

Detailed Control Plane specifications belong in the Control Plane repository:

https://github.com/Period-Inc/Control-Plane
