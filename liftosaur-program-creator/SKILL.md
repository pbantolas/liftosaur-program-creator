---
name: liftosaur-program-creator
description: Writes and edits workout programs for the Liftosaur app using Liftoscript language. Use when creating programs, adding exercises, configuring progression logic, writing progress/update scripts, or debugging Liftoscript code.
---

# Liftoscript Program Authoring

Use this skill for Liftosaur program text and Liftoscript logic.

## Canonical formatting contract

- Default to slash-style exercise format in outputs:
  - `Exercise Name / set expressions / section: value / section: value`
- Keep one separator style per line; do not mix slash and freeform section placement.
- Prefer explicit section names for non-set data (`progress:`, `update:`, `warmup:`, `superset:`, `used:`, `id:`).
- If editing existing text that uses another style, preserve local style unless user asks to normalize.

## When to use

- User asks to write or edit Liftosaur workout program lines.
- User asks for progression logic (`lp`, `dp`, `sum`, or `custom()`).
- User asks to remove repetition via reuse (`...Exercise`) or templates.
- User asks to debug `progress: custom()` or `update: custom()` behavior.

## Operating rules

- Keep terminology consistent: use "exercise line", "set", "progress", "update", "state variable", "set variation".
- Prefer built-in progression (`lp`, `dp`, `sum`) before custom scripts.
- For scripting tasks, identify execution context first: `progress: custom()` vs `update: custom()`.
- Timer literals by context:
  - Exercise-line sets use timer suffixes like `45s`, `120s`.
  - Scripts use numeric timer values (for example `timers[5] = 20`, not `20s`).
  - Timed reps are not supported in set syntax (avoid `3x60s`); use `3x60` as workaround.
- Set-variation authoring best practice:
  - Prefer grouped shared load/timer after set variations to reduce repetition.
  - Example: `OHP_T2: Overhead Press / 4x12 / 4x10 / 4x8 / 60% 120s / progress: ...`
  - Interpret grouped `60% 120s` as applying to all listed set variations.
- Unit resolution policy:
  - Reuse units from nearby program text when present.
  - Else use explicit user preference from conversation.
  - Else default to `kg`.
  - Do not silently mix `kg` and `lb` in the same generated snippet.
- Exercise naming policy:
  - Prefer canonical exercise/equipment names from `resources/exercise-list.txt`.
  - Use exact `Exercise, Equipment` naming when a match exists.
  - If no match exists, it is still valid to use a custom exercise name.
  - Note in output that unmatched exercises can be added manually in Liftosaur.
- Use a validation loop: draft -> check writable variables/scope/indexing -> correct -> finalize.
- Preserve user intent and existing structure; change only what is required.

## Routing by task

- Basic syntax and set notation -> `references/language-core.md`
- Weeks, days, comments, labels, warmups, supersets, tags -> `references/program-structure.md`
- Built-in progression choice and arguments -> `references/progression-builtins.md`
- Reuse, repeat, templates, overrides -> `references/reuse-and-templates.md`
- `progress: custom()` authoring -> `references/custom-progress-scripts.md`
- `update: custom()` authoring -> `references/update-scripts.md`
- Read/write variables and indexing rules -> `references/runtime-reference.md`
- Liftoscript built-in functions -> `references/builtins-reference.md`
- End-to-end examples and fix patterns -> `references/recipes.md`
- Canonical exercise name resolution -> `references/exercise-name-resolution.md`
- Known pitfalls and quick fixes -> `references/common-failure-modes.md`

## Minimal workflow

1. Classify request: syntax, progression, reuse, custom script, or debug.
2. Read only the needed reference file(s) above.
3. Produce the smallest correct change.
4. Validate constraints (especially writable variables and index scope).
5. Return final program/script text and a short rationale.

## Preflight validator (must pass before final output)

- Section separators are correct and consistent for each exercise line.
- Set and set-variation syntax is structurally valid.
- Script assignments target writable variables for the selected context.
- Script assignment literals use valid types for the target variable.
- Timer literals follow context rules (`45s` in exercise text, numeric in scripts).
- Rep tokens are numeric counts (no `s` suffix on reps; use `3x60`, not `3x60s`).
- Units are resolved from context/user preference or defaulted to `kg`.
- No forbidden unit mismatches in generated output.
- Exercise name/equipment pair is canonical when available in `resources/exercise-list.txt`.
- If exercise is not in canonical list, output remains valid and mentions manual add path in Liftosaur.
