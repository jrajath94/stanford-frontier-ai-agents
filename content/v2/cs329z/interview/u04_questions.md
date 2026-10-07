# U04 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define a DSPy signature, module, and optimizer in one line each.
B2. Name the five workflow patterns and the one property that makes a task fit each.
B3. What distinguishes a workflow from an agent?
B4. Define short-term and long-term memory for an agent.
B5. What is a handoff envelope, and what are its four keys?
B6. Name the four stopping rules.

## Deep ladders (2 x 5)

### Ladder 1: ReAct

L1.1 Define: the three trace symbols t, a, o.
L1.2 Toy: write the 7-step trace for "is 42 prime?".
L1.3 Derive: why does conditioning each thought on the full trace make the loop adaptive?
L1.4 Implement and complexity: write the trace builder. State cost per step.
L1.5 Compare: ReAct vs plan-and-execute on cost per success using the toy numbers.

### Ladder 2: error propagation

L2.1 Define: per-stage reliability and effective reliability with a check.
L2.2 Toy: 3 stages at 0.9, checks catch 0.8. Compute R with and without checks.
L2.3 Derive: where does a check pay most?
L2.4 Implement and complexity: write the simulator. State its cost.
L2.5 Compare: per-stage checks vs one end-to-end check.

## Analytical/quantitative (2)

A1. A summary compresses 8000 tokens to 500. Recall on 10 facts is 0.70. Give the compression ratio and the standard error of the recall.
A2. Single agent: 0.74 at 1x. Multi: 0.90 at 5x. Compute gain per extra cost and the verdict at bar 0.03.

## Implementation/debug (1)

I1. Your stall detector never fires, but loops spin for the full budget. Name two bugs and how you check each.

## Changed-constraint scenarios (2)

S1. The task fits in the context window with room to spare. Which of C06-C09 do you drop?
S2. Two agents must share one secret. Blackboard or messages, and what is the first test?

## Research critique (1)

R1. "Multi-agent systems are strictly more capable than single agents." State the strongest version, then give two reasons it fails and one experiment that would change your mind.
