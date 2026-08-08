# YoAuto MCP

Official public metadata repository for the YoAuto B2A MCP Gateway.

This repository intentionally contains no backend source code. It exists so MCP registries and agent clients can discover and verify the hosted YoAuto MCP server while the private YoAuto marketplace backend remains closed.

## Production Status

YoAuto MCP is a production remote FastMCP server for AI-agent vehicle marketplace workflows in Moldova. The server is live on the YoAuto domain, published through the main MCP discovery channels, and documented for agent builders.

- 10 production FastMCP tools.
- Remote SSE transport hosted at `yoauto.md`.
- JSON Schema documentation for tool inputs.
- Query auth fallback for MCP clients that cannot set custom headers.
- JSON-RPC 2.0 error payloads for agent-readable failures.
- Public registry listings without exposing backend source code or secrets.

## MCP Endpoint

```text
https://yoauto.md/api/mcp/sse
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
- MCP SSE endpoint: https://yoauto.md/api/mcp/sse
- Official MCP Registry name: `io.github.atomix-spec/yoauto-mcp`
- Smithery: https://smithery.ai/servers/atomix-spec/yoauto-mcp
- Glama: https://glama.ai/mcp/servers/atomix-spec/yoauto-mcp

## Production FastMCP Tools

YoAuto MCP exposes 10 tools for vehicle marketplace workflows:

- Search YoAuto car and vehicle listings.
- Retrieve listing details.
- Review dealer marketplace context.
- Check VIN-history availability.
- Read account credit or energy balance where authorized.
- Save vehicles to an agent's favorites list with notes.
- Retrieve a dealer's current vehicle catalog.
- Request a callback or vehicle inspection appointment.
- Send internal marketplace messages when explicitly requested by the user.
- Start allowed YoAuto energy top-up flows when explicitly requested by the user.

The public documentation page includes per-tool JSON Schemas, accepted enum values, default parameters, authentication options, Energy-cost notes, and JSON-RPC 2.0 error examples.

## Architecture

```text
Private YoAuto backend
  -> hosts production MCP endpoint
  -> https://yoauto.md/api/mcp/sse

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
      "url": "https://yoauto.md/api/mcp/sse"
    }
  }
}
```

## Safety Notes

- Search and lookup tools are read-only.
- Messaging and energy top-up tools are not read-only and should be called only after explicit user intent.
- The MCP server is hosted at `yoauto.md`; this repository only publishes discovery metadata.
- Do not place production tokens, private backend source, database credentials, customer records, or server logs in this repository.

## Registry Publication

See [docs/MCP_REGISTRIES.md](docs/MCP_REGISTRIES.md).
