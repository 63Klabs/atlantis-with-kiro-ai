# Steering

Steering files are Markdown instructions that Kiro reads as project context. Each example here is a standalone file. Copy the ones you need into your project's `.kiro/steering/` directory.

```
path/to/your/project/.kiro/steering/
```

The example files use front matter to decide when Kiro loads them. Each one loads only when files matching its pattern are in use, so the rules stay out of the way for unrelated work. Edit the pattern if your folder layout differs.

Available steering:

- [Changelog Convention (Application)](./changelog-convention-application.md)
- [Changelog Convention (Package)](./changelog-convention-package.md)
- [Multi-Resource Source Layout](./atlantis-multi-resource-src.md)
- [Naming Conventions (Common)](./naming-conventions-common.md)
- [Naming Conventions (CloudFormation/SAM)](./naming-conventions-cloudformation.md)
- [Naming Conventions (CloudFormation/SAM, Atlantis)](./naming-conventions-cloudformation-atlantis.md)
- [Naming Conventions (JavaScript/TypeScript)](./naming-conventions-javascript.md)
- [Naming Conventions (Python)](./naming-conventions-python.md)
- [Naming Conventions (Shell)](./naming-conventions-shell.md)
- [Python Dependency Management](./atlantis-python-dependency-management.md)
- [Spec Naming Convention](./spec-naming-convention.md)
- [WebApi with Node.js and cache-data](./atlantis-webapi-node-cache-data.md)
