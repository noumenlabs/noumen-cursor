# Noumen for Cursor

Live on-chain data and a second-opinion model router for your coding agent.

- **22 free data tools, no key needed:** tokens, wallets and chains on Solana, Ethereum, Base, BNB Chain and Robinhood Chain, plus tokenized stocks and real-world assets on Robinhood Chain.
- **Noumen's AI models while you code:** ask one model for a review, or compare up to four, billed per token to your Noumen API key.

The plugin connects Cursor to Noumen's hosted MCP server at `https://www.noumen.xyz/api/mcp`. Nothing is installed and nothing runs on your machine.

## What's inside

| Component | What it does |
|---|---|
| MCP server `noumen` | The hosted Noumen MCP server |
| Skill `onchain-research` | Due diligence on a token, chain scans, wallet profiles, and checking a token contract before you write code against it |
| Skill `stock-research` | Tokenized stocks and RWAs: quotes, scans, charts, earnings, news and on-chain supply |
| Skill `second-opinion` | Ask another model to review your code, or compare several, and report the cost |
| Rule `noumen` | When to reach for Noumen, never to paste secrets or handle a private key, and to report what model calls cost |

### Tools

| Tool | Key | Cost |
|---|---|---|
| `list_models` | no | free |
| `token_search`, `token_overview`, `token_holders`, `token_holder_group`, `token_social`, `token_chart`, `token_contract` | no | free |
| `token_trending`, `token_hot`, `token_rank`, `token_signals`, `wallet_profile`, `market_overview`, `chain_activity` | no | free |
| `stock_search`, `stock_scan`, `stock_quote`, `stock_chart`, `stock_technicals`, `stock_earnings`, `stock_news`, `stock_onchain` | no | free |
| `ask` | yes | per token |
| `compare` (2 to 4 models) | yes | per token, per model |
| `balance` | yes | free |

Free tools allow 60 calls an hour per address without a key, and 60 a minute per key.

## Install

Once listed, install **Noumen** from the Cursor Marketplace or [cursor.directory](https://cursor.directory).

Or from this repository:

```bash
git clone https://github.com/noumenlabs/noumen-cursor ~/.cursor/plugins/local/noumen
```

Then run **Developer: Reload Window**.

To add only the MCP server, open this link in a browser with Cursor installed:

```
cursor://anysphere.cursor-deeplink/mcp/install?name=noumen&config=eyJ1cmwiOiJodHRwczovL3d3dy5ub3VtZW4ueHl6L2FwaS9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgJHtlbnY6Tk9VTUVOX0FQSV9LRVl9In19
```

## Try it, then add a key

With nothing configured, every data tool and `list_models` work. Ask the agent something like:

- "What is trending on Solana right now, and is the top token safe to research?"
- "Before I hard-code this token address, check its decimals, owner and authorities on Base."
- "Quote NVDA on Robinhood Chain and tell me its premium to the share."

`ask`, `compare` and `balance` need a Noumen API key (`nm_sk_…`):

- **Free demo key:** 24 hours, $0.02 of usage, answers up to 1,024 tokens. Create one at [noumen.xyz/docs](https://www.noumen.xyz/docs#try), or:

  ```bash
  curl -X POST https://www.noumen.xyz/api/demo/keys
  ```

- **Prepaid key:** sign in at [noumen.xyz](https://www.noumen.xyz), fund your balance, and create a key under **API access** with its own spending limit and model allowlist.

Set it in your environment, then restart Cursor:

```bash
export NOUMEN_API_KEY=nm_sk_...
```

The plugin sends it as `Authorization: Bearer $NOUMEN_API_KEY`. A wrong or expired key is reported on every tool call, so unset the variable to go back to the free tools.

Then try: "Ask a Noumen reasoning model to review this function for edge cases."

## Fewer tools

26 tools take room in the agent's context. To load only some groups, edit the URL in `mcp.json`:

| URL | Tools |
|---|---|
| `https://www.noumen.xyz/api/mcp?tools=models` | `list_models`, `ask`, `compare`, `balance` |
| `https://www.noumen.xyz/api/mcp?tools=token` | the 14 token, wallet and chain tools |
| `https://www.noumen.xyz/api/mcp?tools=stock` | the 8 stock and RWA tools |
| `https://www.noumen.xyz/api/mcp?tools=models,token` | any combination |

You can also turn single tools off in Cursor's **Customize** page.

## Other agents

The same server works in any MCP client that speaks Streamable HTTP.

**Claude Code**

```bash
claude plugin marketplace add noumenlabs/noumen-cursor
claude plugin install noumen@noumen
```

Or the server alone:

```bash
claude mcp add --transport http noumen https://www.noumen.xyz/api/mcp --header "Authorization: Bearer $NOUMEN_API_KEY"
```

**Any other client**

```json
{
  "mcpServers": {
    "noumen": {
      "url": "https://www.noumen.xyz/api/mcp",
      "headers": { "Authorization": "Bearer <your nm_sk_ key, or leave the header out>" }
    }
  }
}
```

## Billing and privacy

- Data tools are free. `ask` and `compare` are billed per token at the prices `list_models` shows. Each result reports the tokens, an estimated cost (an upper bound at listed prices) and a usage ID; the final charge settles within minutes and shows in `balance` and in the Noumen app.
- Your key's spending limit, model allowlist and the account's monthly limit apply to every call.
- Noumen's ledger records each request's model, tokens and cost, not its text. To answer, prompts are sent to third-party model providers.
- Cursor itself sees your prompts and the answers, since that is where they come from and go to.
- Market data is a snapshot and is research, not financial advice.

## Links

[noumen.xyz](https://www.noumen.xyz) · [Docs](https://www.noumen.xyz/docs) · [Models](https://www.noumen.xyz/models) · [@NoumenLabs on X](https://x.com/NoumenLabs)

## License

MIT
