# Lab key , U04

Verified outputs from `u04_lab_run.py`, executed 2026-10-07.

## Task 1

| a1 | monthly value $ |
|----|-----------------|
| 0.82 | 7,400 |
| 0.63 | 3,600 |
| 0.50 | 1,000 |

Partial coverage halves the value.

## Task 2

- Three sources, two-year: 180,000 dollars
- Four sources, two-year: 230,000 dollars
- Delta: 50,000 dollars

## Task 3

High volume: cumulative [2.0, 3.8, 5.42, 6.88, 8.19, 9.37]
recall points over 6 months. Low volume (q = 1k):
[0.02, 0.04, 0.05, 0.07, 0.08, 0.09], noise, not a
flywheel.

## Task 4

| Q | generic $/mo | custom $/mo | winner |
|---|--------------|-------------|--------|
| 1B | 4,000 | 31,500 | generic |
| 5B | 20,000 | 37,500 | generic |
| 12B | 48,000 | 48,000 | tie |
| 20B | 80,000 | 60,000 | custom |

At Q = 5B with w = 2,000 per quality point: custom =
11,500 vs generic 20,000, custom wins. Quality value moves
the crossover from 12B to 1.6B.

## Task 5

- Q* = 12,000 (12B tokens per month)
- With idle time (p_h doubled): Q* = 30,000 (30B)
- At 15B tokens per month with idle: API 60,000 vs host
  75,000, API wins. Verdict: do not host a spiky fleet.

## Task 6

| h | effective $/1M | net saving $/mo |
|---|---------------|-----------------|
| 0.0 | 4.000 | -3,000 |
| 0.3 | 2.875 | 13,875 |
| 0.6 | 1.750 | 30,750 |
| 0.9 | 0.625 | 47,625 |

At h = 0 the cache is pure cost.

## Task 7

s = 0.01 (customer desk):

| L ms | latency cost | net $/mo |
|------|--------------|----------|
| 400 | 0 | 0 |
| 600 | 40,000 | -28,000 |
| 900 | 100,000 | -78,000 |
| 1,200 | 160,000 | -130,000 |

No batching wins. s = 0.001 (internal tool):

| L ms | latency cost | net $/mo |
|------|--------------|----------|
| 400 | 0 | 0 |
| 600 | 4,000 | 8,000 |
| 900 | 10,000 | 12,000 |
| 1,200 | 16,000 | 14,000 |

Batch 8 wins by 14k per month.

## Task 8

| e | total $/mo | per task $ |
|---|-----------|------------|
| 0.10 | 19,666.67 | 1.97 |
| 0.04 | 15,666.67 | 1.57 |
| 0.01 | 13,666.67 | 1.37 |

Cutting e from 0.10 to 0.04 saves 4,000 per month.

## Task 9

| s | cost per success $ |
|---|-------------------|
| 0.9 | 0.56 |
| 0.6 | 0.83 |
| 0.3 | 1.67 |
| 0.2 | 2.50 |

Premium model: 2.11. The cheap model wins until s falls
near 0.25.

## Task 10

| Q (1M units) | average $/1M |
|--------------|--------------|
| 100 | 301.50 |
| 500 | 61.50 |
| 2,000 | 16.50 |
| 12,000 | 4.00 |
| 100,000 | 1.80 |

The pilot trap: quoting 61.50 from the pilot misleads the
rollout, where the true number nears 2.00.

## Task 11

| d $/mo | payback months |
|--------|----------------|
| 5,000 | 50.0 |
| 12,000 | 20.8 |
| 20,000 | 12.5 |

With the 5-point quality penalty at d = 12k: net monthly
saving = 12,000 - 41,666.67 = -29,666.67. Do not switch.

## Task 12

| w $ | break-even tasks/mo |
|-----|---------------------|
| 5 | 13,427.6 |
| 3 | 30,894.3 |
| 2 | 88,372.1 |

Soft w = 5 with only 2 hard: contribution 0.43, needs
88,372 tasks against 18k actual. Verdict: do not proceed
on hard dollars.
