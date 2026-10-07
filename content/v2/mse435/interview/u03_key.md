# Interview key , U03

## B1

Sufficient: AI turns labor-like services into software-priced
products. Condition: the AI output meets the quality bar.
Strong: adds the linearity argument (human linear, AI
sublinear in tasks).
Red flags: "AI replaces all labor".
Rubric: 1 for the thesis, 1 for the condition, 1 for the
cost shape.
Remediation: C01.

## B2

Sufficient: P* = 16, Q* = 68.
Strong: states units (dollars per 1M tokens, B tokens per
day).
Red flags: unit errors.
Rubric: 1 per value, 1 for units.
Remediation: C05.

## B3

Sufficient: amortized 10, total 14 $/1M. Inference dominates
(4 vs 10... check: 10 > 4, so training still leads at 500B,
the crossover is 1.25T).
Strong: catches that at 500B training still leads and names
the 1.25T crossover.
Red flags: "training never matters".
Rubric: 1 for the numbers, 2 for the dominance call.
Remediation: C07.

## B4

Sufficient: true unit cost, margin, risk buffer. Cost pays
the fleet, margin pays the business, buffer pays for abuse
and spikes.
Strong: notes the buffer is the first lie in a price war.
Red flags: "price equals cost".
Rubric: 1 per slice.
Remediation: C11.

## B5

Sufficient: open 920k, closed 1,010k, open wins by 90k.
Strong: adds that the control premium only needs to be
non-negative here.
Red flags: ignoring integration.
Rubric: 2 for the totals, 1 for the winner.
Remediation: C03.

## B6

Sufficient: ranks drivers by swing on the outcome. Limit:
one-at-a-time, no interactions, not a forecast.
Strong: adds "rank by actionable swing".
Red flags: reading it as a prediction.
Rubric: 1 for the rank, 1 for the limit, 1 for the
actionable note.
Remediation: C12.

## L1

L1.1 A long contract is price insurance: lock the price and
the demand against market moves.
L1.2 Contract PV 895.27, market 914.20, contract wins.
L1.3 Market PV 724.87, market wins. The path flipped the
deal.
L1.4 Year-2 billing stays 360 dollars for 60 used blocks:
effective 6.00 per block, double the headline.
L1.5 It bought insurance against high prices plus a
take-or-pay obligation. Proven bad by: realized market PV
below contract PV, or usage far under commit.
Red flags: "3 dollars was cheap".
Rubric: 2 for L1.2-L1.3, 1 each for the rest.
Remediation: C08.

## L2

L2.1 Training: one-time tuition spread over tokens.
Inference: rent per token forever.
L2.2 Amortized 100, total 104 $/1M.
L2.3 T/V x 1M = i gives V = 1.25T tokens.
L2.4 Unit = (500k x 12)/V x 1M + i, tuition recurs yearly.
L2.5 Retraining cadence (monthly/weekly) keeps tuition
material, or tiny lifetime volume.
Red flags: dropping T entirely.
Rubric: 2 for L2.2, 1 each for the rest.
Remediation: C07.

## A1

Sufficient: 1,000 x 50 x 0.85 x 86,400 = 3.672T tokens per
day = 3,672,000 blocks. Revenue capacity = 3,672,000 x 4 =
14.688M per day. Fleet cost = 1.08 x 1,000 x 24 = 25,920
per day. Gross margin = 14.662M per day.
Strong: notes the margin is gross (no staff, no failures)
and that competition attacks exactly this gap.
Red flags: unit slips (tokens vs blocks).
Rubric: 2 for supply, 1 for revenue, 1 for cost, 1 for
margin.
Remediation: C04, C11.

## A2

Sufficient: rate = 45 rps. Utils: 0.375, 1.0, 0.5. Upgrade
stage 2 (the bottleneck) to 90: new rate = min(120, 90, 90)
= 90 rps. The next 300k buys nothing until stage 1 or 3
moves, the next binding stage is 1 and 3 tied at 90... now
min(120, 90, 90) = 90, so the next upgrade must target
stage 1 or 3 (both bind at 90 after stage 2 is fixed...
check: stages [120, 90, 90], min = 90, stages 2 and 3
bind). Correct read: after the first upgrade the line is
[120, 90, 90], stages 2 and 3 bind, the next 300k goes to
stage 3 (or 2), giving [120, 90, 180] -> 90, still bound
by stage 2. So the next 300k should double stage 2 again
to 180: [120, 180, 90] -> 90, bound by stage 3. The honest
answer: each 300k moves the min one step, sequence the
upgrades 2, 3, 2 (or 2, 2, 3) and remeasure each time.
Strong: states the moving-bottleneck rule explicitly.
Red flags: spending both on stage 1.
Rubric: 2 for rate and utils, 2 for the first upgrade, 2
for the sequence logic.
Remediation: C06.

## D1

Sufficient: bug: the market leg discounts the SUM of prices
once at the final year instead of discounting each year's
price at its own year. Fix:

```python
m_pv = q * sum(p / (1 + r) ** (t + 1)
               for t, p in enumerate(path))
```

Check: at a flat path the market PV must equal the contract
PV when pc equals that flat price.
Red flags: "fixing" by changing the contract leg.
Rubric: 1 for the bug, 2 for the fix, 1 for the check.
Remediation: C08.

## S1

Sufficient: tokens go by rate-limit tier, contract size, or
queue order. Implicit price = wait cost + forgone value.
The most price-sensitive and least locked-in customers
leave first (self-serve, small accounts).
Strong: notes the vendor learns demand from the queue and
that the freeze subsidizes large incumbents.
Red flags: "everyone is fine, price is stable".
Rubric: 1 per part, 1 for who leaves.
Remediation: C05 section 11.

## S2

Sufficient: quality loss = 5 x 100k x 2 years = 1M. Open
total = 920k + 1M = 1.92M vs closed 1.01M. Closed wins.
Rule: quality deltas price in dollars first, hosting math
second.
Strong: states the general rule as "never let a small
certain saving override a large uncertain quality loss
without pricing it".
Red flags: keeping the hosting-only answer.
Rubric: 2 for the rework, 1 for the rule.
Remediation: C03 section 11.

## R1

Sufficient: threats: (1) self-selection (only winners
publish), (2) no control (maybe tickets fell anyway),
(3) cost shifting (the AI cost hides in another budget).
Tests: (1) ask for the full client list, not three, (2)
before/after with a comparable non-adopter, (3) audit the
full cost stack. Belief needs: randomized or
matched-control rollout with full costs.
Strong: prices the missing counterfactual explicitly.
Red flags: accepting case studies as evidence.
Rubric: 1 per threat with test, 1 for the belief bar.
Remediation: C01, C02, C12.
