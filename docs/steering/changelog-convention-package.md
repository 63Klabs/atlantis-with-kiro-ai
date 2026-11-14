# Steering: Changelog Convention (Package)
Loads when `CHANGELOG.md` or Markdown files under `.kiro/specs/` are in use. Use it in Node.js package repositories where the agent adds changelog entries as part of a spec and the release version comes from `package.json`.

[View example steering: changelog-convention-package.md](../../examples/steering/changelog-convention-package.md)

What it covers:
- **Where entries go:** Only under the `(unreleased)` heading for the current `package.json` version. Dated sections are never edited. If the version is already dated, the agent stops and tells you to run `npm version [major|minor|patch]`.
- **Version check before a spec:** A read-only check before any spec file is created, so a version bump is not blocked by a dirty git tree.
- **Categories:** Security, Fixed, Breaking Changes, Added, Changed, Deprecated, Removed, and Dependencies, in that order. Empty categories are left out.
- **Entry format:** A bold title, a ` - ` separator, a description written for package users, and spec and issue links at the end. Issue links use `bugs.url` from `package.json`.
- **Special entries:** Rules for documentation and internal changes, breaking changes (major bump and migration guide), deprecations, and security entries without exploit detail.
- **Editing unreleased entries:** The agent may merge or re-summarize them but keeps spec links, version ranges, and migration text.
- **Release dates and intros:** The agent never writes these. Use the [release-changelog-package](../skills/release-changelog-package.md) skill when you are ready to release.

Copy it to `.kiro/steering/` in your package repository. The examples use `example-org/example-package` as a placeholder, so no repository URL needs editing. The `.kiro/specs/` pattern assumes you use Kiro specs, so change the pattern if you do not.
