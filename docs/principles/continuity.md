# Continuity and Substitutability

Development continuity is a framework-level requirement.

## Requirement

A project must not depend on the continued presence of one human, one AI conversation, one workstation, or one execution worker in order to remain understandable and continuable.

The target state is:

- a human can leave and later continue through a network-accessible environment;
- another authorized human can assume responsibility;
- an AI actor can receive a role-appropriate projection rather than private implicit context;
- a worker can be replaced without losing project state;
- interrupted and unfinished work remains visible.

## Implications

Projects and framework components should make the following durable and observable where relevant:

- objective;
- current state;
- decisions;
- constraints;
- blockers;
- unresolved questions;
- next actions;
- ownership/responsibility;
- evidence and provenance;
- relevant artifacts and relationships.

Handoff is therefore not only a document format. It is a property of the development system.

## Worker principle

Execution nodes should be treated as replaceable capacity. Durable state should remain in repositories or other explicitly designated canonical systems.

## Interface principle

Continuity must not depend on one interface. Humans may use a web interface; AI actors may use structured machine interfaces. Both should derive from compatible semantics.
