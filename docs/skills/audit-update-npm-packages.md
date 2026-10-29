# Skill: Audit and Update npm Packages

This skill scans every `package.json` in the repository, runs `npm audit`, and updates vulnerable packages to fixed versions. Production dependencies are handled first.

It can be installed in one of two places:

- `~/.kiro/skills/audit-update-npm-packages/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/audit-update-npm-packages/SKILL.md` if you want to keep it with one project.

Invoke it with `/audit-update-npm-packages`, or ask the agent to audit npm packages, fix npm audit findings, or update Node.js dependencies.

What it does:

- **Edits direct dependencies:** Sets the fixed version in `package.json` and keeps your pinning style (exact, caret, or tilde).
- **Handles transitive packages separately:** Fixes packages you do not list directly through the lock file, and labels them that way in the report.
- **Runs checks:** Runs `npm install`, `npm audit`, and `npm test` after the changes.
- **Reports:** Lists old and new versions, severity, major version bumps, and anything it could not fix.
- **Keeps scope tight:** It does not add or remove dependencies or reformat `package.json`.

It changes `package.json` and the lock file, so review the diff before you commit.

[View example skill: audit-update-npm-packages](../../examples/skills/audit-update-npm-packages/SKILL.md)
