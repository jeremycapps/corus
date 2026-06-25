# Relation Model

Corus v1 uses relation modeling instead of container modeling.

## Core relation

```text
Objective relates requirements.
Requirement defines expected state.
```

The requirement does not know whether it is required for progress or proves completion.

The objective owns that relation.

```yaml
objective:
  id: objective.validated_fix
  workstream: design_systems_bug_intake
  requires:
    - requirement.request_reported
    - requirement.task_done
  completion: requirement.validation_present
```

```yaml
requirement:
  id: requirement.validation_present
  path: exception/validation
  value: validated
```

## Layer comparison

```text
Libera:
  Workstream relates paths.
  Path defines valid state address.

Timpos:
  Moment references timpo.
  Timpo locates the recorded change.

Corus:
  Objective relates requirements.
  Requirement defines expected state.
```

## Why relation modeling

Corus does not make workstream a parent container for objectives.

Instead:

```text
An objective is scoped to a workstream.
```

Corus does not make requirement definitions children of objectives.

Instead:

```text
An objective relates requirement ids.
```

This keeps requirements reusable and keeps objective logic where it belongs.

## Keeper

```text
Requirement = path-state expectation.
Objective = relation over requirements.
Completion = requirement id held by the objective.
```
