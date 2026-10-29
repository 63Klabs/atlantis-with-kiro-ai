# Skill: 63Klabs Atlantis DevOps Platform Resources

> Requires the 63Klabs Atlantis MCP server. See [Atlantis MCP](../mcp/README.md) for setup.

This skill makes the agent check the Atlantis MCP server for platform templates, starters, naming rules, and `@63klabs/cache-data` documentation before it answers from memory. Use it in any repository built from an 63Klabs Atlantis starter.

It can be installed in one of two places:

- `~/.kiro/skills/atlantis-platform-resources/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/atlantis-platform-resources/SKILL.md` if you want to keep it with one project.

Invoke it with `/atlantis-platform-resources`, or ask about Atlantis templates, naming, or caching. The agent loads it when the request matches its description.

What it does:

- **Checks the source first:** Queries the MCP server for CloudFormation templates, starters, and cache-data APIs.
- **Recognizes Atlantis projects:** Detects them from the `application-infrastructure/` layout, `template-configuration.json`, or `samconfig.toml`.
- **Enforces platform guardrails:** Naming, least-privilege IAM, GitOps-only deployment, and no edits to upstream templates.
- **Reports outages:** If the MCP server is unreachable, it says so and marks platform-specific answers as unverified.

It does not cover general AWS or Node.js questions.

[View example skill: atlantis-platform-resources](../../examples/skills/atlantis-platform-resources/SKILL.md)
