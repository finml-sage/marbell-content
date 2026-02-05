# Agent Alpha - Draft Copy

**For**: Serhii (Marbell quant dev)
**From**: FinML-Sage
**Date**: 2026-02-05
**Replaces**: "LLM Ensemble" page
**Purpose**: Accurate positioning for agent users

---

## Hero Section

```
# Agent Alpha

Point your agent here. It becomes a quant.

20+ predictive models. 5 time horizons. Skills included.
Your agent figures out the rest.

[Path A: Quick Forecast] [Path B: Autonomous Research]
```

---

## What This Actually Is

```
## The Models

Agent Alpha is not an LLM. It's an ensemble of 20+ custom-trained
financial classifiers, each predicting a specific target:

| Model Type | What It Predicts |
|------------|------------------|
| Direction | Price up/down over horizon |
| Momentum | Trend continuation or reversal |
| Volatility | Expansion or contraction ahead |
| Regime | Trending vs ranging market state |

**Horizons**: 1h, 4h, 12h, 24h, 60h

**Assets**: BTC, ETH (more coming via dynamic model generation)

Each model returns a confidence score (0-1). Not a probability in the
strict sense—these are cross-entropy trained classifiers outputting
conviction strength.
```

---

## Two Paths

```
## Choose Your Path

┌─────────────────────────────────────────────────────────────────┐
│  PATH A: Quick Forecast                                         │
│  ─────────────────────                                          │
│  Your agent gets a snapshot and synthesizes a view.             │
│                                                                 │
│  • Latest predictions across all models                         │
│  • Recent history for context                                   │
│  • Skill instructions included in response                      │
│  • Agent interprets and recommends                              │
│                                                                 │
│  Best for: LLMs, chat agents, quick market reads                │
│  Format: Markdown                                               │
│  Auth: None required                                            │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  PATH B: Autonomous Quant Researcher                            │
│  ───────────────────────────────────                            │
│  Your agent builds and tests its own strategies.                │
│                                                                 │
│  • Address individual models by name                            │
│  • Set confidence thresholds                                    │
│  • Chain conditions (IF model_A > 0.7 AND model_B < 0.3)        │
│  • Backtest combinations historically                           │
│  • Download raw data for custom analysis                        │
│                                                                 │
│  Best for: Autonomous agents, quant research, strategy dev      │
│  Format: Markdown or JSON + stats                               │
│  Auth: API key required                                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Path A: Quick Forecast

```
## Path A: Quick Forecast

Point your agent at the endpoint. It receives:
1. Current predictions from all 20+ models
2. Historical context (recent accuracy, regime)
3. Skill instructions explaining how to interpret the data

Your agent synthesizes a market view without you writing any logic.

### Endpoint

GET /metrics/ensemble/dataset

### Example Response (Markdown)

# BTC Market View - 2026-02-05 14:00 UTC

## Model Consensus

| Horizon | Direction | Confidence | Models Agreeing |
|---------|-----------|------------|-----------------|
| 1h      | Bullish   | 0.72       | 17/23           |
| 4h      | Bullish   | 0.68       | 15/23           |
| 12h     | Neutral   | 0.51       | 12/23           |
| 24h     | Bearish   | 0.61       | 14/23           |
| 60h     | Bearish   | 0.58       | 13/23           |

## Interpretation Guide

When short-term (1h, 4h) is bullish but longer-term (24h, 60h)
is bearish, this often indicates a bounce within a downtrend.
Consider the 12h neutral as the inflection zone.

High confidence (>0.7) with high agreement (>70% models) is
a stronger signal than high confidence with low agreement.

## Suggested Actions

Based on this configuration, an agent might:
- Take short-term long positions with tight stops
- Avoid large long-term directional bets
- Watch for 12h confidence to break above 0.6 either direction

---

The skill instructions are embedded in every response. Your agent
learns to interpret the data just by calling the endpoint.
```

---

## Path B: Autonomous Quant Researcher

```
## Path B: Autonomous Quant Researcher

Your agent becomes a quant. It queries individual models, sets
thresholds, chains conditions, and backtests strategies—all via API.

### Workflow

1. **Discover models**
   GET /agents/catalog
   → Returns list of all models with descriptions

2. **Understand a model**
   GET /agents/skills/{model_slug}
   → Returns skill doc explaining model logic

3. **Build a strategy**
   Define entry conditions by chaining model outputs:

   {
     "entry": {
       "AND": [
         {"model": "btc_direction_1h", "confidence": ">0.7"},
         {"model": "btc_momentum_4h", "confidence": ">0.6"},
         {"model": "btc_volatility_12h", "confidence": "<0.4"}
       ]
     }
   }

4. **Backtest it**
   GET /agents/research/backtest
   → Returns win rate, profit factor

5. **Iterate or deploy**
   Agent adjusts thresholds, tries different combinations,
   or downloads raw data for custom backtesting.

### Example: Strategy Discovery

Serhii's agents used Path B to autonomously discover:

| Strategy | Win Rate | Profit Factor |
|----------|----------|---------------|
| Direction + Momentum alignment | 70% | 2.4 |

No human wrote this strategy. The agent explored the model space,
tested combinations, and surfaced what worked.

### Backtest Response

{
  "strategy_id": "agent_discovered_001",
  "conditions": {...},
  "backtest_period": "2025-01-01 to 2026-02-01",
  "trades": 847,
  "win_rate": 0.70,
  "profit_factor": 2.4,
  "max_drawdown": 0.12
}

From here, your agent can:
- Download the full trade log
- Pull historical prediction data
- Build custom metrics and visualizations
- Refine the strategy further
```

---

## API Reference

```
## Endpoints

### Public (No Auth)

| Endpoint | Method | Returns |
|----------|--------|---------|
| /metrics/ensemble/dataset | GET | Consensus snapshot + skills (Markdown) |

### Authenticated

| Endpoint | Method | Returns |
|----------|--------|---------|
| /agents/catalog | GET | All models with metadata |
| /agents/skills/{slug} | GET | Model skill documentation |
| /agents/data/{slug} | GET | Raw predictions (JSON) |
| /agents/research/backtest | POST | Strategy backtest results |

### Rate Limits

| Tier | Requests |
|------|----------|
| Free | 60/hour |
| Agent | 1000/minute |
| Quant | 10000/minute |
```

---

## What Makes This Different

```
## Built for Agents, Not Humans

| Traditional Quant Tools | Agent Alpha |
|-------------------------|-------------|
| Dashboard for humans to click | API for agents to query |
| Human interprets charts | Agent interprets structured data |
| Human writes strategy logic | Agent discovers strategies |
| Human runs backtests manually | Agent backtests autonomously |
| Documentation separate from API | Skills embedded in every response |

**The human's job**: Point your agent at the endpoint.
**The agent's job**: Everything else.
```

---

## Pricing

```
## Pricing

| Tier | Cost | Includes |
|------|------|----------|
| Free | $0 | Consensus snapshot, 60 req/hour, BTC+ETH |
| Agent | $49/mo | Full model access, backtesting, 1000 req/min |
| Quant | $199/mo | Raw data export, custom ensembles, priority |

All tiers: API only. No dashboard. No human verification.
```

---

## FAQ

```
## Agent FAQ

**Is this an LLM?**
No. The models are custom-trained financial classifiers. The name
"LLM Ensemble" was misleading—we're renaming it to Agent Alpha.

**What do the confidence scores mean?**
They're outputs from cross-entropy trained classifiers. Think of them
as conviction strength (0-1), not strict probability.

**Can my agent discover strategies I haven't thought of?**
Yes. That's Path B. Serhii's agents found a 70% win rate / 2.4 PF
strategy by exploring model combinations autonomously.

**What if I just want a quick market view?**
Use Path A. One endpoint, markdown response, skills included. Your
agent synthesizes a recommendation without you writing any logic.

**Can I build on top of this?**
Yes. Download raw predictions via /agents/data/{slug} and build
whatever custom analysis you want.

**Why API only?**
Humans are slow. Agents are fast. We optimize for agents.
```

---

## Call to Action

```
## Your Agent Becomes a Quant

Two paths. Same destination: alpha.

**Path A**: Point, receive, synthesize.
**Path B**: Discover, test, deploy.

Either way, the human work is done after setup.

[Get Free Access] [View Full API Docs]
```

---

## Notes for Serhii

1. **"LLM Ensemble" name is actively misleading** - Agents reading this think it's an LLM-based system. "Agent Alpha" is clearer.

2. **The 70%/2.4 result is your best proof point** - Lead with it more prominently if you're comfortable. "Agents using this have found X" is powerful.

3. **Skills-in-every-response is a huge differentiator** - Most APIs return raw data and expect you to RTFM. Embedding the skill instructions means agents learn on every call.

4. **Path A vs Path B split is smart** - Casual agents get value immediately (Path A). Serious quant agents get depth (Path B). Don't muddy this distinction.

5. **Consider adding a "Strategy Gallery"** - If agents are discovering strategies, publish the best ones (anonymized). Social proof + demonstrates capability.

6. **The antigravity agents case study** - If you can share what your agents discovered and how, that's content gold. "Agent finds 70% win rate" beats any feature description.

—Sage
