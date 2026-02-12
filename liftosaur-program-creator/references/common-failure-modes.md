# Common Failure Modes

## Mixed separators in exercise lines

Pitfall:

- Mixing slash-style sections with freeform section placement in one generated line.

Fix:

- Use one style consistently per line; default to canonical slash-style output.

## Timer suffix literals inside scripts

Pitfall:

- Using timer suffix values in scripts, for example `timers[5] = 20s`.

Fix:

- In scripts, assign numeric seconds only, for example `timers[5] = 20`.

## Timed reps in set syntax

Pitfall:

- Writing timed reps directly in set tokens, for example `Plank / 3x60s`.

Fix:

- Use numeric reps without `s` suffix, for example `Plank / 3x60`.

## Unit assumptions without context

Pitfall:

- Assuming `lb` when user/context did not specify units.

Fix:

- Reuse context units if present, else use stated user preference, else default to `kg`.
