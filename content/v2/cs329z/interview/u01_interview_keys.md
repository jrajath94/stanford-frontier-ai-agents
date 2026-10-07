# U01 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item. Test-mode answers stay here, separate from questions.

## Breadth

- B1: strong: "A model maps token sequences to token sequences. A compound system joins a model with retrievers, tools, and checks through typed interfaces." Red flag: "a system is a bigger model". Rubric: both definitions plus the interface idea. Remediation: reread C01.
- B2: decomposition, data, evaluation. Red flag: naming only one. Rubric: all three. Remediation: C01 contract 1.
- B3: Attention(Q,K,V) = softmax(QK^T/sqrt(d_k))V, Q,K,V in R^(n x d_k) per head. Scores (n x n). Red flag: missing the scale or the shapes. Rubric: equation plus all shapes. Remediation: C04.
- B4: T < 1 sharpens toward the argmax, T > 1 flattens toward uniform. Entropy rises with T. Red flag: "higher T means more random" without the limit behavior. Rubric: both directions plus one number. Remediation: C05.
- B5: stored keys and values for past tokens. Bytes = 2 L n d x bytes-per-scalar. Red flag: confusing it with the weights. Rubric: purpose plus the formula. Remediation: C06.
- B6: structured I/O constrains the output shape by contract and validates after. Constrained decoding masks logits during sampling so invalid tokens have probability 0. Red flag: "they are the same". Rubric: timing difference (during vs after). Remediation: C07/C08.

## Deep ladders

- L1.1: p_i = exp(z_i/T) / sum_j exp(z_j/T).
- L1.2: [0.09, 0.24, 0.67].
- L1.3: as T -> 0, (z_i - z_max)/T -> -inf for i not argmax, so their mass -> 0 and the argmax keeps mass 1.
- L1.4: cumulative-sum sampler, O(V) per step. Strong code subtracts the max before exp.
- L1.5: temperature reshapes the whole distribution. Top-k truncates to k tokens and renormalizes. Red flag: treating them as interchangeable.
- L2.1: 1 - (1 - p)^k.
- L2.2: 1 - 0.7^8 = 0.942.
- L2.3: vote helps when p > 0.5 (modal answer right). Hurts below.
- L2.4: Bernoulli trials loop. Cost linear in k. Latency linear unless parallel.
- L2.5: 8 small samples: 0.942 at 8x cost, 1 big sample: 0.6 at 4x. Small wins on accuracy per the toy. Big wins on latency. Rubric: both numbers plus the tradeoff.

## Analytical/quantitative

- A1: 2 L n^2 d = 2 x 32 x 8192^2 x 4096 = 1.76e13 FLOPs. Strong answer shows each factor. Red flag: forgetting L or the factor 2.
- A2: SE = sqrt(0.8 x 0.2 / 25) = 0.08. n near 0.16 x (2/0.05)^2 = 256. Red flag: quoting 0.80 without an interval.

## Implementation/debug

- I1: bug 1: mask applied after temperature division with -inf turned into NaN by a bad softmax (check for NaN in p). Bug 2: the allowed set computed from a stale automaton state (log the state per step and assert membership before sampling). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: still apply: greedy decoding, structured output via prompt plus validation, KV cache (one call still decodes), pre/post-training choice. Die: test-time scaling, multi-sample voting, retry loops, agentic loops.
- S2: the fine-tune goes stale hourly. Cheapest fix is retrieval over the fresh corpus (RAG) in front of the frozen model, not hourly retraining.

## Research critique

- R1: strong: steelman = "a 1M window holds the whole corpus, so ranking is unnecessary". Rebuttal 1: cost (quadratic prefill, GBs of cache). Rebuttal 2: distraction (irrelevant tokens hurt accuracy. Lost-in-the-middle). Experiment: fix the task, vary retrieved-set size vs full-context stuffing, measure accuracy and cost. Rubric: steelman first, then two distinct rebuttals, then a falsifiable test.

## Concept-targeted supplements

- CS1: neither ships. SE of 8/10 is sqrt(0.8 x 0.2 / 10) = 0.13. The 0.1 gap sits inside the noise. Grow the eval first. Two lies: non-representativeness (easy-only eval scores 0.95, production 0.5) and train-eval leakage (the score measures memory, not ability). Rubric: the 0.13 computation plus two distinct failure modes.
