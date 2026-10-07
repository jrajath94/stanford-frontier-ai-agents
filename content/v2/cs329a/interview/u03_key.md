# Interview key U03

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: b^d leaves, BFS holds O(b^d), DFS holds O(d). Strong: the
(3, 2) -> 13 nodes / 9 leaves instance. Flags: "BFS is always
better". Rubric: formula 2, memory 3. Remediation: lesson C01.

## B2
Min: set the branching factor per node from an uncertainty or value
signal: wide where uncertain, narrow where settled. Strong: the
marginal-value justification. Flags: "adaptive means random".
Rubric: rule 3, justification 2. Remediation: lesson C02.

## B3
Min: try direct first, decompose only on failure. Saves the
decomposition cost on easy tasks. Strong: the conditional-complexity
framing. Flags: "always decompose". Rubric: rule 2, saving 3.
Remediation: lesson C03.

## B4
Min: the longest dependency chain, paths: A->C = 9, B = 6, critical
path 9. Strong: notes the schedule achieves 11 (wave structure adds
B's slack) while 9 is the floor. Flags: answering 11 as the critical
path. Rubric: definition 2, computation 3. Remediation: lesson C04.

## B5
Min: A_i = (r_i - mean(r)) / std(r), the group replaces the learned
value network as the baseline. Strong: adds the std guard. Flags:
forgetting the std. Rubric: formula 3, replacement 2. Remediation:
lesson C09.

## B6
Min: update data comes from the current policy, stale data biases the
gradient toward old behavior. Strong: the importance-weight
correction and its variance cost. Flags: "off-policy is always
wrong". Rubric: definition 2, failure 3. Remediation: lesson C10.

## Ladder 1
D1.1 Min: node = state plus pending subplan, b = children per node.
d = levels. Strong: states the full-observability assumption.
D1.2 Min: 9 leaves, 13 nodes, BFS order 1, 2, 3, 4 (root then level
1). Strong: draws the tree.
D1.3 Min: b choices at each of d levels multiply to b^d, visiting
each once is O(b^d). Strong: the product-rule step.
D1.4 Min: the BFS code, BFS O(b^d) memory, DFS O(d). Strong: explains
why (frontier vs path).
D1.5 Min: tree wins when intermediate states need scores and
backtracking matters, chains win when branching is wide and scoring
is cheap. Strong: the matched-budget condition.
D1.6 Min: cycles (fix: visited set), infinite action space (fix:
sample actions). Strong: distinguishes the two by the frontier growth
pattern.
D1.7 Min: b is undefined for free text, the tree never starts.
Strong: sampling actions or discretizing via the model's top-k.
D1.8 Min: fixed node budget, both methods, task success metric.
falsified if scores tie (tree adds nothing over sampling). Strong:
adds seed variation and the preregistered metric.
Flags: counting nodes wrong. Rubric: 2 per rung, 16 total, pass at
11. Remediation: lesson C01, C11.

## Ladder 2
D2.1 Min: G responses to one prompt, reward per response, A_i =
(r_i - mean)/std. Strong: states the KL-to-reference term.
D2.2 Min: mean 1.0, std 0.7071, advantages [1.4142, -1.4142, 0, 0].
Strong: verifies the sum is 0.
D2.3 Min: the mean absorbs prompt difficulty, so hard prompts still
rank, std normalizes update scale across prompts. Strong: the
hard-prompt-with-low-rewards example.
D2.4 Min: the code with the var>0 guard, small G makes std noisy.
Strong: quantifies (G = 4 is a toy).
D2.5 Min: PPO's value net earns its keep with small groups or sparse
cross-prompt rewards. Strong: the compute tradeoff.
D2.6 Min: all-equal rewards (fix: prompt selection), G too small with
quantized rewards. Strong: distinguishes by the reward histogram.
D2.7 Min: ambiguous prompts with two valid readings, ranking punishes
the valid minority reading. Strong: proposes per-reading grouping.
D2.8 Min: audit every 10 percent of training: held-out correlation,
human spot-check, drift slope, verdict invalid if gaps exceed
tolerance. Strong: adds the alert-and-pause rule.
Flags: "GRPO has no hyperparameters". Rubric: 2 per rung, 16 total.
pass at 11. Remediation: lesson C09, C12.

## A1
Min: full expansion is 1 + 4 + 16 + 64 = 85 <= 100, so 0 depth-3
nodes go unexpanded. Expected wall-clock: 100 * (0.9*2 + 0.1*60) =
780s. The node budget hides cost heterogeneity: 600 of 780s come
from the 10 percent heavy nodes. Strong: notes the 15 spare
expansions and the variance (not just the mean). Flags: answering 21
unexpanded (the b=3 pattern misapplied). Rubric: expansion math 2,
wall-clock 2, hidden-cost 2, pass at 4. Remediation: lesson C01,
C11.

## A2
Min: gaps 0.18 and 0.20, both above 0.1: verdict INVALID. Gaming
margin: reward rose 0.30, human fell 0.20, margin 0.50. The margin
is the total divergence between the optimized proxy and the human-
judged goal. Strong: notes the margin can exceed 1 in principle and
that the sign pattern (proxy up, goal down) is the signature.
Flags: calling it valid because held-out also rose. Rubric: verdict
2, margin 2, meaning 2, pass at 4. Remediation: lesson C12.

## I1
Min: sketch: sample group -> compute rewards -> audit(rewards,
heldout, human_sample) every K steps -> log gaps -> update. Causes:
(1) reward gaming (proxy climbed, goal flat), (2) human-judge drift
or too-small human sample. Separating measurement: the held-out
reward trend: if held-out also climbs, judges drifted, if held-out is
flat while train climbs, the policy games. Fixes: (1) rotate hidden
tests / fix the proxy, (2) recalibrate judges / enlarge the sample.
Strong: adds the pause-on-invalid rule. Flags: "train longer".
Rubric: sketch 2, causes 2, measurement 2, fixes 2, pass at 5.
Remediation: lesson C08, C12.

## S1
Min: fixed-b trees die. Survivors: sampling chains (replaces
expansion with sampling), MCTS with progressive widening (adds
children as visits grow), beam search over model-ranked
continuations. Strong: states the new assumption each needs (e.g.,
the sampler proposes good actions). Flags: "just set b very large".
Rubric: 2 per survivor with replacement, pass at 4. Remediation:
lesson C01, C02.

## S2
Min: full-trajectory REINFORCE survives (needs the binary signal to
be the true goal), value-model credit survives (needs the value model
to learn from sparse ends, which is hard), ablation credit dies (too
expensive at T = 50). Strong: adds hindsight methods as the
principled alternative. Flags: "just use a bigger baseline".
Rubric: 2 per method with assumption, pass at 4. Remediation: lesson
C05.

## R1
Min: strongest true part: verifiable rewards let RL discover traces
no human wrote. Weakest assumption: that verifiable equals complete
(tests rarely cover the goal). Decisive experiment: matched-compute
STaR vs reasoning RL on tasks where the initial keeper rate is near
zero, if RL wins only there, imitation stays valuable elsewhere.
Strong: adds that the claim confuses discovery with obsolescence.
Flags: "RL always beats imitation". Rubric: true part 2, assumption
2, experiment 3, pass at 5. Remediation: lesson C07, C08.
