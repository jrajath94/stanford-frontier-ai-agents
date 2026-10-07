# Answer key , U06 , Capstone evidence and stakeholder defense

Answers for the assessments in
`lessons/u06_capstone_evidence_stakeholder_defense.md`, item
13 per concept. Keep separate from the lesson.

## C01 , baseline business workflow

Breadth:

1. Without a measured "before", every saving claim is
   fiction: improvement needs a reference number.
2. Time per case, cost per case, error rate per case.

Ladder:

1. A business baseline is the measured cost, time, and
   quality of the current workflow.
2. 200 x 38 x 250 = 1,900,000 dollars per year.
3. Errors: 200 x 250 x 0.04 x 120 = 240,000. Total
   2,140,000.
4. baseline(200, 45, 38, err_rate=0, err_cost=120)[2] ==
   1900000. The errors check guards the total.
5. Direct measurement wins where the investment is large.
   Benchmarks win for small pilots.

Transfer: December at 1.4x: baseline = 2.14M x ~1.1
(seasonal blend), and the 642k claim must be recomputed
against the seasonal baseline. Rule: measure a full
cycle, not a quiet month.

## C02 , adoption assumptions

Breadth:

1. They are stated as certainties ("100 percent by Q2")
   with no plan, and they multiply every value number.
2. A named driver (training, mandate, UX) and a stall
   case.

Ladder:

1. Adoption-gated case value is full-adoption saving
   times the realized ramp, discounted.
2. 128.4k + 321k + 513.6k = 963k over 3 years.
3. PV = 767,891.81 dollars.
4. case_value(642000, [1.0, 1.0, 1.0]) equals the annuity
   PV. The full-ramp check guards the discounting.
5. Mandates win where compliance is real. Phased proof
   wins where it is not.

Transfer: PV = 116.7k + 159.2k + 168.8k = 444.7k.
Verdict: the case collapses. Replan the driver before
spending.

## C03 , measurable outcomes

Breadth:

1. Measurable (a number with a source), pre-registered
   (written before launch), few (three to five).
2. Guardrails stop the team from hitting the primary by
   wrecking quality.

Ladder:

1. Measurable outcomes are the pre-registered metric set
   that decides success or failure.
2. Primary: cost per case <= 30. Guardrails: resolution
   >= 0.85, CSAT >= 4.0.
3. Fail: resolution 0.79 breaches the guardrail.
4. gate with a breached guardrail returns False. The
   guardrail check guards the logic.
5. Three metrics win for decisions. Twenty win for
   exploration, never for a gate.

Transfer: pre-registration broke. Fix: freeze the metric
set before launch. Any change restarts the clock.

## C04 , technical quality gate

Breadth:

1. From the business: accuracy from the error budget,
   latency from the SLA, escalation from staffing.
2. Each blocked rollout is a prevented incident, priced
   at the incident cost avoided.

Ladder:

1. A quality gate is a pass/fail contract on thresholds
   that the model must meet to ship.
2. 0.91 >= 0.90, 1.8 <= 2.0, 0.08 <= 0.10: pass, 3 of 3.
3. Waiting costs 40k. Shipping the miss costs 120k
   expected. Saying no saves 80k.
4. quality_gate(0.89, 1.8, 0.08)[0] is False. The
   one-miss check guards the AND.
5. The hard gate wins where the error budget is real.
   Human review wins where errors are subtle and volume
   is low.

Transfer: Goodhart's law broke it: the gate measures the
tuning. Fix: a fresh held-out gate set.

## C05 , uncertain forecasts

Breadth:

1. The future is a range. A point hides the spread the
   decision needs.
2. The expected value and the downside.

Ladder:

1. An honest forecast is low/base/high cases with
   weights, giving an expected value and a downside.
2. E = 475k, downside 200k.
3. E = 400k, downside -100k. The question becomes "can
   we survive the low case".
4. forecast with weights not summing to 1 must be
   rejected. The weights check guards the math.
5. Three-point wins for the stakeholder meeting. Monte
   Carlo wins for the final call.

Transfer: advocacy broke it: weights encode desire, not
belief. Fix: elicit weights separately, blind to the
desired outcome.

## C06 , sensitivity/tornado scenarios

Breadth:

1. It ranks inputs by swing on the outcome. It does not
   predict, and it ignores interactions.
2. Ignorance shrinks as the pilot de-risks, so the
   ranking changes.

Ladder:

1. Tornado sensitivity ranks drivers by hi-lo swing on
   the outcome.
2. Adoption 500k, labor 250k, volume 180k, quality 120k.
3. Adoption swing 150k: new order labor, adoption,
   volume, quality.
4. tornado returns descending swings. The descending
   check guards the sort.
5. Tornado is right for the first meeting. Monte Carlo
   is right for interactions and the final call.

Transfer: one-at-a-time broke: adoption and quality
interact. Better tool: Monte Carlo over the joint
distribution.

## C07 , total cost

Breadth:

1. Build, run, labor, risk reserve.
2. The build is ~22 percent of 3-year cost. The run tail
   dominates.

Ladder:

1. TCO is the full 3-year bill: build plus run plus
   labor plus risk.
2. 400k + 3 x 450k + 100k = 1,850,000 dollars.
3. Net = 768k - 1,850k = -1,082k. Verdict: do not build
   this design.
4. tco(0, 300k, 150k, 100k) = 1,450k: build share zero.
   The build-share check guards the stack.
5. 3-year is honest for investments. 1-year is honest
   only for pilots.

Transfer: run years 300k + 600k + 600k give TCO =
2,450k. Verdict: worse. Redesign for lower R.

## C08 , governance

Breadth:

1. Review/delay cost against expected incident cost.
2. Friction should scale with blast radius: heavy where
   failure is expensive, light elsewhere.

Ladder:

1. Governance cost is the delay price of review weighed
   against the incident risk it prevents.
2. Board 20k per change, risk 10k. Lighten.
3. Risk 250k > 20k. Keep the board.
4. governance with I = 0 gives risk 0: the board always
   loses. The I check guards the comparison.
5. The board wins where incidents are expensive.
   Automated gates win where changes are frequent and
   testable.

Transfer: the average hid the risky change. Policy:
tiered review, heavy for prompt rewrites.

## C09 , rollout/rollback

Breadth:

1. Entry gate (metrics green), exposure stage, exit
   trigger (metrics red).
2. A meeting cannot fire in minutes. The trigger must be
   automatic or it does not exist.

Ladder:

1. Staged rollout limits exposure per stage with numeric
   entry and exit rules.
2. 0.09 > 0.08 for 90 minutes: roll back.
3. Staged damage 5,400 versus 540,000 unstaged: 100x
   less.
4. rollout_check([0.09]) = (False, 0.09): duration not
   met. The duration check guards the trigger.
5. Staged wins where errors cost. Big-bang wins where
   they do not.

Transfer: 4-hour rollback means 4 hours of damage at
whatever stage is live. Requirement: rollback under 15
minutes, proven by game day.

## C10 , owner/handoff

Breadth:

1. Responsibility: runbook, dashboards, alerts,
   escalation, rollback, contacts, SLOs, and a joint
   drill.
2. It costs money every year and pays only when
   incidents strike: insurance math.

Ladder:

1. Owner/handoff names the human who wakes up and
   transfers the knowledge to do it.
2. Cost 104k, value 36k, net -68k: honest insurance.
3. 3 extra hours x 500 = 1,500 on the first incident.
4. owner_value with 0 incidents gives value 0, net
   -104k. The net check guards the framing.
5. Named on-call wins for critical systems.
   Builders-carry-pagers wins for tiny teams, briefly.

Transfer: value falls to zero (h1 = h0). Policy: named
backup, tested in the drill.

## C11 , alternatives

Breadth:

1. Status quo, buy (vendor), hire (people).
2. Close scores are noise. The margin must survive
   honest scoring error.

Ladder:

1. The alternatives matrix scores options on weighted
   criteria against the status quo.
2. Build 7.8, vendor 7.4, hire 5.8.
3. Status quo 10.0 wins. Verdict: argue the hidden cost
   or stop.
4. score with weights not summing to 1 must be
   rejected. The weights check guards the math.
5. The matrix wins where stakes are high. Cost-only wins
   where criteria truly reduce to cost.

Transfer: advocacy broke it: scores encode desire. Fix:
blind outsider scoring.

## C12 , falsifiable investment decision

Breadth:

1. Investment X, target Y, date D, confidence C, all
   written before the pilot.
2. The point estimate can pass while the interval
   straddles the target. The lower bound is the honest
   evidence.

Ladder:

1. A falsifiable investment decision is a pre-written
   rule: invest iff the pilot clears the target with
   confidence by the date.
2. Interval [13, 23], lower bound 13 < 15: kill.
3. Interval [18, 26], lower bound 18 > 15: invest.
4. decide(0.15, 0.0) = (0.15, 'invest'): boundary
   passes. The lower-bound check guards the rule.
5. The rule wins where stakes are high. Gut feel wins
   where the experiment is cheap.

Transfer: moving D broke pre-registration. Fix: D is
part of the rule. A moved D voids the decision.
