# Interview bank , U03 , Enterprise infrastructure and token markets

Closed-book transfer, not recognition. Answer key is separate in
`u03_key.md`.

## Breadth (6)

B1. State the service-as-software thesis and the one condition
    that must hold for it to work.

B2. A token market has Qd = 100 - 2P and Qs = 20 + 3P (B/day,
    $/1M). Give P* and Q*.

B3. Training cost 5M, lifetime 500B tokens, inference 4 $/1M.
    What is the unit cost, and which part dominates?

B4. Name the three slices of a unit price and what each pays
    for.

B5. Open stack: 30k/mo hosting + 200k integration. Closed:
    40k/mo API + 50k integration, 24 months. Which wins and by
    how much?

B6. What does a tornado chart rank, and what is its key
    limitation?

## Deep ladders (2 x 5)

### L1 , the contract trap

L1.1 Define a long compute contract as insurance.
L1.2 Toy: 120 blocks/yr, 3.00 contract, market [4,3,2], r =
    10 percent, 3 years. Which PV is smaller?
L1.3 The market falls faster: [4,2,1]. Recompute the winner.
L1.4 Usage falls 50 percent in year 2 under take-or-pay.
    What is the effective price per used token?
L1.5 Critique: "we locked a great price". What did the firm
    actually buy, and what would prove it was a bad buy?

### L2 , inference at scale

L2.1 Define the two cost shapes of a model business.
L2.2 Toy: T = 5M, V = 50B, i = 4. Compute the unit cost.
L2.3 Find the lifetime volume where training cost equals
    inference cost per 1M.
L2.4 The lab retrains monthly at 500k per run. Rework the
    formula.
L2.5 Critique: "training cost does not matter at scale".
    Name the case where it still matters.

## Analytical / quantitative (2)

A1. A 1,000-GPU fleet serves 50 tok/s/GPU at U = 0.85. Compute
    B tokens per day. At 4 $/1M tokens, what is the daily
    revenue capacity? The fleet costs 1.08 $/GPU-h. What is
    the daily gross margin?

A2. Three serving stages have capacities [120, 45, 90] rps.
    Find the system rate and each stage's utilization. A
    300k upgrade doubles one stage. Which stage, and what is
    the new rate? What does the next 300k buy?

## Implementation / debug (1)

D1. The contract PV function below has a bug that makes the
    market leg wrong. Find it, fix it, and state the check
    that catches it.

```python
def contract_pv(q, pc, path, r=0.10):
    a = sum(1 / (1 + r) ** (t + 1) for t in range(len(path)))
    c_pv = q * pc * a
    m_pv = q * sum(path) / (1 + r) ** len(path)
    return c_pv, m_pv
```

## Changed-constraint scenarios (2)

S1. Your token equilibrium assumed fast clearing. The vendor
    freezes the price at 16 and rations by rate limit during
    the demand shock. Describe who gets tokens, what the
    implicit price is, and which customers leave first.

S2. Your open/closed math assumed the open model meets the
    quality bar. It scores 5 points worse, and each point
    costs 100k per year in lost conversion. Rework the
    two-year comparison and state the general rule.

## Research critique (1)

R1. A consultancy claims "enterprises save 10x with AI
    service desks" from three self-selected case studies with
    no control group. Name three threats, the cheapest test
    for each, and what evidence would make you believe the
    10x.
