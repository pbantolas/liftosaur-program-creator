# Built-in Functions Reference

## `rpeMultiplier(reps, rpe)`

Returns 1RM multiplier from reps and RPE.

Example:

`state.weight * rpeMultiplier(13, 9)`

## `floor(value)`

Rounds down to nearest integer.

## `ceil(value)`

Rounds up to nearest integer.

## `round(value)`

Rounds to nearest integer.

## `sum(arrayVar)`

Sums values in supported arrays (`completedReps`, `weights`, etc.).

## `min(arrayVar)`

Returns smallest value in supported arrays.

## `max(arrayVar)`

Returns largest value in supported arrays.

## `increment(weight)`

Returns next valid heavier weight based on equipment increment rules.

## `decrement(weight)`

Returns next valid lighter weight based on equipment increment rules.

## `sets(...)` (update context)

Signature:

`sets(fromIndex, toIndex, minReps, maxReps, isAmrap, weight, timer, rpe, shouldLogRpe)`

Notes:

- Used to create or modify set blocks in `update: custom()`.
- If `minReps != maxReps`, resulting set block is a rep range.
- `isAmrap` and `shouldLogRpe` are `0` or `1`.

Example:

`sets(2, 4, 6, 6, 0, 50lb, 0, 8, 0)`
