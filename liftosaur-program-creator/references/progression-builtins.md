# Built-in Progression

## Choose progression type

- Use `lp` for fixed load changes after success/failure counts.
- Use `dp` for rep-range progression then load bump.
- Use `sum` for total completed reps threshold behavior.
- Use `custom()` only when built-ins cannot express requirements.

## Linear progression (`lp`)

Signature:

`lp(weightIncrease, increaseAttempts, currentIncreaseAttempt, weightDecrease, decreaseAttempts, currentDecreaseAttempt)`

Typical examples:

- `lp(5lb)`
- `lp(5lb, 2)`
- `lp(5lb, 2, 1, 10lb, 3)`
- `lp(5%)`

## Double progression (`dp`)

Signature:

`dp(weightIncrease, minReps, maxReps)`

Examples:

- `dp(5lb, 8, 12)`
- `dp(5%, 6, 10)`

## Sum progression (`sum`)

Signature:

`sum(repsThreshold, weightIncrease)`

Example:

- `3x10+ progress: sum(30, 5lb)`

## Program-level consistency rule

For a single exercise identity, progression is program-wide. Do not define conflicting progression types across weeks/days for the same identity.

To use different progression logic for similar movements, split identity with labels (for example `lowrep:` and `highrep:`).

## Deload/disable case

Use `progress: none` to disable progression on specific weeks/days.

## Progression workflow

1. Pick identity (label if needed).
2. Prefer `lp`, `dp`, or `sum`.
3. Validate arguments and units.
4. Check consistency across the program.
5. Use `custom()` only when required behavior is not representable.
