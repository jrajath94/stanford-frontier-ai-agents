# Interview bank U01 , Test-time compute and verification

Provenance: original practice questions. Not actual employer questions.
Keys in `u01_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Define pass@N and state its two assumptions.
B2. What does a verifier do in best-of-N, and what breaks if it is
biased?
B3. Contrast best-of-N with self-consistency: inputs, outputs, and when
each wins.
B4. What is the generator/verifier gap, in one formula?
B5. Define calibration for a verifier. Why does best-of-N need ranking
more than calibration?
B6. Read a cost-success curve: what are the axes, and what does a
crossing mean?

## Deep ladders (2 x 5)

Ladder 1 , best-of-N under a weak verifier.
D1.1 Define best-of-N precisely: inputs, the argmax rule, the output.
D1.2 Toy: N = 4, correctness [1, 0, 0, 1], scores [0.55, 0.95, 0.30,
0.60]. What is picked, and is it right?
D1.3 Derive the success estimate pass@N * a and name what the product
assumes.
D1.4 Implement best_of_n in code and state its time and memory cost.
D1.5 Compare best-of-N with a weak verifier against self-consistency
with no verifier. When does each win?
D1.6 Debug: best-of-16 underperforms best-of-4 on your task. Name two
causes and the measurement that separates them.
D1.7 Critique the product formula's assumptions. Which fails first on
real workloads?
D1.8 Design an experiment that tests whether the verifier or the
generator is the bottleneck, with a fixed total budget.

Ladder 2 , calibration to decision.
D2.1 Define expected calibration error in words and symbols.
D2.2 Toy: compute ECE for two bins from the lesson C10 data.
D2.3 Derive why a monotone score repair (temperature scaling) cannot
change the ranking but can change ECE.
D2.4 Implement ece() and state how many samples per bin you need for a
stable estimate.
D2.5 Compare ECE with AUC: which matters for best-of-N, which for a
deploy threshold, and why?
D2.6 Debug: ECE is 0.02 on validation but the deploy threshold
misfires. Name two causes.
D2.7 Critique: what does ECE assume about the labels?
D2.8 Design a production check that separates ranking decay from
calibration decay.

## Analytical exercises (2)

A1. Prove that pass@N grows monotonically and is concave in N for 0 < p < 1.
Then compute the smallest N with pass@N >= 0.99 for p = 0.2.
A2. A verifier has accuracy 0.7 on easy questions and 0.55 on hard
ones. Hard questions are 30 percent of traffic. Best-of-8 runs at
p = 0.3. Compute the true expected success under the difficulty mix
and compare with the single-number toy estimate.

## Implementation / debug (1)

I1. You are given a best-of-N service whose success fell after the
verifier was "upgraded" to a larger model. The sample generator did
not change. Write the three measurements you would take, in order,
and for each state what outcome implicates the verifier versus the
pipeline. Then sketch the code for the cheapest measurement.

## Changed-constraint scenarios (2)

S1. Constraint change: verifier calls are now 10x the cost of
generation (they were 0.2x). Re-derive the optimal allocation for the
lesson C05 toy and state which plan wins at budget 100.
S2. Constraint change: answers are free text with no reliable
extraction to a discrete set, and no verifier exists. Which methods
survive this constraint, and what new assumption does each need?

## Research critique (1)

R1. "Weak verifiers shrink the generation-verification gap, so
test-time compute can replace train-time compute." Identify the
claim's strongest true part, its weakest assumption, and the single
experiment that would most change your mind.
