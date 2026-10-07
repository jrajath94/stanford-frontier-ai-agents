# Transfer sets , changed-scenario practice

10 sets. Each changes one constraint from a unit mechanism and asks
what survives, what breaks, and what replaces it. Full keys in
`keys-transfer.md`. Provenance: original practice. Not actual
employer questions.

## T1 , U01 test-time compute under a 10x budget cut

Setup: your best-of-N pipeline runs N=64 at 32k tokens per
question (U01 C02, C12). Finance cuts the budget to 3.2k per
question.
Q1: recompute the feasible N at 400 tokens per sample plus 100
per score, and state what happens to the success rate.
Q2: name two mechanisms from U01 that recover performance
without more tokens, and the condition each needs.

## T2 , U01 selection under an adversarial verifier

Setup: your best-of-N verifier is found to reward long answers
(U01 C11 selection bias). Length and correctness correlate 0.1.
Q1: what does best-of-N now select for, and what happens to the
reported success rate?
Q2: name the diagnostic that catches it and the fix, each in
one sentence.

## T3 , U02 agents with the tools taken away

Setup: your ReAct agent (U02 C01) loses all tool access
mid-deployment: no code execution, no search, no calculators.
Q1: which capabilities survive, which die, and what is the
honest new claim about the agent?
Q2: execution feedback (U02 C02) is gone. What replaces it as
the error signal, and what is lost in the replacement?

## T4 , U03 planning with a wrong world model

Setup: your model-based planner (U03 C01-C04) learns the world
model is systematically wrong about one transition: it predicts
success where the world fails.
Q1: what happens to the plan success rate, and which search
component amplifies the error?
Q2: name the mechanism from U03 that bounds the damage, and
the measurement that tells you the model is the problem.

## T5 , U04 evolution under a deceptive objective

Setup: your agent architecture search (U04 C01-C03) optimizes a
proxy metric that is deceptive: the proxy rises while true task
success falls after generation 20.
Q1: what does the population look like at generation 40, and
why is the proxy still rising?
Q2: name the U04 mechanism that catches this (C09, C11, or
C12), and state the exact check.

## T6 , U05 SWE agents with the context halved

Setup: your CodeMonkeys-style pipeline (U05 C01) runs with the
context window halved. The serial depth S and parallel width K
must fit in half the tokens.
Q1: which do you cut first, S or K, and what does the coverage
math say?
Q2: the context share at K=32 was 7.7 percent. Recompute the
pressure: what breaks first when the window halves?

## T7 , U05 kernel agents with no GPU in CI

Setup: your KernelBench-style loop (U05 C05-C07) loses GPU
access in CI: kernels can be written but not executed before
merge.
Q1: what happens to the fast_p metric, and which half
(correctness or speed) becomes unmeasurable?
Q2: name the replacement gate that keeps bad kernels out of
main, and its cost.

## T8 , U06 memory with the archival store deleted

Setup: your MemGPT-style agent (U06 C01) loses its archival
store: evicted facts are gone, not paged out.
Q1: what happens to the 20-turn toy (8 hot, 12 paged out),
and which failure mode appears first?
Q2: name the mechanism from U06 that bounds the damage, and
the capacity math that sets the new limit.

## T9 , U07 proof search with an unsound kernel

Setup: your formal proof pipeline (U07 C02) ships a kernel
with a soundness bug: it accepts 2 percent of false proofs.
Q1: what happens to the reported proof rate, and why is the
damage invisible in normal monitoring?
Q2: name the check that catches it, and state what must be
re-proved.

## T10 , U08 eval with the budget cut 10x

Setup: your GDPVal-style eval (U08 C03, C08) loses 90 percent
of its budget: 1,320 expert comparisons become 132.
Q1: recompute the SE of a 0.50 win rate on 132 tasks, and
state what claims die.
Q2: name two mechanisms from U08 that stretch the budget,
and the bias each introduces.
