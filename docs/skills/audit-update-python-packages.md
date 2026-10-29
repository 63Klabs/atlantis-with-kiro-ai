# Skill: Audit and Update Python Packages

This skill scans the `requirements*.txt` files in the repository, runs `pip-audit`, and updates vulnerable pinned packages to fixed versions. `requirements.txt`, which ships to Lambda, is handled first.

It can be installed in one of two places:

- `~/.kiro/skills/audit-update-python-packages/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/audit-update-python-packages/SKILL.md` if you want to keep it with one project.

Invoke it with `/audit-update-python-packages`, or ask the agent to audit pip packages, fix pip-audit findings, or update Python dependencies.

What it does:

- **Edits direct entries:** Sets the fixed version on lines that name the package and keeps your pin style (`==`, `~=`, `>=`, or a range).
- **Handles transitive packages carefully:** Bumps a parent package if that fixes the issue. Otherwise it reports the issue and does not add a new line.
- **Uses a project virtual environment:** Runs everything in `.ve/` so your system Python is untouched.
- **Runs checks:** Re-runs `pip-audit` and `pytest` when a test setup exists.
- **Keeps scope tight:** It does not add, remove, or move packages, and it keeps your comments.

It changes requirements files, so review the diff before you commit.

[View example skill: audit-update-python-packages](../../examples/skills/audit-update-python-packages/SKILL.md)
