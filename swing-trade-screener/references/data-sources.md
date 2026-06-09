# Data Sources, Scan Recipes & Gate Checklist

Concrete web sources for running the swing screen on Indian markets. Web layouts and metering change — if a source is blocked or thin, fall back to another. Always cross-check a name on **at least two** sources before naming it. Prefer the most recent data and state its as-of time.

## Table of contents
1. Technical pre-screen sources (Step 1)
2. Per-stock deep-analysis sources (Step 2)
3. Market regime sources (Step 0)
4. Compact gate checklist
5. Search query patterns that work

---

## 1. Technical pre-screen sources (narrow the index → shortlist)

**Chartink** (`chartink.com`) — India's go-to technical screener. Public scan result pages list symbols matching a technical condition. Useful ready-made angles to look for / search:
- "Volume breakout" / "Volume shockers" — stocks trading on volume well above their average.
- "Stocks near 52-week high" / "Breakout above resistance".
- "Bullish stocks above 20 & 50 SMA" / "MACD bullish crossover".
- "RSI above 60" with volume confirmation.
Combine a momentum scan and a volume scan and take the overlap.

**NSE India** (`nseindia.com`) — official, authoritative lists. Look for:
- 52-week high list.
- Top gainers (daily/weekly).
- Most active by volume / by value.
- **Volume gainers** (today's volume vs average) — directly serves Gate 2.
- Delivery % data — high delivery = positional conviction.

**Tickertape / Trendlyne / MoneyControl / Investing.com** — screeners and "top movers" pages with technical filters (above DMA, RSI, breakout, volume surge). Trendlyne also surfaces analyst upgrades and SMA/momentum scores.

> Goal of Step 1: ~10–20 candidates that each show at least one momentum signal AND one volume signal. Drop illiquid/penny/governance-flagged names here, before spending effort on deep analysis.

---

## 2. Per-stock deep-analysis sources (Step 2 — the four gates)

For each shortlisted symbol, gather:

**Price / technicals (Gates 1 & 4):**
- Tickertape, Trendlyne, MoneyControl, Investing.com, TradingView — price vs 20/50/200 DMA, RSI(14), MACD, ADX, 52-week high/low, support/resistance levels, recent chart structure.
- NSE quote page — live-ish price, day range, VWAP.

**Volume / delivery (Gate 2):**
- NSE security-wise delivery data — delivery quantity & % (rising delivery = conviction).
- Any technical page showing volume vs average volume; OBV if available.

**Sentiment / news (Gate 3):**
- `screener.in` — financials, latest results, concall summaries, shareholding (watch promoter pledge %), and a news feed per company.
- Google News / web search for the company name — last 1–2 weeks of headlines: results, orders, upgrades/downgrades, legal/regulatory items.
- Trendlyne / MoneyControl — analyst ratings, target prices, recent upgrades/downgrades.
- Check the **earnings calendar** — is a result due inside the trade horizon? That's a binary risk to flag.

---

## 3. Market regime sources (Step 0)

- NSE / any financial site — **Nifty 50** level vs its 20-DMA and 50-DMA, trend direction over last few weeks.
- **India VIX** — elevated/rising VIX = higher risk, wider stops needed.
- Advance/decline or % of stocks above 50-DMA (market breadth) if available — confirms whether momentum is broad or narrow.

A one-line regime read gates the whole run: favorable (proceed), or unfavorable (be strict / return nothing).

---

## 4. Compact gate checklist

A stock qualifies **only if every box is checked.**

**Gate 1 — Momentum**
- [ ] Price > 20-EMA > 50-EMA (uptrend alignment)
- [ ] RSI(14) ≈ 55–72 (strong, not >78–80 overextended)
- [ ] MACD bullish (line > signal, histogram positive)
- [ ] Within ~7–8% of 52-wk high OR fresh base breakout (closing basis)
- [ ] Outperforming Nifty over 1–3 months

**Gate 2 — Volume**
- [ ] Recent volume expanding vs 20-day avg (~1.5×+ on up/breakout days)
- [ ] Volume rises with price (up days heavier than down days)
- [ ] Delivery % healthy/rising (positional buying)

**Gate 3 — Sentiment**
- [ ] Net-positive recent news (results/orders/upgrades/sector tailwind)
- [ ] No major negative overhang (downgrade, legal/regulatory, pledge spike, governance flag, bad gap-down)
- [ ] No earnings landmine inside horizon (or flagged as key risk)

**Gate 4 — Trade-Viability**
- [ ] Logical entry zone exists (not chasing an extended candle)
- [ ] Stop below a clear technical level, risk reasonable
- [ ] ~5% target reachable below next major resistance (room to run)
- [ ] Risk:Reward ≥ ~1.5:1

---

## 5. Search query patterns that work

- `<COMPANY> share news` / `<SYMBOL> stock news` — recent sentiment.
- `<COMPANY> Q<n> results` — latest earnings reaction.
- `<COMPANY> analyst target price upgrade` — analyst sentiment.
- `<SYMBOL> NSE delivery percentage` — conviction check.
- `Nifty 500 volume breakout stocks today` / `stocks near 52 week high NSE today` — pre-screen.
- `Nifty 50 above 50 DMA trend today` / `India VIX today` — regime.

Keep queries dated/recent ("today", "this week") so you pull current data, not stale cached pages.
