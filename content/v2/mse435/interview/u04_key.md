# Interview key , U04

## B1

Sufficient: access connects the model to firm documents
before answering. Conditions: documents exist, are current,
are reachable with permission checks.
Strong: adds that a1 must be measured on the firm's own
questions.
Red flags: "the model just knows more".
Rubric: 1 for the definition, 1 for the conditions.
Remediation: C01.

## B2

Sufficient: h x c_c + (1 - h) x c_m = 1.75 dollars per 1M.
Strong: states it is a weighted average over hit/miss.
Red flags: forgetting the miss term.
Rubric: 1 for the formula, 1 for the number.
Remediation: C06.

## B3

Sufficient: Q* = F / (p_a - p_h) = 12,000 = 12B tokens per
month.
Strong: states the unit (1M-token units) and the taxi/car
intuition.
Red flags: dividing by p_a alone.
Rubric: 1 for the formula, 1 for the number, 1 for units.
Remediation: C05.

## B4

Sufficient: the business buys successes. Retries and
failures make attempts cheap and successes expensive. Use
cost per successful task.
Strong: writes c x attempts / p_ok.
Red flags: comparing models on cost per attempt.
Rubric: 1 for the why, 1 for the replacement.
Remediation: C09.

## B5

Sufficient: re-integration labor, re-validation, data
egress, retraining.
Strong: notes the vendor prices against S.
Red flags: "there is no switching cost with APIs".
Rubric: 1 per part.
Remediation: C11.

## B6

Sufficient: the pilot runs at low volume, so the fixed
floor dominates the average. At rollout volume the true
number nears variable cost.
Strong: quotes F and v separately as the fix.
Red flags: treating 61.50 as the inference cost.
Rubric: 2 for the mechanism, 1 for the fix.
Remediation: C10.

## L1

L1.1 Latency cost = V x s x L / 100 against compute saving.
Faster costs compute, slower loses users.
L1.2 Latency cost = 160k, net = 30k - 160k = -130k per
month.
L1.3 Latency cost = 16k, net = 30k - 16k = +14k. Batching
wins for the internal tool.
L1.4 Linearity breaks: past 2 s the toy understates damage
by 10x. The p99 case, not p50, decides.
L1.5 It destroys value where latency sensitivity times
value at stake exceeds the compute saving.
Red flags: "latency does not matter for cost".
Rubric: 2 for L1.2-L1.3, 1 each for the rest.
Remediation: C07.

## L2

L2.1 Break-even tasks = F / (w x s - v), the volume where
total value covers fixed plus variable cost.
L2.2 38,000 / 2.83 = 13,427.6 tasks per month.
L2.3 38,000 / 1.83 = 20,765. At 18k tasks the workload
loses. Success rate is the lever.
L2.4 w = 2: contribution 0.43, break-even 88,372. Do not
proceed on hard dollars.
L2.5 (1) w may be soft time never redeployed. (2) s and w
are pilot-measured and can drift. The hurdle moves with
them.
Red flags: "break-even is a fixed number".
Rubric: 2 for L2.2-L2.4, 1 each for the rest.
Remediation: C12.

## A1

Sufficient: cached effective = 1.75 per 1M. (a) API with
cache: 15,000 x 1.75 + 3,000 = 29,250. (b) Hosting with
cache: 30,000 + 15,000 x (0.6 x 0.25 + 0.4 x 1.50)... the
hosted variable also gets cached: effective hosted variable
= 0.6 x 0.25 + 0.4 x 1.50 = 0.75 per 1M. Hosting = 30,000 +
11,250 + 3,000 = 44,250. API wins by 15,000 per month.
The cache lowers both variable costs proportionally, so
the break-even moves up: Q* = 30,000 / (1.75 - 0.75) =
30,000 = 30B tokens per month.
Strong: catches that caching applies to the hosted leg too
and recomputes the break-even.
Red flags: applying the cache to one leg only.
Rubric: 2 per leg, 2 for the winner, 2 for the break-even
shift.
Remediation: C05, C06.

## A2

Sufficient: (a) labor = 10,000 x 0.10 x 10/60 x 40 =
6,666.67. Total = 5,000 + 6,666.67 + 8,000 = 19,666.67.
Successes = 8,000. Cost per success = 2.46. (b) value =
8,000 x 5 = 40,000. Profit = 20,333.33 per month. Prompt
work: e = 0.04 gives labor 2,666.67, total 15,666.67,
saving 4,000 per month. Payback = 25,000 / 4,000 = 6.25
months.
Strong: notes the payback ignores quality change from the
prompt work (it likely raises s too).
Red flags: forgetting fixed ops in per-success cost.
Rubric: 2 for (a), 2 for (b), 2 for payback.
Remediation: C08, C09.

## D1

Sufficient: bug: p_ok uses (1 - s) x (r + 1) instead of
(1 - s)^(r + 1). At r = 1, s = 0.6 it gives 1 - 0.8 = 0.2
instead of 0.84. Fix:

```python
p_ok = 1 - (1 - s) ** (r + 1)
```

Check: at s = 1, p_ok = 1 and cost per success = c. Also
at r = 0 the formula must give c / s.
Red flags: "fixing" the attempts term instead.
Rubric: 1 for the bug, 2 for the fix, 1 for the check.
Remediation: C09.

## S1

Sufficient: h = 0.05 gives effective = 0.05 x 0.25 + 0.95 x
4.00 = 3.8125. Saving = 15,000 x 0.1875 = 2,812.50 against
3k infra. Net -187.50 per month. Advise: kill the cache.
Strong: adds that the infra could serve a different
repeating workload instead.
Red flags: keeping the cache "because caching is good".
Rubric: 2 for the rework, 1 for the verdict.
Remediation: C06 section 11.

## S2

Sufficient: idle half the time doubles effective p_h to
3.00. Q* = 30,000 / (4.00 - 3.00) = 30B tokens per month.
At 15B: API 60,000 vs host 75,000. Verdict: stay on API.
Strong: states the general rule (never host a spiky fleet
on 24-hour reservations).
Red flags: keeping the 12B answer.
Rubric: 2 for the rework, 1 for the rule.
Remediation: C05 section 11.

## R1

Sufficient: threats: (1) hand-picked questions (selection),
(2) no control arm (maybe any retrieval helps), (3) demo
tuning (prompts fit the 200). Tests: (1) random sample of
real employee questions, (2) A/B with and without access on
the same questions, (3) fresh questions the vendor never
saw. Belief needs: randomized or blinded evaluation on the
firm's own question mix with a pre-registered metric.
Strong: prices the 37-point claim against the C01 delta
and asks for the corpus coverage behind it.
Red flags: accepting the demo as evidence.
Rubric: 1 per threat with test, 1 for the belief bar.
Remediation: C01, C03.
