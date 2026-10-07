# Lab U06 , Capstone evidence and stakeholder defense

Run `python3 u06_lab_run.py` to verify every computed answer.
The key in `u06_lab_key.md` records the verified outputs. Work
each task by hand first, then check against the runner.

## Task 1 , baseline with seasonality (C01)

n = 200, t = 45, c = 38, d = 250, err 0.04 at 120.
Report the baseline triple. Then December runs 40 percent
hotter for 22 days: report the seasonal uplift.

## Task 2 , adoption ramp with a failed driver (C02)

S = 642k, r = 10 percent. Curves: plan [0.20, 0.50,
0.80], stalled [0.20, 0.30, 0.35]. Report the PV of each
and the verdict.

## Task 3 , metric gate with a moved goalpost (C03)

Targets: cost <= 30, resolution >= 0.85, csat >= 4.0.
Cases: (28, 0.87, 4.2), (28, 0.79, 4.2), (28, 0.79, 4.2)
with the csat floor moved to 3.8 after the miss. Report
the gate at each.

## Task 4 , gate with a tuned set (C04)

Thresholds: acc >= 0.90, p99 <= 2.0, esc <= 0.10.
Models: A (0.91, 1.8, 0.08), B (0.89, 1.8, 0.08), C
(0.93, 2.3, 0.08). Report pass/fail for each.

## Task 5 , forecast with an advocacy case (C05)

Cases (value, weight): honest [(200k, 0.25), (450k,
0.50), (800k, 0.25)], advocacy [(200k, 0.15), (450k,
0.35), (800k, 0.50)]. Report E and downside for each.

## Task 6 , tornado with an interaction note (C06)

Base 768k. Drivers: adoption [400k, 900k], labor cost
[600k, 850k], volume [650k, 830k], quality [700k, 820k].
Report the ranking. Then the pilot narrows adoption to
[700k, 850k]: report the new ranking.

## Task 7 , TCO with runaway run cost (C07)

B = 400k, R = 300k, L = 150k, K = 100k, 3 years. Report
the TCO and the build share. Then R doubles in year 2:
report the new TCO.

## Task 8 , tiered governance (C08)

Changes: 40 low-stakes (d = 0.5 wk, g = 10k, p = 0.01, I
= 200k), 10 high-stakes (d = 2 wk, g = 10k, p = 0.05, I
= 5M). Report board cost and risk per change for each
tier and the regime verdict per tier.

## Task 9 , rollback timing (C09)

b = 0.04, trigger 2x for 1 hour. Canary hours: [0.05,
0.09, 0.10] and [0.05, 0.06, 0.05]. Report trigger/not
for each. Then rollback takes 4 hours at 1 percent traffic,
50k cases per day, 120 per error: report the damage.

## Task 10 , handoff checklist pricing (C10)

s_wk = 2,000, h0 = 4, h1 = 1, c = 500, 24 incidents per
year. Report cost, value, net. Then 6 of 12 checklist
items missing at 30 min each: report the first-incident
price.

## Task 11 , alternatives with blind scoring (C11)

Weights cost 0.6, control 0.4. Team scores: build (7,
9), vendor (9, 5), hire (5, 7). Blind scores: build (6,
7), vendor (9, 5), hire (5, 7). Report both rankings and
the honesty verdict.

## Task 12 , decision rule with a moved threshold (C12)

Y = 0.15. Pilots: (0.18, 0.05), (0.22, 0.04). Report the
lower bound and verdict for each. Then the team moves Y
to 0.10 after seeing the first pilot: report what broke.
