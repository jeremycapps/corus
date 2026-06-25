# Glossary

## Requirement

An expected path-state.

```text
Requirement = path + value
```

Example:

```yaml
id: requirement.task_done
path: movement/task
value: done
```

## Objective

A relation over requirements scoped to a workstream.

An objective defines which requirements are necessary and, optionally, which singular requirement proves completion.

## Workstream

The state-space referenced by an objective.

Corus does not contain or define the workstream. It targets states inside the workstream.

## Current State

The current replayed values for paths inside a workstream.

Corus expects current state as input and derives requirement/objective state from it.

## Requirement State

The derived satisfaction status of a requirement.

Allowed v1 statuses:

```text
satisfied
waiting
```

## Objective State

The derived coordination status of an objective.

Allowed v1 statuses:

```text
waiting
ready_for_completion
complete
```

## Completion

An optional singular requirement id held by an objective.

If completion is defined, it proves closure when satisfied.

If completion is omitted, all required requirements prove closure.

## Waiting

A non-judgmental state meaning one or more expected path-states are not yet satisfied.

Corus v1 uses `waiting`, not `blocked`.
