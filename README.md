# Stock Advisor Pro

![License](https://img.shields.io/badge/license-Apache--2.0-blue) ![Claude Code](https://img.shields.io/badge/Claude%20Code-plugin-8A2BE2)

Pro-grade equity research and valuation, as agents and skills for [Claude Code](https://claude.com/claude-code). Free to run: no Bloomberg, no FactSet, no enterprise data contract.

Anthropic ships a polished finance agent suite in [anthropics/financial-services](https://github.com/anthropics/financial-services), but its agents are wired to paid enterprise connectors (S&P Capital IQ, FactSet, Daloopa, Bloomberg, Morningstar, PitchBook). This is that workflow, rebuilt on free market data so anyone can run it.

> Educational and informational only. **Not financial advice.**

## What you get

**2 agents**

| Agent | Does |
|---|---|
| `market-researcher` | Sector or theme to an industry overview, competitive map, peer comps, and an ideas shortlist with exact entry, stop, and target levels |
| `model-builder` | DCF, LBO, three-statement, and comps models from a ticker and an assumption set |

**10 skills**: sector-overview, competitive-analysis, comps-analysis, idea-generation, dcf-model, lbo-model, 3-statement-model, earnings-analysis, initiating-coverage, thesis-tracker

**7 commands**: `/sector` `/screen` `/comps` `/dcf` `/earnings` `/initiate` `/thesis`

## How it is wired

| Original (paid) | Here (free) |
|---|---|
| S&P Capital IQ, FactSet, Daloopa, Bloomberg | TradingView MCP + Financial Datasets MCP |
| SEC EDGAR connector | Financial Datasets `get_sec_filings` |
| Live sell-side consensus | TradingView ratings and sentiment, flagged as a proxy |
| Excel / Office add-in | Markdown tables (optional headless `.xlsx`) |

Every skill carries the house rules a careful investor wants: exact price levels rather than a vague direction, a push back on a "STRONG BUY" when a name is overextended (RSI above 70, above the upper Bollinger band, more than 5% over the 20-day SMA), no rally chasing, no catching falling knives, and an explicit data-gap flag on every output.

## Install

### Prerequisites: two free MCP servers

1. **TradingView** (no key). Runs via `uvx`, package `tradingview-mcp-server`.
2. **Financial Datasets** (free key). Grab a free key at [financialdatasets.ai](https://financialdatasets.ai) and run the Financial Datasets MCP server. The free tier covers AAPL, GOOGL, NVDA, and TSLA.

Copy [`.mcp.json.example`](.mcp.json.example) to `.mcp.json` in your project, then fill in the path and the key.

### Option A: install as a plugin

```
claude plugin marketplace add rohitjz/stock-advisor-pro
claude plugin install stock-advisor-pro@stock-advisor-pro
```

### Option B: copy the files

Drop `agents/`, `skills/`, and `commands/` into your project's `.claude/` directory.

## Use it

```
/sector semiconductors
/screen high free-cash-flow large caps
/comps NVDA AMD AVGO
/dcf NVDA
/earnings TSLA Q1-2026
/initiate GOOGL
/thesis NVDA
```

Or hand a full job to an agent:

> Use the model-builder agent to build a DCF for NVDA.
> Use the market-researcher agent for the US power and grid theme.

## Free-tier honesty

- Statement-level fundamentals cover **AAPL, GOOGL, NVDA, TSLA** only. For any other ticker, the model and comps skills ask you for inputs instead of inventing them.
- No live sell-side consensus or analyst price targets. The earnings and coverage skills say so and use a sentiment proxy.
- No options flow.
- News and Reddit feeds can return empty. The skills flag that rather than filling the silence.

## Credit and license

Adapted from Anthropic's [anthropics/financial-services](https://github.com/anthropics/financial-services) (Apache-2.0). The agent and skill definitions here are derivative works with the data layer rewired to free sources. Licensed under Apache-2.0; see [LICENSE](LICENSE) and [NOTICE](NOTICE).

Markets carry risk. Do your own work. Not financial advice.
