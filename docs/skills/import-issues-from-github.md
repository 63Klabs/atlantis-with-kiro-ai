# Skill: Import Issues from GitHub

> Issues come from the public. Review each imported ISSUE.md before you plan work from it.

This skill pulls approved GitHub issues into spec directories so they can be planned with the [plan-from-issue](./plan-from-issue.md) skill. It is generic and works in any project whose git remote points to GitHub.

It can be installed in one of two places:

- `~/.kiro/skills/import-issues-from-github/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/import-issues-from-github/SKILL.md` if you want to keep it with one project.

Invoke it with `/import-issues-from-github`, or ask the agent to import, pull, or sync approved GitHub issues.

What it does:

- **Selects issues:** Finds open, unassigned issues that carry the exact label `approved for development`.
- **Writes specs:** Saves each issue to `.kiro/specs/{version}-{slug}/ISSUE.md`. The version comes from the top header in CHANGELOG.md. If that release is already published, the skill adds a new unreleased patch header.
- **Sanitizes text:** Places the title, description, and comments in code fences. It removes hidden characters and HTML comments, redacts reporter names and email addresses, and removes credentials it recognizes.
- **Assigns the issue:** Assigns each imported issue to your GitHub user. It does not comment on, relabel, or close issues.
- **Does not triage:** It makes no judgment about validity, priority, or scope.

Requirements: the `gh` CLI logged in to github.com, git, and python3. The skill stops or asks first when the repository is ambiguous, when you lack triage access, or when more than 10 issues are eligible.

[View example skill: import-issues-from-github](../../examples/skills/import-issues-from-github/SKILL.md)
