# Interview bank U08 , Long-horizon evaluation and research projects

Provenance: original practice questions. Not actual employer questions.
Keys in `u08_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Define the duration curve, and state what it measures.
B2. Define task value, and compute it for 3 h at $120/h.
B3. Name the three DeepScholar-Bench dimensions and one metric
each.
B4. State the mean-min flip in one sentence.
B5. State the stopping rule in one sentence.
B6. Define the contamination gap.

## Deep ladders (2 x 8)

Ladder 1 , duration to reliability.
D1.1 Define the duration curve: axes, units, shape.
D1.2 Toy: (0.25, 0.90), (1, 0.70), (4, 0.50), (8, 0.35).
Compute the drop and the per-doubling fall.
D1.3 Derive the compounding argument for the decay.
D1.4 Implement duration_curve, state the per-point cost.
D1.5 Compare the duration axis with a single success number
and with a step-count axis. When does each win?
D1.6 Debug: the 8 h point is flat while the rest decays.
Name two causes and the measurement that separates them.
D1.7 Critique binary success as the y-axis.
D1.8 Design the experiment that tests exponential decay in
steps, and state the falsification.

Ladder 2 , value to budget.
D2.1 Define task value and the three eval fuels.
D2.2 Toy: 200 tasks, $2 agent, $0.50 judge, 20 audits at $30.
Compute the total and the binding fuel.
D2.3 Derive why the binding fuel sets the re-run frequency.
D2.4 Implement eval_budget, state the lock-in cost.
D2.5 Compare the three-fuel budget with no budget and with
agent-compute-only. When does each win?
D2.6 Debug: the judge bill is 10x the estimate. Name two
causes and the measurement that separates them.
D2.7 Critique the audit sample size as a design choice.
D2.8 Design the survey that tests whether the audit binds
in most evals, and state the falsification.

## Analytical exercises (2)

A1. An agent scores [0.62, 0.88, 0.70] on three task types.
A rival scores [0.73, 0.75, 0.74]. Compute both means and
mins, name the winner by each, and state in two sentences
which number ships and why.
A2. An eval runs 500 tasks. Agent compute is $1.20/task, the
judge is $0.30/task, and 25 audits cost $40 each. Compute the
total and the binding fuel. Then compute the savings from
halving the audit sample, and state in two sentences whether
that cut is safe.

## Implementation / debug (1)

I1. Your eval reports agent success 0.81, but the judge is the
same model as the generator and a spot human audit scores
0.58. Sketch the contamination check you would run (judges,
tasks, metric), then name the two most likely causes of the
0.23 gap and the single measurement that separates them.
State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: the judge budget drops to zero (no paid
judges, no humans). What survives of the eval design, what
dies, and what replaces the judge?
S2. Constraint change: tasks now run 24 hours each, and you
can afford only 10 of them. What survives of the duration
curve, and what must change in the reporting?

## Research critique (1)

R1. "Mean success rate is the right metric for comparing
agents, because it summarizes everything in one number."
Identify the claim's strongest true part, its weakest
assumption, and the single experiment that would most change
your mind.
