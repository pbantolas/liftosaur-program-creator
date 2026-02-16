# Liftosaur Program Creator

![Liftosaur Program Creator Logo](assets/logo.png "Liftosaur Program Creator")

An AI agent skill that teaches language models how to write and debug Liftoscript programs for Liftosaur. Stop wrestling with syntax errors and progression logic. Just describe what you want, and get working code.

## Why use this?

**Before:** You spend 30 minutes reading documentation, testing in the Liftosaur editor, and debugging why your custom progression script won't increment weight properly.

**After:** You tell your AI assistant "I want 5/3/1 for the main lifts with joker sets" and get a complete, working program in seconds.

This skill gives AI agents deep knowledge of Liftoscript syntax, progression patterns, custom scripting, and common pitfalls so they can help you build programs correctly the first time.

## Quickstart

### Using skills.sh (recommended)
Install this skill with a single command:

```bash
npx skills add https://github.com/pbantolas/liftosaur-program-creator --skill liftosaur-program-creator
```

For more information, [visit the skills.sh platform page](https://skills.sh/pbantolas/liftosaur-program-creator/liftosaur-program-creator).

Then use the skill in your AI agent, for example:
```
Create a 5x5 program with squats, bench, and deadlift using linear progression.
Add 2.5kg each session if I complete all reps.
```

## What you can build

### Simple programs with built-in progression

**You:** "Create a push/pull/legs split. Use double progression from 3x8 to 3x12, then add 5kg."

**Result:** A complete 3-day program with proper double progression setup, no custom scripting needed.

### Custom progression logic

**You:** "I want to add 2.5kg to squats every session, but only if I got all reps with RPE 8 or lower. If I miss reps, deload 10%."

**Result:** A `progress: custom()` script that reads your RPE state variable and implements the exact logic you described.

### Wave periodization and complex schemes

**You:** "Create a 4-week wave for bench press: Week 1 is 3x5 at 80%, week 2 is 3x3 at 85%, week 3 is 3x5+ at 80%, week 4 is deload at 60%."

**Result:** A proper week-based structure with percentage-based loading and AMRAP sets where appropriate.

### Debugging broken programs

**You:** "This script is supposed to increment `weights.squat` by 2.5kg but it's not working: [paste your code]"

**Result:** The agent identifies that you're trying to write to `weights.squat` in a `progress: custom()` block (not allowed), and shows you the correct way to modify `state.weight`.

## Common use cases

### "I want to try a new program I read about"

Describe the program structure and progression scheme. The agent handles translating it into valid Liftoscript.

```
Create Candito's 6-week program: control week, volume week, two intensity weeks,
then a heavy single test week. Use percentage-based loading.
```

### "I have a spreadsheet program I want to port"

Share your spreadsheet logic. The agent converts percentage calculations and weekly progressions into Liftoscript.

```
I have an Excel program where squats start at 75% of max for 5x5, and each week
adds 5% until week 6 hits 90% for triples. Convert this to Liftoscript.
```

### "My custom script has a bug"

Paste your code. The agent understands variable scopes, writable state, and common mistakes.

```
This update script crashes on week 2: [paste code]
```

### "I want to reuse the same progression for multiple exercises"

The agent can refactor your program using templates to eliminate duplication.

```
My squat, bench, deadlift, and OHP all use the same 5/3/1 progression.
Use templates so I don't repeat the same script four times.
```

## What's inside

This skill includes:

- **Complete Liftoscript reference** covering syntax, progression, scripting, and templates
- **Exercise database** with canonical names and equipment pairings
- **Common failure modes** guide to catch errors before they happen
- **Recipe library** with working examples of popular progression schemes

The agent automatically reads only what it needs for your specific request.

## Works with any agent

While optimized for Claude Code, this skill works with any AI agent that can read markdown documentation. The skill structure is standard and portable.

## Tips

- **Be specific about numbers**: "Add 2.5kg" is clearer than "add a little weight"
- **Mention your units**: Say "kg" or "lb" to avoid assumptions
- **Share your existing code** when debugging or making edits
- **Describe the goal**: "Linear progression until I stall" is more helpful than "make it work"

## About Liftosaur

[Liftosaur](https://www.liftosaur.com) is a workout tracking app for strength training. Liftoscript is its programming language for creating custom workout programs with automatic progression.

## License

MIT License - see LICENSE file for details.
