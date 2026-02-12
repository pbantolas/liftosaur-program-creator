# Program Structure

## Weeks and days

- Full mode uses `# Week N` and `## Day N` headings.
- Exercises under a week/day belong to that block.

## Descriptions

- Exercise descriptions are comments and can use Markdown.
- Week/day descriptions can also be attached in full mode.
- Description reuse carries forward until overwritten.
- Explicit empty comment stops carry-forward reuse.

## Exercise labels

Prefix with `label:` to distinguish otherwise same exercise names.

Example:

- `main: Squat / 5x5 / progress: lp(2.5kg)`
- `accessory: Squat / 3x8 / progress: dp(2.5kg, 8, 12)`

Use labels when progress logic must differ by role.

## Warmups

- Define with `warmup:`.
- Use set-like notation for warmups.
- `warmup: none` disables warmup generation.
- Warmup percentages are based on first work set weight (not 1RM).

## Supersets

- Group using `superset: A` (or any group key).
- Exercises with same group key are cycled together.
- Per-set timers can override superset default timer.

## Tags for cross-exercise state access

- Add tags using `id: tags(1, 101)`.
- Read/write tagged state in scripts with `state[tag].variable`.
- Use tags when one exercise must influence another exercise state.

## Set variations and description variations

- Multiple set schemes in one exercise are supported.
- Active set scheme is controlled by `setVariationIndex`.
- Multiple descriptions are supported.
- Active description is controlled by `descriptionIndex`.
- Best practice: place shared load/timer once after variation blocks when common.

Example:

- `OHP_T2: Overhead Press / 4x12 / 4x10 / 4x8 / 60% 120s / progress: ...`

In this pattern, `60% 120s` applies to all set variations.

## Structure workflow

1. Place week/day blocks.
2. Define exercise identity and labels.
3. Add warmup/superset/tag metadata.
4. Add progression/update logic.
5. Confirm carry-forward description behavior is intentional.
