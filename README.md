# ClickDrag Finance: cost segregation tools for assistants and agents

A remote [Model Context Protocol](https://modelcontextprotocol.io) server, an [Agent Plugins](https://agent-plugins.org) package and a Claude skill that let an AI assistant estimate, price and request a cost segregation workpaper or study for US rental and commercial property.

ClickDrag Finance runs the server. This repository holds only the manifests and the skill that point an assistant at it; there is no code to install and no API key.

## Connect

**MCP server (Streamable HTTP):** `https://www.clickdragfinance.com/api/mcp`

```bash
claude mcp add --transport http clickdrag https://www.clickdragfinance.com/api/mcp
```

Any MCP client that supports remote servers over Streamable HTTP (MCP protocol 2025-03-26 or later) can add the same URL. No account and no API key are needed. If MCP is not available, the same operations are plain HTTP; the OpenAPI 3.1 spec is at <https://www.clickdragfinance.com/openapi.json>.

**Claude plugin:**

```
/plugin marketplace add CostSeg-Solutions/clickdrag-agent-tools
/plugin install clickdrag-cost-segregation@clickdrag-finance
```

## Tools

| Tool | What it does | Side effects |
|---|---|---|
| `quote_cost_segregation_study` | Estimates first-year depreciation with and without a study on one US property, and the 5-, 7-, 15- and 27.5- or 39-year split | None |
| `get_cost_segregation_pricing` | Prices in USD for the low-cost cost segregation workpaper and the cost segregation study | None |
| `get_cost_segregation_benchmarks` | Allocation planning bands by property type, with a citation string. Each is a planning band, not a promise, and not a measurement of our delivered studies or an industry survey; published under CC BY 4.0 | None |
| `get_cost_segregation_provider_facts` | Who prepares and reviews each product, who signs a study, what each includes, and the refund policy | None |
| `book_cost_segregation_consult` | Requests a consultation: returns a scheduling link and a reference code. An email address is required | **Records a lead and emails the person's details to the ClickDrag Finance team. Not idempotent: two calls make two requests.** Call it only when the person has asked to speak to someone |

What these tools cannot do:

- **They cannot sell anything.** There is no payment tool, so neither the workpaper nor a study can be bought through them; `get_cost_segregation_pricing` returns each product, its price and the property size it suits.
- **They give no tax advice.** Everything returned is educational.
- **An estimate is not a completed study.** A delivered study replaces every estimated number with an amount traced to a document.

## What is in this repository

| File | Purpose |
|---|---|
| `server.json` | The entry for the [official MCP Registry](https://registry.modelcontextprotocol.io) (`com.clickdragfinance/cost-segregation`) |
| `plugin.json`, `mcp.json` | The Agent Plugins package, including the ChatGPT and Codex listing fields |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json` | The Claude plugin and its marketplace entry |
| `skills/clickdrag-cost-segregation/SKILL.md` | The Claude skill: when to use each tool and the conditions that change the answer |
| `assets/icon.png` | The icon |

Every file except this README, the LICENSE and the icon is generated from the server's contract (the version in `server.json`) and copied here unchanged. If a file here disagrees with the live server, the live server is right: its MCP `tools/list` reply and <https://www.clickdragfinance.com/openapi.json> are the authority.

## Links

- Developer documentation: <https://www.clickdragfinance.com/developers>
- Integration guide: <https://www.clickdragfinance.com/agents>
- Privacy: <https://www.clickdragfinance.com/privacy> · Terms: <https://www.clickdragfinance.com/terms>
- Support: <https://www.clickdragfinance.com/support> · howard@clickdragfinance.com

## License

The files in this repository are released under the [MIT License](LICENSE), except the ClickDrag Finance name and the icon in `assets/`, which identify ClickDrag Finance and are not licensed for other use. Use of the server itself is governed by the ClickDrag Finance [terms](https://www.clickdragfinance.com/terms).
