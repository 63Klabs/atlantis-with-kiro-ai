# Atlantis with Kiro AI

Steering documents, hooks, and MCP settings for the Kiro IDE to get the most out of the Atlantis DevOps Templates and Scripts Platform.

You can utilize the Atlantis MCP server in your IDE to automate checks and downloads of new document versions.

In your IDE's chat, just instruct:

```
What steering documents are available from atlantis?
```

Response:

```md
Let me check what steering documents are available from Atlantis:Great! Here are the available steering documents from Atlantis:

## Available Atlantis Steering Documents

There are 6 steering documents available:

1. **atlantis-multi-resource-src.md** (12.6 KB)
   - Multi-resource source guidance

2. **atlantis-python-dependency-management.md** (4 KB)
   - Python dependency management guidance

3. **atlantis-webapi-node-cache-data.md** (18.6 KB)
   - Web API guidance for Node.js with @63klabs/cache-data (most relevant to your repo)

4. **automate-audit-update-npm-packages.md** (3.2 KB)
   - Automation for npm package audits and updates

5. **automate-audit-update-python-packages.md** (4.2 KB)
   - Automation for Python package audits and updates

6. **automate-update-lambda-layers.md** (2 KB)
   - Automation for updating Lambda layers

The **atlantis-webapi-node-cache-data.md** document is most relevant to your project since you're using @63klabs/cache-data. Would you like me to fetch and review any of these steering documents? The multi-resource and web API ones would be particularly useful for understanding best practices in your Atlantis setup.
```

Or:

```
Check for updates from Atlantis for steering/automate-audit-update-npm-packages.md
```

And after reviewing the response:

```
Fetch the automate-audit-update-npm-packages.md and add it to .kiro/steering
```

For more about the Atlantis MCP server, visit [mcp.atlantis.63klabs.net](https://mcp.atlantis.63klabs.net)