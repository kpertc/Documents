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
- `uvx` = `uv tool run` (ephemeral isolated env — why MCP server configs use it; `uv run` runs inside the current project env)

Server
- Tools
- Resource - data / database
- Prompts

Client
- Sampling - server ask client to run an LLM completion for it
- Roots - filesystem scope
- Elicitation - server ask user for more information

```

```

transportType: `stdio` `Streamable HTTP` (HTTP+SSE deprecated in spec rev 2025-03-26, kept only for backwards compat) 


Markets:
https://mcp.so/
https://mcpmarket.com/
https://smithery.ai/