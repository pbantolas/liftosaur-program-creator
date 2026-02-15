# Reuse and Templates

## Exercise reuse (`...Exercise`)

Reuse sets/reps/load/timer/warmup and script sections from another exercise.

Examples:

- `Squat / ...Bench Press`
- `Squat / ...Bench Press[2]` (day 2 in current week)
- `Squat / ...Bench Press[2:1]` (week 2, day 1)

## Override on top of reuse

You can reuse a source exercise and override selected fields in the target.

Example:

- `Bench Press / ...Squat / 150lb / progress: lp(5lb)`

## Repeat across weeks

Use week ranges after exercise name:

- `Bench Press[1-4] / 3x8`

Optional explicit ordering for ambiguous cases:

- `Squat[1,1-4] / ...t1`

## Description reuse

Reuse comments similarly to sets reuse:

- `// ...Squat`
- `// ...Squat[3]`
- `// ...Squat[3:2]`

## Templates (`used: none`)

Create source patterns that are not part of performed workouts.

Placement rule (full mode with week/day headings):

- Place template lines inside a day block, not directly under `# Week N`.
- For week-scoped templates, place them immediately after the `## Day 1` heading (before normal day exercises).
- Do not place template lines between `# Week N` and the first `## Day N` heading.

Examples:

- `T1 / used: none / 1x10+, 3x10 70% / progress: lp(5lb)`
- `t1: Bench Press / ...T1`

Templates reduce drift because the source line itself does not progress as a performed exercise.

## Reuse caveat

When reused exercises diverge after progression, Liftosaur may materialize overrides to preserve behavior.

## Reuse workflow

1. Choose canonical source line (prefer template for large programs).
2. Reuse by default from same week/day rules.
3. Add explicit `[day]` or `[week:day]` only when needed.
4. Keep overrides minimal and intentional.
5. Re-check after progression-related drift.
