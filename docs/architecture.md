# Architecture

Corus evaluates coordination state from expected path-states.

## Boundary

Corus does not define workstream paths.

Workstream paths are defined outside Corus, commonly by Libera. Corus references those paths as addresses for expected state.

Corus does not record moments.

Observed state changes are recorded outside Corus, commonly by Timpos. Corus consumes the current replayed state of a workstream.

Corus does not render role-specific meaning.

Role-specific meaning and surfaces belong above Corus.

## Authored objects

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

## Derived objects

### Requirement State

A requirement state is derived by comparing a requirement's expected path-state to the current replayed value at that path.

### Objective State

An objective state is derived by reducing requirement states.

```text
waiting
ready_for_completion
complete
```

Corus v1 does not model `blocked`.
