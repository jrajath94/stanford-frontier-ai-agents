# Applied capstone , cs329a U01-U08

Status: EXECUTED 2026-10-07. `run_applied_capstone.py` simulates the
full staged rollout: 8 weeks, 4 acceptance gates, weekly monitoring
with alerts, break-even economics, and a rollback drill. Figure:
`figs/applied_capstone.png` (the gate dashboard, computed by the
script, metadata stripped in-script). Supersedes
`superseded/pilot_applied.py`.

Honesty note: every number below is HYPOTHETICAL (labeled as such).
The run exercises the gate arithmetic and the monitoring logic. It
is NOT evidence the gates will hold in production. Model
sophistication is not the business goal.

## Discovery (hypothetical)

A 12-engineer team triages about 40 small bug-fix tickets per week.
Each ticket takes a median of 90 minutes of engineer time. The team
wants an agent that drafts fixes, but will not accept unreviewed
machine patches in the main branch.

## Workflow baseline (hypothetical)

Today: engineer reads the ticket, writes the fix, runs the visible
tests, opens a PR, a teammate reviews. Median ticket cost: 1.5
engineer-hours. Defect escape rate to production: about 4 percent
of fix PRs.

## Objectives

Cut median ticket time to 45 minutes with no rise in the escape
rate. The agent drafts, a human approves every merge. Success is
measured in engineer-hours saved and escape rate, not in model
scores.

## Constraints

No direct pushes to main. No network access for the agent. The
agent sees only the ticket text and the repo snapshot. Every agent
action is logged. A kill switch halts the agent fleet in one
command.

## Trust boundaries

The agent is untrusted code-writing machinery. The test suite is
semi-trusted (written by humans, reviewed). The human approver is
the trust anchor. The hidden test suite (U02 C12) is locked and
never shown to the agent.

## Alternatives considered

A1: full autonomy (rejected: no trust anchor). A2: agent as
linter-only (rejected: saves too little). A3: human writes, agent
reviews (kept as the fallback if draft quality is low).

## Acceptance gates

G1: on a 200-ticket historical set, agent drafts pass visible tests
at >= 70 percent. G2: hidden-suite pass of accepted drafts >= 95
percent. G3: human reviewers accept >= 60 percent of drafts without
major rewrites. G4: escape rate in the 8-week rollout <= 4 percent.
All four must hold before the next stage starts.

## Cost and latency assumptions (hypothetical)

Draft cost: $0.40 per ticket (model + sandbox). Review cost: 15 min
engineer time per shown draft. Break-even: each accepted draft
saves 45 min of engineer time against 15 min of review plus $0.40
of compute.

## Rollout (executed toy)

Week 1-2: shadow mode (drafts logged, never shown). Week 3-4: 3
engineers see drafts. Week 5-8: full team, human approval required.
Each stage needs its gate metrics before the next starts. Toy
result: G1 0.78 PASS, G2 0.953 PASS, G3 0.666 PASS, G4 0.009 PASS.

## Monitoring (executed toy)

Dashboard: drafts per week, accept rate, hidden-suite pass rate,
reviewer time per draft, escape rate. Alerts fired on the toy: week
6, an escape traced to an agent draft (rollback drill exercised).
week 8, accept rate fell 0.65 to 0.47 (10-point drop rule fired.
on the toy this is simulation noise, in production it would page
the owner).

## Rollback (executed toy)

One-command kill switch stops new drafts. In-flight drafts are
marked stale. The team reverts to the baseline workflow with no
config change. The rollback drill ran at the week-6 alert in the
simulation.

## Ownership and handoff

Owner: the team's on-call engineer rotates the agent's operation.
Handoff: runbooks for the kill switch, the log schema, and the
gate dashboard (the figure). Stakeholder defense: the 4 gates, the
break-even math (98.2 engineer-hours saved vs $128.00 draft cost on
the toy), and the rollback plan go to the engineering leaders
before week 1.

## Results (toy, hypothetical)

All four gates hold on the toy. Economics: baseline 480
engineer-hours over 8 weeks, 98.2 saved, $128.00 draft cost,
break-even holds. Two alerts fired and were handled (week-6 traced
escape with rollback drill, week-8 accept-rate drop). The dashboard
figure records both.

## Limitations

Hypothetical numbers throughout. The simulation cannot validate
draft quality, reviewer behavior, or the true escape rate. The
week-8 alert is noise in the toy. In production the same alert
must be treated as real until cleared. A production pilot needs
real tickets, real reviewers, and the locked hidden suite.
