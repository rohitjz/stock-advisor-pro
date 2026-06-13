---
name: idea-generation
description: Stock screening and idea sourcing that combines quantitative screens, scanners, and thematic sweeps to surface a shortlist with exact levels. Use to run a screen, find new ideas, or do a thematic sweep. Triggers on "idea generation", "stock screen", "find ideas", "what looks interesting", "screen for", "new ideas", "pitch me something".
---

# Idea Generation

Surface candidates from screens and scanners, then hand back a shortlist where every name carries a metric line and exact levels. Screens surface candidates, not conclusions; each one still needs fundamental work.

## Workflow

### Step 1: Define criteria

Confirm: direction (long, short, or both), market-cap band, sector or cross-sector, style (value, growth, quality, special situation, event-driven), geography, and any thematic angle (AI, reshoring, aging demographics). If the user gives nothing, default to a large-cap quality screen.

### Step 2: Run the screens and scanners

Map the style to the free toolset:

- Movers and momentum: `mcp__tradingview__top_gainers` and `top_losers` for what is leading and lagging now.
- Rating filter: `mcp__tradingview__rating_filter` to pull names by technical rating (rough proxy for sentiment; live sell-side consensus is not available).
- Volume and breakout: `mcp__tradingview__volume_breakout_scanner` and `smart_volume_scanner` for names breaking out on real participation, not thin tape.
- Mean reversion and stretch: `mcp__tradingview__bollinger_scan` for names at or outside the bands (stretched up = caution, washed-out down = watch for basing).
- Fundamentals overlay for the covered names only (AAPL, GOOGL, NVDA, TSLA): `mcp__financial-datasets__get_income_statements`, `get_balance_sheets`, `get_cash_flow_statements` to check growth, margins, leverage, and FCF on anything that screens through.

Style cues: value leans on cheap multiples, FCF yield above 5%, insider buying; growth on revenue above 15% and earnings above 20% YoY with acceleration and expanding margins; quality on 5-plus years of consistent growth, ROE above 15%, low debt, high FCF conversion; short on decelerating revenue, margin compression, receivables or inventory rising vs. sales, valuation premium without justification, accounting red flags.

### Step 3: Thematic sweep

For a thematic idea: state the thesis, map the value chain (direct vs. indirect beneficiaries), separate pure-play from diversified exposure, judge what is already priced in vs. under-appreciated, and look for second-order beneficiaries the market has not connected to the theme yet.

### Step 4: Validate each candidate against the house rules

Before a name makes the shortlist, pull `mcp__tradingview__combined_analysis` for its technical posture and apply the filters:

- No rally chasing. If a long candidate is overextended (RSI above 70, above the upper Bollinger band, or more than 5% above the 20 SMA), it does not make the list as a buy-now; flag it as "wait for an EMA20 or EMA50 pullback" with the pullback zone as the entry.
- No falling knives. A name in freefall needs basing or a resistance reclaim first; until then it is a watch, not a buy.
- Retail dip-buying is contrarian. Heavy Reddit dip-buying in `market_sentiment` is a caution flag, not confirmation.
- Avoid crowded trades. Check how stretched and how widely owned the name already is. Short ideas need higher conviction; timing is harder and risk is asymmetric.

### Step 5: Build the shortlist

For each surviving name, one line of metrics plus exact levels:

**[TICKER] - [Long/Short] - [one-line thesis hook]** | metric line (cap, valuation, growth, margin, FCF yield where sourceable, or the screen signal that surfaced it) | Entry [zone], Stop [level], Target 1 [level] | confidence and the catalyst.

## Output

A shortlist of 5 to 10 names in the format above, the screen criteria and tools used stated up top, and a prioritized "research first" order. Contrarian names without a catalyst get downgraded; early without a catalyst is the same as wrong. End with: Not financial advice.

## Data and limits

Uses `mcp__tradingview__{top_gainers, top_losers, rating_filter, volume_breakout_scanner, smart_volume_scanner, bollinger_scan, combined_analysis, market_sentiment}` for screening and posture; `mcp__financial-datasets__*` statements for fundamentals on AAPL, GOOGL, NVDA, TSLA only. Cannot source: live sell-side consensus or price targets, options flow, short-interest feeds, insider-transaction feeds, fundamentals for tickers outside the covered four (request inputs rather than invent). Flag every data gap on the shortlist.
