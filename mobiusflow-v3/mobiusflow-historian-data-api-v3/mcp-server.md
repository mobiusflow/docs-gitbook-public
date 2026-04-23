---
description: Details of the Historian MCP Server for use with AI LLMs / Agents
---

# MCP Server

The historian MCP is hosted as part of the Historian Data API on the following endpoint:

```
/api/historian/v3/mcp
```

Please note that the server does not support connection via the deprecated STDIO standard.

## Authentication

Authentication works in the same way as all calls in the Historian Data API. You must include _x-api-key_ as a header:

```
x-api-key: YOUR_KEY
```

Keys can be managed via the MobiusFlow View application.

## Tools

All tools are exposed when connecting to the MCP server. Currently available tools include:

* get-all-objects-name-uri-map
* get-closest-matching-object-by-name
* get-telemetry-for-mulitple-series
* get-profiles

Input formats for all tools can be obtained by connecting to the MCP server.

Documentation for output formats is coming soon, however is not normally required for agentic application.
