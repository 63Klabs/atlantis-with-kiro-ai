# Changelog

All notable changes to the Atlantis with Kiro AI assets will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v0.0.11 (2026-11-16)

### Added

- **steering/naming-conventions-common.md**: Always-loaded naming rules shared by all languages: follow existing code, `UPPER_SNAKE_CASE` constants, `PascalCase` classes, acronyms written as words, and boolean prefixes.
- **steering/naming-conventions-javascript.md, naming-conventions-python.md, naming-conventions-shell.md**: Short per-language naming rules that load when matching files are open.
- **steering/naming-conventions-cloudformation.md**: Generic CloudFormation/SAM naming rules for parameters, logical IDs, conditions, outputs, tags, and physical names.
- **steering/naming-conventions-cloudformation-atlantis.md**: Atlantis `Prefix`, `ProjectId`, and `StageId` naming rules and S3 bucket patterns, checked with the Atlantis MCP `validate_naming` tool.
- **steering/spec-naming-convention.md**: Names spec directories `{version}-{feature-name}`. The version always comes from the `(unreleased)` heading in `CHANGELOG.md`.
- **steering/changelog-convention-application.md**: Rules for maintaining `CHANGELOG.md` in an application repository where the changelog version is the release of several components. The agent asks you to confirm the release version before creating a spec.
- **.kiro/steering/maintaining-examples.md**: Conventions for maintaining the skills and steering examples in this repository: file naming, keeping files generic and concise, and keeping docs in sync.
- **docs/**: Documentation for each new steering file.

### Changed

- **skills/audit-update-npm-packages**: Always advances `@63klabs/cache-data` to its latest published version in every `package.json` that lists it, then reinstalls so the lock file matches. Flags major version bumps and never adds the package.
- **skills/import-issues-from-github**: When there is no `(unreleased)` heading in `CHANGELOG.md`, it now stops and follows the repository's changelog steering, or asks for the version, instead of adding a patch heading itself.
- **skills/update-aws-lambda-layers**: Leaves layers that use the `{{resolve:ssm:...}}` format untouched, because AWS public parameters always resolve to the latest version at deploy time. It no longer converts them to Mappings, and falls back to a Mapping only when a deployed region has no public parameter. Lambda Insights stays in Mappings.

## v0.0.10 (2026-11-13)

### Added

- **skills/release-changelog-package**: Run manually when ready to release. Sets the release date on the `(unreleased)` section of `CHANGELOG.md` for the current `package.json` version and adds a short intro, without touching the entries.
- **steering/changelog-convention-package.md**: Rules for maintaining `CHANGELOG.md` in a Node.js package repository: entries go only under the `(unreleased)` heading, a read-only version check runs before a spec starts, and release dates and intros are left to the `release-changelog-package` skill.
- **docs/**: Documentation for `release-changelog-package` and `changelog-convention-package`.

## v0.0.9 (2026-10-29)

### Added

Documentation and skills for importing issues from GitHub and generating a pre-spec-driven workflow PLAN.md based on an imported or manually created ISSUE.md

- **skills/import-issues-from-github**: Import unassigned issues labeled for development from GitHub and generate an `ISSUE.md`
- **skills/plan-from-issue**: Generate a plan from an ISSUE.md (imported or otherwise) that verifies the issue, reviews the codebase, and identifies gaps before presenting the user with a set of questions, options, and recommendations prior to starting the spec-driven process.
- **docs/**: Documentation on each of the assets.

## v0.0.6 (2026-10-05)

### Added

Skills for 63Klabs Atlantis DevOps Platform. Converted some steering documents into skills so Kiro and other agents can use them.

- **skills/atlantis-platform-resources**
- **skills/audit-update-npm-packages**
- **skills/audit-update-python-packages**
- **skills/update-lambda-layers**

## v0.0.6-v0.0.8 (2026-10-08)

Resolving release packaging issues.

## v0.0.5 (2026-09-02)

### Changed

- **steering/automate-audit-update-npm-packages.md** - Instructed AI to advance versions, not just rely on `audit --fix`
- **steering/automate-audit-update-python-packages.md** - Instructed AI to advance versions, not just rely on python audit
