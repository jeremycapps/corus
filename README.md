# Corus

Corus is a small protocol for coordinating objective state from expected path-states.

Libera defines valid workstream paths. Timpos records observed path changes. Corus evaluates whether objective requirements are satisfied by the current replayed state of a workstream.

## Core model

```text
Requirement = expected path-state.
Objective = relation over requirements.
Completion = optional singular requirement.
Objective State = derived coordination status.
```

## Objects

Corus v1 has two authored objects:

- **Requirement**: one expected value at one Libera path.
- **Objective**: a relation over requirements, scoped to a workstream.

Corus v1 derives:

- **Requirement State**: whether a requirement is satisfied by current replayed state.
- **Objective State**: waiting, ready for completion, or complete.

## Status

Corus v1 does not model `blocked`.

```text
waiting:
  one or more required requirements are unsatisfied

ready_for_completion:
  all required requirements are satisfied
  completion is defined
  completion is unsatisfied

complete:
  completion is defined and satisfied
  OR completion is not defined and all required requirements are satisfied
```

## Relation model

```text
Libera:
  Workstream relates paths.

Timpos:
  Moment references timpo.

Corus:
  Objective relates requirements.
```

## Repository layout

```text
protocol/
  objective.schema.yaml
  requirement.schema.yaml
  current_state.schema.yaml
  requirement_state.schema.yaml
  objective_state.schema.yaml

examples/
  design_systems_bug_intake/
    objectives.yaml
    requirements.yaml
    current_state.yaml
    requirement_state.yaml
    objective_state.yaml

docs/
  architecture.md
  glossary.md
  relation_model.md
  status_logic.md
```

## Keeper

```text
Corus does not contain workstreams.
Corus targets states inside workstreams.
```
