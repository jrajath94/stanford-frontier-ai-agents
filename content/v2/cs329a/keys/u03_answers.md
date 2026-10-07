# Answer key , U03 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
Leaves: 4^2 = 16. Total nodes: 1 + 4 + 16 = 21.

## E1.2
BFS frontier holds up to b^d = 5^6 = 15,625 nodes. DFS holds one path:
d + 1 = 7 nodes.

## E1.3
A cycle lets expansion revisit the same states forever. Track visited
states and skip them, or the tree never terminates.

## E2.1
Leaves: 3 + 3 * 1 = 6.

## E2.2
Fixed b = 3, d = 2 gives 9 leaves. Adaptive gives 6. Saving: 3 leaves
at the same depth.

## E2.3
A noisy uncertainty signal allocates branches at random. The tree then
underperforms fixed branching while also paying the signal compute.

## E3.1
Direct: 4^3 = 64 leaves. Two subtasks of b = 2, d = 2: 4 leaves each,
8 total, plus the combiner. Saving: 64 down to about 8.

## E3.2
Topic, length, audience, deadline. The outline flows from planning to
each section, the style guide is shared, the combiner checks total
length against the limit.

## E3.3
Humor lives in the coupling of setup and punchline. Written separately
with only a thin interface, the combination is grammatical but not
funny.

## E4.1
Serial: 2 + 3 + 4 = 9. Parallel: A and B run together (3s), then C
(4s): 7s. Critical path: max(2 + 4, 3 + 4) = 7.

## E4.2
The critical path A->C is 9 in the lesson's numbers (4 + 5), but wave 1
must wait for the slowest parallel task B (6s) before C can start, so
the schedule is 6 + 5 = 11. Wave structure adds B's slack on top of
the critical path.

## E4.3
A write-write race: two parallel subtasks writing the same file
corrupt it. Shared mutable state breaks the independence assumption.

## E5.1
Total 1.0. Shares: s1 0.5, s2 0.05, s3 0.45.

## E5.2
Two redundant steps: removing either alone changes nothing, so each
gets zero marginal credit. Removing both breaks everything. Marginal
credit misses joint necessity.

## E5.3
When the trajectory is short and each evaluation is cheap. At scale,
replace it with a learned value model and keep ablations as spot
checks.

## E6.1
520 of 1000 traces kept.

## E6.2
Each round trains on the filtered output of the last round. The filter
is stricter than the generator is good, so the kept set is above
average and imitation raises the average.

## E6.3
All 1000 traces follow one template. The kept set teaches one trick
and the policy collapses to it.

## E7.1
0.60 + 0.025 = 0.625.

## E7.2
The initial policy must be good enough to produce some keepers. The
kept set is above average, so imitating it raises the average. With
zero keepers there is nothing to imitate.

## E7.3
Rationalization: hint the correct answer, generate the rationale
afterward, keep the triple if the rationale supports the answer. It
fills the keeper gap on hard questions.

## E8.1
Mean 0.4. Advantages: [0.6, 0.6, -0.4, -0.4, -0.4]. They sum to 0.

## E8.2
STaR fine-tunes on the winning traces only. Reasoning RL also pushes
away from the losing traces through negative advantages.

## E8.3
Drop prompts the policy always solves and prompts it never solves.
All-zero groups carry no gradient, so they waste the sampling budget.

## E9.1
Mean 2.0, variance 1.0, std 1.0. Advantages: [1.0, -1.0, -1.0, 1.0].

## E9.2
The group mean absorbs the prompt's difficulty level. A hard prompt
with all-low rewards still yields a useful within-group ranking,
because the baseline is the group's own average.

## E9.3
When variance is 0 the function returns std 1.0 instead of dividing by
zero. It triggers when all rewards in the group are equal, the
advantages are then all zero.

## E10.1
Weight = 0.3 / 0.9 = 0.333. The corrected gradient is one third of the
naive stale push.

## E10.2
The new policy assigns probability 0 to the action, so it dropped the action
it. Stale successes of an abandoned action get weight 0 and teach
nothing.

## E10.3
Regenerate the data every few updates. Keep the staleness small by
procedure instead of correcting large staleness with noisy weights.

## E11.1
Depth 3 holds 81 nodes. The budget expands 60 of them. Unexpanded: 21.

## E11.2
The true best leaf is the 101st node expanded. The budget stopped at
100, so the reported best is the second-best leaf. The budget hides
the tail it never saw.

## E11.3
Budget in real cost units (dollars or seconds), not node counts. Or
weight each expansion by its measured cost in the ledger.

## E12.1
Gaps: 0.85 - 0.80 = 0.05, 0.85 - 0.82 = 0.03. Both within 0.1.
Verdict: valid.

## E12.2
The training reward rose 0.30 while the human pass rate fell 0.20. The
gap between the proxy's rise and the goal's fall is the gaming margin:
0.50 of divergence.

## E12.3
The held-out tests leak into the training data. Every instrument then
agrees and every instrument is wrong, because the separation that made
them independent is gone.
