# Lab key , U02

Verified outputs from `u02_lab_run.py`, executed 2026-10-07.

## Task 1

| U | capex | power | staff | total $/GPU-h |
|---|-------|-------|-------|---------------|
| 0.20 | 3.57 | 0.14 | 0.10 | 3.81 |
| 0.40 | 1.78 | 0.14 | 0.10 | 2.02 |
| 0.60 | 1.19 | 0.14 | 0.10 | 1.43 |
| 0.85 | 0.84 | 0.14 | 0.10 | 1.08 |
| 1.00 | 0.71 | 0.14 | 0.10 | 0.95 |

## Task 2

Break-even chip counts:

| NRE \ s | 0.40 | 0.82 | 1.20 |
|---------|------|------|------|
| 20M | 6,715 | 3,276 | 2,238 |
| 50M | 16,788 | 8,189 | 5,596 |

## Task 3

| I (FLOP/B) | attainable (TFLOP/s) | bound |
|------------|----------------------|-------|
| 40 | 80 | memory-bound |
| 100 | 200 | memory-bound |
| 150 | 300 | compute-bound (ridge) |
| 500 | 300 | compute-bound |

## Task 4

- Path A PV: 571.55M dollars
- Path B PV: 512.16M dollars
- Difference: 59.39M dollars (the opex path dominates the
  decision, not the build)

## Task 5

- 50 MW: 35,714 GPUs. 100 MW: 71,428 GPUs. 1000 MW: 714,285
  GPUs.
- Demand 70 MW: served 70, waiting 0. Demand 140 MW: served
  100, waiting 40.

## Task 6

Payback years:

| elec \ U | 0.40 | 0.85 |
|----------|------|------|
| 0.06 | 9.51 | 4.48 |
| 0.10 | 5.71 | 2.69 |
| 0.16 | 3.57 | 1.68 |

Liquid pays only where power is dear and racks run hot.

## Task 7

- GPUs: 714,285.7. Homes: 800,000. Build: 10.0B dollars.
  Annual energy: 700.8M dollars.
- Interruptible break-even discount: 0.0714 $/kWh. Below that
  discount, take firm power, above it, take the interruption
  for training.

## Task 8

U* at lease 1.50: 0.796. At 2.50: 0.478. At 3.50: 0.341.
Cheaper rent pushes the crossover up.

## Task 9

Effective $/used GPU-h: U=0.40: 5.05. U=0.60: 3.37. U=0.85:
2.38. U=0.95: 2.13. Delay cost per job at 0.95: 1,600
dollars, which exceeds the GPU saving versus 0.85 (0.25 $/h)
for any job needing more than 6,400 GPU-hours.

## Task 10

| year | book | market |
|------|------|--------|
| 0 | 200,000 | 200,000 |
| 1 | 150,000 | 120,000 |
| 2 | 100,000 | 72,000 |
| 3 | 50,000 | 43,200 |
| 4 | 0 | 25,920 |

Largest gap: year 1 (30,000 dollars, book above market).

## Task 11

- Base HHI: 5250, high.
- After entry: 4050, high. Entry helped but the market stays
  highly concentrated.

## Task 12

| scenario | build PV | lease PV | winner |
|----------|----------|----------|--------|
| fast fall | 33.17M | 24.99M | lease |
| flat | 33.17M | 41.65M | build |
| shortage | 33.17M | 58.31M | build |
| supply freeze | 33.17M | n/a | build |

Resilient pick: build (wins 3 of 4, worst loss 8.18M vs lease's
worst loss 25.14M). The fourth scenario removes the lease
column entirely: availability, not price, decides.
