# notation_and_shapes.md , cs329a U01-U04

Every symbol below is defined before its first use in lessons.

## Sampling and verification (U01)

- N: number of independent samples drawn for one prompt. Unit: count.
  Shape: scalar integer, N >= 1.
- p: single-sample success probability. Unit: probability in [0, 1].
- pass@N: probability that at least one of N samples is correct.
  pass@N = 1 - (1 - p)^N under independence.
- G: generator policy. Maps prompt x to a distribution over completions y.
- V: verifier. Maps (x, y) to a scalar score s in [0, 1] or R.
- s_i: verifier score of sample i. Shape: scalar.
- B: compute budget. Unit: tokens, FLOPs, or dollars. Always name the unit.
- c_s: cost per sample. Total cost of best-of-N is about N * c_s.

## Feedback and tools (U02)

- Trace T: ordered list of steps. T = [t_1, ..., t_K].
- Step t_k: triple (thought_k, action_k, observation_k).
- action_k: tool call with name and typed arguments.
- observation_k: tool return, typed as value or error.
- r_k: reward signal at step k. Scalar. Outcome reward sets r_k = 0 for
  k < K and r_K in {0, 1} or R. Process reward allows nonzero r_k for
  k < K.
- Critique C(y): text judgment of output y. No weight change follows.
- Policy update: weight change from data, for example one gradient step.

## Planning, search, train-time RL (U03)

- Node n: state plus pending subplan in a search tree.
- b: branching factor. d: search depth. Leaf count of full expansion: b^d.
- pi_theta: policy with parameters theta. pi_theta(a | s) is the action
  probability.
- Trajectory tau: (s_0, a_0, r_0, ..., s_T). Return R(tau) = sum of rewards.
- Advantage A(s, a): Q(s, a) - V(s). In GRPO, advantage of response i in a
  group of G responses is (r_i - mean(r)) / std(r).
- KL(pi || pi_ref): divergence penalty that keeps the policy near a
  reference policy. Unit: nats.
- On-policy: update data comes from pi_theta itself.

## Evolution and deep research (U04)

- Population P_t: set of candidate agents at generation t. |P_t| = M.
- Fitness f(c): scalar score of candidate c on the validation split.
- Mutation m(c): stochastic edit of candidate c.
- Selection: keep top-k by fitness, or sample proportional to fitness.
- Holdout H: locked test set, never used for selection or tuning.
- Provenance record: (claim, source, retrieval path, date) for every
  evidence-backed statement a research agent makes.

## General

- Seed: integer that fixes all RNG draws in a run. Always reported.
- CI: confidence interval, with the method named (for example Wilson).
- All toy numbers in lessons are computed by hand-traceable arithmetic or
  by the executed lab scripts. Nothing is a benchmark claim.
