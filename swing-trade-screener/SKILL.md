---
name: swing-trade-screener
description: Screen the Indian stock market (NSE/BSE) for swing-trade setups that combine strong positive sentiment, price momentum, and rising volume, and return a full trade plan (entry, stop-loss, ~5% target, position sizing) only for stocks that clear every technical gate. Built for a trader targeting ~5% per trade per month who wants disciplined, capital-protecting selection — if nothing qualifies, it returns NO stock names and explains why. Use this skill whenever the user asks to find swing trades, momentum stocks, breakout candidates, stocks with bullish sentiment, "what should I buy this month", high-volume movers, or any technical/sentiment-driven stock screen on Indian markets. Triggers on phrases like "find me swing trades", "screen for momentum stocks", "which stocks have strong sentiment and volume", "give me a trade idea for 5% this month", "scan Nifty for breakouts", "swing picks", even if the user never says the word "skill". Indian (NSE/BSE) markets, web-sourced data.
---

# Swing Trade Screener (Indian Markets)

Find Indian-listed stocks that are set up for a swing trade — a multi-day to few-week hold targeting roughly **5%**, selected because **sentiment is positive, price momentum is strong, and volume is expanding**. The output is a concrete trade plan per qualifying stock, or an honest "nothing qualifies today" if the setups aren't there.

This skill reads public web data (screeners, NSE, news) and writes/returns analysis. **It does not place trades and is not SEBI-registered investment advice** — it is a disciplined screening assistant. The user makes the final call and verifies live prices with their broker before acting.

## The one rule that matters most

**Never force a pick.** A clean swing setup with positive sentiment, real volume, and a sane risk/reward toward 5% is not available every day, and certainly not for every stock. The fastest way to lose money in momentum trading is to trade when there's no edge. So:

- A stock is named **only if it clears ALL four gates** (Momentum, Volume, Sentiment, Trade-Viability — defined below).
- If zero stocks clear all gates, **return no names.** Say so plainly, name the gate the near-misses failed on, and tell the user to wait. This is the skill working correctly, not failing.
- Quality over quantity: 0–3 high-conviction names beats a long list of marginal ones. Cap output at the **top 5** even on a strong day.

## Inputs

- **Universe** (default: **Nifty 500**). The user may instead pass a smaller index (Nifty 50 / Nifty 100 / Nifty Midcap 150) or their own watchlist of NSE symbols. A tighter universe = a faster, more thorough run.
- **Target** (default: ~5% per trade). Used to size the take-profit and judge risk/reward.
- **Risk per trade** (default: assume 1–2% of capital at risk; mention it but the user sets the rupee amount).

If the user just says "find me swing trades" with no universe, default to Nifty 500 and proceed — don't block on questions.

## Workflow

The screen is a funnel: start wide and cheap, end narrow and deep. Don't try to deep-analyze 500 stocks — that's neither feasible nor useful. Let pre-built screeners do the wide filtering, then spend your effort on the survivors.

### Step 0 — Market regime check (do this first, always)

Swing-long momentum strategies have poor odds when the broad market is falling — you'd be buying strength into a tape that drags everything down. Before screening anything, check the **Nifty 50 index** trend (`WebFetch` NSE / a financial site):

- Is Nifty above or below its 20-DMA and 50-DMA? Rising or falling? Where's India VIX?
- **Uptrend / sideways-up:** proceed normally.
- **Clear downtrend (Nifty below 50-DMA and falling):** raise the bar. Be extra strict, prefer defensive/relative-strength leaders only, and be ready to return nothing. Tell the user the regime is unfavorable.

State the regime in one line at the top of the output — it frames everything.

### Step 1 — Technical pre-screen (narrow the index to a shortlist)

Use ready-made Indian technical screeners to pull a candidate list of stocks already showing momentum + volume, instead of scanning the index by hand. See `references/data-sources.md` for concrete sources, Chartink scan recipes, and NSE list URLs.

Aim for a shortlist of roughly **10–20 candidates** that already show at least one momentum signal AND one volume signal, e.g.:
- Trading near 52-week highs / breaking out of consolidation
- Above 20 & 50 DMA
- Volume surge (well above the 20-day average) on an up move

Pull from a couple of independent sources and take the intersection/union sensibly — don't rely on a single page that might be stale or thin. Drop anything illiquid (very low average traded value), penny stocks, or names with known governance flags before deep analysis.

### Step 2 — Deep analysis of each candidate (the four gates)

For each shortlisted candidate, gather data and judge it against all four gates. A stock must pass **every** gate to qualify. Be skeptical — it's cheaper to reject a marginal name now than to lose on it later.

**Gate 1 — Price Momentum** (is the trend strong and intact?)
- Price above 20-EMA and 50-EMA, with 20 above 50 (uptrend alignment).
- RSI(14) roughly **55–72**: strong, but not a blow-off (RSI >78–80 is overextended → caution, late entry risk).
- MACD bullish (line above signal, histogram positive/expanding).
- Near a breakout: within ~7–8% of the 52-week high, or freshly breaking a multi-week base on a closing basis.
- Relative strength: outperforming Nifty over the last 1–3 months. A leader, not a laggard.
- *Why:* swing trades ride existing momentum. You want a stock the market is already voting up, caught early in a move — not extended, not broken.

**Gate 2 — Volume** (is the move backed by real participation?)
- Recent volume **expanding** vs the 20-day average (a surge of ~1.5×+ on the breakout/up days is a healthy sign).
- Volume rises *with* price — up days on heavier volume than down days. Price up on shrinking volume is a warning (no conviction).
- Indian edge: **delivery %** rising (high delivery = positional buying, not just intraday churn). Check NSE delivery data where available.
- *Why:* the user explicitly wants increasing volume. Volume is the fuel; a breakout without it tends to fail and trap buyers.

**Gate 3 — Sentiment** (is the news/positioning net positive, with no landmine?)
- Recent news flow net positive: strong results, order wins, guidance upgrades, analyst upgrades / rising target prices, sector tailwind.
- **No major negative overhang:** pending bad news, downgrades, regulatory/legal trouble, a spike in promoter share pledging, auditor/governance red flags, or a sharp recent gap-down on bad news.
- Sector is in favor (sector momentum supports the name).
- **Earnings awareness:** if results are due within the trade horizon, flag it — earnings are a binary event that can blow through a stop. Prefer setups with no earnings landmine inside the hold, or note it as a key risk.
- *Why:* momentum + volume can be a pump or a trap. Positive, clean sentiment is what makes the move likely to be *sustained* rather than a one-day spike.

**Gate 4 — Trade-Viability** (does a real ~5% trade exist with sane risk?)
- A logical **entry zone** exists — near support, a breakout level, or a shallow pullback. Not chasing a vertical, extended candle.
- A defined **stop-loss** sits below a clear technical level (recent swing low / breakout level / support), and the risk to that stop is reasonable (ideally tighter than the 5% reward).
- The **~5% target** is achievable — it sits at or below the next meaningful resistance, with room to run. If 5% would slam straight into heavy overhead supply, the setup is weak.
- **Risk:Reward ≥ ~1.5:1.** If risk to stop is bigger than the reward to target, skip it — the math doesn't work even if the chart looks pretty.
- *Why:* a great-looking chart with no room to the upside or a far-away stop is a bad *trade*. This gate enforces that 5% is realistically reachable for the risk taken.

### Step 3 — Rank and build trade plans

For every stock that cleared all four gates, write a full trade plan using the template below. Rank by combined conviction (strength across the gates + cleanest risk/reward). Keep the top 5 at most.

If **none** cleared all four gates, skip the template entirely and deliver the "no qualifying setups" message (see Output).

## Output

Always lead with the **regime + scan summary**, then either the trade plans or the no-trade verdict.

### When stocks qualify

```
# Swing Trade Screen — Indian Markets — <YYYY-MM-DD>

**Market regime:** <Nifty trend in one line — e.g. "Nifty above 20 & 50 DMA, uptrend intact, VIX low — favorable for momentum longs.">
**Universe scanned:** <e.g. Nifty 500>  |  **Candidates analyzed:** <N>  |  **Qualified:** <M>

---

## 1. <NSE SYMBOL> — <Company> (<Sector>)   ⭐ Conviction: <High/Medium>
**Current price:** ₹<x>   |   **52-wk high:** ₹<x>

- **Momentum:** <1–2 lines — MA alignment, RSI, MACD, distance from 52w high, rel. strength>
- **Volume:** <1–2 lines — recent vs 20-day avg, delivery %, volume-with-price>
- **Sentiment:** <1–2 lines — recent news/results/upgrades, sector, any caveat>

**Trade plan**
| Entry zone | Stop-loss | Target (~5%) | Risk:Reward | Horizon |
|------------|-----------|--------------|-------------|---------|
| ₹<a>–<b>   | ₹<s> (−<x>%) | ₹<t> (+<x>%) | <1:R>     | <e.g. 2–4 weeks> |

**Key risk / invalidation:** <what kills the trade — e.g. "Earnings on <date> inside horizon" or "Loses ₹<level> support">

---
(repeat for each qualifier, max 5)

**Position sizing reminder:** Risk only ~1–2% of capital per trade. Size = (capital × risk%) ÷ (entry − stop). The 5%/month target is a portfolio goal across disciplined trades, not a per-name guarantee.
```

### When nothing qualifies

Be direct and useful — don't pad it. Example:

> **No qualifying swing setups today (<date>).**
> Scanned <universe>; <N> candidates showed some momentum/volume, but none cleared all four gates.
> Closest misses: **<SYM>** (strong momentum + volume, but earnings in 3 days — binary risk) and **<SYM>** (good setup but already +9% extended above 20-EMA — no low-risk entry, R:R < 1.5).
> **Recommendation:** wait. Forcing a trade here has poor odds. <If regime is weak, add: "Nifty is below its 50-DMA — momentum longs are low-probability until the broad tape stabilizes.">

This restraint is the point. The user asked for exactly this discipline.

## Guardrails (always honor)

- **Data freshness:** web data may be delayed or end-of-day. State the data's as-of time and tell the user to confirm live prices and levels with their broker before acting.
- **Not advice:** this is educational screening, not SEBI-registered investment advice. No guarantees — momentum strategies have losing trades; the stop-loss is non-negotiable risk control.
- **Verify, don't invent:** if a number (RSI, volume ratio, delivery %, a price level) couldn't be sourced, say "not available" rather than guessing. A fabricated level is worse than a missing one. Cross-check a stock on at least two sources before naming it.
- **Liquidity:** skip illiquid names and penny stocks — slippage and gap risk wreck the 5% math.

See `references/data-sources.md` for sources, Chartink scan recipes, and the gate checklist in compact form.
