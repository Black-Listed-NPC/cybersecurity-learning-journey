# Day 4 — Module 3: Bash & Python Fundamentals + Assignment 4

**Date:** 11 Oct 2026 · **Lectures:** Bash — Variables (30m), Bash — Arrays & Conditionals (35m), Python Fundamentals (1h27m) · **Assignment:** 4 · *Module 3 complete *

> All hands-on work below was done only in my own isolated lab VMs or on the course's dedicated TryHackMe rooms, for learning purposes.

## Covered today
### Bash scripting
- Every script starts with the shebang `#!/bin/bash`; `echo` prints output.
- **Variables:** no spaces around `=` (`name="Yash"`), read with `$name`.
- **Arrays:** `transport=('car' 'train' 'bike')`, index from 0, `${transport[@]}`, `unset`.
- **Conditionals:** `if / elif / else / fi` with `[ condition ]`.

### Python fundamentals
- Why Python for security: automation (scanning, traffic/log analysis) and custom tooling.
- Core basics: indentation-defined blocks, `print()`, `input()`.
- Data types: `int`, `float`, `str`, `list` (mutable), `tuple` (immutable), `dict` (key–value).
- Operators, string manipulation, conditionals and loops.

## Assignment completed (TryHackMe)
| # | Task | Focus |
|---|------|-------|
|  | Python  | variables, arrays, conditionals — leap-year, even/odd, range check, calculator scripts |
|  | Bash  | basic scripting |

**Proof:** `Assignment 4.zip`

## Reflection
Bash for quick system automation, Python for anything heavier. Both are the glue for the offensive and defensive tooling that comes next.
