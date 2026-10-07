# Lab U01 , AI economics and the full value chain

Run `python3 u01_lab_run.py` to verify every computed answer. The
key in `u01_lab_key.md` records the verified outputs. Work each
task by hand first, then check against the runner.

## Task 1 , equilibrium solver (C01)

Three toy GPU-hour markets. For each, compute P* and Q* by hand,
then verify.

- M1: Qd = 100 - 2P, Qs = 20 + 3P
- M2: Qd = 140 - 2P, Qs = 20 + 3P
- M3: Qd = 80 - P, Qs = 10 + 2P

## Task 2 , classify pairs (C02)

Classify each pair as complements, substitutes, or independent
from the percent changes, and compute the cross elasticity.

- GPUs and power: GPU price -20 percent, power demand +6 percent
- API tokens and self-host: API price -20 percent, self-host
  demand -10 percent
- Two model vendors: vendor A price -10 percent, vendor B demand
  -8 percent

## Task 3 , break-even sweep (C03)

FC = 100,000 dollars per month, v = 5 dollars per block. Sweep
price P over [10, 15, 20, 25]. For each, compute Q_be and ATC at
Q = 50,000.

## Task 4 , buy versus rent (C04)

Server capex 200,000, maintenance 5,000 per year, rent 60,000 per
year, horizon 4 years. Compute buy PV and rent PV at r = 0.05,
0.10, 0.15. Name the rate where the decision is closest.

## Task 5 , capture shares (C05)

Chain A: costs [5, 4, 8, 10], prices [11, 21.4, 45.2, 100].
Chain B (free model layer): costs [5, 4, 8, 10], prices
[11, 21.4, 29.4, 70]. Compute each layer's capture share and the
total created value. Where did the freed value go?

## Task 6 , stack shock (C06)

One answer costs chip 0.002 + facility 0.010 + model 0.008 =
0.020 dollars. Apply a 50 percent chip price cut, then a 50
percent facility cost cut. Report the total after each shock and
the percent saved.

## Task 7 , churn shock (C07)

Consumer toy: 10M users, 2 percent convert, ARPU 20 dollars,
cost 2.5M per month. Recompute monthly profit if conversion
falls to 1.5 percent. Then compute the profit change per 0.1
point of conversion.

## Task 8 , gain curve sweep (C08)

g_max = 0.30, adoption a = 0.50. Sweep k over [0.1, 0.25, 0.5].
Report realized gain for each k and state what k means in words.

## Task 9 , score forecasts (C09)

Observed price 4 dollars per 1M. Set A forecasts [2, 3, 7].
Set B forecasts [5, 6, 7]. Report bias, MSE, variance for each.
Which set is fixable, and how?

## Task 10 , decompose a price fall (C10)

2024 premium price 10, 2026 premium price 6, 2026 blend price 4.
Report matched change, observed change, and mix effect.

## Task 11 , capacity under uncertainty (C11)

Outcomes [0.5, 1.0, 2.0] B tokens/day, probs [0.25, 0.50, 0.25].
Capacity cost 1.0M per unit, shortfall cost 3.0M per unit.
Compute expected cost of building 1.0 and 1.5 units. Which
build wins, and what does the winner assume about the 2.0 case?

## Task 12 , label claims (C12)

Label each claim with class and evidence.

1. "Week 3 covers gigawatt-scale AI factories."
2. "The materials page lists a Crusoe lecture recording."
3. "ATC falls from 15 to 7 dollars in the C03 toy."
4. "Token prices fell 60 percent since 2024."
5. "A guest said inference will be nearly free."
6. "Q* = 68 in the C01 toy market M1."
