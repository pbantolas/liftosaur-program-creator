# Liftosaur Program Creator

<img src="assets/logo.png" alt="Liftosaur Program Creator Logo">

An AI skill that helps your assistant write, edit, and debug Liftoscript programs for Liftosaur.

Instead of wrestling with syntax and progression logic, you describe what you want in plain language and get working program code.

> New to Liftosaur? [Liftosaur](https://www.liftosaur.com) is a strength training app. Liftoscript is its language for creating custom programs with automatic progression.

## Quickstart

Install with [skills.sh](https://skills.sh/pbantolas/liftosaur-program-creator/liftosaur-program-creator):

```bash
npx skills add https://github.com/pbantolas/liftosaur-program-creator --skill liftosaur-program-creator
```

Then try a prompt like:

```text
Create a 5x5 program with squats, bench, and deadlift.
Add 2.5kg each session if I complete all reps.
```

## Tips for best results

- Specify units (`kg` or `lb`) so nothing is guessed.
- Give exact numbers (`add 2.5kg`) instead of vague wording.
- Paste your current code when asking for debugging help.
- Describe the goal, not just the problem (for example, "linear progression until stall, then deload 10%")

## What this helps with

Build a program from scratch:

```text
Create a push/pull/legs split.
Use double progression from 3x8 to 3x12, then add 5kg.
```

Port a program from a spreadsheet or article:

```text
I have an Excel program where squats start at 75% for 5x5,
then add 5% weekly until week 6 reaches 90% for triples.
Convert it to Liftoscript.
```

Write custom progression logic:

```text
Add 2.5kg to squats each session only if I hit all reps at RPE 8 or lower.
If I miss reps, deload 10%.
```

Debug broken scripts:

```text
This script should increment squat weight but it doesn't: [paste code]
```

Refactor repeated logic with templates:

```text
My squat, bench, deadlift, and OHP all use the same 5/3/1 progression.
Use templates so I do not repeat the same script four times.
```

## License

MIT - see [LICENSE](LICENSE).
