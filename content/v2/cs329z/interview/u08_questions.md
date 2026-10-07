# U08 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define grounding and the computer-use loop.
B2. What is a modality ablation, and what does the 0.15 premium mean?
B3. Write the cost-per-finding formula for a science agent.
B4. Name the three long-horizon roles.
B5. Define span, trace, mean cost, p99.
B6. Name the four recovery levels in order.

## Deep ladders (2 x 5)

### Ladder 1: production readiness

L1.1 Define: span, trace, p99, spike alert.
L1.2 Toy: 100 tasks, mean $0.48, p99 $1.60. A deploy triples one step's cost. What do you look at first?
L1.3 Derive: why is cost attributed per span rather than per task?
L1.4 Implement and complexity: write the dashboard. State its storage cost.
L1.5 Compare: trace-based diagnosis vs bill-only on time to diagnose.

### Ladder 2: long-horizon architecture

L2.1 Define: planner, worker, checker, milestone.
L2.2 Toy: per-step 0.99, 500 steps. Compute flat vs hierarchical success.
L2.3 Derive: where does the 0.0066 come from, and what do the checkers change?
L2.4 Implement and complexity: write the 20-line loop. State the coordination overhead.
L2.5 Compare: hierarchy vs longer context on what each buys.

## Analytical/quantitative (2)

A1. 1000 agents coordinate. Compute all-to-all vs hub messages per round and the seconds per round at 1 ms per message. At what n does all-to-all exceed 1 hour per round?
A2. Recovery mix: 12 retry (1x), 4 rollback (5x), 3 escalate (50x), 1 compensate (20x). Compute total cost units and the escalation share. If escalation cost doubles, what is the new share?

## Implementation/debug (1)

I1. Your cost dashboard shows $0.48 mean but the bill says $1.20 per task. Name two leak sources and how you check each.

## Changed-constraint scenarios (2)

S1. The product must run 10,000 agents with sub-second coordination rounds. Redesign the C07 topology.
S2. Trace storage costs exceed the compute budget. Redesign the C05 monitoring.

## Research critique (1)

R1. "Our agent is production-ready because the demo works." State the strongest version, then give two reasons it fails and one experiment that would change your mind.

## Concept-targeted supplements

CS1. (U08-C12) Two guest lectures (S10, S16) are TBA. You keep a gap log instead of guessing their content. What goes into a row when a guest is announced, and what must the log never claim?
