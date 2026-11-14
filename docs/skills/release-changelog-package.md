# Skill: Release Changelog (Package)

> This skill is for Node.js package repositories that keep a `CHANGELOG.md` with `## v<version> (unreleased)` headings. It works together with the [changelog-convention-package](../steering/changelog-convention-package.md) steering, which tells the agent to leave release dates and intro text to this skill.

This skill locks the `(unreleased)` section of `CHANGELOG.md` for the current `package.json` version. It sets the release date and adds a short intro under the version heading. Run it when you are ready to release. The agent should never run it on its own.

It can be installed in one of two places:
- `~/.kiro/skills/release-changelog-package/SKILL.md` for use in any package project on your machine.
- `path/to/your/project/.kiro/skills/release-changelog-package/SKILL.md` if you want to keep it with one project.

Invoke it with `/release-changelog-package`, or ask the agent to prepare the changelog for release. You can give it a release date, or ask for no intro.

What it does:
- **Finds the section:** Looks for the `## v<version> ` heading that matches `package.json`. It stops if the version is already dated, or if there are zero, several, or mismatched `(unreleased)` headings.
- **Picks the date:** Uses the date you give, or today's date. It asks if that date is earlier than the previous release.
- **Reviews the entries without changing them:** Reports an empty section, spec links to folders that do not exist, a Breaking Changes entry without a major version bump, exploit detail in Security entries, and out-of-order categories. It asks before continuing if the section is empty, a spec link is missing, or a breaking change is unexplained.
- **Drafts the intro:** One to three plain sentences based only on the entries. It leads with what you must do (upgrade or migrate), then names the main themes. If an intro already exists, it asks whether to keep or replace it.
- **Edits only the heading and intro:** The heading becomes `## v<version> (<date>)`. Nothing else in the file changes, and `git diff` confirms it.
- **Keeps scope tight:** It does not run `npm version`, run tests, commit, tag, or publish. Those release steps are yours.

The intro is a draft, so read it and edit it before you release.

[View example skill: release-changelog-package](../../examples/skills/release-changelog-package/SKILL.md)
