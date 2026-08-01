# Atlantis MCP

The Atlantis MCP server provides AI-assisted development tools for the 63Klabs Atlantis DevOps Templates and Scripts Platform. Discover, validate, and utilize CloudFormation templates, starter code, and documentation. 

- [Learn more about the Atlantis MCP Server](https://mcp.atlantis.63klabs.net/)
- [Complete information about integrating Atlantis MCP with Kiro](https://mcp.atlantis.63klabs.net/docs/integration/kiro.html)

```json
{
  "mcpServers": {
    "atlantis": {
      "url": "https://mcp.atlantis.63klabs.net/mcp/v1",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Adding Your API Key

[Register for a free account](https://mcp.atlantis.63klabs.net/register/) to get an API key with higher [rate limits](https://mcp.atlantis.63klabs.net/docs/rate-limits/). After registration, copy your unique API key and add it to the configuration:

```json
{
  "mcpServers": {
    "atlantis": {
      "url": "https://mcp.atlantis.63klabs.net/mcp/v1",
      "headers": {
        "x-api-key": "atl_your_api_key_here"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

If you need to regenerate your key, visit your [profile page](https://mcp.atlantis.63klabs.net/profile/).

## Auto-Approve Tools

Configure which tools run without confirmation:

```json
{
  "mcpServers": {
    "atlantis": {
      "url": "https://mcp.atlantis.63klabs.net/mcp/v1",
      "disabled": false,
      "autoApprove": [
        "validate_naming",
        "list_categories",
        "list_templates",
        "get_template",
        "list_template_versions",
        "list_tools",
        "list_starters",
        "get_starter_info",
        "search_documentation",
        "check_template_updates",
        "get_template_chunk"
      ]
    }
  }
}
```