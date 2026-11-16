# Steering: Changelog Convention (Application)

Loads when `CHANGELOG.md` or Markdown files under `.kiro/specs/` are in use. Use it in application repositories that hold several components (Lambda functions, scripts, templates, packages), where each component may have its own version and the changelog version is the release of the whole application.

[View example steering: changelog-convention-application.md](../../examples/steering/changelog-convention-application.md)

What it covers:

- **Release version:** The changelog heading is the version of the whole application, not of any one component. If the newest heading is dated, the agent asks you for the next version before creating any spec file, suggests the next patch number, and adds the `(unreleased)` heading only after you confirm.
- **Where entries go:** Only under the `(unreleased)` heading. Dated sections are never edited.
- **Categories:** Security, Fixed, Breaking Changes, Added, Changed, Deprecated, Removed, and Dependencies, in that order. Empty categories are left out.
- **Entry format:** A bold component name (with the component's own version when it has one), a ` - ` separator, a description written for people who deploy or use the application, and spec and issue links at the end. A change that touches several components is one entry with a sub-bullet per component.
- **Special entries:** Rules for documentation and internal changes, breaking changes with migration steps, deprecations, and security entries without exploit detail.
- **Editing unreleased entries:** The agent may merge or re-summarize them but keeps spec links, release ranges, and migration text.
- **Release dates and intros:** The agent never writes these. You add them when you release and tag.

For a single package whose version lives in `package.json`, use [Changelog Convention (Package)](./changelog-convention-package.md) instead.

Copy it to `.kiro/steering/` in your application repository. The examples use `example-org/example-app` as a placeholder. The agent reads the real issues URL from existing changelog links or the `origin` remote. The `.kiro/specs/` pattern assumes you use Kiro specs, so change the pattern if you do not.
