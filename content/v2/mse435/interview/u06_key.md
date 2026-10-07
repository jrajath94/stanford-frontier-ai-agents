# Interview key , U06

## B1

Sufficient: without a measured "before", saving claims are
fiction. The three numbers: time, cost, and error rate per
case.
Strong: adds that the baseline needs a full seasonal
cycle.
Red flags: "we know roughly what it costs".
Rubric: 1 for the why, 1 for the three numbers.
Remediation: C01.

## B2

Sufficient: realized_t = a_t x S, discounted. Each step
needs a driver (training, mandate, UX) or it is a wish.
Strong: adds the stall case explicitly.
Red flags: "100 percent by Q2".
Rubric: 1 for the formula, 1 for the driver rule.
Remediation: C02.

## B3

Sufficient: measurable, pre-registered, few. Guardrails
stop the team from hitting the primary by wrecking
quality.
Strong: gives the claims-desk example.
Red flags: twenty metrics.
Rubric: 1 per property set, 1 for guardrails.
Remediation: C03.

## B4

Sufficient: a pass/fail contract on thresholds. Thresholds
come from the business: error budget, SLA, staffing.
Strong: adds "a gate without teeth is a suggestion".
Red flags: thresholds from the eval set.
Rubric: 1 for the definition, 1 for the source.
Remediation: C04.

## B5

Sufficient: build, run, labor, risk reserve. The build is
about 22 percent of the 3-year total.
Strong: states the stakeholder question ("and then what
does it cost to run").
Red flags: pricing the build only.
Rubric: 1 for the parts, 1 for the share.
Remediation: C07.

## B6

Sufficient: invest X iff the pilot measures Y by date D
with confidence C, else kill. Parts: X, Y, D, C.
Strong: adds that the interval, not the point, decides.
Red flags: writing the rule after the pilot.
Rubric: 1 for the rule, 1 for the parts.
Remediation: C12.

## L1

L1.1 The measured cost, time, and quality of the current
workflow.
L1.2 1.9M + 240k errors = 2.14M per year.
L1.3 642k against 2.14M. 450k against the 1.5M guess. The
baseline moves the claim 192k.
L1.4 200 x 22 x 38 x 0.40 = 66,880 dollars.
L1.5 Nothing was measured. Proof needs: a measured
baseline, a control or pre/post comparison, and
guardrails holding.
Red flags: "the vendor's ROI calculator says so".
Rubric: 2 for L1.2-L1.4, 1 each for the rest.
Remediation: C01.

## L2

L2.1 A pre-written rule: invest X iff the pilot clears Y
with confidence C by date D.
L2.2 Interval [13, 23], lower bound below 15: kill.
L2.3 Interval [18, 26], lower bound above 15: invest.
L2.4 Pre-registration broke: D is part of the rule, and
moving it voids the decision.
L2.5 The error: judging by the point estimate instead of
the interval's lower bound.
Red flags: "18 is above 15, we invest".
Rubric: 2 for L2.2-L2.3, 1 each for the rest.
Remediation: C12.

## A1

Sufficient: (a) 2,140,000 per year. (b) TCO = 400k + 3 x
450k + 100k = 1,850,000. Net = 767,891.81 - 1,850,000 =
-1,082,108.19. Verdict: do not build. (c) savings PV
444,721.26, net worse: -1,405,278.74. Verdict stands,
stronger.
Strong: notes the redesign options (lower R via caching
or a smaller model, bigger S).
Red flags: comparing build cost alone to savings.
Rubric: 2 for (a), 2 for (b), 2 for (c).
Remediation: C01, C07.

## A2

Sufficient: (a) low tier: board 5,000 vs risk 2,000 per
change. High tier: board 20,000 vs risk 250,000. (b)
low: lighten. High: board. (c) one in ten at p = 0.30:
expected risk = 0.9 x 2,000 + 0.1 x 60,000 = 7,800 per
change, above the 5,000 board cost. Policy: tier by
actual blast radius, heavy review for prompt rewrites.
Strong: states the general rule (averages hide the
risky change).
Red flags: keeping one tier for all changes.
Rubric: 2 for (a), 1 for (b), 3 for (c).
Remediation: C08.

## D1

Sufficient: bug: the function uses the UPPER bound (hi)
instead of the LOWER bound (lo). At (0.18, 0.05) it
returns invest on hi = 0.23 when the honest rule kills on
lo = 0.13. Fix:

```python
lo = measured - half_width
verdict = "invest" if lo >= Y else "kill"
return round(lo, 3), verdict
```

Check: at (0.18, 0.05) the fixed function must return
kill.
Red flags: "fixing" by changing Y.
Rubric: 1 for the bug, 2 for the fix, 1 for the check.
Remediation: C12.

## S1

Sufficient: TCO = 400k + 1,500k + 450k + 100k = 2,450,000.
Against 768k PV: net -1,682,000. Verdict: do not build.
redesign for lower run cost.
Strong: names caching and smaller models as the levers.
Red flags: keeping the steady-state TCO.
Rubric: 2 for the rework, 1 for the verdict.
Remediation: C07 section 11.

## S2

Sufficient: Goodhart's law broke it: the gate measures
the tuning, not the model. Fix: a fresh held-out gate
set, never used in development. Catch it in the readout:
shadow-traffic metrics will miss while gate metrics
pass.
Strong: adds that gate-set reuse must be logged like
data leakage.
Red flags: "the model passed, ship it".
Rubric: 1 per part, 1 for the catch.
Remediation: C04 section 11.

## R1

Sufficient: missing: (1) measured baseline, (2) adoption
ramp with drivers, (3) guardrail metrics, (4) priced
alternatives including status quo. Cheapest evidence:
(1) one quarter of cost-center data, (2) a 50-user pilot
cohort, (3) 90 days of quality metrics, (4) a
one-page matrix. Believable with: pre-registered metrics,
a control group, and full TCO against the baseline.
Strong: prices the 3x against the missing baseline
explicitly.
Red flags: accepting the ROI calculator.
Rubric: 1 per piece with evidence, 1 for the belief bar.
Remediation: C01, C02, C03, C11.
