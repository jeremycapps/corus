# Protocol

Corus v1 defines expected path-states and derives objective state from current replayed workstream state.

## Authored schemas

- `requirement.schema.yaml`: expected value at a Libera path.
- `objective.schema.yaml`: relation over requirements scoped to a workstream.

## Input schema

- `current_state.schema.yaml`: current replayed path values for a workstream.

## Derived schemas

- `requirement_state.schema.yaml`: satisfaction state of one requirement.
- `objective_state.schema.yaml`: reduced coordination status for an objective.

## Boundary

Corus references Libera paths but does not define them.

Corus consumes replayed Timpos state but does not record moments.
