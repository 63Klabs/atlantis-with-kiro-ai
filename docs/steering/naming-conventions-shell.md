# Steering: Naming Conventions (Shell)

Loads when `.sh` or `.bash` files are in use. Use it to keep Bash script names consistent.

[View example steering: naming-conventions-shell.md](../../examples/steering/naming-conventions-shell.md)

What it covers:

- **Variables and functions:** `snake_case` for local variables and functions, with a leading underscore for private functions.
- **Constants and environment variables:** `UPPER_SNAKE_CASE`, declared with `readonly`.
- **File names:** `kebab-case.sh` or `snake_case.sh`, following the project's majority style.

Copy it to `.kiro/steering/` in your project. Use it together with [Naming Conventions (Common)](./naming-conventions-common.md).
