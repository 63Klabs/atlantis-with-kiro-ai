# Steering

Steering files are Markdown instructions that Kiro reads as project context. Each example here is a standalone file. Copy the ones you need into your project's `.kiro/steering/` directory.

```
path/to/your/project/.kiro/steering/
```

The example files use front matter to decide when Kiro loads them. Each one loads only when files matching its pattern are in use, so the rules stay out of the way for unrelated work. Edit the pattern if your folder layout differs.

Available steering:

- [Multi-Resource Source Layout](./atlantis-multi-resource-src.md)
- [Python Dependency Management](./atlantis-python-dependency-management.md)
- [WebApi with Node.js and cache-data](./atlantis-webapi-node-cache-data.md)
