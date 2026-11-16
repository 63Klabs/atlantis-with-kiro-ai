# Steering: Naming Conventions (Python)

Loads when `.py` files are in use. Use it to keep Python names consistent and in line with PEP 8.

[View example steering: naming-conventions-python.md](../../examples/steering/naming-conventions-python.md)

What it covers:

- **Core styles:** `snake_case` for variables, functions, methods, files, and modules, `PascalCase` for classes, and `UPPER_SNAKE_CASE` for global constants.
- **Exceptions:** `PascalCase` ending in `Error`.
- **Private members:** A leading underscore, with double underscore only when name mangling is needed.
- **Tests:** Functions start with `test_` and describe the behavior.

Copy it to `.kiro/steering/` in your project. Use it together with [Naming Conventions (Common)](./naming-conventions-common.md).
