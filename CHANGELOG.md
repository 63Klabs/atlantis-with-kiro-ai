# Changelog

All notable changes to the Atlantis with Kiro AI assets will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v0.0.6] (2026-10-05)

### Added

Skills for Atlantis DevOps Platform. Converted some steering documents into skills so Kiro and other agents can use them.

- **skills/atlantis-platform-resources**
- **skills/automate-audit-update-npm-packages**
- **skills/automate-audit-update-python-packages**
- **skills/automate-update-lambda-layers**

## [v0.0.5] (2026-09-02)

### Changed

- **steering/automate-audit-update-npm-packages.md** - Instructed AI to advance versions, not just rely on `audit --fix`
- **steering/automate-audit-update-python-packages.md** - Instructed AI to advance versions, not just rely on python audit

---

## Release Notes Format

Each release should include changes under these categories:

- **Added**: New features, tools, or capabilities
- **Changed**: Modifications to existing functionality
- **Deprecated**: Features marked for removal (with sunset date)
- **Removed**: Features removed in this version
- **Fixed**: Bug fixes and corrections
- **Security**: Security-related changes or fixes

### Breaking Changes

Breaking changes should be clearly marked and include:
- Description of the breaking change
- Migration guide link
- Deprecation timeline for old version

Example:
```markdown
### Breaking Changes
- **steering/automate-audit-update-npm-packages.md** - Instructed AI to update versions, not just rely on `audit --fix`
```

### Version Links

[Unreleased]: https://github.com/63klabs/atlantis-with-kiro-ai/
[v0.0.6]: https://github.com/63klabs/atlantis-with-kiro-ai/releases/tag/v0.0.6
[v0.0.5]: https://github.com/63klabs/atlantis-with-kiro-ai/releases/tag/v0.0.5
