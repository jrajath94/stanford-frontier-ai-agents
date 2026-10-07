# Interview bank , U01 , AI economics and the full value chain

Closed-book transfer, not recognition. Answer key is separate in
`u01_key.md`. Do not reveal answers through titles.

## Breadth (6)

B1. A token API cuts price 20 percent and its volume doubles.
    What happened to revenue, and what does that imply about
    demand elasticity?

B2. Name the four value-chain layers and one sentence on what
    each sells.

B3. Fixed cost 2M per year, variable cost 1 dollar per unit,
    price 3 dollars. What is break-even, and what breaks if price
    falls to 1 dollar?

B4. State the difference between a forecast and an observation,
    and name one decision that needs the range, not the point.

B5. Two firms sell the same model API. Firm A cuts price 10
    percent and firm B's volume falls 8 percent. Substitutes or
    complements?

B6. A deck says "AI got 10x cheaper in two years" from a blended
    price index. What two questions do you ask before you repeat
    the claim?

## Deep ladders (2 x 5)

### L1 , equilibrium under a supply shock

L1.1 Define market equilibrium without the word "balance".
L1.2 Toy: Qd = 120 - 2P, Qs = 30 + 4P. Solve by hand.
L1.3 A chip shortage cuts supply at every price by 20 units.
    Write the new supply curve and solve again.
L1.4 Your solver returns a negative price. Name two data errors
    that cause this and the guard you add.
L1.5 Critique: a colleague says "the model proves prices will
    rise". What does the model actually prove, and what would
    falsify the prediction?

### L2 , value capture along the chain

L2.1 Define value capture without symbols.
L2.2 Toy: costs [10, 5], prices [20, 35]. Compute each layer's
    capture share.
L2.3 The model layer goes open-source and its price falls to
    its cost. Recompute and say where the value went.
L2.4 Your capture table shows a negative share for the cloud
    layer. Name two real causes.
L2.5 Critique: "the app layer always captures most". Give a
    counterexample chain where it does not, and name the
    structural reason.

## Analytical / quantitative (2)

A1. A data-center operator considers a 4-year server buy: capex
    1.2M, maintenance 30k per year, versus renting at 380k per
    year. Discount rate 8 percent. Compute both present values
    and recommend. Then state the one assumption most likely to
    flip the answer.

A2. Forecasts for next-year token demand (B per day): [0.4, 0.9,
    2.2] against an eventual observation of 1.0. Compute bias,
    MSE, and variance. Is this forecaster biased or noisy, and
    what is the fix?

## Implementation / debug (1)

D1. The function below should return break-even quantity but
    fails on some inputs. Find the bugs, fix them, and state the
    checks you would add.

```python
def breakeven(fc, v, p):
    return fc / (p - v)
```

## Changed-constraint scenarios (2)

S1. Your equilibrium model assumed fast adjustment. The good is
    now data-center capacity with a 2-year build time, and demand
    jumps 30 percent overnight. Describe what the market does in
    year 1, what your model predicts for the resting point, and
    which prediction a buyer should use for a 1-year contract.

S2. Your consumer/prosumer split assumed 2 percent conversion.
    Apple features the app and conversion jumps to 6 percent for
    one month, then falls back. How does this change the revenue
    math, the cost math, and the decision you would make about
    hiring support staff?

## Research critique (1)

R1. A paper claims "each 10 percent fall in GPU prices caused a
    4 percent rise in AI startup formation" from a single
    time series of 8 quarters. Name three threats to this causal
    claim, the cheapest test that would weaken each, and what
    evidence would make you believe it.
