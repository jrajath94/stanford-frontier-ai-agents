# Capstone B (executed): agentic refund assistant (FDE)

Status: EXECUTED 2026-10-07. Applied/FDE capstone. Every number below is HYPOTHETICAL: produced by `run_fde.py` (seed 7, n = 1000) for method demonstration. "NorthPay" is a fictional company. Nothing here describes real customers, real money, or real systems.

## Discovery

Fictional NorthPay's support team handles about 1000 refund requests per day. Human agents take a median 8 minutes per request. The queue grows on weekends. Two incident classes dominate: slow refunds on small amounts (customer anger) and occasional large refunds issued without a second look (losses).

Stakeholders: support lead (owns the queue), risk officer (owns fraud losses), finance (owns the cost per request).

## Workflow baseline

Human-only queue. Every request waits for an agent, who reads the order, checks the policy from memory, and issues or denies. Median handling 8 minutes. Cost per request about $2.40 in agent time (hypothetical).

## Objectives

- Median handling time under 2 minutes across all requests.
- Auto-approval precision at or above 0.98 (fraction of auto-approved refunds that are legitimate).
- Cost per request under $0.50.
- No agent-issued refund above $50 without a human.

## Constraints

- PCI data never touches the agent. The agent sees order metadata, never card numbers.
- Hard cap: the agent may not issue refunds above $50. The boundary enforces it (U07-C04), not the prompt.
- Every action is logged with the trace (U08-C05).

## Trust boundaries

- The agent reads: order id, amount, item list, account age, fraud flags.
- The agent may: approve refunds up to $50 when no fraud flag and policy checks pass.
- The agent may not: touch payment instruments, issue over $50, or contact the customer directly.
- Escalations go to the human queue with the agent's evidence pack attached.

## Alternatives considered

1. Human-only (baseline): precise, slow, $2.40 per request.
2. Rules engine: fast, brittle. It cannot read the order notes or handle the long tail of policy exceptions.
3. Agent with tiers (chosen): the agent handles the routine bulk, humans handle the risky tail. The tiers match U07-C05.

## Acceptance gates

| gate | bar | measured (hypothetical) | verdict |
| --- | --- | --- | --- |
| auto-approval precision | >= 0.98 | 0.9988 | PASS |
| auto p99 latency | < 30 s | 13.3 s | PASS |
| cost per request | < $0.50 | $0.53 | FAIL |

## The failed gate (the finding)

Cost per request is $0.53 against a $0.50 bar. The driver: the escalation rate is 19.2 percent, and each escalation costs the hypothetical $2.40 of human time. The agent's own compute ($0.08 per auto) is negligible. The math: 0.808 x 0.08 + 0.192 x 2.40 = 0.53.

This is not a reason to ship anyway. The gate did its job: it priced the tail. Remediation options for the stakeholder:

- Option A: raise the auto-approve cap to $75 with the same precision bar. Cuts escalations but needs the precision re-measured.
- Option B: improve the fraud/policy flags to cut false escalations. The 19.2 percent includes flag noise.
- Option C: renegotiate the bar to $0.60 with finance, showing the $1.87 saving over the $2.40 baseline.

Recommendation: Option B first (measure the flag noise), then A. Do not ship on a failed gate.

## Rollout plan

1. Shadow mode (week 1-2): the agent proposes, humans dispose. Measure precision against the human labels.
2. 10 percent of traffic (week 3-4): auto-approve live under the gates. Roll back on any gate failure.
3. 50 percent (week 5-6), then 100 percent (week 7+). Each step needs all gates green for 5 consecutive days.

## Monitoring

Dashboard per U08-C05: auto-approval precision (daily), latency p50/p99 per tier, cost per request, escalation rate, fraud-flag rate. Alerts: precision below 0.98, p99 above 30 s, cost above $0.50, escalation rate drift beyond 2 SE. Figures: `fig_latency_tiers.png`, `fig_gates.png`.

## Rollback

One command returns the queue to human-only. The rollback is rehearsed in the week-2 drill. Target: under 10 minutes from decision to full manual operation. The agent's pending auto-approvals drain first. Nothing is approved during the rollback window.

## Ownership

Owner: the support lead, with the on-call rotation covering nights. Runbook: the cost-spike page (U08-C10) adapted to refunds: 1) open the dashboard, 2) find the spiking tier, 3) check the flag rates, 4) roll back if a deploy matches, 5) page risk if precision drops.

## Handoff

The support team gets: the tier rules in one page, the evidence-pack format, the escalation SLA, and the rollback command. Training: one 30-minute session on reading the agent's evidence packs. The handoff is done when three agents resolve a simulated escalation without help.

## Stakeholder defense

- Risk officer: "Precision is 0.9988 on 808 auto-approvals, measured against the stub oracle. The $50 hard cap bounds the worst case. Every action is logged."
- Finance: "Cost is $0.53, above the $0.50 bar. The gate fails honestly. Option B cuts the flag noise before we ask for more budget."
- Support lead: "Median handling drops from 8 minutes toward seconds on 80 percent of requests. The 20 percent tail keeps human judgment."

## Limitations

Every number is hypothetical. The stub oracle (human accuracy 0.99) is assumed. It is not measured. Real fraud adapts. The flags will decay. The latency model ignores queueing. Re-run with real data before any real decision.

## Reproducibility

`run_fde.py`, seed 7. Re-run: `python3 run_fde.py`. Figures are metadata-stripped PNGs.
