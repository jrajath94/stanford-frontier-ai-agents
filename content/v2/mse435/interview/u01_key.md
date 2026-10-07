# Interview key , U01

Each answer: minimum sufficient explanation, strong answer,
common red flags, scoring rubric, remediation.

## B1

Sufficient: revenue = P x Q. 0.8P x 2Q = 1.6PQ, revenue rose 60
percent. Volume rose more than price fell, so demand is elastic
(|E| > 1).
Strong: computes the arc elasticity: (dQ/Q)/(dP/P) = 1.0 /
-0.2 = -5, elastic.
Red flags: "revenue fell because price fell", confusing
elasticity sign.
Rubric: 2 points for the revenue arithmetic, 1 for the
elasticity conclusion.
Remediation: rework C02 with the percent-change definition.

## B2

Sufficient: chips sell compute, clouds/DCs sell reliable compute
at scale, model labs sell intelligence (weights or API), apps
sell outcomes.
Strong: adds the interface at each handoff (network, API/weights,
UI/API) and one sentence on why layers stay separate (different
efficient scales).
Red flags: naming companies instead of functions, merging cloud
and chips.
Rubric: 1 point per layer named with its product.
Remediation: redraw the C06 stack from memory.

## B3

Sufficient: contribution 2 dollars, break-even 1M units. At price
1 dollar the contribution is zero and no volume breaks even.
Strong: adds that the formula returns a negative or zero, which
is the algebra refusing the question, and that the firm should
shut down if price stays at variable cost.
Red flags: reporting a positive break-even at P = v.
Rubric: 2 for the number, 1 for the P = v diagnosis.
Remediation: C03 derivation of Q_be and the P > v condition.

## B4

Sufficient: a forecast is a bet about the future with
uncertainty, an observation is measured reality. Capacity or
contract decisions need the range.
Strong: names bias versus noise and says the range sets the
hedge (commit level, option value).
Red flags: treating a point forecast as a promise.
Rubric: 1 for the distinction, 1 for a decision that needs the
range, 1 for bias/noise.
Remediation: C09 and C11.

## B5

Sufficient: substitutes. Cross elasticity = (-0.08)/(-0.10) =
+0.8 > 0.
Strong: notes the magnitude (strong substitution) and the
short-run caveat (contracts may delay the switch).
Red flags: sign error.
Rubric: 2 for sign and classification, 1 for the caveat.
Remediation: C02 toy pairs.

## B6

Sufficient: (1) is the basket identical across the two years?
(2) what is the matched-model change versus the mix effect?
Strong: asks for the quality adjustment too, and refuses to
repeat until the decomposition is shown.
Red flags: accepting the index at face value.
Rubric: 1 per question, 1 for refusing without the split.
Remediation: C10.

## L1

L1.1 Sufficient: the price where quantity demanded equals
quantity supplied.
L1.2 120 - 2P = 30 + 4P gives 90 = 6P, P = 15, Q = 90.
L1.3 New supply: Qs = 10 + 4P. 120 - 2P = 10 + 4P gives
110 = 6P, P = 18.33, Q = 83.33.
L1.4 Causes: demand intercept below supply intercept (a < c),
or a sign error on a slope. Guard: assert a > c and b, d > 0
before solving.
L1.5 The model proves the direction and size of the resting
point under its assumptions. It proves nothing about timing.
Falsified by: persistent off-equilibrium prices (controls,
contracts) or a measured supply curve that did not shift.
Red flags: treating the comparative static as a dated
prediction.
Rubric: 2 points each for L1.2-L1.3 arithmetic, 1 each for the
rest.
Remediation: C01 sections 5 and 11.

## L2

L2.1 Value capture: the share of total created value a firm or
layer keeps as profit.
L2.2 Chips: 20 - 10 = 10. App: 35 - 20 - 5 = 10.
L2.3 Model price = cost makes its share zero, recompute with
the freed margin flowing to buyers (lower final price) or to
adjacent layers, per the new prices.
L2.4 Real causes: (1) loss-leader pricing to win the workload,
(2) transfer price set by policy inside an integrated firm.
L2.5 Counterexample: a commodity app over a scarce model or
scarce chips, the bottleneck layer captures most. Reason:
capture follows the inability to route around the layer.
Red flags: confusing capture with revenue.
Rubric: 2 for L2.2, 1 each for the rest.
Remediation: C05.

## A1

Sufficient: annuity factor at 8 percent, 4 years =
(1 - 1.08^-4)/0.08 = 3.3121. Rent PV = 380,000 x 3.3121 =
1,258,606. Buy PV = 1,200,000 + 30,000 x 3.3121 = 1,299,364.
Rent wins by about 40,758. Assumption most likely to flip:
rent escalation or server life beyond 4 years.
Strong: also gives the crossover (buy wins if rent rises ~3
percent per year or life extends past ~4.5 years).
Red flags: forgetting maintenance, ignoring discounting.
Rubric: 2 for PVs, 1 for recommendation, 1 for the fragile
assumption.
Remediation: C04 lab task 4.

## A2

Sufficient: errors [-0.6, -0.1, +1.2]. Bias = 0.5/3 = 0.167.
MSE = (0.36 + 0.01 + 1.44)/3 = 0.603. Variance = 0.603 -
0.028 = 0.575. Noisy more than biased, fix is better
calibration of the upside case, not a uniform shift.
Strong: notes n = 3 makes the variance estimate itself noisy.
Red flags: calling it biased because one error is large.
Rubric: 2 for the numbers, 1 for the diagnosis, 1 for the fix.
Remediation: C09.

## D1

Sufficient: bugs: (1) division by zero when p == v, (2) silent
negative or zero result when p < v. Fix: return None (or raise)
when p <= v. Checks: p <= v guard, fc, v >= 0, result > 0.
Strong: also validates types and adds a test at Q_be where
profit is zero.
Red flags: catching the exception instead of guarding the
domain.
Rubric: 1 per bug, 1 for the fix, 1 for checks.
Remediation: C03 section 7.

## S1

Sufficient: year 1: price spikes or queues form, quantity cannot
move. The model gives the resting point after capacity arrives
(~2 years). A 1-year contract should be priced on year-1
conditions (scarcity), not the resting point.
Strong: names the mechanism (existing capacity allocated by
queue or surge pricing) and says the buyer should buy options
or shorter commits.
Red flags: quoting the equilibrium price for a 1-year deal.
Rubric: 2 for year-1 dynamics, 1 for the resting point, 1 for
the contract advice.
Remediation: C01 section 11.

## S2

Sufficient: revenue math: one month at 3x conversion, then back
to base, do not annualize the spike. Cost math: support load
spikes with users, and bad hires persist after the spike.
Decision: staff with temps or overtime, hire permanent only on
sustained conversion.
Strong: computes the one-month revenue bump (10M x 0.06 x 20 =
12M vs 4M base) and names the trap (extrapolating a feature
spike).
Red flags: multiplying the spike month by 12.
Rubric: 1 per math change, 2 for the staffing decision.
Remediation: C07 and C08.

## R1

Sufficient: threats: (1) confounders (model releases,
funding cycles move both), (2) reverse causality (more
startups bid up GPU demand and prices), (3) n = 8, overfit.
Cheapest tests: (1) control for release dates/funding, (2)
lag the price (does formation follow price?), (3) split sample
or permutation test. Belief needs: out-of-sample prediction or
an instrument (e.g. a supply shock unrelated to demand).
Strong: names the identifying assumption explicitly and
proposes a falsifier (formation rises while prices are flat).
Red flags: accepting correlation as cause, demanding a perfect
experiment instead of a better design.
Rubric: 1 per threat with test, 1 for the belief condition.
Remediation: C09, C12, P22.
