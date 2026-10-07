# Lab key , U01

Verified outputs from `u01_lab_run.py`, executed 2026-10-07.
All values computed, none hand-typed.

## Task 1

- M1: P* = 16.0, Q* = 68.0
- M2: P* = 24.0, Q* = 92.0
- M3: P* = 23.33, Q* = 56.67

## Task 2

- GPUs and power: E = -0.30, complements
- API tokens and self-host: E = +0.50, substitutes
- Vendor A and B: E = +0.80, substitutes

## Task 3

FC = 100,000, v = 5, Q = 50,000 gives ATC = 7.0 in all rows.

| P | Q_be |
|---|------|
| 10 | 20,000 |
| 15 | 10,000 |
| 20 | 6,666.67 |
| 25 | 5,000 |

## Task 4

| r | buy PV | rent PV |
|---|--------|---------|
| 0.05 | 217,729.75 | 212,757.03 |
| 0.10 | 215,849.33 | 190,191.93 |
| 0.15 | 214,274.89 | 171,298.70 |

Rent wins at all three rates in this toy. The decision is
closest at r = 0.05 (gap 4,972.72 dollars).

## Task 5

- Chain A shares: chips 6.0, cloud 6.4, model 15.8, app 44.8.
  Total created value = 73.0 dollars.
- Chain B shares: chips 6.0, cloud 6.4, model 0.0, app 30.6.
  Total created value = 43.0 dollars.
- The freed value mostly left the chain: the final price fell
  from 100 to 70, so 27 of the 30 freed dollars went to buyers
  and 3.6 stayed with the app (44.8 - 30.6 = 14.2 lost by the
  app, 15.8 lost by the model, buyers gained 30).

## Task 6

- Base: 0.0200 dollars per answer
- After 50 percent chip cut: 0.0190 (5.0 percent saved)
- After 50 percent facility cut: 0.0150 (25.0 percent saved)

## Task 7

- Base profit: 1,500,000 dollars per month
- At 1.5 percent conversion: 500,000 dollars per month
- Sensitivity: 2,000,000 dollars per percentage point of
  conversion, i.e. 200,000 dollars per 0.1 point

## Task 8

k = 0.1: 0.2500. k = 0.25: 0.2000. k = 0.5: 0.1500. Larger k
means more friction: gains arrive slower with adoption.

## Task 9

- Set A: bias 0.0, MSE 4.667, variance 4.667
- Set B: bias +2.0, MSE 4.667, variance 0.667
- Set B is fixable: subtract 2 from every forecast. Set A has
  no bias to fix.

## Task 10

- Matched change: -40 percent
- Observed change: -60 percent
- Mix effect: -20 points

## Task 11

- Build 1.0: expected cost 1.875M dollars
- Build 1.5: expected cost 2.375M dollars
- Build 1.0 wins. It accepts a 0.25 probability of shortfall in
  the 2.0 case (expected 0.75M) to avoid 0.5M of extra certain
  capacity cost.

## Task 12

1. OFFICIAL-SCHEDULE , materials page, fetched 2026-10-07
2. OFFICIAL-SCHEDULE , materials page, fetched 2026-10-07
3. TOY , computed in lesson C03
4. NOT IN SOURCE , no dated price series inspected
5. SPEAKER CLAIM , EVIDENCE PENDING, recording not watched
6. TOY , computed in lesson C01
