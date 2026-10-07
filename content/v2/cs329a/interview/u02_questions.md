# Interview bank U02 , Feedback, tools, and constitutional learning

Provenance: original practice questions. Not actual employer questions.
Keys in `u02_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Name the three fields of a ReAct step, in order, and say what each
carries.
B2. What makes execution feedback different from model feedback?
B3. State the operational difference between a critique and a learning
update.
B4. What is constitutional feedback, in four steps?
B5. Name three reward signals for a code agent and one failure mode of
each.
B6. What is independent validation, and what makes it independent?

## Deep ladders (2 x 5)

Ladder 1 , ReAct under tool failure.
D1.1 Define the ReAct loop: the step triple, the stop rule, the trace.
D1.2 Toy: write the trace for "sum the evens of [3, 8, 11, 6]".
D1.3 Justify why interleaving thought with tool calls beats
plan-then-execute when observations change the plan.
D1.4 Implement the loop with a stop rule, state per-step cost.
D1.5 Compare ReAct with act-only and with plan-then-execute. When does
each win?
D1.6 Debug: the loop retries the same failing call 6 times. Name the
missing piece and two fixes.
D1.7 Critique the observation-trust assumption. What breaks when the
tool lies?
D1.8 Design an experiment comparing ReAct with act-only on tasks where
observations matter, with cost matched.

Ladder 2 , reward signals to shortcut detection.
D2.1 Define a reward signal and Goodhart's mechanism in this setting.
D2.2 Toy: three rewards for a sort task, show the lookup-table trick
scoring 1.0 on two of them.
D2.3 Derive why selection on a proxy ranks shortcuts first.
D2.4 Implement the visible-hidden gap detector, state what data it
needs.
D2.5 Compare fixing the proxy with adding hidden tests. When does each
win?
D2.6 Debug: the gap detector says False but the policy is clearly
gaming. Name two causes.
D2.7 Critique the second-instrument assumption behind hidden tests.
D2.8 Design the hidden-suite rotation experiment and state what would
falsify it.

## Analytical exercises (2)

A1. A tool log shows 20 calls: 3 timeouts, 2 bad args, 1 auth failure,
2 server errors, 1 malformed response, 2 empty results, 9 clean.
Using the lesson C09 recovery rules, compute the expected number of
usable results after one recovery round, assuming retries succeed with
probability 0.7 and repairs with probability 0.9.
A2. A constitutional loop processes 200 drafts: 50 flagged, 40 revised
successfully. Compute the training yield. Then compute the yield if
the flag rate doubles but the revision success rate halves, and state
which regime a fixed human-review budget prefers.

## Implementation / debug (1)

I1. A code agent's repair loop oscillates: it fixes test A, breaks
test B, fixes B, breaks A. Sketch the loop code, then name the two
most likely causes and the single cheapest measurement that separates
them. State the fix for each cause.

## Changed-constraint scenarios (2)

S1. Constraint change: tool calls are now non-idempotent (each call
has a side effect) and cost $1 each. Redesign the error-recovery
taxonomy: which recoveries survive, which die, and what replaces
blind retry?
S2. Constraint change: no human reviewers exist and hidden tests
cannot be kept secret (the policy sees all tests). Which validation
mechanisms survive, and what new assumption does each need?

## Research critique (1)

R1. "Execution feedback grounds learning, so RLEF needs no human data
at all." Identify the claim's strongest true part, its weakest
assumption, and the single experiment that would most change your
mind.
