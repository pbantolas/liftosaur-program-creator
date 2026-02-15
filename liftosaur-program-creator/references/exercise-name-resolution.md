# Exercise Name Resolution

## Source of truth

Use `references/exercise-list.md` as the built-in exercise list.

Entries may be either:

- `Exercise Name`
- `Exercise Name, Equipment`

## Resolver

1. If user intent specifies equipment/variant, use `Exercise Name, Equipment` and require an exact match in `references/exercise-list.md`.
2. Otherwise, use alias-only `Exercise Name` and require an exact bare-name match in `references/exercise-list.md`.
3. Preserve existing style when editing unless user requests a change.

## Fallback

- If a requested exercise is not in `references/exercise-list.md`, keep the requested name and continue generating valid Liftoscript.
- Add a short note that custom exercises can be added manually in Liftosaur.
