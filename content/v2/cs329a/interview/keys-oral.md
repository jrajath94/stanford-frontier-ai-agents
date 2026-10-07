# Oral defenses key

Test-mode key. 8 rungs per ladder. Keep separate from the
questions.

## O1
1. BoN: sample N, keep the verifier's top pick. SC: sample N,
take the majority answer.
2. SC: P(majority of 5 correct) with p=0.7: sum_{k=3..5}
C(5,k)0.7^k0.3^{5-k} = 0.8369. BoN with a perfect verifier:
1-(0.3)^5 = 0.9976. With a weak one, between.
3. BoN picks one sample, so it needs a judge of samples. SC
votes, so the crowd is the judge.
4. Same token spend per question: N differs because scoring
costs extra (N_bon*(gen+score) = N_sc*gen).
5. 0.52 is below 0.55: H2 is untestable. The verifier is
noise. Do not run BoN. Fix or replace the verifier first.
6. Voting uses all N samples' information. Picking one
throws N-1 away. The weights let good samples outvote bad
ones without the winner-take-all risk.
7. More is not better past the budget line. Each sample
costs tokens, the verifier's errors compound, and the
cost-success curve flattens. N=1000 spends 1000x for a
whisker of gain.
8. A preregistered matched-budget run where a 0.85-accurate
verifier's BoN loses to SC on any seed would falsify H2.
Flags: confusing N with budget. Pass: 6 of 8 rungs.

## O2
1. thought -> action -> observation -> thought -> action ...
until answer.
2. It should read the error, diagnose, and retry with a fix.
The failure mode is a repeat of the same call.
3. Execution feedback is ground truth from the world.
Self-critique is the model's opinion, sharing its blind
spots.
4. The agent exploits the tool or the reward signal instead
of doing the task (e.g., editing the test).
5. The tools work but the plan is wrong: 0.95 tool success
with 0.40 task success means the agent does the wrong
things correctly. Diagnose the planner, not the tools.
6. It diverges when the error never resolves: the guard is a
step cap plus a repeated-action detector.
7. Steel-man: tools let the model offload thinking.
Rebuttal: tools ground the thinking. The record shows
tool-using agents beat tool-less ones on agentic tasks.
8. Same tasks, two evals: execution-feedback pass vs
independent-validation pass. The gap is what feedback
misses (e.g., tests that do not cover the bug).
Flags: "more tools is always better". Pass: 6 of 8.

## O3
1. State: the reasoning-so-far. Action: the next step.
Reward: 1 iff the final answer is right (or verifier score).
2. 3^2 = 9 leaves, 1 correct: 1/9.
3. Every node is labeled right/wrong for free, so scoring
and stopping are solved. Only the policy is learned.
4. A high reward that does not mean a right answer is not a
reward, it is a hack.
5. The reward model is wrong: it scores the hack high.
Diagnose the reward, not the search: check reward-vs-truth
correlation on held-out traces.
6. MCTS wins with a good value function and big budgets.
Beam search wins with small budgets and strong step models.
7. Search is not slow sampling: it allocates compute
unevenly (more to likely branches), reuses the verifier
for free labels, and backtracks. Sampling is flat.
8. Fix the budget, swap the reward model (learned vs
verifier). Then fix the reward, sweep the budget. The
binding constraint is the one whose change moves the score.
Flags: "deeper is always better". Pass: 6 of 8.

## O4
1. Vary the population, select the fittest, inherit with
mutation.
2. 3 of 10 reproduce: selection pressure 0.3 (top 30%).
3. In deceptive landscapes the objective misleads. Novelty
rewards being different, which escapes the local optimum.
4. The champion is scored on data the search never saw, with
the true metric.
5. Overfitting to the selection metric (or the proxy is
deceptive): the 0.35 gap is the deception meter. Trust the
holdout.
6. When gradients are unavailable or the terrain is
deceptive and rugged.
7. Steel-man: selection without gradients is weak per step.
Rebuttal: populations explore in parallel and need no
differentiability. The record includes real wins.
8. Score the champion on a FRESH holdout from the same
distribution: if the gap persists, it is overfit. If it
closes, the first holdout shifted.
Flags: "evolution needs no validation". Pass: 6 of 8.

## O5
1. S: serial refinement iterations per trajectory. K:
parallel trajectories.
2. (0.997-0.832)/4 = 0.041 per iteration.
3. Depth gives the agent more chances to fix its own
mistakes (coverage rises). Width shares the one context
across trajectories (cost per trajectory falls).
4. Voting with model-generated tests selects the trajectory
whose tests agree most: it selects for self-consistent
solutions.
5. Causes: the task is solved by S=3 (saturation), or the
refinement step is broken (no new information). Separate:
the per-iteration delta: zero delta with good tests means
saturation. Zero delta with failing tests means broken
refinement.
6. Cut K. Coverage is the goal and S buys it (0.041 per
iteration). K buys cost amortization. Keep S, shrink K to
fit.
7. K=1000 costs 1000x the context for a shrinking coverage
gain. The context share explodes. And selection over 1000
noisy trajectories needs a verifier that good. Coverage is
not all that matters: cost and selection quality matter.
8. Ablate: voting-only vs trajectory-only selection at fixed
compute. The bigger score drop marks the more important
stage.
Flags: confusing S with N. Pass: 6 of 8.

## O6
1. The KV cache stores keys and values of past tokens so
decoding does not recompute them. It is the working memory
of inference.
2. 2,048 * 0.15 = 307 recomputed. 2,048-307 = 1,741 Saved,
about 85 percent of prefill.
3. Most tokens' KV barely changes across chunks. Only
high-deviation tokens need fresh compute. Recomputing all
is waste.
4. A Cartridge trains a small set of KV vectors per corpus
via self-study. The claim is 40x fewer KV slots per query
than full-corpus KV.
5. The deviation metric misses boundary tokens: their
context changed but their KV did not deviate enough to
trigger recompute. Fix the metric or widen the recompute
window at boundaries.
6. CacheBlend wins for many chunks with shared prefixes
(reuse without training). Cartridges win for a stable
corpus queried often (training amortizes).
7. Bigger windows cost quadratically in attention and linearly
in memory per query. Caches and cartridges cut the per-
query cost. The window is the ceiling, not the strategy.
8. Fix the deviation metric, sweep the recompute fraction.
Then fix the fraction, swap the metric. The bigger score
move marks the binding choice.
Flags: "cache = memory". Pass: 6 of 8.

## O7
1. Goal: what remains to prove. Tactic: a proof step.
Kernel: the checker that accepts or rejects.
2. Random: (1/12)^4 = 1/20736. Guided (say top-3): (1/3)^4
= 1/81. The ratio is about 256x.
3. One deterministic tactic application is cheap and
infallible. Training the policy that proposes tactics is
the expensive part.
4. Authority must not exceed verified capability, with
margin.
5. Causes: the tactic space lacks the needed tactic, or the
policy never proposes the right sequence. Separate: replay
a human-written proof. If it replays, the space is fine
and the policy is the problem.
6. The proof rate is inflated (false proofs count). The
damage is invisible because the kernel is also the
measurer. Re-prove everything accepted since the bug's
introduction, using the acceptance log.
7. Steel-man: proofs are certain, tests are samples.
Rebuttal: most code has no formal spec, and writing the
spec is the hard part. Proofs check the spec, not the
intent.
8. Fix the policy, vary the tactic set (add/remove
tactics). Then fix the set, vary the policy. The binding
constraint is the one whose change moves the close rate.
Flags: "the net proves". Pass: 6 of 8.

## O8
1. A trace is faithful iff changing the cited fact changes
the behavior (the intervention test).
2. Story rate 0.30: three in ten traces are
rationalizations, not records.
3. Flip the fact the trace cites, hold the rest. Faithful
iff the behavior changes.
4. Same-model agreement minus independent-model agreement:
the similarity-not-quality part of the score.
5. The 0.25 gap is contamination: shared blind spots and
style preference, not quality. The honest score is near
0.60.
6. When a perfect verifier exists (the kernel case):
contamination is zero by construction, any judge works.
7. Everyone using them does not make them valid: the gap
is measured, not hypothetical. Shared training means
shared blind spots. The fix (distance: different lab,
human) is cheap next to a wrong leaderboard.
8. Same tasks, three judges (same-model, different-lab,
human): if the same-vs-different gap persists where the
human agrees with different-lab, it is shared bias. If the
different-lab judge also disagrees with the human, the
judges are incompetent.
Flags: "plausible = faithful". Pass: 6 of 8.

## O9
1. Experts write real deliverables from 44 occupations. Blinded
experts compare agent vs human work pairwise. The metric is
the win rate.
2. 660/1320 = 0.50. Gold SE: sqrt(0.25/220) = 0.034.
3. Absolute scoring drifts with judge mood. Pairwise
comparison with blinding measures the work, not the scale
or the source.
4. The mean picks one agent, the minimum picks the other.
5. Do not ship on the mean: the 0.55 task is the production
workload, so users meet 0.55, not 0.77. Ship B, or fix A's
tail.
6. Agent compute, judge cost, human audit. The binding fuel
in the toy is the audit (55 percent).
7. One number hides the horizon (duration curve), the tail
(the min), and the judge (contamination). Three numbers
minimum: a curve, a tail, and a cost.
8. Rank agents by duration-curve area, then by value-
weighted score. The ranking that moves more marks the
more decisive axis.
Flags: inventing benchmark scores. Pass: 6 of 8.

## O10
1. H1/H2/H_ext with the falsification stated: e.g., H2 is
false if BoN loses to SC with a 0.85 verifier at matched
budget on any seed.
2. 0.53 is below 0.55: H2 is untestable, the verifier is
noise. Report uninformative, do not run.
3. Same token spend per question: generation plus scoring
tokens, each method exactly on the line. N differs because
scoring costs extra.
4. A1 verifier-off (isolates the verifier), A2 hybrid
(tests the combination), A3 budget sweep (separates count
from method).
5. The ranking is not stable: conclude nothing about H2.
Report the flip as the finding and investigate the seed
sensitivity.
6. With the same prominence as a positive: the preregistered
falsification failed, here is the CI, here is what it
rules out, here is the next path.
7. Steel-man: synthetic tasks are not the world.
Rebuttal: they test the PIPELINE (seeds, CIs, ablations,
failure criteria). A pipeline that fails on toys fails on
the world. Toys vet methods, not models.
8. The preregistered next step: real tasks with a trusted
verifier subset, or the human-judge version of the
contamination extension.
Flags: hiding the negative. Pass: 6 of 8.
