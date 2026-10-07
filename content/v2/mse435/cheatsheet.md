# mse435 cheatsheet , formulas, rules, numbers

One page per section. Every formula, every decision
rule, every toy constant. Numbers are TOY unless marked.

## Master formulas

| Name | Formula |
|------|---------|
| Market clearing | 100 - 2P = 20 + 3P, P* = 16, Q* = 68 |
| Average cost | F/Q + v |
| Unit inference cost | C_train/V + c_inf |
| Servable tokens/day | GPUs x tok/s x U x 86,400 |
| PUE | total power / IT power |
| Depreciation | purchase x 0.6^t |
| Access value | q x (a1 - a0) x v |
| Flywheel month t | q x corr x gain x decay^(D-t) |
| Hosting break-even | Q* = F / (p_a - p_h) |
| Cached effective price | h x c_c + (1 - h) x c_m |
| Latency tradeoff net | V x s x dL - saving |
| Review labor | tasks x e x min/60 x wage |
| Cost per success | (r+1) x c / (1 - (1-s)^(r+1)) |
| Blended margin | sum share_i x (price_i - cost_i) |
| Amdahl | 1 / ((1-p) + p/s) |
| Funnel total | sum n_i x c_i |
| Savings PV (ramped) | sum a_t x S / (1+r)^t |
| TCO 3-year | B + 3(R + L) + K |
| Pilot rule | invest iff L > Y |
| Pilot sample size | n = (1.96/half-width)^2 x p(1-p) |

## Decision rules

| Situation | Rule |
|-----------|------|
| Falling token prices | Never sign take-or-pay beyond the visible horizon |
| Host vs API | Host iff volume > F / (p_a - p_h) |
| Cache | Build iff h x saving x volume > infra |
| Batching | Batch iff V x s x dL < saving |
| License vs build | License iff vendor TCO < build TCO over 3 years |
| Pilot | Pre-register Y, D, instrument. Invest iff L > Y |
| Pilot breach | Kill on two consecutive guardrail breaches |
| Rollback | 15-minute button, game-day tested |
| Quality gate | a1 >= 0.75 binary |
| Contract | Price-cap or 90-day termination for convenience |
| Build vs lease | Build base load, lease peaks |
| Retraining | Add n_runs x C_train/V when cadence is quarterly |

## Toy constants (do not quote)

| Constant | Value |
|----------|-------|
| Token market | P* = 16, Q* = 68 |
| API price | 4.00 per 1M |
| Hosted price | 1.50 per 1M |
| Cache serve | 0.25 per 1M |
| Fixed hosting cost | 30k per month |
| Break-even | 12B tokens per month |
| Training cost | 5M |
| Lifetime volume | 500B tokens |
| GPU throughput | 50 tok/s, U = 0.85 |
| Power per GPU | 0.7 kW |
| Cooling overhead | 0.3 W per W |
| PUE target | <= 1.3 |
| Depreciation | 40 pct per year |
| Access quality lift | a1 - a0 = 0.37 |
| Flywheel decay | 0.9 per month |
| Review wage | 40 per hour, 10 min per task |
| Retry success | s = 0.6, r = 1, cost 1.19 |
| Savings ramp (HYPOTHETICAL) | [0.20, 0.50, 0.80], r = 10 pct |
| Savings PV (HYPOTHETICAL) | 767.9k |
| Lean TCO (HYPOTHETICAL) | 680k, net +87.9k |
| Hosted TCO (HYPOTHETICAL) | 1,850k, build share 21.6 pct |
| Pilot | 5,000 cases, 4 weeks, Y = 0.15 |

## Watch-outs

- The pilot average (61.50) is not the steady-state
  rate. Never quote pilot cost as the unit price.
- Analytic hit-rate models overstate small caches by
  ~12 percent (capstone 1, H1 FAIL). Measure h.
- Doubling cache 500 to 1,000 gains ~5 points:
  diminishing, not linear.
- Moving Y or D after the pilot voids the decision.
- Build-only business cases understate cost 3-4x.
- The softest inputs: adoption ramp, success rate,
  review labor. Instrument all three before investing.
- Speaker forecasts are [SPEAKER CLAIM, EVIDENCE
  PENDING]. Never build on an unlabeled claim.
