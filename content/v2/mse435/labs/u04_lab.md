# Lab U04 , Enterprise knowledge and inference cloud

Run `python3 u04_lab_run.py` to verify every computed answer.
The key in `u04_lab_key.md` records the verified outputs. Work
each task by hand first, then check against the runner.

## Task 1 , access value with partial coverage (C01)

1,000 questions per month, a0 = 0.45, v = 20 dollars. Sweep
a1 over [0.82, 0.63, 0.50]. Report the monthly value at
each.

## Task 2 , integration stack with a fourth source (C02)

Base: 3 sources, 40k build each, 5k per year maintenance
each, 30k filter, 2 years. Add a fourth source. Report both
two-year totals and the delta.

## Task 3 , flywheel with decay (C03)

q = 100k, c = 0.02, g = 0.001, decay 0.9, 6 months. Report
the cumulative gain each month. Then the low-volume case:
q = 1k, same c and g, 6 months.

## Task 4 , custom versus generic with quality value (C04)

F = 30k, p_g = 4.00, p_c = 1.50, q_g = 0.78, q_c = 0.91.
Sweep Q over [1B, 5B, 12B, 20B] with w = 0, then repeat at
Q = 5B with w = 2,000 per quality point. Report the winner
at each.

## Task 5 , break-even with idle time (C05)

F = 30k, p_a = 4.00, p_h = 1.50. Report Q*. Then the fleet
idles half the time, so effective p_h doubles. Report the
new Q* and the verdict at 15B tokens per month.

## Task 6 , cache economics with infra cost (C06)

15B tokens per month, c_m = 4.00, c_c = 0.25, cache infra
3k per month. Sweep h over [0.0, 0.3, 0.6, 0.9]. Report
effective cost per 1M and net monthly saving at each.

## Task 7 , latency tradeoff across batch sizes (C07)

V = 2M, s = 0.01 per 100 ms, L0 = 400. Batch sizes [1, 2,
4, 8] give L = [400, 600, 900, 1200] and compute savings
[0, 12k, 22k, 30k]. Report latency cost and net at each.
Then repeat with s = 0.001.

## Task 8 , unit cost with labor (C08)

10,000 tasks per month, 0.50 compute each, t = 10 min,
wage 40, f_ops 8k. Sweep e over [0.10, 0.04, 0.01]. Report
total and per-task cost at each.

## Task 9 , cost per success across success rates (C09)

c = 0.50, r = 1. Sweep s over [0.9, 0.6, 0.3, 0.2].
Report cost per success at each, plus the premium model
(c = 2.00, s = 0.95, r = 0).

## Task 10 , average cost curve and the pilot trap (C10)

F = 30k, v = 1.50. Sweep Q (1M units) over [100, 500,
2,000, 12,000, 100,000]. Report the average at each. Flag
the pilot trap at Q = 500.

## Task 11 , switch payback with a quality penalty (C11)

S = 250k. Sweep monthly saving d over [5k, 12k, 20k].
Report payback at each. Then vendor B scores 5 points
worse at 100k per point per year: rework the d = 12k case.

## Task 12 , break-even with soft versus hard value (C12)

F = 38k, v = 1.17 (0.50 compute + 0.67 review labor), s =
0.8. Sweep w over [5, 3, 2] (hard dollars). Report
break-even tasks at each. Then w = 5 soft with only 2 hard:
report the honest verdict against 18k actual tasks.
