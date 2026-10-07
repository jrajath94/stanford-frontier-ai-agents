# Interview bank , U06 , Capstone evidence and stakeholder defense

Closed-book transfer, not recognition. Answer key is separate in
`u06_key.md`.

## Breadth (6)

B1. Why must the business baseline be measured before any AI
    proposal, and what three numbers make it?

B2. Write the adoption-gated case value formula and explain
    why each ramp step needs a named driver.

B3. State the three properties of measurable outcomes and the
    role of guardrails.

B4. Define a technical quality gate and where its thresholds
    come from.

B5. Name the four parts of 3-year TCO and the share the
    build typically takes.

B6. Write the falsifiable investment decision rule and name
    its four parts.

## Deep ladders (2 x 5)

### L1 , the baseline trap

L1.1 Define a business baseline.
L1.2 Toy: n = 200, c = 38, d = 250, errors 4 percent at
    120 each. Compute the full baseline.
L1.3 The AI claims 30 percent savings. Compute the claim
    against the full baseline versus a guessed 1.5M.
L1.4 December runs 40 percent hotter for 22 days.
    Compute the seasonal uplift.
L1.5 Critique: "we save 30 percent". What was never
    measured, and what would prove the claim?

### L2 , the decision rule

L2.1 Define a falsifiable investment decision.
L2.2 Toy: Y = 0.15, pilot 18 percent +/- 5. Judge it.
L2.3 Pilot 22 percent +/- 4. Judge it.
L2.4 The team extends the pilot to 6 weeks "to get a
    better number". Name what broke.
L2.5 Critique: "the pilot hit 18 percent, above the 15
    target, so we invest". Name the exact statistical
    error.

## Analytical / quantitative (2)

A1. A claims desk baseline: 200 cases per day, 38 dollars
    each, 250 days, 4 percent errors at 120 each. (a)
    Compute the yearly baseline. (b) The AI case: build
    400k, run 300k per year, labor 150k per year, risk
    100k, 3-year TCO. Compute it and judge against a
    savings PV of 767,891.81. (c) Adoption stalls at
    [0.20, 0.30, 0.35], PV 444,721.26. Rework the
    judgment.

A2. Governance: 40 low-stakes changes (delay 0.5 wk at 10k
    per week, incident p = 0.01 at 200k) and 10
    high-stakes changes (delay 2 wk at 10k per week,
    p = 0.05 at 5M). (a) Compute board cost versus risk
    per change for each tier. (b) State the regime per
    tier. (c) One low-stakes change in ten is secretly a
    prompt rewrite with p = 0.30. Rework the low-tier
    average and the policy.

## Implementation / debug (1)

D1. The decision function below approves too often. Find
    the bug, fix it, and state the check that catches it.

```python
def decide(measured, half_width, Y=0.15):
    hi = measured + half_width
    verdict = "invest" if hi >= Y else "kill"
    return round(hi, 3), verdict
```

## Changed-constraint scenarios (2)

S1. Your TCO assumed steady run cost. Usage doubles run
    cost in year 2 (300k, then 600k, 600k). Rework the
    3-year TCO from B = 400k, L = 150k per year, K =
    100k, and state the verdict against 768k savings PV.

S2. Your gate assumed honest measurement. The team tunes
    on the gate set until it passes. Name what broke,
    the fix, and how you would catch it in the 90-day
    readout.

## Research critique (1)

R1. A consultancy's "AI business case" shows 3x ROI with
    no baseline, no adoption ramp, no guardrails, and no
    alternatives. Name four missing pieces, the cheapest
    evidence for each, and what would make the 3x
    believable.
