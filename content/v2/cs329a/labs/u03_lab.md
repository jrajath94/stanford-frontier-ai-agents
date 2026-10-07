# Lab U03 , Planning, search, and train-time RL

Run script: `runs/run_u03.py`. Deterministic, no seed needed. Status:
executed 2026-10-07. Observed outputs are recorded below.

## Exercise 1 , BFS counts

Task: count nodes and leaves by real expansion for (b, d) in
{(3, 2), (3, 3), (4, 2)}.

Expected: (13, 9), (40, 27), (21, 16).

Observed: (13, 9), (40, 27), (21, 16).

Verdict: PASS. Matches lesson C01 items 2 and 6.

Analysis questions (answers in `keys/u03_key.md`):
L1.1: why does the node total equal the geometric sum?
L1.2: what would the leaf count be with a cycle in the state graph?

## Exercise 2 , GRPO advantages

Task: compute group advantages for rewards [2, 0, 1, 1] and for
[1, 1, 1, 1].

Expected: [1.4142, -1.4142, 0, 0], sum 0, all-equal gives zeros.

Observed: [1.4142, -1.4142, 0.0000, 0.0000], [0.0, 0.0, 0.0, 0.0].

Verdict: PASS. Matches lesson C09 item 6.

Analysis questions:
L2.1: why must the advantages sum to 0?
L2.2: what does the all-equal case teach about group size?

## Exercise 3 , budgeted search

Task: run the toy budgeted search at budgets 0, 10, 100.

Expected: spent never exceeds budget, budget 0 returns best -1.

Observed: (0, -1), (10, 9), (100, 99).

Verdict: PASS.

Analysis questions:
L3.1: the best at budget 100 is 99, the 100th node id. What real
information is lost by reporting only this number?

## Exercise 4 , STaR ratchet

Task: simulate three STaR rounds with gains 0.15, 0.10, 0.05.

Expected: keepers 30, 45, 55, accuracies 0.45, 0.55, 0.60.

Observed: keepers 30/45/55, acc 0.45/0.55/0.60.

Verdict: PASS. Matches lesson C07 item 6.

Analysis questions:
L4.1: the simulation assumes the gain schedule. What in a real run
sets the gains?

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for multi-step reasoning). They are not
the course homework and do not reproduce any assessed artifact.
