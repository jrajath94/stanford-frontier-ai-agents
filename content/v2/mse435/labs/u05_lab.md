# Lab U05 , Coding/application and life-science economics

Run `python3 u05_lab_run.py` to verify every computed answer.
The key in `u05_lab_key.md` records the verified outputs. Work
each task by hand first, then check against the runner.

## Task 1 , vibe versus verified with expensive defects (C01)

L = 1,000, d_v = 40, d_f = 4 per 100, r = 3,000. Sweep f
over [25, 100]. Report both totals at each and the tie
review cost.

## Task 2 , dataset cost with expert labels (C02)

n = 100k, T = 200k. Sweep c over [0.50, 5.00]. Report D and
the total at each.

## Task 3 , cohort margins with a viral shift (C03)

p = 10. Cohorts (share, usage): light (0.80, 0.50), medium
(0.15, 5.00), power (0.05, 25.00). Report the blended
margin. Then the viral shift: power share 0.15 at usage
50, light 0.70. Report the new blend.

## Task 4 , license versus service with churn (C04)

L = 500, p = 20, i = 3, n = 36. Sweep churn over [0, 0.03,
0.10]. Report the service margin at each and the winner.

## Task 5 , workflow speedup with a quality penalty (C05)

T_d = 2, T_w = 4, k = 7. Sweep extra_cycles over [0, 0.30,
0.60]. Report the speedup and the time ratio at each.

## Task 6 , funnel with correlated failures (C06)

Base funnel: ns = [10k, 200, 5, 1], cs = [0.10, 5k, 2M,
100M]. Report the total. Then AI doubles assay survivors
to 400. Then triage cuts assays to 100 with n1 = 100k at
c1 = 0.01. Report all three totals.

## Task 7 , protection with a sensitivity sweep (C07)

L = 50M, C = 200k. Sweep p over [0.001, 0.004, 0.01,
0.02]. Report E and the decision at each.

## Task 8 , validation caps with assay innovation (C08)

B = 400k. Sweep c over [5k, 1k]. Report feasible n at
each. Then n = 200 proposals: report the bill at each c.

## Task 9 , expert bottleneck with triage (C09)

w = 300, 320 expert hours per month. Sweep h over [500,
150, 80]. Report the bill and max releases per month at
each.

## Task 10 , adoption ramp with a stall case (C10)

V = 1M, r = 10 percent. Curves: base [0.10, 0.35, 0.70],
trained [0.20, 0.55, 0.85] with 200k cost, stall [0.10,
0.10, 0.10]. Report the PV of each.

## Task 11 , escalation with an upgrade payback (C11)

50,000 tasks per year, c_e = 150, compute 2.00. Sweep e
over [0.05, 0.02]. Report per-task and yearly cost at
each. An upgrade costs 500k once and moves e from 0.05 to
0.02: report the payback in years.

## Task 12 , OOD value with a novelty floor (C12)

v = 50k, c = 5k, a_in = 0.95, a_ood = 0.55. Sweep o over
[0, 0.3, 0.7, 1.0]. Report true accuracy and expected net
at each. Then a_ood = 0.20 at o = 0.70: report the net.
