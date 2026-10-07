# Answer key , U01 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
p = 0.1. pass@1 = 0.1. pass@2 = 1 - 0.81 = 0.19. pass@3 = 1 - 0.729 =
0.271. pass@4 = 1 - 0.6561 = 0.3439.

## E1.2
pass@N = 1 - (1 - p)^N. The term (1 - p)^N falls as N rises for
0 < p < 1, so pass@N rises. First difference: pass@N - pass@(N-1) =
p(1 - p)^(N-1), which falls as N rises. Falling first differences mean
concave.

## E1.3
Need 0.75^N <= 0.05. ln(0.05)/ln(0.75) = 10.41, so N = 11. Check:
0.75^10 = 0.05631, pass@10 = 0.94369 < 0.95. 0.75^11 = 0.04224,
pass@11 = 0.95776 >= 0.95.

## E1.4
Temperature 0 makes decoding deterministic, so all N samples are
identical. The independence assumption fails and pass@N = p.

## E2.1
Argmax of [0.1, 0.8, 0.7, 0.2, 0.3] is index 1 with 0.8. Correctness[1]
= 0, so best-of-5 returns sample 2 and it is wrong. The correct sample
was index 2.

## E2.2
A perfect verifier scores every correct sample above every wrong one.
Argmax then picks a correct sample exactly when at least one exists.
That event has probability pass@N.

## E2.3
Correctness [1, 0], scores [0.4, 0.95]. The verifier can be accurate on
average across many questions yet still rank this pair wrong. Accuracy
is aggregate, selection is per instance.

## E3.1
Counts: 7 -> 3, 3 -> 2, 9 -> 1. Winner 7, vote share 3/6 = 0.5.

## E3.2
[7, 7, 3, 3] ties 7 and 3 at 2 votes each. The stated rule picks the
smallest tied answer: 3.

## E3.3
When all paths share one flawed step, every path gives the same wrong
answer and the majority amplifies the shared flaw instead of
correcting it.

## E4.1
Fixed R1: (0.70 + 0.66)/2 = 0.68. Per-task pick: (0.78 + 0.66)/2 =
0.72. Gain 0.04 absolute.

## E4.2
No. Standard error of a 0.75 rate on 40 questions is about
sqrt(0.75 * 0.25 / 40) = 0.068. A 0.08 gap is near one standard error,
so the winner is noise-plausible.

## E4.3
Test-set leakage. The search tuned on the test questions, so the
reported number is no longer a held-out measurement.

## E5.1
p = 0.4. Cheap: pass@20 = 1 - 0.6^20 = 0.99996, times 0.70 = 0.7000.
Strong: pass@8 = 1 - 0.6^8 = 1 - 0.01680 = 0.98320, times 0.90 =
0.88488. The strong plan still wins.

## E5.2
Success = pass@N * a <= 1 * a = a. No sample count beats the verifier
accuracy under the toy model.

## E5.3
The single-number verifier accuracy. Real accuracy varies with question
difficulty, and hard questions both need more samples and fool the
verifier more.

## E6.1
a = 0.55: 0.97175 * 0.55 = 0.53446. a = 0.80: 0.97175 * 0.80 = 0.77740.

## E6.2
Need 0.97175 * a > 0.30, so a > 0.30872. Below about 0.31 the
best-of-10 plan stops helping.

## E6.3
Open-ended creative writing, subjective taste judgments, and novel
research claims: checking has no ground truth there, so verification is
not easier than generation.

## E7.1
Weak: N = 100 // 6 = 16, success about 0.61937. Strong: N = 100 // 16
= 6, pass@6 = 1 - 0.65^6 = 1 - 0.07542 = 0.92458, times 0.90 =
0.83212. The strong plan wins the toy on success, the weak plan wins on
latency.

## E7.2
The generator's wrong answers share a flattering style. The weak
verifier scores style, not correctness, so its accuracy on the wrong
subset is 0.30 even though its overall accuracy is 0.62. Selection then
picks styled wrong answers.

## E7.3
A small verifier scores N samples in roughly the time the generator
draws one sample. Best-of-N latency is generation plus one cheap
scoring pass, not N expensive judgments.

## E8.1
Outcome reward: 0.0, because the final answer is wrong. Process reward:
[1.0, 1.0, 0.0, 1.0]. The process signal credits the good steps of a
failed trace, the outcome signal reports total failure.

## E8.2
Outcome reward attaches to the final answer only, so it never says
which step caused success or failure. Learning must guess the credit
from the whole trace.

## E8.3
An automatic step labeler can mark correct steps wrong when the phrasing
is unusual, or a human labeler can err under hindsight. Either injects
bias into the dense signal.

## E9.1
Sample 4: logit = 0 - 2.0 = -2.0, s = 0.1192. Label 0. Contribution:
-log(1 - 0.1192) = -log(0.8808) = 0.1269, about 0.127.

## E9.2
With 10 percent flipped labels, even the Bayes-optimal classifier is
wrong on about 10 percent of items. More capacity cannot fix wrong
supervision.

## E9.3
Training on short human-written solutions while scoring long
model-generated samples. Length and style shift, the verifier learns
brevity as a proxy for quality.

## E10.1
Sorted pairs: (0.12,0), (0.30,0), (0.41,0), (0.55,1), (0.62,0),
(0.78,1), (0.81,1), (0.88,0), (0.92,1), (0.95,1). Five bins of 2:
conf/acc = 0.21/0, 0.48/0.5, 0.70/0.5, 0.845/0.5, 0.935/1.0. Gaps:
0.21, 0.02, 0.20, 0.345, 0.065. ECE = 0.2 * 0.84 = 0.168.

## E10.2
AUC measures order only. Scores in [0.49, 0.51] can order every pair
correctly while never matching the observed 0/1 rates, so ranking is
perfect and calibration is bad.

## E10.3
Fit the repair map on held-out data only. The test set never tunes the
calibration map.

## E11.1
With s_i = q_i + w * z_i: sample 1 needs 1 + 0.15w to beat sample 4's
w, sample 3's 0.75w, and sample 2's 0.60w. Binding constraint is sample
4: 1 > 0.85w, so w < 1.176. Below about 1.18 the correct sample wins.

## E11.2
Argmax chases the largest score. The maximum of the bias feature over
the set grows with N while quality is capped, so the bias term wins
more often as the candidate set grows.

## E11.3
Correlation between verifier scores and the suspected bias feature on
labeled data, plus a best-of-N rerun with the feature normalized out.

## E12.1
Evaluate floor budgets in steps of 5. At 60: A gives 0.67782, B gives
0.61523, A wins. At 65: A gives 0.68337, B gives 0.68643, B wins. The
crossing lies between 60 and 65, so the nearest 10 is 60. (The executed
lab run confirms: first budget where strong beats cheap is 65.)

## E12.2
The budget cannot afford one full sample at that unit cost. The curve
starts where spending starts.

## E12.3
Labeled runs at each budget point, and enough trials per point that
the success estimate is stable (standard errors reported, not just
point estimates).
