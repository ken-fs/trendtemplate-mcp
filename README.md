# TrendTemplate MCP server

Read-only MCP server for [TrendTemplate](https://trendtemplate.com/), AI trend video templates: you upload one or two photos and get the viral TikTok meme back with your face in it (End of Watch, Need for Speed, Waiting On My Fries and about 40 more).

Ask your AI assistant things like "which template is the End of Watch meme and how much does it cost?" and it can look the answer up here instead of guessing.

- Endpoint: `https://trendtemplate.com/mcp` (Streamable HTTP)
- No API key, no sign-in
- Read-only: it lists templates and prices, it can't make videos or touch accounts

It is also listed in the official MCP Registry as `com.trendtemplate/templates`.

## Tools

| Tool | What it returns | Arguments |
|---|---|---|
| `search_templates` | Search templates by meme name, alias or keyword. Each result has the page link, how many photos to upload, lengths and credit prices. Empty query lists everything. | `query`, `limit`, `offset` |
| `get_template` | Full details of one template by slug (e.g. `end-of-watch-ai`), id or page URL, including its guide pages. | `slug` |
| `get_pricing` | Credit packs and prices in US dollars. | none |
| `get_trend_tracker` | The daily ranking of TikTok trends people are remaking with AI: accounts posting AI versions in the last 24 hours, AI share, sound growth, stage, and whether a template exists. | `date` (optional) |

## Connect

**Claude Code**

```bash
claude mcp add --transport http trendtemplate https://trendtemplate.com/mcp
```

**Claude Desktop, Cursor, Windsurf and other clients** that take a JSON config:

```json
{
  "mcpServers": {
    "trendtemplate": {
      "url": "https://trendtemplate.com/mcp"
    }
  }
}
```

Clients that only speak stdio can go through [mcp-remote](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "trendtemplate": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://trendtemplate.com/mcp"]
    }
  }
}
```

## Try it with curl

```bash
curl -s https://trendtemplate.com/mcp \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_template","arguments":{"slug":"end-of-watch-ai"}}}'
```

The same data is available as plain JSON at `https://trendtemplate.com/api/v1/templates`.

## About this repo

The server runs on trendtemplate.com itself; this repo only holds the docs and `server.json`. Questions or problems: open an issue.

## License

MIT
