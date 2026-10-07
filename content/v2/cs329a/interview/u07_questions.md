# Interview bank U07 , Reasoning, formal systems, and autonomy

Provenance: original practice questions. Not actual employer questions.
Keys in `u07_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. List the four guest sessions with their topics, and state the
evidence level for each.
B2. Define goal, tactic, and kernel in formal proof search.
B3. What is the AlphaGeometry talent split, in one sentence?
B4. Distinguish conjecture, search, and proof in two sentences.
B5. State the autonomy envelope rule in one sentence.
B6. What is the intervention test for trace validity?

## Deep ladders (2 x 8)

Ladder 1 , formal proof to AlphaGeometry.
D1.1 Define the symbolic environment: state, action, reward.
D1.2 Toy: 12 tactics, a 4-tactic proof. Compute the random-play
and guided-play success rates.
D1.3 Derive why a perfect verifier makes search tractable.
D1.4 Implement proof_search, state the node cost.
D1.5 Compare neural-guided search with uniform search and with
pure symbolic search. When does each win?
D1.6 Debug: the system proves nothing after the full budget.
Name two causes and the measurement that separates them.
D1.7 Critique the tactic action space as a design choice.
D1.8 Design the experiment that tests whether neural proposals
beat uniform search, and state the falsification.

Ladder 2 , autonomy to safety.
D2.1 Define capability, authority, and the envelope.
D2.2 Toy: 4 configs (c=0.95/0.60, a=low/high). Which does the
envelope admit?
D2.3 Derive the expected-harm argument for the envelope.
D2.4 Implement envelope_ok, state the measurement cost.
D2.5 Compare envelope gating with full autonomy and with
human-in-loop everything. When does each win?
D2.6 Debug: incidents rise after a capability upgrade. Name two
causes and the measurement that separates them.
D2.7 Critique the margin: when is it too big, when too small?
D2.8 Design the experiment that tests whether envelope-gated
rollouts cut incidents, and state the falsification.

## Analytical exercises (2)

A1. A proof search tries 40 tactic sequences. The kernel accepts
3. The accepted proofs have lengths 4, 6, and 9 steps. Compute
the success rate and the mean proof length. Then compute the
search cost per proof step for the shortest proof, and state in
two sentences why the shortest proof is usually the one to keep.
A2. A robot fuses vision, force, and proprioception with miss
rates 0.20, 0.10, 0.30. Compute the fused miss rate under
independence. Then compute it if vision and force share a
failure mode (their misses coincide), and state in two
sentences what the comparison proves about the independence
assumption.

## Implementation / debug (1)

I1. Your agent's traces always sound plausible, but
interventions show 30 percent are stories. Sketch the trace
audit pipeline you would add (sampling, intervention, verdict),
then name the two most likely causes of story traces and the
single measurement that separates them. State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: the proof assistant is replaced by a
learned verifier with 5 percent error. What survives of the
proof-search loop, what dies, and what new mechanism replaces
the kernel's certainty?
S2. Constraint change: the robot must act with no human in the
building (full autonomy, no approval possible). What survives
of the safety layer, and what must be added before the first
unsupervised run?

## Research critique (1)

R1. "Formal verification will replace testing for AI-generated
code, because proofs are certain and tests are not." Identify
the claim's strongest true part, its weakest assumption, and
the single experiment that would most change your mind.
