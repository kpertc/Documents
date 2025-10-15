"API" for LLM?
like REST API / GraphQL

> MCP (Model Context Protocol) is an open-source standard for connecting AI applications to external systems.
> https://modelcontextprotocol.io/

[What is the Model Context Protocol (MCP)?](https://modelcontextprotocol.io/docs/getting-started/intro)

MCP Host (LLM)

MCP Clients
↓
MCP Protocol (API / “USB-C”)
↓
MCP Servers (functions)

mostly written with Python and Node.js
- `uvx` = `uv run`

Server
- Tools
- Resource - data / database
- Prompts
- Samplings - server ask client for more information

```

```

transportType: `stdio` `SSE` (Server-Sent Events) 


Markets:
https://mcp.so/
https://mcpmarket.com/
https://smithery.ai/