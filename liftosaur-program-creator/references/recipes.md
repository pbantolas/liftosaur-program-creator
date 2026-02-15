# Recipes

## Recipe: author a simple exercise

Goal: one clean exercise line with clear set, load, and timer intent.

1. Start with `Exercise / 3x8`.
2. Add intensity (`@8`) or explicit load (`75%` or `60kg`).
3. Add timer if needed (`90s`).
4. Add progression (`lp`, `dp`, or `sum`).

Example:

`Bench Press / 3x8@8 90s / progress: dp(2.5kg, 8, 12)`

## Recipe: convert repetitive program to reusable templates

1. Create template lines with `used: none`.
2. Reuse templates with `...TemplateName`.
3. Add week repeats `[from-to]` to remove duplication.
4. Add small per-exercise overrides only when required.

Example pattern:

- `t1 / 1x6, 3x3 80% / used: none`
- `Squat[1-4] / ...t1`
- `Bench Press[1-4] / ...t1`

## Recipe: compact set variations with shared TM % and timer

1. List each set variation as its own slash block.
2. Add one shared percent and timer block after variations.
3. Add progression section normally.

Example:

`OHP_T2: Overhead Press / 4x12 / 4x10 / 4x8 / 60% 120s / progress: dp(2.5kg, 8, 12)`

This applies `60% 120s` to all listed set variations and keeps long workouts compact.

## Recipe: add a stateful custom progression

1. Define state variables in `custom(...)`.
2. Trigger on explicit completion condition.
3. Update load/reps only when condition is met.
4. Reset state deterministically.

Starter:

```text
Squat / 3x8 / progress: custom(attempt: 0, bump: 2.5kg) {~
  if (completedReps >= reps) {
    state.attempt += 1
    if (state.attempt >= 3) {
      weights += state.bump
      state.attempt = 0
    }
  }
~}
```

## Recipe: dynamic drop sets with update script

1. Gate on exact `setIndex`.
2. Read first set outcome.
3. Increase `numberOfSets`.
4. Use `sets()` to define added sets.

Starter:

```text
Bench Press / 3x8 / update: custom() {~
  if (setIndex == 1 && completedReps[1] >= reps[1]) {
    numberOfSets = 5
    sets(3, 5, floor(reps[1] / 2), floor(reps[1] / 2), 0, weights[1], 0, 0, 0)
  }
~}
```

## Recipe: debug a broken script quickly

1. Identify context: `progress` or `update`.
2. Check every assignment target for legality in that context.
3. Check index shape (`[week:day:setVariation:set]` vs `[set]`).
4. Check trigger condition and units (`lb`/`kg`/`%`).
5. Re-run mental trace for success and failure paths.

## Recipe: split one identity into two progression tracks

1. Add labels to create separate identities.
2. Assign different progression per label.
3. Keep each identity internally consistent.

Example:

- `lowrep: Bench Press / 3x3 / progress: dp(2.5kg, 3, 6)`
- `highrep: Bench Press / 3x8 / progress: dp(2.5kg, 8, 12)`
