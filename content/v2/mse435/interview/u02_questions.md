# Interview bank , U02 , Silicon, power, and data centers

Closed-book transfer, not recognition. Answer key is separate in
`u02_key.md`.

## Breadth (6)

B1. A GPU costs 25k dollars, lasts 4 years, draws 1.4 kW at
    0.10 $/kWh, staff 0.10 $/h. Write the cost-per-GPU-hour
    formula and name which term moves with utilization.

B2. State the roofline rule and what the ridge point marks.

B3. Define PUE. A rack draws 150 kW total for 100 kW of IT.
    What is the PUE, and what does the 0.5 represent?

B4. What is HHI, and what are its three bands?

B5. Build costs 30M + 1M/yr for 4 years at r = 10 percent.
    Lease is 2.50 $/GPU-h for 1000 GPUs. What single number
    decides the winner, and which way does it cut?

B6. Name the four data-center lifecycle phases and the phase
    whose cost shrinks most under discounting.

## Deep ladders (2 x 5)

### L1 , the utilization trap

L1.1 Define utilization and effective cost per used hour.
L1.2 Toy: sticker 3.00 $/h, U = 0.50. Compute effective cost.
L1.3 Your fleet reports U = 0.95 but researchers wait days.
    Explain how both can be true.
L1.4 You are bonused on U. Name two ways to game it and the
    metric fix for each.
L1.5 Critique: "we should target 100 percent utilization".
    When is that right, and when is it wrong?

### L2 , power as the wall

L2.1 Define the power constraint in one sentence.
L2.2 Toy: 200 MW site, 2 kW per GPU. How many GPUs?
L2.3 Demand is 300 MW against your 200 MW site. Describe
    served, waiting, and the price-vs-queue allocation choice.
L2.4 The grid offers the megawatts but the county denies the
    water permit. Which constraint binds now?
L2.5 Critique: "power is the only constraint that matters".
    Name two builds where it was not, and what bound instead.

## Analytical / quantitative (2)

A1. Custom chip: NRE 80M dollars, saves 1.00 $/chip-hour,
    U = 0.80. Compute the break-even fleet size. Then: the
    compiler slips a year and first-year saving is zero on a
    4-year life. Recompute the effective N* and state the
    lesson.

A2. Server 300,000 dollars, 5-year straight line, 8 GPUs at
    U = 0.75. Compute the annual book charge and the per
    GPU-hour capital charge. A buyer offers 90,000 for the
    3-year-old server while the book says 120,000. What does
    the gap tell you?

## Implementation / debug (1)

D1. The roofline function below mislabels a workload. Find the
    bug, fix it, and state the invariant the fix restores.

```python
def roofline(peak, bw, intensity):
    if intensity < peak / bw:
        return peak, "compute-bound"
    return intensity * bw, "memory-bound"
```

## Changed-constraint scenarios (2)

S1. Your build/lease model assumed flat lease rates. The
    provider now cuts rates 15 percent per year. Rework the
    comparison logic: which direction does U* move, and what
    new input does the decision need?

S2. Your cooling payback assumed full racks. A recession cuts
    fleet utilization to 35 percent for two years. Recompute
    the decision logic for the liquid retrofit and name the
    option-value argument for waiting.

## Research critique (1)

R1. A vendor whitepaper claims "our custom chip cuts TCO 40
    percent versus GPUs" from one benchmark at batch size 1.
    Name three threats to the claim, the cheapest test for
    each, and the evidence that would make you believe it.
