# Runtime Reference

## Contents

- Types and values
- Operators and control flow
- Read-only variables
- Writable variables (`progress`)
- Writable variables (`update`)
- Indexing model
- State and temporary variables

## Types and values

- Number (for counts and comparisons)
- Weight (`lb` or `kg` suffix)
- Percentage (`%`)
- Boolean (condition results)

Prefer explicit `lb`/`kg` when manipulating load.

## Operators and control flow

- Math: `+ - * / %`
- Boolean: `> < >= <= == && ||`
- Ternary: `condition ? a : b`
- Branching: `if / else if / else`
- Loop: `for (var.i in arrayExpr)`

## Read-only variables (both contexts unless noted)

- `weights[n]` (`w[n]`)
- `originalWeights[n]`
- `completedWeights[n]`
- `reps[n]` (`r[n]`)
- `completedReps[n]` (`cr[n]`)
- `completedRepsLeft[n]`
- `RPE[n]`
- `completedRPE[n]`
- `rm1`
- `day`, `week`, `dayInWeek`
- `programNumberOfSets`
- `numberOfSets` (`ns`)
- `completedNumberOfSets`
- `setVariationIndex`
- `descriptionIndex`
- `amraps[n]`, `logrpes[n]`, `askweights[n]`
- `setIndex` (update context only)

## Writable variables in `progress: custom()`

- `weights[week:day:setVariation:set]`
- `reps[week:day:setVariation:set]`
- `RPE[week:day:setVariation:set]`
- `timers[week:day:setVariation:set]`
- `amraps[week:day:setVariation:set]`
- `logrpes[week:day:setVariation:set]`
- `askweights[week:day:setVariation:set]`
- `numberOfSets[week:day:setVariation]`
- `rm1`
- `setVariationIndex`
- `descriptionIndex`
- `state.variable`

Literal constraints (important):

- `timers[...]` expects numeric values (seconds as number), for example `timers[5] = 20`.
- Do not use timer suffix literals in scripts (avoid `timers[5] = 20s`).

## Writable variables in `update: custom()`

- `weights[set]`, `weights`
- `reps[set]`, `reps`
- `RPE[set]`, `RPE`
- `timers[set]`, `timers`
- `numberOfSets`
- `amraps[set]`, `logrpes[set]`, `askweights[set]`
- `rm1`

Literal constraints (important):

- `timers[...]` expects numeric values (seconds as number), for example `timers[2] = 45`.
- Do not use timer suffix literals in scripts (avoid `timers[2] = 45s`).

No cross-week/day/set-variation targeting in `update` context.

## Indexing model

Progress context supports dimensioned targeting:

`[week:day:setVariation:set]`

Rules:

- Each dimension accepts number/expression or `*` wildcard.
- Omitted leading dimensions are treated as wildcard.
- Use explicit indices for surgical edits and predictable behavior.

Update context uses only `[set]` for set-level targets.

## State and temporary variables

- Persistent state: declared in `custom(...)`, accessed by `state.name`.
- Prompted state: `name+: default`.
- Temporary scratch vars: `var.name`.

## Debug checklist

1. Confirm context (`progress` vs `update`).
2. Confirm every assignment target is legal.
3. Confirm index shape is legal for the context.
4. Confirm script literal types are valid for assignment targets.
5. Confirm timer assignments are numeric in scripts.
6. Confirm unit consistency for load math.
7. Confirm branch conditions reflect intended trigger.
