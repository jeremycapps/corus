# Architecture

Corus coordinates objective state from expected path-states.

## Boundary

Corus does not define workstream paths.

Workstream paths are defined outside Corus, commonly by Libera. Corus references those paths as addresses for expected state.

Corus does not record moments.

Observed state changes are recorded outside Corus, commonly by Timpos. Corus may consume the current replayed state of a workstream, but replay input is not a top-level Corus protocol object in v1.

Corus does not render role-specific meaning.

Role-specific meaning and surfaces belong above Corus.

## Authored objects

Corus v1 has two authored objects.

### Requirement

A requirement is one expected value at one path.

```yaml
requirement:
  id: requirement.task_done
  path: movement/task
  value: done
```

### Objective

An objective relates requirements inside a workstream.

```yaml
objective:
  id: objective.validated_fix
  workstream: design_systems_bug_intake
  requires:
    - requirement.request_reported
    - requirement.task_done
  completion: requirement.validation_present
```

`requires` is all-of.

`completion` is optional and singular.

If `completion` is omitted, all required requirements prove closure.

## Derived behavior

Requirement state and objective state are derived behavior, not authored protocol objects.

A requirement state is derived by comparing a requirement's expected path-state to the current replayed value at that path.

An objective state is derived by reducing requirement satisfaction across an objective's `requires` and optional `completion` relation.

```text
waiting
ready_for_completion
complete
```

Corus v1 does not model `blocked`.

## Relation model

```text
Libera:
  Workstream relates paths.

Timpos:
  Moment references timpo.

Corus:
  Objective relates requirements.
```
