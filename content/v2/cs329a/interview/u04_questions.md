# Interview bank U04 , Open-ended evolution and deep research

Provenance: original practice questions. Not actual employer questions.
Keys in `u04_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Define the agent design space in architecture search: what is a
design, and what is fitness?
B2. What is mutation, and what is the locality claim?
B3. Name three selection rules and say how they differ in pressure.
B4. What does the holdout rule forbid, in one sentence?
B5. Name the four stages of the AlphaCode-style pipeline.
B6. List three sandbox rules for a self-modifying agent loop.

## Deep ladders (2 x 5)

Ladder 1 , evolution to holdout.
D1.1 Define population, fitness, mutation, selection.
D1.2 Toy: fitnesses [0.41, 0.55, 0.62, 0.68, 0.71, 0.73], keep 3 by
truncation. Compute the selection differential.
D1.3 Derive why the max of noisy validations is biased upward.
D1.4 Implement truncation and the optimism estimate, state the cost
of each.
D1.5 Compare truncation with tournament selection. When does each
win?
D1.6 Debug: fitness rises on validation but the holdout is flat
across generations. Name two causes and the measurement that
separates them.
D1.7 Critique the fitness-reliability assumption behind truncation.
D1.8 Design the experiment that tests whether the holdout gap
matches the predicted optimism, and state the falsification.

Ladder 2 , search-enhanced reasoning to provenance.
D2.1 Define the SEARCH action and the reasoner's loop.
D2.2 Toy: 20 fact-needing questions, compute the expected score with
retriever accuracy 0.8 and reasoning-given-fact accuracy 0.9.
D2.3 Derive the gain decomposition (retrieval quality times reasoning
quality) and say which factor usually binds.
D2.4 Implement the reason-search loop with source recording, state
the latency cost.
D2.5 Compare search-enhanced reasoning with upfront RAG. When does
each win?
D2.6 Debug: scores fall after adding search. Name two causes and the
measurement that separates them.
D2.7 Critique retriever relevance. What breaks downstream?
D2.8 Design the provenance audit for a research agent's 50 claims and
state the verdict rule.

## Analytical exercises (2)

A1. An evolution run uses M = 50 designs, E = 200 evals, c = $0.02,
G = 3 generations, t = 2s per eval, W = 10 workers, k = 5 survivors
reviewed at 10 min each. Compute the three-fuel sheet and name the
binding fuel against a $400 wallet. Then recompute with M = 30 and
state what changed.
A2. A novelty checklist processes 25 claims with sequential kill
rates 0.4 (literature), 0.3 (baseline), 0.1 (ablation). Compute the
expected survivors. Then explain why the funnel order (literature
first) is also the cost order, in two sentences.

## Implementation / debug (1)

I1. Your agent-architecture search keeps rediscovering the same design
family and fitness stayed flat for 3 generations. Sketch the loop
code with the diversity instrumentation you would add, then name the
two most likely causes and the single measurement that separates
them. State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: evaluations are destructive (each eval consumes
a physical sample worth $50) and non-repeatable. Redesign the
evolution loop: what survives, what dies, and what replaces the
population-based search?
S2. Constraint change: the agent must cite sources, but all sources
are offline documents with no URLs. What survives of evidence
provenance, and what new mechanism replaces the retrieval path?

## Research critique (1)

R1. "Open-ended evolution will automate AI research, so human
researchers should move to review-only roles." Identify the claim's
strongest true part, its weakest assumption, and the single
experiment that would most change your mind.
