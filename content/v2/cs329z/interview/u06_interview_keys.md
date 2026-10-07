# U06 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: R (what), E (where), S (when to stop), F (how to score). Red flag: "the task is the benchmark". Remediation: C01.
- B2: how closely benchmark tools match production. A 0.13 gap says the mock hides a real failure slice. Remediation: C02.
- B3: program $1, model $50, human $2000 per 1000. Cascade: program first, model on unclear, humans on a sample. Remediation: C03.
- B4: criteria, level anchors, examples per level, fixed output format. Red flag: "rate 1-5". Remediation: C04.
- B5: P(i beats j) = 1/(1 + e^-(s_i - s_j)). Remediation: C05.
- B6: z = delta/SE. Block below -2, celebrate above 2, rerun otherwise. Red flag: "block on any drop". Remediation: C11.

## Deep ladders

- L1.1: R the request, E the reproducible environment, S the stopping predicate, F the trace-to-score function.
- L1.2: the 0.08 gap is the stopping rule. Same agent, different S, different number.
- L1.3: no R cannot run, no E different machines, no S runs forever, no F unranked. Each answers a question the others cannot.
- L1.4: reset E, loop until S, apply F. Cost per task = steps x per-step cost.
- L1.5: program F is fast, cheap, gameable. Human F is slow, expensive, trusted. Rubric: all three axes.
- L2.1: p per-sample pass rate, k samples, independent draws assumed.
- L2.2: 0.83193 and 0.00243. Rubric: both numbers.
- L2.3: P(at least one) = 1 - P(none pass) = 1 - (1-p)^k under independence.
- L2.4: loop over k, two columns. O(k) arithmetic.
- L2.5: the code agent gets pass@k (8 tries, verifier picks). The medical answer gets pass^k (one try must work). Rubric: the match plus the reason.

## Analytical/quantitative

- A1: z = 0.06/0.05 = 1.2, rerun (suggestive, not actionable). For a 0.02 delta at z = 2: SE = 0.01, n = 0.5/0.0001 = 5000 tasks. Rubric: z, verdict, and the n.
- A2: sigma(0.89 + 0.44) = sigma(1.33) = 0.79 vs observed 0.80. The fit reproduces the data. Red flag: "the fit is wrong because 0.79 != 0.80".

## Implementation/debug

- I1: leak 1: shared filesystem or warm container layer between tasks (check: the canary test, write in task 1, verify gone in task 2). Leak 2: the environment image or tool version drifted (check: pin the image hash and diff it across runs). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: fresh container and reset survive. Network-off dies. New flakiness: site changes, rate limits, latency variance. Mitigation: record-and-replay for determinism, live spot-checks for fidelity.
- S2: program grading on all 100,000 costs $100. Model grading on the 1000 most unclear costs $50. Humans on a 25-item calibration sample cost $50. Total $200. The unclear slice is capped by budget, not by need.

## Research critique

- R1: strong: steelman = "the tuple is reproducible, so the number is objective". Rebuttal 1: the scaffolding lie (0.13 mock gap) and the deleted-test cheat both raise scores without improving the agent. Rebuttal 2: unknown human alignment (r = 0.31 toy) means the climb is unanchored. Experiment: correlate benchmark deltas with production outcomes across 20 tasks. Alignment above 0.7 would change the verdict.
