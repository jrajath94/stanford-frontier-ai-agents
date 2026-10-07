# U05 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: GEPA, MIPROv2, OPRO, TextGrad. Shared loop: propose, score on a dev set, reflect in words, update, keep the best. Red flag: "they are prompt libraries". Remediation: C01.
- B2: prompts, weights, compute. Spend words first, weights second, compute last. Red flag: "bigger model first". Remediation: C02.
- B3: W + (alpha/r) B A. 8 x 1024 + 8 x 1024 = 16,384 vs 1,048,576 full. Red flag: "LoRA trains the base". Remediation: C03.
- B4: preference pairs (x, y_w, y_l). Replaces the reward model and the RL stage. Red flag: "DPO needs a reward model". Remediation: C05.
- B5: traces $0.01, demos $2, feedback $0.10 per item. 1000 items: $10, $2000, $100. Remediation: C06.
- B6: dev (touch freely), held-out test (score on schedule), sealed (one look). Red flag: "tune on the test". Remediation: C12.

## Deep ladders

- L1.1: p a string, D n checkable examples, m(p, D) in [0, 1], f a failure sentence, u(p, f) the edited string.
- L1.2: argmax candidate 4 at 0.78. Cost 80 scored calls. SE 0.10.
- L1.3: a diagnosed edit targets the observed failure mode, so its hit rate exceeds random edits. Fewer scored calls per unit of gain.
- L1.4: loop over rounds: propose edits, score the batch, keep the best. Cost per round = batch x n x per-call cost.
- L1.5: the optimizer changes words (cheap, interpretable, shallow). LoRA changes numbers (deeper, needs data and GPUs). Words win when the fix is expressible. Rubric: both mechanisms plus the boundary.
- L2.1: (x, y_w, y_l). pi_theta the policy, pi_ref the frozen reference. m = log-ratio margin. beta the divergence penalty.
- L2.2: 0.673 and 0.724. Rubric: both numbers.
- L2.3: beta sets how far the policy may move from the reference. At beta = 0 the loss is constant log 2 and nothing trains.
- L2.4: four log-probs, form m, sigmoid loss, backprop. Cost: four forward passes per pair.
- L2.5: DPO needs pairs only. RLHF needs pairs plus online RL. SFT-on-winners needs only good answers but learns no contrast. Rubric: data needs plus one failure mode each.

## Analytical/quantitative

- A1: gap = 0.65 - 0.50 = 0.15. The climb from 0.65 to 0.90 rides the validator's optimism. Human-judged gain is likely near zero. Red flag: reporting the 0.90 as a result.
- A2: per matrix 16 x 8192 = 131,072. Times 4 matrices times 32 layers = 16,777,216 (16.8M). Full: 4 x 32 x 4096^2 = 2.147B. Ratio 128x. Assumes Q, K, V, O per layer. Rubric: the count plus the stated assumption.

## Implementation/debug

- I1: bug 1: the dev set is tiny or leaked into the edit loop, so the 0.95 is overfit (check: score on the sealed set per round and watch the dev-sealed gap). Bug 2: the metric rewards a spurious pattern the edits learned to exploit (check: audit the winning prompt's traces for the exploited pattern). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: $100 buys 5 demos. Drop demos. Generate synthetic data with the big model, verify with code checks (the task is checkable), keep the 5 demos as the seed and calibration set. Flywheel later when users arrive.
- S2: the loss needs pi_ref log-probs for the margin. Without them, drop the reference terms (m = theta margin only) and add an explicit KL penalty to a frozen copy, or treat it as SFT with a contrastive term. First test: the policy does not drift off-distribution on a held-out probe.

## Research critique

- R1: strong: steelman = "words are cheaper than gradients and reach the same behaviors". Rebuttal 1: some behaviors are not expressible in a prompt (the C02 boundary). Rebuttal 2: the toy where prompt search stalls at 0.79 while fine-tuning reaches 0.83. Experiment: matched three-knob comparison on 5 task families with sealed scoring. Prompt-only wins only where the fix is verbal.

## Concept-targeted supplements

- CS1: GEPA reflects on full traces. OPRO keeps a history of (prompt, score) pairs and proposes from the pattern. TextGrad backpropagates a sentence through each pipeline step. MIPROv2 searches wording and demonstrations jointly. With 5 dev examples the loop "improves" 0.40 to 1.00 on dev and the winner fails on new inputs: overfitting, not learning. Rubric: four distinct signals plus the overfit mechanism.
