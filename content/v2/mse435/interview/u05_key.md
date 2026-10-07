# Interview key , U05

## B1

Sufficient: vibe = L/100 x d_v x f, verified = r + L/100 x
d_f x f. Vibe wins where fix cost is near zero.
Strong: names the tie review cost explicitly.
Red flags: "AI code is free".
Rubric: 1 for the formulas, 1 for the condition.
Remediation: C01.

## B2

Sufficient: the dataset plus the training recipe. The
dataset is the moat when proprietary, not when
replicable.
Strong: notes compute is rentable, data is not.
Red flags: "the model weights are the moat".
Rubric: 1 per part.
Remediation: C02.

## B3

Sufficient: 0.8 x 9.5 + 0.15 x 5 + 0.05 x (-15) = 7.60
dollars per user per month.
Strong: notes the power cohort loses 15 per user while the
blend looks fine.
Red flags: averaging usage instead of margin.
Rubric: 2 for the number, 1 for the cohort read.
Remediation: C03.

## B4

Sufficient: AI speeds design only. The 4-week wet lab is
unchanged and dominates. 6 / (2/7 + 4) = 1.40x.
Strong: names Amdahl-style reasoning explicitly.
Red flags: "AI speeds everything".
Rubric: 2 for the mechanism, 1 for the number.
Remediation: C05.

## B5

Sufficient: cost lives at the bottom (assays, preclinical,
clinical). AI's value is triage quality, not candidate
quantity.
Strong: shows more candidates can raise the total.
Red flags: "cheaper discovery means cheaper drugs".
Rubric: 1 per part, 1 for the inversion.
Remediation: C06.

## B6

Sufficient: buy protection when C < p x L, dollars per
year.
Strong: sensitivity-tests p over 10x.
Red flags: "our vendor promised no training".
Rubric: 1 for the rule, 1 for the sensitivity habit.
Remediation: C07.

## L1

L1.1 Many cheap candidates enter, few survive. Stage costs
rise steeply down the funnel.
L1.2 111,001,000 dollars.
L1.3 112,001,000. The "saving" cost an extra million: more
survivors mean more assay spend.
L1.4 110,501,000, saving 500k. Lesson: triage quality is
the value, not quantity.
L1.5 The error: it prices the design step, not the
program. The expensive tail is unchanged.
Red flags: celebrating candidate counts.
Rubric: 2 for L1.2-L1.4, 1 each for the rest.
Remediation: C06.

## L2

L2.1 Flat price with variable per-user inference cost:
heavy users can cost more than they pay.
L2.2 7.60 dollars per user per month.
L2.3 0.8 x 9.5 + 0.15 x 5 + 0.05 x (-40) = 6.35.
L2.4 0.7 x 9.5 + 0.15 x 5 + 0.15 x (-40) = 1.40.
L2.5 Hidden risk: the power cohort grows and the blend
collapses. Fix: usage-based pricing or caps.
Red flags: "average usage is low, we are safe".
Rubric: 2 for L2.2-L2.4, 1 each for the rest.
Remediation: C03.

## A1

Sufficient: (a) per task = 2.00 + 0.05 x 150 = 9.50.
Yearly = 475,000. (b) new yearly = 250,000, saving
225,000 per year. Payback = 500,000 / 225,000 = 2.22
years. (c) theater = 375,000 per year for zero safety.
Fix: measure overturn rate, tie incentives to real
review, or cut e with a better model.
Strong: notes the upgrade payback assumes e stays at
0.02, which must be monitored.
Red flags: pricing the task at 2.00.
Rubric: 2 for (a), 2 for (b), 2 for (c).
Remediation: C11.

## A2

Sufficient: (a) PV = 906,085.65. (b) net PV =
1,074,981.22, gain 168,895.57 over (a). (c) PV =
248,685.20. Verdict: the case fails. Fix workflow fit
before spending on the model.
Strong: states the general rule (adoption investment
beats model investment when the ramp binds).
Red flags: using the 3M naive total.
Rubric: 2 for (a), 2 for (b), 2 for (c).
Remediation: C10.

## D1

Sufficient: bug: the loop adds n + c instead of n x c.
At base it gives 10,105 + 5,200 + 2,000,005 +
100,000,001 = 102,015,311 instead of 111,001,000. Fix:

```python
total += n * c
```

Check: doubling one stage's count must add exactly one
stage-cost of dollars (the T6 check).
Red flags: "fixing" by changing the loop bounds.
Rubric: 1 for the bug, 2 for the fix, 1 for the check.
Remediation: C06.

## S1

Sufficient: vibe = 10 x 40 x 100 = 40,000. Verified =
3,000 + 10 x 4 x 100 = 7,000. Tie at r = 36,000.
Strong: states the general rule (weird defects raise f,
which raises the verification budget).
Red flags: keeping the 9k tie point.
Rubric: 2 for the rework, 1 for the rule.
Remediation: C01 section 11.

## S2

Sufficient: true = 0.3 x 0.95 + 0.7 x 0.20 = 0.425. Net =
0.425 x 50,000 - 5,000 = 16,250 dollars. Policy:
restrict to in-distribution until OOD accuracy is
measured.
Strong: notes the budget must survive clustered bad
months.
Red flags: using the 0.55 number.
Rubric: 2 for the rework, 1 for the policy.
Remediation: C12 section 11.

## R1

Sufficient: threats: (1) design-step timing is not
end-to-end time, (2) no control program (maybe the team
was faster anyway), (3) no quality data (faster designs
may fail more). Tests: (1) time full cycles before and
after, (2) matched team without AI, (3) count assay
survival per design. Belief needs: controlled cycle-time
comparison with quality held equal.
Strong: invokes the Amdahl bound explicitly (10x design
cannot give 10x end to end with a fixed wet lab).
Red flags: accepting step timing as program evidence.
Rubric: 1 per threat with test, 1 for the belief bar.
Remediation: C05, C06.
