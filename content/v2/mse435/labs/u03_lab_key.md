# Lab key , U03

Verified outputs from `u03_lab_run.py`, executed 2026-10-07.

## Task 1

| ai_share | cost $/mo |
|----------|-----------|
| 1.0 | 25,000 |
| 0.9 | 74,500 |
| 0.7 | 173,500 |
| 0.5 | 272,500 |

With 5 percent errors on AI tasks at 0.9 share: error cost =
9,000 x 0.05 x 200 = 90,000. True total = 164,500.

## Task 2

- Base two-year: 695,000 dollars
- Overrun two-year: 945,000 dollars
- Delta: 250,000 dollars (plumbing +100k, workflow +150k)

## Task 3

| api $/mo | open | closed | winner |
|----------|------|--------|--------|
| 20,000 | 920,000 | 530,000 | closed |
| 30,000 | 920,000 | 770,000 | closed |
| 40,000 | 920,000 | 1,010,000 | open |
| 60,000 | 920,000 | 1,490,000 | open |

Crossover between 30k and 40k per month.

## Task 4

| tok/s | B tokens/day | blocks/day |
|-------|--------------|------------|
| 15 | 1,101.6 | 1,101.6 |
| 30 | 2,203.2 | 2,203.2 |
| 50 | 3,672.0 | 3,672.0 |
| 80 | 5,875.2 | 5,875.2 |

## Task 5

- Overnight (supply fixed at 68): P* = 46.00 $/1M
- After supply adjusts: P* = 28.00 $/1M
- The sticky-supply spike is 64 percent above the later
  equilibrium.

## Task 6

Rate sequence: 40, then 80, then 80 rps. Final caps: [100,
160, 80]. The second upgrade was wasted on the batcher, it
should have gone to stage 3.

## Task 7

| lifetime tokens | amortized $/1M | total $/1M |
|-----------------|----------------|------------|
| 10B | 500.0 | 504.0 |
| 50B | 100.0 | 104.0 |
| 200B | 25.0 | 29.0 |
| 500B | 10.0 | 14.0 |
| 2T | 2.5 | 6.5 |

## Task 8

| path | contract PV | market PV | winner |
|------|-------------|-----------|--------|
| [4,3,2] | 895.27 | 914.20 | contract |
| [4,2,1] | 895.27 | 724.87 | market |
| [3,3,3] | 895.27 | 895.27 | tie (float dust) |
| [5,5,5] | 895.27 | 1,492.11 | contract |

## Task 9

| lift $/yr | own PV | rent PV | winner |
|-----------|--------|---------|--------|
| 0 | 2,746,056 | 1,243,426 | rent |
| 500,000 | 1,502,630 | 1,243,426 | rent |
| 1,000,000 | 259,204 | 1,243,426 | own |
| 2,000,000 | -2,227,648 | 1,243,426 | own |

Crossover lift is between 500k and 1M per year.

## Task 10

- Fence cost: 150,000 $/mo
- Benefit: p=0.005: 8,333, p=0.01: 16,667, p=0.05: 83,333
  $/mo
- The fence pays on expected value only at p = 0.05 with a
  20M loss, otherwise it needs a tail (reputation) argument.

## Task 11

| c | margin + buffer | loses? |
|---|-----------------|--------|
| 2.00 | 2.00 | no |
| 2.50 | 1.50 | no |
| 3.00 | 1.00 | no |
| 3.50 | 0.50 | no |

No case loses at 4.00, but at c = 3.50 the buffer is nearly
gone: one shock flips it.

## Task 12

Ranking by swing: utilization 2.40, power price 1.60, batch
size 1.20, chip cost 1.00.
