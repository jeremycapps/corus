# Corus

A small protocol for coordinating objective state from expected domain-bound path-states.

Corus defines authored coordination objects. It does not store replay input or derived state as top-level protocol objects.

Libera defines valid address grammar. Domain binds those addresses to meaning. Timpos records observed path changes. Corus defines the expected path-states an objective cares about.

## Path-state format

A Corus requirement has the form:

```text
{path} = {value}
```

Example:

```text
movement/change/facia_surface_model.status = updated
```

The path uses Libera path syntax. The meaning of the path comes from a Domain binding. Corus references paths and bindings but does not define either.

## Core model

Corus v1 has two authored objects:

```text
Requirement = expected domain-bound path-state
Objective   = relation over requirements
```

## Requirement

A Requirement defines one expected value at one Libera path, optionally through a Domain binding.

```yaml
requirement:
  id: requirement.surface_model_updated
  binding: binding.facia_surface_model_change
  path: movement/change/facia_surface_model.status
  value: updated
```

## Objective

An Objective relates requirements inside a program.

```yaml
objective:
  id: objective.facia_v2
  program: protocol_design
  domain: domain.protocol_design

  requires:
    - requirement.surface_model_updated
    - requirement.routes_updated

  completion: requirement.examples_updated
```

`requires` is all-of.

`completion` is optional and singular.

If `completion` is omitted, all required requirements prove closure.

## Derived state

Corus can derive requirement state and objective state by comparing requirements against current replayed program state.

Those derived states are documented as behavior, not modeled as top-level authored protocol objects.

```text
requirement_state:
  satisfied | waiting

objective_state:
  waiting | ready_for_completion | complete
```

Corus v1 does not model `blocked`. Use `waiting_on` in derived output language to describe unsatisfied requirements without implying failure or negative conditions.

Complete state belongs to Corus. Facia only surfaces active state when coordination, implementation, or verification is still needed.

## Relation model

```text
Libera:
  Defines filesystem motion.

Domain:
  Binds Libera motion to domain meaning.

Timpos:
  Moment records observed state at an address.

Corus:
  Objective evaluates requirements into satisfied or unsatisfied state.

Facia:
  Routes active evaluated state into use.
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

Corus does not define Libera paths.

Corus does not define Domain meaning.

Corus does not record moments.

Corus does not store replay inputs as protocol fixtures.

Corus does not render role-specific meaning or active-use surfaces.

## Keeper

```text
Requirement = expected domain-bound path-state.
Objective = relation over requirements.
Completion = optional singular requirement.
Derived state is behavior, not a top-level authored object.
```
