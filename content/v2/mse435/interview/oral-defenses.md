# Oral defenses , mse435

Ten deep ladders, eight follow-ups each. Each ladder runs:
define, intuitive toy, derive, implement and complexity,
compare, debug, critique assumptions, design the experiment
or production transfer. Closed-book. Keys are separate in
`keys-oral.md`.

## D1 , the token market (U01, U03)

D1.1 Define a token market equilibrium without symbols.
D1.2 Toy: Qd = 100 - 2P, Qs = 20 + 3P. Find P* and Q*
    with units.
D1.3 Derive P* from the two equations, showing each
    step.
D1.4 Implement a clearing function and state its
    complexity.
D1.5 Compare fast-clearing with sticky overnight supply:
    who pays the difference?
D1.6 Debug: a student's code returns P* = 32. Find the
    likely error.
D1.7 Critique: name two assumptions the toy needs and
    one real market that breaks each.
D1.8 Design: how would you test whether a real token
    market clears in minutes or days?

## D2 , the inference cost stack (U02, U03, U04)

D2.1 Define inference unit cost without symbols.
D2.2 Toy: training 5M, lifetime 500B tokens, inference
    4 per 1M. Compute the unit cost.
D2.3 Derive the lifetime volume where training cost
    equals inference cost per 1M.
D2.4 Implement the unit-cost function and state the
    large-volume limit.
D2.5 Compare a GPU fleet owner with an API reseller: who
    keeps the margin when utilization falls?
D2.6 Debug: the function returns 504.0 at 10B tokens but
    the student expected ~14. What did they confuse?
D2.7 Critique: name the assumption about retraining
    cadence and the case where it breaks the math.
D2.8 Design: what would you meter for one quarter to
    replace every assumed input?

## D3 , the contract as insurance (U03, U04)

D3.1 Define a long compute contract as insurance without
    symbols.
D3.2 Toy: 120 blocks per year, 3.00 contract, market
    path [4,3,2], r = 10 percent, 3 years. Which PV is
    smaller?
D3.3 Derive the contract PV formula from the discount
    definition.
D3.4 Implement both PV legs and state the flat-price
    check.
D3.5 Compare take-or-pay with pay-as-you-go under a 50
    percent usage drop.
D3.6 Debug: the market leg discounts the sum of prices
    once at the final year. State the fix.
D3.7 Critique: "we locked a great price". What was
    actually bought, and what proves it was a bad buy?
D3.8 Design: what contract term would you demand before
    signing in a falling-price market?

## D4 , the knowledge flywheel (U04, U06)

D4.1 Define the enterprise data flywheel without
    symbols.
D4.2 Toy: q = 100k per month, correction rate 0.02,
    gain 0.001 per correction, decay 0.9. Compute the
    6-month cumulative gain.
D4.3 Derive why the naive linear sum overstates the
    gain.
D4.4 Implement the flywheel and state the decay = 1.0
    check.
D4.5 Compare the flywheel with scheduled expert review:
    when does each win?
D4.6 Debug: the cumulative gain exceeds the naive sum.
    Name the bug.
D4.7 Critique: name the assumption about correction
    quality and the failure it hides.
D4.8 Design: what instrument would you add on day one
    to make the loop measurable?

## D5 , the latency/quality frontier (U04)

D5.1 Define the latency/quality tradeoff in dollars
    without symbols.
D5.2 Toy: V = 2M, s = 0.01 per 100 ms, batch 8 moves
    latency 400 to 1,200 ms and saves 30k per month.
    Compute the net.
D5.3 Derive the batch size where the net crosses zero.
D5.4 Implement the tradeoff function and state the
    L1 = L0 check.
D5.5 Compare batching with speculative decoding as
    latency reducers.
D5.6 Debug: the student prices latency with p99 but
    converts with p50. State the error.
D5.7 Critique: name the linearity assumption and the
    abandonment cliff that breaks it.
D5.8 Design: describe the two-week latency experiment
    that measures s.

## D6 , the discovery funnel (U05)

D6.1 Define the discovery-to-clinical funnel without
    symbols.
D6.2 Toy: ns = [10k, 200, 5, 1], cs = [0.10, 5k, 2M,
    100M]. Compute the total.
D6.3 Derive why doubling assay survivors raises the
    total instead of lowering it.
D6.4 Implement the funnel total and state the doubling
    check.
D6.5 Compare AI discovery with cheaper assays as
    investments.
D6.6 Debug: the function adds n + c instead of n x c.
    State the check that catches it.
D6.7 Critique: name the survival-independence
    assumption and the correlated-failure case.
D6.8 Design: describe the controlled comparison that
    must run before scaling AI-designed candidates.

## D7 , the falsifiable investment (U06)

D7.1 Define a falsifiable investment decision without
    symbols.
D7.2 Toy: Y = 0.15, pilot 18 percent +/- 5. Judge it.
D7.3 Derive why the interval's lower bound decides, not
    the point estimate.
D7.4 Implement the decision function and state the
    boundary check.
D7.5 Compare the rule with gut-feel investing on speed
    and on error rate.
D7.6 Debug: the function uses the upper bound. State
    the fix and the case that catches it.
D7.7 Critique: name the two ways teams void the rule
    after the pilot.
D7.8 Design: size the pilot (cases and weeks) to get
    an interval half-width of 0.04.

## D8 , the cost per success (U04, U05)

D8.1 Define cost per successful task without symbols.
D8.2 Toy: c = 0.50, s = 0.6, one retry. Compute it.
D8.3 Derive the success probability with r retries
    from the failure probability.
D8.4 Implement the function and state the s = 1 check.
D8.5 Compare retrying a cheap model with buying a
    premium model at c = 2.00, s = 0.95.
D8.6 Debug: the code uses (1 - s) x (r + 1) for the
    failure probability. State the fix.
D8.7 Critique: name the retry-independence assumption
    and the hard-question case that breaks it.
D8.8 Design: what would you log for one month to test
    the formula against reality?

## D9 , the TCO reckoning (U06, U02, U04)

D9.1 Define 3-year TCO without symbols.
D9.2 Toy: B = 400k, R = 300k per year, L = 150k per
    year, K = 100k. Compute it and the build share.
D9.3 Derive why build-only business cases understate
    cost 3-4x.
D9.4 Implement the TCO function and state the
    zero-build check.
D9.5 Compare the hosted design with the lean design
    (B = 120k, yearly 170k, K = 50k) against 768k
    savings PV.
D9.6 Debug: the student sums 3 years of build cost.
    State the fix.
D9.7 Critique: name the steadiness assumption and the
    runaway-run-cost case.
D9.8 Design: what quarterly review would catch TCO
    drift before it kills the case?

## D10 , the stakeholder defense (U06, all units)

D10.1 Define the stakeholder defense in one minute
    without symbols.
D10.2 Toy: baseline 2.14M, savings PV 768k, lean TCO
    680k. State the net and the verdict.
D10.3 Derive the adoption-gated PV from the ramp
    [0.20, 0.50, 0.80] at r = 10 percent.
D10.4 Implement the case-value function and state the
    full-ramp check.
D10.5 Compare defending the lean design with defending
    the hosted design: which numbers change the story?
D10.6 Debug: the defense quotes the 61.50 pilot average
    as the inference cost. State the error.
D10.7 Critique: name the three softest inputs in the
    case and the evidence each needs.
D10.8 Design: write the 4-week pilot plan (gates, kill
    criteria, decision date) in five lines.
