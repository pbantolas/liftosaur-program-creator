# Custom Progress Scripts

## Purpose

Use `progress: custom(...) {~ ... ~}` to mutate future program values after workout completion.

## Script block

- Script body must be inside `{~` and `~}`.
- Reuse another script body with `{ ...ExerciseName }` (without tildes).

## State variables

- Declare state in `custom(name: value, ...)`.
- Access with `state.name`.
- State persists across workouts.
- User-prompted state uses `+` suffix in declaration (`flag+: 0`).

## Temporary variables

- Use `var.name` for temporary values inside a script.

## Control flow

- `if / else if / else`
- `for (var.i in someArray)` where index starts at 1

## Targeted writes

In `progress` context, writes can target dimensions with:

`[week:day:setVariation:set]`

Use `*` for wildcard; omitted leading dimensions default to wildcard.

## Typical pattern

```text
Bench Press 3x8 progress: custom(attempt: 0, increment: 5lb) {~
  if (completedReps >= reps) {
    state.attempt += 1
    if (state.attempt > 3) {
      weights += state.increment
      state.attempt = 0
    }
  }
~}
```

## Set/description variation control

- Change `setVariationIndex` to switch active set scheme.
- Change `descriptionIndex` to switch active description text.

## Authoring workflow

1. Start from required behavior in plain language.
2. Pick trigger condition (`completedReps`, `completedWeights`, etc.).
3. Define persistent state only if needed.
4. Perform minimal legal writes.
5. Validate index scope and units (`lb`, `kg`, `%`).
