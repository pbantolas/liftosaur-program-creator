# Update Scripts

## Purpose

Use `update: custom() {~ ... ~}` to mutate the currently running workout.

## Execution timing

- Runs once before any set completion (`setIndex == 0`).
- Runs again each time a set is tapped/completed.

## Critical constraints

- Cannot mutate program-wide state variables.
- Cannot target other weeks/days/set variations.
- Only current workout set-level writes are allowed.
- Already completed sets cannot be modified.

## Writable targets in update context

- `weights[set]` or `weights`
- `reps[set]` or `reps`
- `RPE[set]` or `RPE`
- `timers[set]` or `timers`
- `numberOfSets`
- `amraps[set]`, `logrpes[set]`, `askweights[set]`

## Dynamic set editing with `sets()`

Use:

`sets(fromIndex, toIndex, minReps, maxReps, isAmrap, weight, timer, rpe, shouldLogRpe)`

## Typical guard pattern

Always gate update logic by `setIndex` to avoid accidental repeated rewrites.

```text
Bench Press / 3x8 / update: custom() {~
  if (setIndex == 1 && completedReps[1] >= reps[1]) {
    numberOfSets = 4
    sets(2, 4, floor(reps[1] / 2), floor(reps[1] / 2), 0, weights[1], 0, 0, 0)
  }
~}
```

## Reusing update logic

Reuse another update script with `{ ...ExerciseName }`.

## Update workflow

1. Define the trigger set (`setIndex`).
2. Read completed values from finished sets.
3. Apply allowed writes only.
4. Use `sets()` for batch set creation/edit.
5. Re-check behavior at `setIndex == 0` and at trigger index.
