# Capstone 1 , Replication: cache hit-rate economics

Runner: `cap01_run.py` (seed 20261007, pure stdlib plus
matplotlib). Figures: `figures/cap01_hitrate.png`,
`figures/cap01_cost.png`. All numbers below are computed by
the runner. Nothing is quoted.

## Replicated claim

U04-C06 teaches the cache effective-cost formula E = h x
c_c + (1 - h) x c_m and treats the hit rate h as an input.
This capstone replicates the missing step: it predicts h
itself from a Zipf-distributed query mix served by an LRU
cache, then checks the full chain from query distribution
to dollars.

## Method

- Query stream: 50,000 queries over 5,000 templates, Zipf
  s = 1.2 (a standard skew for support-desk traffic, TOY).
- Cache: LRU with capacities 100, 250, 500, 1,000, 2,000.
- Analytic model (independent reference model): LRU hit
  rate ~= total probability mass of the hottest C
  templates.
- Costs: c_c = 0.25, c_m = 4.00 dollars per 1M.

## Pre-registered hypotheses

- H1: the analytic model predicts the measured LRU hit
  rate within 10 percent relative, at every cache size.
- H2 (extension): doubling the cache from 500 to 1,000
  slots raises the hit rate by less than 5 points
  (diminishing returns).

## Results

| cache | analytic h | measured h | rel error |
|-------|-----------|------------|-----------|
| 100 | 0.7697 | 0.6760 | 12.16 pct |
| 250 | 0.8406 | 0.7702 | 8.37 pct |
| 500 | 0.8863 | 0.8327 | 6.05 pct |
| 1,000 | 0.9262 | 0.8847 | 4.48 pct |
| 2,000 | 0.9609 | 0.9230 | 3.94 pct |

- H1: FAIL. The analytic model overstates the hit rate at
  small caches (12.16 percent error at C = 100, above the
  10 percent bar). It passes at C >= 250. Cause: cold
  start and recency effects, which the independent
  reference model ignores, bite hardest when the cache is
  small relative to the template catalog.
- H2: FAIL (narrowly). Measured gain 500 -> 1,000 is
  0.0520, just above the 0.05 bar. The practical
  conclusion (diminishing returns) is visible in the
  curve, but the pre-registered bar was missed. The bar
  is not moved after the fact.

Effective cost per 1M tokens (from measured h): 1.465,
1.112, 0.877, 0.682, 0.539 dollars across the five cache
sizes.

## What the failure teaches

The U04-C06 formula is exact given h. The risk sits one
level down: predicting h from traffic models. Anyone who
buys cache infrastructure on analytic hit-rate math
should derate small-cache predictions by ~12 percent or,
better, measure h on their own traffic for two weeks
before sizing the cache. That measurement habit is the
durable lesson, and it is exactly what H1's failure
proves necessary.

## Limitations

Synthetic Zipf traffic, not production queries. One seed
(the seed is fixed and the stream is long, so seed noise
is small, but it is not zero). LRU only. Other eviction
policies were not tested. Cost numbers are toy billing
rates.

## Reproducibility

Run `python3 cap01_run.py`. It prints the table, the H1/H2
verdicts, and re-renders both figures with metadata
stripped. Expected terminal line: `H1: FAIL | H2: FAIL`.
