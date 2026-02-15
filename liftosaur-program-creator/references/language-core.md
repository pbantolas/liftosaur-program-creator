# Liftoscript Language Core

## Contents

- Scope
- Strict syntax pattern (canonical)
- Exercise line model
- Set expressions
- Intensity and load
- Best practice: grouped load/timer for set variations
- Timing
- Units
- Split long lines
- Primitive checklist

## Scope

Use this file for core exercise-line syntax and set expressions.

## Strict syntax pattern (canonical)

Use this canonical pattern when generating new lines:

`Exercise Name / set expressions / section: value / section: value`

### Good vs bad

Good:

- `Bench Press / 3x8 / progress: lp(2.5kg)`
- `OHP_T2: Overhead Press / 4x12 / 4x10 / 4x8 / 60% 120s / progress: dp(2.5kg, 8, 12)`
- `Deadlift / 3x5 / superset: A / used: none`

Bad:

- `Bench Press 3x8 progress: lp(5lb)` (mixed non-canonical spacing/section style when canonical output is expected)
- `Squat / 3x8 progress: lp(5kg)` (missing slash separator before `progress:`)
- `Deadlift / 3x5 / progress lp(5kg)` (missing `:` in section key/value)
- `Plank / 3x60s` (timed reps are not valid set syntax)

## Exercise line model

Canonical model:

`[optional label:] Exercise Name[, Equipment] / set expressions / section: value / section: value`

Sections are slash-style fields such as `progress:`, `update:`, `warmup:`, `superset:`, `id:`, `used:`.

Exercise identity should resolve from built-in names in `references/exercise-list.md` when available.
If a requested exercise is not in the list, custom naming is still valid.

## Set expressions

- Single pattern: `3x8`
- Rep range: `3x8-12`
- Multiple blocks: `1x5, 1x3, 1x1, 5x5`
- AMRAP reps: `1x5+`
- Quick add sets: `3+x5`
- Set label: `4x5 (Main), 1x5+ (AMRAP)`
- Set labels are limited to 8 characters max.
- Timed reps are not supported (`3x60s` is invalid); use numeric reps (`3x60`) as workaround.

## Intensity and load

- RPE target: `3x12@8`
- Log RPE after set: `1x5+@8+`
- Percent-based load: `3x12 80%` (often used as TM-based percentage in program design)
- Absolute load: `3x12 60kg` or `3x12 135lb`
- Ask performed weight: `100lb+` or `70%+`

## Best practice: grouped load/timer for set variations

When an exercise has multiple set variations, prefer one grouped load/timer section instead of repeating it per variation.

Recommended pattern:

`OHP_T2: Overhead Press / 4x12 / 4x10 / 4x8 / 60% 120s / progress: ...`

Interpretation:

- `4x12`, `4x10`, and `4x8` are set variations.
- `60% 120s` is shared and applies to all listed variations.

This is preferred because it keeps workouts compact and makes TM-percentage programming easier to maintain.

## Timing

- Per-set timer inline is valid but verbose: `1x12 20s 60%, 5x5 20s 60%`
- Prefer shared timer/load sections whenever values are the same across variations.
- In exercise-line set text, timers use `s` suffix (`45s`, `120s`).

## Units

- Prefer one load unit per generated snippet.
- If context provides units, match context.
- If user preference is explicit, use it.
- If neither exists, default to `kg`.

## Split long lines

Use `\` to continue one exercise line on the next line.

Example:

`Squat / 1x5@8 75% 120s, 3x8@9 60s / \`

`warmup: 1x5 20kg, 1x3 40kg / \`

`progress: lp(2.5kg)`

## Primitive checklist

When authoring or debugging a line, verify each primitive explicitly:

1. Exercise identity (name, optional label, optional equipment)
2. Set structure (count, reps, ranges, AMRAP)
3. Load expression (percent, weight, or computed)
4. Effort expression (RPE/log RPE)
5. Timing (timers)
6. Attached sections (`progress`, `update`, `warmup`, etc.)
