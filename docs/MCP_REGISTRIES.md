# YoAuto MCP Registry Publication

YoAuto exposes a remote MCP server at:

```text
https://yoauto.md/api/mcp/openai/sse
```

The OpenAI plugin submission is useful for ChatGPT, but agents discover MCP servers through registries. This public meta-repository exists only for discovery metadata. The private YoAuto backend stays in the private `automarket` repository.

## Current Public Listings

| Registry | Status | Public link |
| --- | --- | --- |
| Official MCP Registry | Active as `io.github.atomix-spec/yoauto-mcp` | https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.atomix-spec/yoauto-mcp |
| Smithery.ai | Published as `atomix-spec/yoauto-mcp` | https://smithery.ai/servers/atomix-spec/yoauto-mcp |
| Glama.ai | Published as `atomix-spec/yoauto-mcp` | https://glama.ai/mcp/servers/atomix-spec/yoauto-mcp |

Do not add OpenAI draft/edit URLs, API keys, verification tokens, `.env` values, customer data, backend logs, or private repository links to this public repository.

## Official Documentation

- YoAuto MCP documentation: https://yoauto.md/api-mcp
- YoAuto MCP documentation: https://yoauto.md/ru/api-mcp
- Production public-safe MCP SSE endpoint: https://yoauto.md/api/mcp/openai/sse

## Official MCP Registry

Metadata lives in the repository root:

```text
server.json
```

The published registry name is:

```text
io.github.atomix-spec/yoauto-mcp
```

Publish manually:

```bash
curl -L "https://github.com/modelcontextprotocol/registry/releases/latest/download/mcp-publisher_$(uname -s | tr '[:upper:]' '[:lower:]')_$(uname -m | sed 's/x86_64/amd64/;s/aarch64/arm64/').tar.gz" | tar xz mcp-publisher
./mcp-publisher login github
./mcp-publisher publish
curl "https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.atomix-spec/yoauto-mcp"
```

Or run the GitHub Actions workflow:

```text
Publish MCP Registry
```

The workflow uses GitHub OIDC and publishes `server.json` without any registry secret.

## Smithery.ai

YoAuto is already hosted, so publish it as a URL-based remote server:

```bash
npm install -g smithery@latest
smithery auth login
smithery mcp publish "https://yoauto.md/api/mcp/openai/sse" -n "atomix-spec/yoauto-mcp"
smithery mcp search "yoauto"
```

After publication, users can add it from Smithery/Cursor/Claude-style clients through Smithery's generated install command.

## Glama.ai

Glama indexes open-source MCP repositories and also surfaces official registry entries. Use maintainer GitHub OAuth and submit:

```text
Repository: https://github.com/atomix-spec/yoauto-mcp
MCP endpoint: https://yoauto.md/api/mcp/openai/sse
Transport: SSE
Name: YoAuto MCP
```

Submission URL:

```text
https://glama.ai/mcp/servers
```

After Glama indexes the repository, verify search by querying YoAuto on Glama and checking that the tool list includes the production MCP tools.

## Smoke Tests

Before publishing or after each deploy:

```bash
curl -i https://yoauto.md/.well-known/openai-apps-challenge
curl -i https://yoauto.md/api/mcp/openai/sse
```

The MCP endpoint must not return a Cloudflare 5xx response. For SSE, keep proxy buffering disabled and ensure the upstream FastMCP process stays open long enough for registry scanners to inspect it.
