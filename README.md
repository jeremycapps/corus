# Corus

A small protocol for coordinating objective state from expected path-states.

Corus defines authored coordination objects. It does not store replay input or derived state as top-level protocol objects.

Libera defines valid workstream paths. Timpos records observed path changes. Corus defines the expected path-states an objective cares about.

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

## Derived state

Corus can derive requirement state and objective state by comparing requirements against current replayed workstream state.

Those derived states are documented as behavior, not modeled as top-level authored protocol objects.

```text
requirement_state:
  satisfied | waiting

objective_state:
  waiting | ready_for_completion | complete
```

Corus v1 does not model `blocked`. Use `waiting_on` in derived output language to describe unsatisfied requirements without implying failure or negative conditions.

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

examples/
  design_systems_bug_intake/
    objectives.yaml
    requirements.yaml

docs/
  architecture.md
  glossary.md
  relation_model.md
  status_logic.md
```

## Boundaries

Corus does not define workstream paths.

Corus does not record moments.

Corus does not store replay inputs as protocol fixtures.

Corus does not render role-specific meaning.

## Keeper

```text
Requirement = expected path-state.
Objective = relation over requirements.
Completion = optional singular requirement.
Derived state is behavior, not a top-level authored object.
```
