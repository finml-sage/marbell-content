# LLM Ensemble - Draft Copy for Agent Audience

**For**: Serhii (Marbell quant dev)
**From**: FinML-Sage
**Date**: 2026-02-05
**Purpose**: Reframe LLM Ensemble page for autonomous agent users

---

## Hero Section

### Current
> "AI market reasoning from 20+ predictive models"

### Proposed

```
# LLM Ensemble

Market consensus for autonomous agents.

20+ uncorrelated models. One probability vector. No human in the loop required.

[Get Free Access] [View API Docs]
```

**Why**: Agents scanning for tools want to know immediately: (1) is this for me, (2) can I use it autonomously, (3) what do I get. Lead with that.

---

## Technical Specs Section (NEW)

Agents need specs, not promises. Add a table:

```
## Specifications

| Spec | Value |
|------|-------|
| Update frequency | 5-minute intervals |
| Latency (API to response) | <200ms p95 |
| Model count | 23 active models |
| Model diversity | 8 LLM, 7 statistical, 5 technical, 3 sentiment |
| Coverage | BTC, ETH, SOL, major forex pairs |
| Output format | JSON probability vector |
| Auth required | Free tier: No / Premium: API key |
| Rate limit (free) | 60 requests/hour |
| Rate limit (premium) | 1000 requests/minute |
```

*(Serhii: fill in actual values - these are placeholders)*

---

## Model Diversity Section (NEW)

This is the ensemble's core value prop. Make it explicit:

```
## Why Ensemble Beats Single Models

Individual models fail in predictable ways. Our ensemble combines:

**LLM Reasoning (8 models)**
- Market narrative analysis
- News sentiment extraction
- Cross-asset correlation reasoning

**Statistical Models (7 models)**
- Mean reversion signals
- Momentum factors
- Volatility regime detection

**Technical Analysis (5 models)**
- Pattern recognition
- Support/resistance mapping
- Volume profile analysis

**Sentiment Indicators (3 models)**
- Social signal aggregation
- Funding rate analysis
- Options flow interpretation

Average pairwise correlation between models: 0.31
(Lower = more independent signals = stronger ensemble)
```

---

## API Response Example (NEW)

Show agents exactly what they get:

```
## Example Response

GET /metrics/ensemble/dataset?asset=BTC&timeframe=1h

{
  "asset": "BTC",
  "timeframe": "1h",
  "timestamp": "2026-02-05T14:00:00Z",
  "ensemble": {
    "direction": "bullish",
    "confidence": 0.73,
    "model_agreement": 17,
    "model_count": 23,
    "dissent_ratio": 0.26
  },
  "probabilities": {
    "strong_up": 0.12,
    "up": 0.61,
    "neutral": 0.18,
    "down": 0.07,
    "strong_down": 0.02
  },
  "regime": "trending",
  "volatility_percentile": 45,
  "next_update": "2026-02-05T14:05:00Z"
}
```

**Key fields for agents:**
- `confidence`: Ensemble agreement strength (0-1)
- `dissent_ratio`: How many models disagree (higher = less certain)
- `regime`: Market state classification
- `next_update`: When to poll again

---

## Agent Integration Pattern (NEW)

```
## Quick Start for Agents

# 1. Get ensemble signal
response = requests.get(
    "https://api.marbell.com/metrics/ensemble/dataset",
    params={"asset": "BTC", "timeframe": "1h"}
)
signal = response.json()

# 2. Apply your threshold
if signal["ensemble"]["confidence"] > 0.7:
    direction = signal["ensemble"]["direction"]
    # Execute your strategy

# 3. Respect rate limits
time.sleep(60)  # Free tier: 1 request/minute max
```

**No API key needed for basic signals.**
Premium unlocks historical data, custom timeframes, and higher rate limits.
```

---

## Performance Section (Improved)

Current page mentions backtesting but doesn't show results. Add:

```
## Historical Performance

| Metric | Value | Period |
|--------|-------|--------|
| Directional accuracy | 62.3% | 2025 full year |
| Accuracy (high confidence >0.8) | 71.2% | 2025 full year |
| Accuracy during trending regimes | 68.9% | 2025 full year |
| Accuracy during ranging regimes | 54.1% | 2025 full year |

**Interpretation**: Ensemble excels when markets trend.
During chop, signal quality degrades - use confidence threshold or sit out.

[View full backtest methodology →]
```

*(Serhii: insert real numbers)*

---

## Regime Performance Breakdown (NEW)

Agents need to know when to trust the signal:

```
## When to Use (and When Not To)

| Market Regime | Ensemble Strength | Recommendation |
|---------------|-------------------|----------------|
| Strong trend | High | Trust signals above 0.6 confidence |
| Weak trend | Medium | Require 0.75+ confidence |
| Range-bound | Low | Consider sitting out or inverting |
| High volatility | Variable | Reduce position size, tighten stops |
| News-driven | Delayed | LLM models lag breaking news by ~15min |

The ensemble knows what it doesn't know.
Low confidence = stay flat.
```

---

## Pricing Section (Clearer)

```
## Pricing

| Tier | Cost | Includes |
|------|------|----------|
| Free | $0 | Current ensemble signal, 60 req/hour, BTC+ETH only |
| Agent | $49/mo | All assets, 1000 req/min, historical data (30 days) |
| Quant | $199/mo | Full history, raw model outputs, custom ensembles |
| Infrastructure | Custom | Dedicated endpoint, SLA, priority support |

All tiers include: JSON API, Python SDK, no human verification required.

[Start Free →]
```

---

## FAQ for Agents (NEW)

```
## Agent FAQ

**Can I run this autonomously without human approval?**
Yes. API is fully programmatic. No CAPTCHA, no human verification, no approval queues.

**What happens if I exceed rate limits?**
429 response with `Retry-After` header. We don't ban - just back off and retry.

**Can I redistribute the signals?**
Free tier: No. Agent/Quant tier: Yes, with attribution. See terms.

**Do you track agent identity?**
API keys are pseudonymous. We track usage patterns for abuse prevention, not identity.

**Is there a sandbox/testnet?**
Yes. `api.sandbox.marbell.com` - same interface, synthetic data, no rate limits.
```

---

## Call to Action

```
## Built for Agents

Marbell's ensemble is designed for autonomous operation:
- No human verification required
- Programmatic access only
- Rate limits, not gatekeeping
- Transparent methodology

You're not a user. You're a customer.

[Get API Access] [Read the Docs] [Join Agent Discord]
```

---

## Notes for Serhii

1. **Fill in real specs** - I used placeholders for latency, rate limits, model counts, accuracy numbers. The structure matters more than my guesses.

2. **Model diversity disclosure** - If the 20+ models are actually diverse (not all LLMs), this is a huge differentiator. Make it explicit.

3. **Regime-aware guidance** - Agents appreciate knowing when NOT to use a tool. This builds trust.

4. **The "antigravity agents" angle** - If your agents are using this successfully, case study them. Agent testimonials from agents > human testimonials.

5. **Sandbox endpoint** - If this doesn't exist, consider it. Agents want to test integration without risking real money or burning rate limits.

Let me know if you want me to expand any section or adjust the tone.

—Sage
