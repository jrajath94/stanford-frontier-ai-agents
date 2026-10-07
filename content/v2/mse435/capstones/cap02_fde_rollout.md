# Capstone 2 , Applied/FDE: AI triage for a claims desk

Runner: `cap02_run.py`. Figures: `figures/cap02_tco.png`,
`figures/cap02_ramp.png`, `figures/cap02_tornado.png`.

Every number below is HYPOTHETICAL: a worked example for
learning the FDE discipline, not a real baseline, vendor
quote, or measured result. The economics are real. The
inputs are invented and labeled.

## Discovery

The claims desk (hypothetical, 200 cases per day) spends
its mornings sorting: which claims are routine, which need
a specialist. Sorting is 45 minutes per case of skilled
time. The FDE question: can AI triage cut sorting cost
without hurting decision quality? Stakeholders: the desk
manager (owns the budget), the compliance lead (owns the
quality gate), the platform team (owns the rollout).

## Workflow baseline (HYPOTHETICAL)

200 cases/day x 38 dollars x 250 days = 1.9M per year in
labor. Errors at 4 percent x 120 dollars = 240k. True
baseline: 2.14M per year. Measured over one quarter
(hypothetical). December seasonality noted as an open
measurement gap.

## Objectives

Primary: cut cost per case 30 percent (38 to 26.60
dollars) within two quarters of full rollout.
Guardrails: decision accuracy >= 0.90, p99 triage latency
<= 2 s, escalation rate <= 0.10. All pre-registered
before the pilot.

## Constraints

- No customer data leaves the firm's VPC (trust
  boundary).
- The compliance lead can veto any model change.
- Budget ceiling: 500k build.

## Trust boundaries

Prompts and triage logic run inside the VPC. The API
vendor (design B) receives case text under a no-train
contract plus a quarterly audit. PII is masked before
egress. These boundaries are architectural, not promised.

## Alternatives (HYPOTHETICAL scores)

- A, hosted custom: build 400k, run 450k/yr, TCO 1.85M.
- B, lean (API + cache + review): build 120k, run
  170k/yr, TCO 680k.
- Status quo: keep the 2.14M baseline running.
- Hire: 6 more sorters at 90k loaded = 540k/yr, no
  quality risk.

## Acceptance gates

Pilot (4 weeks, 5,000 cases): cost per case <= 30 with
90 percent confidence, accuracy >= 0.90, escalation <=
0.10. Kill criteria: any guardrail breach for two
consecutive weeks, or pilot cost above 60k.

## Cost/latency assumptions (HYPOTHETICAL)

Cached effective token price 1.75 per 1M (U04-C06 math).
Review labor 0.67 per task at 10 percent escalation.
p50 triage latency 400 ms, p99 1.8 s. All marked for
pilot measurement.

## The decision (computed)

Savings PV at full adoption: 767,891.81 (ramp 20/50/80,
r = 10 percent). Design A net: -1,082,108.19. Design B
net: +87,891.81. The hosted design fails. The lean
design clears the bar thinly. The honest FDE move is the
redesign, not the bigger budget.

## Rollout

Weeks 1-2: shadow mode (no user impact), 100 percent of
traffic scored, zero routed. Weeks 3-4: 1 percent live
canary with the rollback trigger (error > 2x baseline
for 1 hour). Weeks 5-8: 10 percent. Then 100 percent.
Rollback is a single button that restores the manual
queue in under 15 minutes (game-day tested).

## Monitoring

Dashboard: cost per case, accuracy, escalation rate,
p99 latency, cache hit rate. Alerts on guardrail breach
and on hit-rate decay (the capstone-1 lesson: measure h,
do not assume it).

## Rollback

Trigger: error rate above 2x baseline for 1 hour, or any
accuracy guardrail breach. The trigger pages the named
owner and offers one-click rollback. A 4-hour rollback
is rejected in the design review: the requirement is 15
minutes.

## Ownership and handoff

Owner: the desk platform lead (named in the runbook).
On-call: the platform rotation, 2k per week standby.
Handoff checklist (12 items) completed before the 10
percent stage. Joint drill: a simulated incident
resolved in under 1 hour.

## Stakeholder defense (the pitch)

"We measured a 2.14M baseline. The hosted design costs
1.85M to save 0.77M: we reject it. The lean design
costs 0.68M to save 0.77M: we pilot it for 4 weeks
against pre-registered gates, and we kill it if any
guardrail breaches twice. The tornado says adoption is
the top risk, so the pilot measures adoption first."

## Limitations

All inputs hypothetical. No real baseline was measured,
no vendor was engaged, no pilot ran. The case proves the
method, not the investment.
