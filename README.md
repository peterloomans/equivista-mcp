# Equivista MCP

[![Equivista MCP on AI Agents Listing](https://aiagentslisting.com/equivista-mcp/badge.svg?claim=e965951f2c08a1fdf598463669c6ce4c)](https://aiagentslisting.com/mcp/equivista-mcp)

Read-only Belgian company search, KBO data, financials, employees and company relationships.

[Documentation](https://equivista.be/api/docs) · [Website](https://equivista.be) · [Official registry](https://registry.modelcontextprotocol.io/v0.1/servers/io.github.peterloomans%2Fequivista/versions/latest)

This repository contains public integration documentation, client configurations and draft plugin metadata. The hosted service implementation is maintained separately. The MIT license covers this repository's integration files; it does not license the hosted service or underlying datasets.

## Connect

- Transport: Streamable HTTP
- Endpoint: `https://equivista.be/mcp`
- No local installation, npm package, Python package or Docker image is needed.
- Optional authentication: `Authorization: Bearer YOUR_API_KEY`. Never commit a real key.

For Cursor, add this to your MCP settings:

```json
{"mcpServers":{"equivista":{"url":"https://equivista.be/mcp"}}}
```

For authenticated use, add `"headers": {"Authorization": "Bearer YOUR_API_KEY"}` to the server configuration and replace the placeholder locally. Omit the entire header for anonymous use; an empty or invalid token returns an authentication error.

API keys are created from a confirmed Equivista account. See the [public documentation](https://equivista.be/api/docs) for current registration and account links; contact [Equivista support](https://equivista.be/en/contact) if registration is unavailable.

## Tools

| Tool | Purpose |
| --- | --- |
| `search_companies` | Exact and fuzzy Belgian company-name search |
| `get_company` | KBO profile, address, legal form and NACE codes |
| `get_financials` | Annual financial summary |
| `get_employees` | Average/closing employment, FTE, movements, hours and personnel costs |
| `get_mandates` | Current mandates in a company |
| `get_held_mandates` | Current mandates held in other companies |
| `get_shareholders` | Latest-known shareholders |
| `get_participations` | Latest-known company participations |

Use a Belgian company number such as `0550639702`. Company lookups accept dots, spaces and a BE prefix. `locale` is `nl`, `fr` or `en` where supported. Optional `year` is the accounting closing year; omission selects the latest available filing.

## Limits and data handling

Search Belgian companies and retrieve KBO profiles, annual financial summaries, employment figures, current mandates, shareholders and participations. Equivista provides eight read-only MCP tools over a hosted HTTPS endpoint. Data comes from the existing Equivista database; requests do not trigger live scraping. Dutch, French and English are supported where available. Anonymous access allows one distinct data-bearing request per IP per day. Confirmed accounts can create API keys; new accounts have five daily requests shared across their keys and endpoints. Higher limits require contacting Equivista. Missing data is not invented, and this service does not provide financial advice.

Same-day identical requests replay their saved response without another daily use. Quotas reset at midnight Europe/Brussels. Requests and key usage are subject to the [privacy policy](https://equivista.be/en/privacy) and [terms](https://equivista.be/en/terms-and-conditions).

## Example prompts

- Find Lexgo Belgium by name.
- Look up Belgian company 0550639702 in English.
- Get the latest financial summary for company 0550639702.
- Show current mandates for company 0550639702.

## Client and marketplace files

- `.cursor/mcp.json`: Cursor client configuration.
- `.mcp.json`: Claude Code client configuration.
- `gemini-extension.json`: Gemini CLI extension manifest.
- `plugin.json` and `mcp.json`: portable plugin draft for ChatGPT/Codex.
- `.cursor-plugin/plugin.json`: Cursor Marketplace plugin draft.
- `server.json`: published official registry metadata.

Marketplace review is separate from client configuration. Draft metadata does not imply marketplace approval or completed client testing. The OpenAI and Claude no-auth routes can access public data, but their reviewer workflows need enough quota. Authenticated marketplace use may require OAuth; do not publish a shared API key.

## Privacy policy

See [Equivista's privacy policy](https://equivista.be/en/privacy). Support: [contact@equivista.be](mailto:contact@equivista.be).
