# Protocol

Corus v1 defines authored coordination objects.

## Authored schemas

- `requirement.schema.yaml`: one expected value at one Libera path.
- `objective.schema.yaml`: relation over requirements scoped to a workstream.

## Derived behavior

Corus can derive requirement state and objective state from current replayed workstream state, but those are behavior descriptions, not top-level authored protocol objects in v1.

## Boundary

Corus references Libera paths but does not define them.

Corus consumes replayed Timpos state but does not record moments or store replay fixtures.
