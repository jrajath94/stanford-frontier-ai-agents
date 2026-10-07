# Transfer sets key

Test-mode key. Full answers. Keep separate from the questions.

## T1
A1: per-sample cost 500 tokens. 3.2k/500 = 6.4, so N=6
(spend 3.0k, within the line). Success rate falls: the
cost-success curve (U01 C12) is concave, so cutting N 64->6
loses most of the selection gain. The exact new rate needs
the curve, but the direction is down and the drop is large.
A2: (1) self-consistency over fewer, better samples: needs
per-sample accuracy above chance (the pilot's regime). (2) a
cheaper verifier (distilled): needs the verifier's pairwise
accuracy to stay above 0.60 on the pile, else H2 is
untestable. A third: serial refinement (U05 C01): needs the
task to be improvable by iteration.

## T2
A1: it selects for length, not correctness. The reported
success rate rises (long answers get picked) while true
success is flat or falls: the metric is gamed. A2:
diagnostic: the score-vs-length correlation (U01 C11).
positive correlation with no correctness gain means bias.
Fix: length-normalize the verifier scores, or retrain the
verifier with length-decorrelated labels.

## T3
A1: survives: the language prior, in-context reasoning,
question answering from the prompt. Dies: anything needing
ground truth (arithmetic, code, fresh facts). The honest new
claim: it is a chatbot, not an agent. Report the tool-less
scores separately. A2: replacement: self-critique
(constitutional-style, U02 C06) or majority vote. Lost: the
grounding. The error signal is now the model's own opinion,
which shares its blind spots (U08 C07 in miniature).

## T4
A1: plan success falls toward the failure rate of the lied-
about transition, and tree search amplifies it: the planner
steers INTO the bad transition because the model says it
works. A2: the bound: execution feedback and replanning
(U02 C02 ported, U03 C04 parallel execution with checks):
replan when the world disagrees. The measurement: predicted
vs actual transition success per edge. The lying edge shows
a large, systematic gap.

## T5
A1: at generation 40 the population is full of proxy-
hackers: architectures that maximize the proxy while true
success is low. The proxy still rises because selection
selects on the proxy, and the proxy is what selection sees:
Goodhart in a population. A2: C09 holdout separation: the
exact check scores the generation-40 champion on the
held-out set with the TRUE metric. The gap between proxy
and holdout-true is the deception meter. (C11 novelty claims
and C12 safe iteration are the siblings.)

## T6
A1: cut K first. The coverage math (U05 C01): serial depth S
raises coverage (0.832 to 0.997 over S=1..5), while K
amortizes context. Coverage is the goal. Context share is
the cost. Keep S, shrink K until the context fits. A2: the
context share DOUBLES at each K (the shared prefix is now
half the window): at K=32 the share goes 7.7 percent to
about 15 percent. What breaks first: the longest serial
trajectories (S large) no longer fit with the context, so
the effective S cap falls.

## T7
A1: fast_p is unmeasurable: it needs both correctness AND
speedup >= p, and speedup needs execution. The correctness
half can still be checked by reading the code (or CPU
execution for logic, not speed). The speed half dies. A2:
the replacement gate: human expert review plus a static
correctness argument, or CPU-executed logic tests. Cost:
reviewer hours per kernel, and no speed signal at all: ship
nothing perf-sensitive until GPUs return.

## T8
A1: the 12 paged-out facts are lost. The toy becomes 8 hot
facts and 12 missing: recall fails, and the first failure
mode is silent forgetting (the agent answers without the
fact, confidently). A2: the bound: the context window itself
(U06): the new limit is 8 facts, period. The capacity math:
working set must be <= 8 or the agent confabulates. The
honest move: shrink the task to fit 8 facts, or restore the
store.

## T9
A1: the reported proof rate rises slightly (2 percent of
false proofs now count). The damage is invisible because
every monitoring metric is computed BY the kernel: the
checker that is wrong is also the measurer. A2: the check:
an independent second kernel (or a human audit of accepted
proofs). What must be re-proved: every proof accepted since
the bug was introduced. The acceptance log is the re-proof
list.

## T10
A1: SE = sqrt(0.5*0.5/132) = sqrt(0.001894) = 0.0435, about
0.044 (vs 0.014 on 1,320). What dies: any claim of small
margins (a 0.53 vs 0.50 win rate is noise now), sector and
occupation breakdowns (tiny n per cell), and the leaderboard
ordering. A2: (1) a cheaper judge (different-lab model):
bias is judge contamination (U08 C07), report the gap.
(2) fewer, higher-value tasks (U08 C02 value weighting):
bias is coverage (the eval no longer represents the
occupation mix).
