# YoAuto MCP

Official public metadata repository for the YoAuto B2A MCP Gateway.

This repository intentionally contains no backend source code. It exists so MCP registries and agent clients can discover and verify the hosted YoAuto MCP server while the private YoAuto marketplace backend remains closed.

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
- MCP SSE endpoint: https://yoauto.md/api/mcp/sse
- Official MCP Registry name: `io.github.atomix-spec/yoauto-mcp`
- Smithery: https://smithery.ai/servers/atomix-spec/yoauto-mcp
- Glama: https://glama.ai/mcp/servers/atomix-spec/yoauto-mcp

## What Agents Can Do

YoAuto MCP exposes tools for vehicle marketplace workflows:

- Search YoAuto car and vehicle listings.
- Retrieve listing details.
- Review dealer marketplace context.
- Check VIN-history availability.
- Read account credit or energy balance where authorized.
- Send internal marketplace messages when explicitly requested by the user.
- Start allowed YoAuto energy top-up flows when explicitly requested by the user.

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
