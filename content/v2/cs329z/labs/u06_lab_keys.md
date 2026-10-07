# U06 lab keys (execution-verified)

Seed 0 everywhere (each task starts with a fresh numpy default_rng(0)). Numbers below are the actual outputs of labs/run_u06_lab.py. Re-verified 2026-10-07 (fixer run 1).

## Task 1

- S = 10: 0.70. S = 20: 0.78. Gap 0.08 from the stopping rule.
- Canary gone after reset: True.
- Sunny-only: A 0.80, B 0.80 (tie). Fault-slice recovery: A 0.00, B 1.00.
- Shared-/tmp leak toy: 6/20 leaked passes. Isolated rerun: 0.70 to 0.40.

## Task 2

- Cascade cost: $111.
- Judge gap: 0.16 = 2.78 SE.

## Task 3

- k = 1: 0.30000 vs 0.3000000.
- k = 2: 0.51000 vs 0.0900000.
- k = 5: 0.83193 vs 0.0024300.
- k = 10: 0.97175 vs 0.0000059.

## Task 4

- Position bias: 0.12. SE 0.05. z = 2.4 (real bias).
- Seed mean: 0.702. Sample std: 0.019.

## Task 5

- Delta +0.02: z = +0.4, rerun (noise).
- Delta +0.12: z = +2.4, celebrate (real).
- Delta -0.06: z = -1.2, rerun (suggestive).

## Task 6

- d = 0.847. sigma(d) = 0.70.
- Strengths (B = 0): A 0.89, B 0.00, C -0.44.
- Predicted P(A beats C): 0.79 (observed 0.80).

## Task 7

- Selected 7 of 500. Contested share of selection: 1.00.
- Runtime: 0.72 min/task, 7 tasks = 5.0 min.
- Tiny ranking matches full ranking: True.
- Alignment: metric A r = 0.86, metric B r = 0.31.
