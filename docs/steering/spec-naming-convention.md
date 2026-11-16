# Steering: Spec Naming Convention

Always loaded. Use it when you create Kiro specs and want each spec directory prefixed with the release version it ships in.

[View example steering: spec-naming-convention.md](../../examples/steering/spec-naming-convention.md)

What it covers:

- **Directory names:** `.kiro/specs/{version}-{feature-name}/`, such as `1-4-2-retry-option`, where the version is the `(unreleased)` version in `CHANGELOG.md`.
- **Missing version:** If `CHANGELOG.md` has no `(unreleased)` heading, the agent follows the version check in your `changelog-convention-*` steering file, or asks you if there is none.
- **File names:** `requirements.md`, `design.md`, and `tasks.md` in each spec.

Copy it to `.kiro/steering/` in your project. It needs a `CHANGELOG.md` with version headings.
