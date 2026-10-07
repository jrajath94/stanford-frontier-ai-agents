# Interview bank , U05 , Coding/application and life-science economics

Closed-book transfer, not recognition. Answer key is separate in
`u05_key.md`.

## Breadth (6)

B1. Write the vibe-versus-verified cost comparison and state
    when vibe coding wins.

B2. What is the "source code" in Software 2.0, and when is
    the dataset the moat?

B3. A 10-dollar seat has cohorts: 80 percent at 0.50 usage,
    15 percent at 5.00, 5 percent at 25.00. Compute the
    blended margin per user.

B4. Why does a 7x design speedup give only 1.4x end-to-end
    cycle speedup?

B5. In the discovery funnel, where does the cost live, and
    what is the real value of AI discovery?

B6. Write the expected-loss rule for buying privacy
    protection.

## Deep ladders (2 x 5)

### L1 , the funnel trap

L1.1 Define the discovery-to-clinical cost funnel.
L1.2 Toy: ns = [10k, 200, 5, 1], cs = [0.10, 5k, 2M,
    100M]. Compute the total.
L1.3 AI doubles assay survivors to 400. Recompute the
    total. What happened to the "saving"?
L1.4 Triage cuts assays to 100. Recompute and state the
    lesson.
L1.5 Critique: "AI makes drug discovery 100x cheaper".
    Name the exact error.

### L2 , the distribution skew

L2.1 Define the AI distribution problem under flat
    pricing.
L2.2 Toy: p = 10, cohorts as in B3. Compute the blend.
L2.3 Power users double usage to 50 (share still 0.05).
    Recompute the blend.
L2.4 The viral shift: power share 0.15 at usage 50, light
    0.70. Recompute.
L2.5 Critique: "blended margin is 7.60, we are fine".
    What is the hidden risk, and what pricing fixes it?

## Analytical / quantitative (2)

A1. A clinic runs 50,000 AI recommendations per year.
    Compute 2.00 each, escalation e = 0.05 at 150 each.
    (a) Compute the true per-task cost and the yearly
    bill. (b) A model upgrade costs 500k once and cuts e
    to 0.02. Compute the payback in years. (c) The
    clinicians rubber-stamp: overturn rate falls to zero.
    Price the theater and state the fix.

A2. A tool saves 1M per year at full adoption. (a) Adoption
    ramps [0.10, 0.35, 0.70] over 3 years, r = 10 percent.
    Compute the PV. (b) Training costs 200k and lifts the
    curve to [0.20, 0.55, 0.85]. Compute the net PV and
    the gain over (a). (c) Adoption stalls at 10 percent
    all three years. Compute the PV and give the verdict.

## Implementation / debug (1)

D1. The funnel function below misprices the AI scenario.
    Find the bug, fix it, and state the check that catches
    it.

```python
def funnel_total(ns, cs):
    total = 0
    for n, c in zip(ns, cs):
        total += n + c
    return total
```

## Changed-constraint scenarios (2)

S1. Your vibe-coding math assumed a 25-dollar fix cost.
    Vibe defects turn out weirder and cost 100 dollars
    each. Rework the 1,000-line toy and the tie review
    cost.

S2. Your OOD math assumed a_ood = 0.55. On truly novel
    targets a_ood = 0.20 and o = 0.70. Rework the expected
    net per proposal at v = 50k, c = 5k, and state the
    policy.

## Research critique (1)

R1. A startup claims "our AI designs drugs 10x faster" from
    design-step timing alone, with no wet-lab cycle data
    and no control program. Name three threats, the
    cheapest test for each, and what evidence would make
    you believe the 10x end-to-end claim.
