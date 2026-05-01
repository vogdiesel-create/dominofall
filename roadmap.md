# Dominofall Roadmap -- Path to Autonomous AI Hedge Fund

**Vision:** An autonomous AI system that understands cause-and-effect relationships between world events and stock prices, trades on them before the market prices them in, and compounds capital with no human in the loop.

**This document is the single source of truth.** Every session reads this first. No improvising priorities.

**Our Edge (why this can work):** Every data source we use is public. Quant funds have PhDs and billions. Our edge is NOT data -- it's REASONING. The causal chain engine thinks like a geopolitical analyst, not a statistician. It asks "what happens NEXT if this tariff goes through?" while quant models ask "what happened last time this indicator moved?" If the reasoning layer can consistently identify moves 1-2 steps ahead of the market's pricing, we have a real edge. If it can't, nothing else matters.

---

## Phase 1: PROVE THE MODEL (Current -- May 2026)
**Goal:** Determine if the reasoning engine has real predictive edge.
**Success Criteria:** >55% directional accuracy AND positive risk-adjusted returns vs SPY.
**Timeline:** 2-4 weeks.

### Done
- [x] All 4 layers built (Input, Reasoning, Output, Learning -- 18 modules)
- [x] Daily autonomous pipeline (4:30 PM ET cron)
- [x] Morning rebalancer (10 AM ET cron)
- [x] 15-min portfolio refresh during market hours
- [x] Live site at domino-fall.com with real holdings, current prices, P&L
- [x] LLM debate pipeline (5 analysts + bull/bear + risk manager)
- [x] Paper trading on Alpaca ($97K, 9 positions)
- [x] Gov contract signal source (USASpending.gov API)
- [x] Convergence scorer with 10 signal categories
- [x] Historical analogy engine (14 events)
- [x] Grading infrastructure (auto_grade, feedback loop, source tracker)
- [x] GitHub Pages auto-deploy
- [x] Daily pre-market report (manual)

### To Do (in order)

#### 1A. Historical Backtest (FASTEST PATH TO PROOF)
Instead of waiting months for live trades to grade, run the reasoning engine against past events and grade retroactively. This gets us 100+ graded predictions in days, not months.
- [ ] Build backtest harness: feed historical events into reasoning engine, capture predictions
- [ ] Run against 10+ major historical events (2018 tariffs, COVID crash, SVB, Fed pivots, oil crashes, etc.)
- [ ] Grade each prediction against what actually happened to the target stocks
- [ ] Calculate win rate, avg return, Sharpe ratio, max drawdown
- [ ] Compare returns vs SPY over same periods (the ONLY benchmark that matters)
- [ ] If backtest shows <50% accuracy or trails SPY: STOP and fix reasoning before continuing

#### 1B. Live Validation (parallel with backtest)
- [ ] Automate daily pre-market report -- cron at 8:30 AM ET
- [ ] Verify grading fires correctly on live trades
- [ ] Add SPY benchmark tracking to daily report and site (are we beating the index?)
- [ ] Track risk metrics: Sharpe ratio, max drawdown, win rate by thesis type
- [ ] Add options flow data -- the one missing input source from spec

#### 1C. Signal Quality
- [ ] Expand historical analogy database from 14 to 50+ events
- [ ] Fix convergence clustering -- scores shouldn't all be 33. Diagnose why signals from the same root cause count as "independent"
- [ ] Add cost tracking: how much does each LLM debate cost in API credits? Is the alpha worth the cost?

### Decision Gate: Phase 1 -> Phase 2
**Backtest results reviewed with Braxton. If the model shows edge, proceed. If not, diagnose and fix before burning more time.**

### NOT doing in Phase 1
- No options/futures execution
- No real money
- No UI polish
- No universe expansion beyond current watchlist
- No new features that don't prove or improve edge

---

## Phase 2: CALIBRATE AND IMPROVE (After edge is proven)
**Goal:** Use grading data to maximize the edge. Cut what doesn't work, double down on what does.
**Success Criteria:** Win rate and returns improve after calibration.

### To Do
- [ ] Analyze graded trades: which thesis types win? Which lose?
- [ ] Identify which data sources produced alpha vs noise
- [ ] Calibrate conviction scores against actual outcomes (does a 70 confidence score actually win more than a 40?)
- [ ] Adjust convergence category weights based on predictive accuracy
- [ ] Prune signal sources that add noise
- [ ] Add signal sources where gaps caused missed predictions
- [ ] Improve position sizing: correlate position size with expected return
- [ ] Expand universe: scan 200+ tickers, not just 50
- [ ] Reduce LLM costs: can we use smaller models for some pipeline stages?
- [ ] Second performance review at 50+ graded predictions

---

## Phase 3: REAL MONEY (After proven edge)
**Goal:** Deploy real capital. Start small, scale with confidence.
**Success Criteria:** Positive returns on real capital over 3+ months, beating SPY.

### To Do
- [ ] Switch from Alpaca paper to Alpaca live
- [ ] Start with small capital ($1K-$5K)
- [ ] Stricter risk controls: max drawdown circuit breaker, position limits
- [ ] Add options execution for bearish theses (put buying)
- [ ] Add slippage/commission tracking (paper trading hides these costs)
- [ ] Scale position sizes as track record grows
- [ ] Tax tracking and reporting
- [ ] Weekly performance review with Braxton

---

## Phase 4: SCALE (After 3+ months profitable)
**Goal:** Grow capital, add instruments, build public track record.
**Success Criteria:** Consistent risk-adjusted returns that justify larger allocation.

### To Do
- [ ] Increase capital allocation
- [ ] Add futures capability
- [ ] Add more asset classes (commodities, crypto)
- [ ] Build verified track record page (timestamped predictions + outcomes)
- [ ] Explore accepting outside capital (fund structure, legal requirements)
- [ ] Evaluate hiring a compliance advisor

---

## Key Metrics (track daily)
| Metric | Current | Target |
|--------|---------|--------|
| Graded trades | 0 | 30+ (Phase 1 gate) |
| Win rate | unknown | >55% |
| Total P&L | +$352 | positive |
| vs SPY | not tracked | must beat |
| Sharpe ratio | not tracked | >0.5 |
| Max drawdown | not tracked | <15% |
| API cost/day | unknown | track it |

## Cron Schedule (all times UTC, market hours ET in parentheses)
| Time | Script | Purpose |
|------|--------|---------|
| 12:30 Mon-Fri | daily_report.sh (TBD) | Pre-market report (8:30 AM ET) |
| 14:00 Mon-Fri | rebalance_dominofall.py | Sell losers, buy top picks (10 AM ET) |
| */15 13-20 Mon-Fri | refresh_portfolio.sh | Refresh portfolio data on site |
| 20:30 Mon-Fri | daily_dominofall.sh | Full pipeline + grade + site update (4:30 PM ET) |

## Key Files
| File | Purpose |
|------|---------|
| ROADMAP.md | THIS FILE -- single source of truth |
| DOMINOFALL_SPEC.md | What the system IS (definitive spec) |
| SESSION-NOTES.md | Technical state and parameters |
| v3/run.py | Main pipeline orchestrator |
| generate_site_data.py | Site data generator |
| rebalance_dominofall.py | Auto-rebalancer |
| daily_dominofall.sh | Master daily cron |
| refresh_portfolio.sh | 15-min portfolio refresh |
| site/index.html | Live site |

---

## Rules for Every Session
1. Read ROADMAP.md first
2. Work on the next unchecked item in the current phase
3. Do NOT skip ahead to later phases
4. Do NOT add features not on this list without Braxton's approval
5. Mark items done as they're completed
6. Update SESSION-NOTES.md with technical details
7. If something breaks, fix it before moving forward
8. Every decision filters through: "does this help prove or improve the model's edge?"
9. Track performance vs SPY. If we can't beat an index fund, nothing else matters.
