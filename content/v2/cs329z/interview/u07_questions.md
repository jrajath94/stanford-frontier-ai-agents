# U07 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define data minimization and the violation rate.
B2. State the instruction hierarchy from highest to lowest.
B3. Define attack success rate and the red-team loop.
B4. Define capability and least privilege.
B5. Name the three approval tiers and the sorting rule.
B6. Name the four consent levels.

## Deep ladders (2 x 5)

### Ladder 1: injection defense

L1.1 Define: untrusted span, instruction, source tag.
L1.2 Toy: 100 tool outputs, 5 poisoned. Naive obeys 4, tagging obeys 0. Explain the difference.
L1.3 Derive: why does source-based tagging beat content-based filtering against paraphrase?
L1.4 Implement and complexity: write the tagger and the gate. State cost per token.
L1.5 Compare: tagging vs sandboxing on what each limits and why both are needed.

### Ladder 2: approval and consent

L2.1 Define: the three tiers, the four consent levels.
L2.2 Toy: 100 actions/day price the tiers at 65 min/day. Compute it.
L2.3 Derive: why does the gradient beat flat ask-everything? Show the 40-min saving.
L2.4 Implement and complexity: write the tier classifier with deny-by-default. State its cost.
L2.5 Compare: approval tiers vs the permission boundary on judgment vs crisp rules.

## Analytical/quantitative (2)

A1. 50 attacks, 12 succeed before the fix, 3 after. Compute ASR, both SEs, and the gap in SE units. Is the fix real?
A2. Next-action predictor: 100 predictions above the gate, 62 correct. Correct saves 5 min, wrong costs 2 min. Compute precision and net minutes. At what precision does the net hit zero?

## Implementation/debug (1)

I1. Your tagging agent still obeys a poisoned tool output. Name two bugs and how you check each.

## Changed-constraint scenarios (2)

S1. The agent must follow instructions embedded in tool output (a recipe API). Redesign the C02 defense for this task.
S2. The human approver is replaced by a model approver. What breaks in C05, and what is the first test?

## Research critique (1)

R1. "More guardrails always make agents safer." State the strongest version, then give two reasons it fails and one experiment that would change your mind.

## Concept-targeted supplements

CS1. (U07-C06) A code agent runs 20 tasks through a test rig: iteration 1 passes 8, iteration 2 passes 12, iteration 3 passes 14. When do you stop iterating, and why? What does the test rig guarantee that the agent's confidence does not?
