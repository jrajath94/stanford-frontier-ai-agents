# U08 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: mapping language to screen coordinates. Loop: observe, ground, act, verify. Remediation: C01.
- B2: toggling modalities and measuring the gap. 0.15 = the accuracy vision adds over the table. Red flag: "vision always helps". Remediation: C02.
- B3: cost per finding = hypotheses x cost / verified. Remediation: C03.
- B4: planner (milestones), worker (bounded execution), checker (verification). Remediation: C04.
- B5: span = one logged unit with tokens and cost. Trace = the span tree. p99 = the 1-percent-exceedance cost. Remediation: C05.
- B6: retry, rollback, escalate, compensate. Red flag: "retry, escalate". Remediation: C06.

## Deep ladders

- L1.1: span one logged unit, trace the tree, p99 the tail cost, alert the 2-SE drift gate.
- L1.2: the per-step cost bars. The spiking step names the deploy's victim.
- L1.3: per-task cost hides which step burns. Per-span cost attributes the dollars.
- L1.4: logger plus aggregator. Storage = spans x span size, sampled at 10 percent at scale.
- L1.5: trace 25 min, bill-only 4 hours on the toy. Rubric: both numbers plus the attribution reason.
- L2.1: planner sets milestones, worker executes bounded subtasks, checker verifies, milestone a verifiable subgoal.
- L2.2: flat 0.0066, hierarchical near 0.90. Rubric: both numbers.
- L2.3: 0.99^500 = e^-5.025. Checkers catch errors at each milestone, resetting the compounding.
- L2.4: planner/worker/checker loop. Overhead = milestones x check cost.
- L2.5: hierarchy buys reliability through verification. Longer context buys detail without checks. Rubric: the check-vs-detail split.

## Analytical/quantitative

- A1: 999,000 vs 2,000 messages. 999 s vs 2 s per round. All-to-all exceeds 1 hour when n(n-1) > 3,600,000, at n near 1898. Rubric: the counts, the seconds, and the n.
- A2: total 202 units, escalation share 150/202 = 0.743. Escalation at 100x: total 352, share 300/352 = 0.852. Rubric: both shares.

## Implementation/debug

- I1: leak 1: retries or background steps not logged as spans (check: sum the dashboard total against the bill line by line). Leak 2: the price table is stale (check: recompute one task's cost by hand from token counts). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: hierarchy of hubs (hubs of hubs), sharding by region, async gossip instead of rounds. Sub-second needs O(log n) depth, not O(n) fan-in.
- S2: sample traces at 1 percent, keep full spans only for the p99 tail and the incident window. Aggregate counters always on, detail on demand.

## Research critique

- R1: strong: steelman = "the demo exercises the full path". Rebuttal 1: the demo has no trace, no cost attribution, no recovery ladder, no owner, no rollback (the C05-C10 checklist). Rebuttal 2: the toy where the demo scores 0.80 and production p99 triples on the first traffic spike. Experiment: run the production-readiness gate (cost p99 under budget, recovery drill passed, rollback rehearsed, owner named) on 5 launches. Zero gates passed means zero production-ready.

## Concept-targeted supplements

- CS1: when announced, the row gains speaker, topic, and which unit it extends. Until then the rows stay open. The log never claims guest content: no score, claim, or citation may rest on untaught material. What is taught and assessed is the method: name the unknowns, write the update rule, keep the rows open. Rubric: the row schema plus the no-content-claim boundary.
