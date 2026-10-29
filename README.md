# Atlantis with Kiro AI

Steering documents, skills, hooks, and MCP settings for the Kiro IDE to get the most out of the [63Klabs Atlantis DevOps Platform for Serverless Deployments on AWS](https://atlantis.63klabs.net).

You can utilize the [63Klabs Atlantis MCP server](https://mcp.atlantis.63klabs.net) in your IDE to automate checks and downloads of new document versions.

In your IDE's agentic chat, just instruct:

```markdown

USER: What steering documents are available from atlantis?

---

AGENT:  Let me check what steering documents are available from Atlantis:Great! Here are the available steering documents from Atlantis:

## Available Atlantis Steering Documents

There are 3 steering documents available:

1. **atlantis-multi-resource-src.md** (12.6 KB)
   - Multi-resource source guidance

2. **atlantis-python-dependency-management.md** (4 KB)
   - Python dependency management guidance

3. **atlantis-webapi-node-cache-data.md** (18.6 KB)
   - Web API guidance for Node.js with @63klabs/cache-data (most relevant to your repo)

The **atlantis-webapi-node-cache-data.md** document is most relevant to your project since you're using @63klabs/cache-data. Would you like me to fetch and review any of these steering documents? The multi-resource and web API ones would be particularly useful for understanding best practices in your Atlantis setup.

```

Or:

```markdown

USER: Check Atlantis for updates to the audit-update-npm-packages skill

---

AGENT: *Checks Atlantis MCP and finds a newer version, asking user if they would like to replace existing version with newer version.*

```

- [Review Documentation](./docs/README.md) for how to install and use the Atlantis MCP server, skill, steering, and more
- [Review the Example Files](./examples/) provided through the Atlantis MCP server or to download manually for your project.
- [Visit mcp.atlantis.63klabs.net](https://mcp.atlantis.63klabs.net) for more information about the Atlantis MCP server
- [Visit atlantis.63klabs.net](https://atlantis.63klabs.net) for more information about the 63Klabs Atlantis DevOps Platform for Serverless Deployments on AWS