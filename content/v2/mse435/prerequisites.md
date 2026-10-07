# Prerequisites , mse435

Shared prerequisite modules are linked, not rebuilt. Each unit
below links its bridges and carries local remediation: the smallest
self-contained repair that lets a learner continue without leaving
this file.

## Shared bridges (linked)

- P01 , Numeracy, algebra, and notation:
  `../shared/prerequisites/p01_numeracy.md`
- P15 , Hardware and computer architecture:
  `../shared/prerequisites/p15_hardware.md`
- P16 , Distributed systems and networking:
  `../shared/prerequisites/p16_distributed.md`
- P23 , Economics and decision analysis:
  `../shared/prerequisites/p23_economics.md`
- P24 , Production ML and stakeholder foundations:
  `../shared/prerequisites/p24_production_ml.md`

## U01 , bridges P01, P23

Local remediation U01-R1 , numbers with units. Every quantity in
U01 carries a unit: dollars, tokens, hours, or dollars per unit.
Check the unit of each term before adding two numbers. If the units
do not match, the addition is wrong even when the arithmetic is
right. Example: 100 dollars of fixed cost + 5 dollars per token of
variable cost is not 105 dollars. It is 100 + 5 x, where x counts
tokens.

Local remediation U01-R2 , percentages and ratios. A 10 percent
price cut on a 20 dollar base gives 18 dollars, computed as
20 x (1 - 0.10). A ratio has no unit: cost divided by revenue is a
pure number. A percentage point is not a percent: a margin that
moves from 20 percent to 25 percent rose 5 percentage points, which
is a 25 percent relative rise.

Local remediation U01-R3 , supply and demand reading. Read P23
sections on supply/demand, fixed/variable costs, capital/operating
expense, and unit economics. The U01 lesson re-derives every curve
it uses, so P23 is a reference, not a gate.

## U02 , bridges P15, P23

Local remediation U02-R1 , power and energy. Power is a rate,
measured in watts (joules per second). Energy is an amount, measured
in watt-hours or joules. A GPU that draws 700 W for one hour uses
0.7 kWh of energy. Cost scales with energy, capacity scales with
power. Confusing the two breaks every data-center calculation in
U02.

Local remediation U02-R2 , FLOPs versus FLOP/s. FLOPs count
operations (an amount). FLOP/s counts operations per second (a
rate). A training run needs FLOPs. A cluster delivers FLOP/s. Time
equals FLOPs divided by FLOP/s, adjusted for utilization below 1.

Local remediation U02-R3 , straight-line depreciation. An asset
that costs C dollars and lasts T years loses C / T dollars of book
value per year. The U02 lesson re-derives the per-GPU-hour capital
charge from this rule.

## U03 , bridges P16, P23, P24

Local remediation U03-R1 , tokens as the unit of account. One
million tokens is the billing block in the U03 toy market. Price
quotes in dollars per 1M tokens convert to dollars per token by
dividing by 1,000,000. Keep the block unit explicit in every
calculation.

Local remediation U03-R2 , contracts as cash-flow series. A
contract that pays X dollars per year for T years has present value
sum over t of X / (1 + r)^t, with discount rate r. The U03 lesson
re-derives this for the long-contract concept.

Local remediation U03-R3 , latency versus throughput. Read P16 on
latency versus throughput before U03-C06 and U03-C07. Batching
raises throughput and usually raises latency. The lesson shows the
trade with numbers.

## U04 , bridges P19, P23, P24

Local remediation U04-R1 , hit rate arithmetic. The hit rate h
is a share between 0 and 1. Effective price = h x cheap +
(1 - h) x dear. At h = 0.6, cheap 0.25, dear 4.00: 0.15 +
1.60 = 1.75. Measure h on your own traffic. Vendor slides
overstate it.

Local remediation U04-R2 , break-even division. Q* = F /
(p_a - p_h). Fixed cost in dollars per month divided by a
price difference in dollars per block gives blocks per
month. If p_a - p_h is negative, hosting never wins: check
the sign before dividing.

Local remediation U04-R3 , retry compounding. Success with
r retries = 1 - (1 - s)^(r+1), a power, not a product.
At s = 0.6, r = 1: 1 - 0.16 = 0.84.

## U05 , bridges P21, P22, P23, P24

Local remediation U05-R1 , finite horizons. A 36-month
contract gives at most 36 months of retained life, not the
infinite-horizon 1/churn. At 3 percent monthly churn the
finite life is 22.2 months. Use the contract length.

Local remediation U05-R2 , funnel multiplication. Funnel
cost = sum over stages of survivors x cost per survivor.
Doubling survivors doubles every downstream stage's cost.
Add, do not average.

Local remediation U05-R3 , expected loss. Expected loss =
probability x loss. Buy protection when its price is below
the expected loss with margin.

## U06 , bridges P07, P22, P23, P24

Local remediation U06-R1 , TCO addition. TCO = build +
3 x (run + labor) + risk reserve. Build is paid once, run
and labor recur, the reserve is a cushion. Never present
build as the total.

Local remediation U06-R2 , ramped present value. Savings
in year t are a_t x S / (1 + r)^t with the adoption ramp
a_t, not S / (1 + r)^t. The ramp [0.20, 0.50, 0.80] cuts
the naive PV by more than half.

Local remediation U06-R3 , pre-registration. Fix the
threshold Y, the duration D, and the instrument before the
pilot starts. Invest iff the interval's lower bound L
exceeds Y. Moving Y or D after seeing data voids the
decision.

Answer closed-book. Score with `keys/diagnostic_key.md`. Any score
below 8 means: read the matching shared bridge first, then the
local remediation above.

1. A server costs 12,000 dollars and draws 1,200 W. Electricity
   costs 0.10 dollars per kWh. What is the energy cost of running it
   for 30 days at full draw? (U02-R1)
2. Fixed cost 50,000 dollars per month, variable cost 3 dollars per
   unit, price 8 dollars per unit. What monthly volume breaks even?
   (U01-R1)
3. A price falls from 40 dollars to 30 dollars. State the change in
   percentage points is wrong here, why, and give the percent
   change. (U01-R2)
4. A workload needs 10^18 FLOPs. A cluster delivers 10^15 FLOP/s at
   40 percent utilization. How many seconds does the run take?
   (U02-R2)
5. An asset costs 90,000 dollars and lasts 3 years. What is the
   straight-line depreciation per year? (U02-R3)
6. A token price is 4 dollars per 1M tokens. A request uses 2,000
   tokens. What does the request cost? (U03-R1)
7. A contract pays 100,000 dollars at the end of each of 2 years.
   Discount rate 10 percent. What is the present value? (U03-R2)
8. Demand is Q = 100 - 2P. Supply is Q = 20 + 3P. What are the
   equilibrium price and quantity? (U01)
9. Raising batch size from 1 to 8 doubles throughput but triples
   latency. A user needs latency under 2 seconds and the 8-batch
   latency is 3 seconds. Which constraint binds? (U03-R3)
10. Fixed cost 0, variable cost 5 dollars per unit, price 5 dollars
    per unit. What is the margin per unit, and what does a zero
    margin imply for scaling losses? (U01-R1)
