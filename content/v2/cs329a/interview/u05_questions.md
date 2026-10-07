# Interview bank U05 , Software-engineering and kernel agents

Provenance: original practice questions. Not actual employer questions.
Keys in `u05_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Define serial and parallel test-time scaling for code tasks.
B2. What is the sample-filter-select pipeline, and what does each
stage cost?
B3. State the fast_p metric in one sentence.
B4. Why is correctness a gate and speed a ranking, not a weighted
sum?
B5. Name four sandbox layers and what each blocks.
B6. What four fields does a run receipt need?

## Deep ladders (2 x 8)

Ladder 1 , CodeMonkeys to selection.
D1.1 Define context, generation, and selection in issue
resolution.
D1.2 Toy: S = 3, K = 8, context $0.40, $0.05 per serial
iteration. Compute the per-issue cost and the context share.
D1.3 Derive why parallel sampling amortizes a fixed context
cost.
D1.4 Implement the three-stage loop, state the cost of each
stage.
D1.5 Compare serial-only, parallel-only, and mixed scaling. When
does each win?
D1.6 Debug: coverage is high but the chosen edits keep failing
hidden tests. Name two causes and the measurement that separates
them.
D1.7 Critique the assumption that generated tests are honest
judges.
D1.8 Design the experiment that tests whether co-developed tests
beat fixed tests at fixed budget, and state the falsification.

Ladder 2 , KernelBench to deployment.
D2.1 Define correctness, speedup, and fast_p.
D2.2 Toy: 10 kernels with the lesson table. Compute fast_1 and
fast_2.
D2.3 Derive why two-gate grading beats a single combined score.
D2.4 Implement the scorer, state the timing-stability cost.
D2.5 Compare gate-then-rank with weighted scoring. When does
each win?
D2.6 Debug: a kernel posts 283x speedup. Name two causes and the
measurement that separates them.
D2.7 Critique binary correctness under a fixed tolerance.
D2.8 Design the experiment that tests whether profile-guided
edits beat unguided edits, and state the falsification.

## Analytical exercises (2)

A1. A repair loop runs at most 4 iterations per issue. Each
iteration costs $0.10 in model calls plus one test run at $0.02.
The loop stops at the first pass. On 100 issues the observed pass
iteration counts are: 30 at iteration 1, 25 at iteration 2, 20 at
iteration 3, 10 at iteration 4, 15 never pass. Compute the total
cost. Then compute the cost if the cap were 2 iterations, and
state how many fixes are lost.
A2. A suite has 100 tests, 10 are quarantined as flaky with
f = 0.10. Each normal test runs once, each quarantined test runs
3 times. Compute the total runs per suite pass and the expected
false alarms per 200 suite passes. Then explain in two sentences
why quarantine beats quarantining nothing.

## Implementation / debug (1)

I1. Your agent's repair loop keeps "fixing" code that was already
correct, and each fix introduces a new failure. Sketch the loop
with the instrumentation you would add to catch this, then name
the two most likely causes and the single measurement that
separates them. State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: test runs are destructive (each run
consumes a $50 hardware sample) and non-repeatable. Redesign the
execution-grounded loop: what survives, what dies, and what
replaces reruns?
S2. Constraint change: the agent must produce a kernel, but the
target GPU is unknown at generation time (it will run on one of
three architectures). What survives of the profile-then-optimize
rule, and what new mechanism replaces hardware-specific tuning?

## Research critique (1)

R1. "Test-time scaling will make hand-written software obsolete,
because sampling plus selection beats human coding on every
task." Identify the claim's strongest true part, its weakest
assumption, and the single experiment that would most change your
mind.
