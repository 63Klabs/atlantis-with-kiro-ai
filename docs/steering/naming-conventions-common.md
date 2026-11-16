# Steering: Naming Conventions (Common)

Always loaded. Use it in any repository where you want the agent to follow one set of naming rules across languages.

[View example steering: naming-conventions-common.md](../../examples/steering/naming-conventions-common.md)

What it covers:

- **Existing code first:** The agent follows the convention most files in a module already use and does not rename existing names unless you ask.
- **Shared rules:** `UPPER_SNAKE_CASE` for constants and environment variables, `PascalCase` for classes and types, acronyms written as words (`ApiClient`, not `APIClient`), and `is`/`has`/`can`/`should` prefixes for booleans.
- **Style table:** Where each naming style is normally used.

It is short because it loads in every session. Pair it with the language files: [JavaScript](./naming-conventions-javascript.md), [Python](./naming-conventions-python.md), [Shell](./naming-conventions-shell.md), and [CloudFormation](./naming-conventions-cloudformation.md).

Copy it to `.kiro/steering/` in your project. Edit the rules if your team's choices differ.
