---
name: stock-research
description: Look up tokenized stocks and real-world assets (index funds, treasuries, commodities, credit) on Robinhood Chain with Noumen's stock tools. Use for a quote, a session scan, charts and indicators, earnings, news, or the token's on-chain supply, holders, pools and share multiplier.
---

# Tokenized stocks and RWAs with Noumen

All `stock_` tools are free and work without a key.

## When to use

- The user asks about a tokenized stock or ETF (NVDA, SPY, GLD, SGOV and others) or a real-world asset token on Robinhood Chain.
- The user wants to know how a token trades against its underlying share, or what moved today.
- You are building something that reads these tokens and need their addresses, multipliers or pools.

## Instructions

1. `stock_search` by ticker or name (optionally an asset class), or `stock_scan` to rank today's gainers, losers, widest ranges or halted listings.
2. `stock_quote` for the price, the session, the token's premium or discount to its share, and how unusual the move is.
3. `stock_chart` and `stock_technicals` for the path and indicators; `stock_earnings` and `stock_news` for the company.
4. `stock_onchain` for the token's supply, holders, liquidity, pools and the ERC-8056 share multiplier.

## Rules

- Session, indicator and earnings figures describe the underlying share on its US exchange. The token quote and everything `stock_onchain` reports describe the token on chain. Keep the two apart and say which one a figure belongs to.
- A pool price is per raw token; multiply by the share multiplier before comparing it with the share price.
- Indicator thresholds are conventions, not predictions, and headlines are not verified causes. This is research, not financial advice.
