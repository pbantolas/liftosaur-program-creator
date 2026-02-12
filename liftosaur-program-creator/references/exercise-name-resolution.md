# Exercise Name Resolution

## Source of truth

Use `resources/exercise-list.txt` as the canonical reference for exercise names and equipment pairs.

Canonical format in the list is:

`Exercise Name, Equipment`

Example canonical entries:

- `Bench Press, Barbell`
- `Overhead Press, Dumbbell`
- `Romanian Deadlift, Barbell`

## How to apply in generated lines

- If the requested exercise exists in `resources/exercise-list.txt`, use the canonical name/equipment pair.
- In Liftoscript lines, render equipment using normal exercise syntax:
  - `Bench Press, Barbell / 3x8 / progress: dp(2.5kg, 8, 12)`

## Fallback when exercise is not listed

- Missing from `resources/exercise-list.txt` does not block output.
- Use the requested/custom exercise name and continue generating valid Liftoscript.
- Add a short note that custom exercises can be added manually in Liftosaur.

## Fast check workflow

1. Try exact match in `resources/exercise-list.txt`.
2. If no exact match, try closest canonical variant by equipment.
3. If still no match, keep user name and proceed.
4. Mention manual add path for custom exercise names.
