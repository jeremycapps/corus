# Status Logic

Corus v1 derives objective state from requirement satisfaction.

## Requirement state

A requirement is satisfied when the current replayed value at its path equals its expected value.

```text
satisfied:
  current[path] == requirement.value

waiting:
  current[path] != requirement.value
```

## Objective status

Allowed v1 statuses:

```text
waiting
ready_for_completion
complete
```

## Rules

### waiting

```text
one or more requirements listed in `requires` are waiting
```

### ready_for_completion

```text
all requirements listed in `requires` are satisfied
completion is defined
completion is waiting
```

### complete

```text
completion is defined and satisfied
OR
completion is not defined and all requirements listed in `requires` are satisfied
```

## No blocked

Corus v1 does not model `blocked`.

Use `waiting_on` to represent sequence without implying failure, contradiction, or negative conditions.

```yaml
objective_state:
  status: waiting
  requires:
    waiting_on:
      - requirement.task_done
```

## Completion

`completion` is optional and singular.

Multiple completion requirements are intentionally not supported in v1. If multiple states are necessary before closure, model them under `requires` and use one optional completion requirement as the final proof.
