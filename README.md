# Corus

A small protocol for coordinating objective state from expected path-states.

Corus evaluates whether objective requirements are satisfied by the current replayed state of a workstream.

Libera defines valid workstream paths. Timpos records observed path changes. Corus evaluates expected path-states.

## Path-state format

A Corus requirement has the form:

```text
{path} = {value}
```

Example:

```text
movement/task = done
```

The path uses Libera path syntax. Corus references paths but does not define them.

## Core model

Corus v1 has two authored objects:

```text
Requirement = expected path-state
Objective   = relation over requirements
```

Corus v1 derives:

```text
Requirement State = whether a requirement is satisfied
Objective State   = waiting, ready_for_completion, or complete
```

## Requirement

A Requirement defines one expected value at one Libera path.

```yaml
requirement:
  id: requirement.task_done
  path: movement/task
  value: done
```

## Objective

An Objective relates requirements inside a workstream.

```yaml
objective:
  id: objective.validated_fix
  workstream: design_systems_bug_intake

  requires:
    - requirement.request_reported
    - requirement.task_done
    - requirement.review_completed

  completion: requirement.validation_present
```

`requires` is all-of.

`completion` is optional and singular.

If `completion` is omitted, all required requirements prove closure.

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
  README.md
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

## Boundaries

Corus does not define workstream paths.

Corus does not record moments.

Corus does not render role-specific meaning.

## Keeper

```text
Requirement = expected path-state.
Objective = relation over requirements.
Completion = optional singular requirement.
Objective State = derived coordination status.
```
