# Changelog

All notable changes to the Atlantis with Kiro AI assets will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v0.0.10 (unreleased)

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
