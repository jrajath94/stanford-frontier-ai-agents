# U06 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Name the four parts of the eval tuple and the question each answers.
B2. What is scaffold fidelity, and what does a 0.13 mock-vs-real gap tell you?
B3. Price program, model, and human grading per 1000 items and name the cascade order.
B4. What are the four parts of a judge prompt?
B5. Write the Bradley-Terry win probability formula.
B6. State the z-gate rule for regressions.

## Deep ladders (2 x 5)

### Ladder 1: eval tuple

L1.1 Define: R, E, S, F.
L1.2 Toy: write the null-bug tuple. Two teams use S = 10 and S = 20 and report 0.70 vs 0.78. Explain.
L1.3 Derive: why is each part necessary? Name what breaks when one is absent.
L1.4 Implement and complexity: write the runner. State cost per task.
L1.5 Compare: tuple-with-program-F vs tuple-with-human-F on cost, speed, and gameability.

### Ladder 2: pass@k vs pass^k

L2.1 Define: p, k, and the independence assumption.
L2.2 Toy: p = 0.3, k = 5. Compute both numbers.
L2.3 Derive: P(at least one) = 1 - P(none). Show the steps.
L2.4 Implement and complexity: write the table generator. State its cost.
L2.5 Compare: which metric for a code agent with 8 tries and a verifier? Which for a single-shot medical answer?

## Analytical/quantitative (2)

A1. Old version 0.70, new version 0.76, n = 200 paired tasks. Compute z and the gate verdict. How many tasks would you need to call a 0.02 delta real?
A2. A beats B 7/10, B beats C 6/10, A beats C 8/10. The fitted strengths (B = 0) are A 0.89, C -0.44. Compute the predicted P(A beats C) and compare with the observed 0.80.

## Implementation/debug (1)

I1. Your benchmark scores drift across runs with no code change. Name two leak sources and how you check each.

## Changed-constraint scenarios (2)

S1. The agent under test needs live network access (a web task). Which isolation rules survive, and what new flakiness appears?
S2. The judge must grade 100,000 traces overnight. The cascade budget is $200. Redesign the grading.

## Research critique (1)

R1. "A higher benchmark score means a better agent." State the strongest version, then give two reasons it fails and one experiment that would change your mind.
