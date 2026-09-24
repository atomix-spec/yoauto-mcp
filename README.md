# YoAuto MCP

Official public metadata repository for the YoAuto B2A MCP Gateway.

This repository intentionally contains no backend source code. It exists so MCP registries and agent clients can discover and verify the hosted YoAuto MCP server while the private YoAuto marketplace backend remains closed.

## Production Status

YoAuto MCP is a production remote FastMCP server for AI-agent vehicle marketplace workflows in Moldova. The server is live on the YoAuto domain, published through the main MCP discovery channels, and documented for agent builders.

- Production FastMCP tools for vehicle discovery and marketplace workflows.
- Public-safe remote SSE transport hosted at `yoauto.md`.
- JSON Schema documentation for tool inputs.
- Query auth fallback for MCP clients that cannot set custom headers.
- JSON-RPC 2.0 error payloads for agent-readable failures.
- Public registry listings without exposing backend source code or secrets.

## MCP Endpoint

```text
https://yoauto.md/api/mcp/openai/sse
```

Transport:

```text
SSE
```

Registry name:

```text
io.github.atomix-spec/yoauto-mcp
```

## Public Links

- GitHub: https://github.com/atomix-spec/yoauto-mcp
- YoAuto MCP docs: https://yoauto.md/api-mcp
- YoAuto MCP docs: https://yoauto.md/ru/api-mcp
- MCP SSE endpoint: https://yoauto.md/api/mcp/openai/sse
- Official MCP Registry name: `io.github.atomix-spec/yoauto-mcp`
- Smithery: https://smithery.ai/servers/atomix-spec/yoauto-mcp
- Glama: https://glama.ai/mcp/servers/atomix-spec/yoauto-mcp

## Production FastMCP Tools

YoAuto MCP exposes public-safe tools for vehicle marketplace workflows:

- Search YoAuto car and vehicle listings.
- Retrieve listing details.
- Review dealer marketplace context.
- Check VIN-history availability.
- Retrieve general YoAuto marketplace information.

The public documentation page includes per-tool JSON Schemas, accepted enum values, default parameters, authentication options, and JSON-RPC 2.0 error examples.

## Architecture

```text
Private YoAuto backend
  -> hosts production MCP endpoint
  -> https://yoauto.md/api/mcp/openai/sse

Public yoauto-mcp repository
  -> publishes server.json and documentation
  -> used by Official MCP Registry, Smithery, and Glama
```

## Installation

For MCP clients that support remote SSE servers:

```json
{
  "mcpServers": {
    "yoauto": {
      "type": "sse",
      "url": "https://yoauto.md/api/mcp/openai/sse"
    }
  }
}
```

## Safety Notes

- Search and lookup tools are read-only.
- The public registry endpoint intentionally exposes only search and lookup workflows.
- The MCP server is hosted at `yoauto.md`; this repository only publishes discovery metadata.
- Do not place production tokens, private backend source, database credentials, customer records, or server logs in this repository.

## Registry Publication

See [docs/MCP_REGISTRIES.md](docs/MCP_REGISTRIES.md).
