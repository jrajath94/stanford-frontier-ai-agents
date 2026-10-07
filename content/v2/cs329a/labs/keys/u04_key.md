# Lab key U04

Keep separate from the lab. Test-mode answers live here only.

## L1.1
Truncation keeps only the top-k, so its survivor mean is the top of
the distribution. Proportionate selection keeps some low-fitness
candidates by lottery, which drags its expected survivor mean down.

## L2.1
Convergence on the optimum (nothing better exists in reach), or
stalling on a local optimum (better exists but mutation cannot reach
it). The fitness curve alone cannot tell them apart.

## L2.2
Single-bit flips: children differ from parents by one bit, so their
fitness differs by at most 1. Small edits cause small fitness changes,
which is the locality claim.

## L3.1
When the per-design errors are not normal or not independent, for
example heavy-tailed task scores or shared tasks across designs. The
constant is also wrong when n_designs is small.

## L4.1
Non-uniform eval costs: hard tasks run long traces that cost 10x.
That hits the money and time fuels while the sheet assumes uniform
cost.
