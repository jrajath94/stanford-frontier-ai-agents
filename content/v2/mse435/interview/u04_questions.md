# Interview bank , U04 , Enterprise knowledge and inference cloud

Closed-book transfer, not recognition. Answer key is separate in
`u04_key.md`.

## Breadth (6)

B1. Define internal knowledge access and the three conditions
    for it to create value.

B2. Write the cache effective-cost formula and compute it for
    h = 0.6, c_m = 4.00, c_c = 0.25.

B3. State the API-versus-hosting break-even formula. F = 30k,
    p_a = 4.00, p_h = 1.50. Give Q*.

B4. Why is cost per attempt the wrong unit for an AI workload,
    and what replaces it?

B5. Name the four parts of a vendor switching cost.

B6. A pilot reports inference at 61.50 dollars per 1M tokens.
    Why is that number misleading for the rollout plan?

## Deep ladders (2 x 5)

### L1 , the latency trap

L1.1 Define the latency/quality tradeoff in dollars.
L1.2 Toy: V = 2M, s = 0.01 per 100 ms, batch 8 moves L from
    400 to 1,200 ms and saves 30k per month in compute.
    Compute the net.
L1.3 The same batching serves an internal tool with
    s = 0.001. Recompute the net and the verdict.
L1.4 Abandonment makes s jump 10x past 2 seconds. The batch
    pushes p99 to 2.4 s. What breaks in the toy?
L1.5 Critique: "batching always cuts cost". Name the exact
    condition where it destroys value.

### L2 , the break-even hurdle

L2.1 Define workload break-even.
L2.2 Toy: F = 38k, v = 1.17, s = 0.8, w = 5. Compute the
    break-even task volume.
L2.3 The success rate falls to 0.6. Recompute. What is the
    verdict at 18k tasks per month?
L2.4 The "value" w = 5 is analyst time that is never
    redeployed. Only 2 dollars are hard. Rework the
    decision.
L2.5 Critique: "we break even at 13k tasks and we do 18k,
    so we are safe". Name two ways this comfort is false.

## Analytical / quantitative (2)

A1. A support desk runs 15B tokens per month. API price 4.00
    per 1M. Hosting: 30k fixed plus 1.50 per 1M. A cache
    with h = 0.6, c_c = 0.25, infra 3k per month sits in
    front of either option. Compute monthly cost for (a)
    API with cache, (b) hosting with cache. Which wins and
    by how much? What does the cache change about the
    break-even?

A2. 10,000 tasks per month. Compute 0.50 each. Escalation
    e = 0.10, review 10 min at 40 per hour. Fixed ops 8k.
    Each success is worth 5 dollars, s = 0.8. Compute (a)
    cost per successful task including labor and fixed ops,
    (b) monthly profit. Then: prompt work costs 25k once
    and cuts e to 0.04 permanently. What is the payback in
    months?

## Implementation / debug (1)

D1. The cost-per-success function below is wrong for r > 0.
    Find the bug, fix it, and state the check that catches
    it.

```python
def cost_per_success(c, s, r=1):
    attempts = 1 + (1 - s) * r
    p_ok = 1 - (1 - s) * (r + 1)
    return c * attempts / p_ok
```

## Changed-constraint scenarios (2)

S1. Your caching math assumed repeat queries. The product
    pivots to fresh, unique tickets and h falls to 0.05.
    Cache infra still costs 3k per month on 15B tokens.
    Rework the economics and advise.

S2. Your hosting break-even assumed steady volume. Traffic
    turns spiky: the fleet idles half the time. Rework
    p_h, the break-even, and the verdict at 15B tokens per
    month.

## Research critique (1)

R1. A vendor claims "our enterprise search lifts answer
    accuracy from 45 to 82 percent" from a demo on 200
    hand-picked questions with no control arm. Name three
    threats, the cheapest test for each, and what evidence
    would make you believe the 37-point lift.
