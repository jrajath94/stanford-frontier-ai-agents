# Interview key U01

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: pass@N = 1 - (1 - p)^N, assumes independent samples and binary
correctness. Strong: adds the complement derivation and the
temperature-0 counterexample. Flags: confusing pass@N with best-of-N
success. Rubric: formula 2, assumptions 2, counterexample 1.
Remediation: lesson C01 items 5 and 11.

## B2
Min: the verifier scores each sample, argmax picks the winner, a
biased verifier picks high-bias samples over correct ones. Strong:
adds that bias harm grows with N (max of the bias feature grows).
Flags: "a better verifier is always better" without the per-instance
caveat. Rubric: role 2, failure 2, N-scaling 1. Remediation: lesson
C02 item 6, C11.

## B3
Min: best-of-N needs a verifier and returns the top-scored sample.
self-consistency needs discrete answers and returns the majority.
Strong: adds the cost comparison (verifier calls vs parsing) and the
exact boundary (verifier exists -> best-of-N, discrete answers and no
verifier -> vote). Flags: claiming one dominates the other.
Rubric: inputs 1, outputs 1, boundary 3. Remediation: lesson C02
item 10, C03 item 10.

## B4
Min: usable gap = pass@N * a - p, with a the verifier accuracy.
Strong: explains both gaps inside it (coverage gap pass@N - p, and the
verifier's discrimination). Flags: defining the gap as p - a.
Rubric: formula 3, interpretation 2. Remediation: lesson C06.

## B5
Min: calibration is the match between stated confidence and observed
accuracy. Strong: adds that best-of-N only needs order (ranking),
while thresholds and abstention need absolute values. Flags:
confusing calibration with accuracy. Rubric: definition 2, ranking-vs-
threshold 3. Remediation: lesson C10 items 3 and 10.

## B6
Min: x is budget, y is success, a crossing is the budget where the
recommended plan changes. Strong: adds that curves come from
plan_success at floor(N) and smooth interpolation is a drawing aid.
Flags: reading the highest point on the menu instead of the highest
affordable point. Rubric: axes 2, crossing 2, construction caveat 1.
Remediation: lesson C12.

## Ladder 1
D1.1 Min: N samples, verifier scores, argmax, one completion out.
Strong: states the tie rule and the scoring-cost assumption.
D1.2 Min: picks sample 2, wrong. Strong: notes the oracle ceiling
would succeed (samples 1 and 4 correct).
D1.3 Min: P(pick correct) = P(coverage) * P(verifier right), assumes
verifier errors are independent of coverage. Strong: flags the
correlation failure.
D1.4 Min: the loop from lesson C02, O(N) time, O(1) streaming memory.
Strong: notes verifier latency on the critical path.
D1.5 Min: weak verifier wins when a > 0.5 on the pile, vote wins with
discrete answers and no scorer. Strong: adds the cost axis.
D1.6 Min: causes: verifier degrades on harder samples, selection bias
grows with N. Measurement: score-vs-length correlation and per-N
verifier accuracy. Strong: designs the ablation (fixed samples, swap
verifiers).
D1.7 Min: the single-number accuracy fails first, real accuracy varies
with difficulty. Strong: adds error-correlation between generator and
verifier.
D1.8 Min: fix samples, sweep verifier strength, fix verifier, sweep N.
compare gains per dollar. Strong: adds the matched-budget control and
the falsification reading.
Flags: skipping the tie rule, treating a as a constant of nature.
Rubric: 2 points per rung, 16 total, pass at 11.
Remediation: lesson C02, C06, C11.

## Ladder 2
D2.1 Min: ECE = sum over bins of weight * |acc - conf|. Strong: states
the perfect-calibration condition P(correct | s) = s.
D2.2 Min: 0.134 from the lesson toy. Strong: shows the bin table.
D2.3 Min: monotone maps preserve order, so ranking (AUC) is fixed.
absolute scores move, so ECE changes. Strong: notes this is why
calibration repair is post-hoc and safe.
D2.4 Min: the ece() code, tens of samples per bin. Strong: explains
the bias-variance tradeoff in bin count.
D2.5 Min: AUC for best-of-N ranking, ECE for thresholds. Strong: the
[0.49, 0.51] counterexample (perfect rank, terrible calibration).
D2.6 Min: distribution shift, threshold set on the wrong operating
point. Strong: separates score shift from label shift.
D2.7 Min: labels are correct. Strong: label noise caps measurable
calibration.
D2.8 Min: track AUC and ECE on a schedule, rank decay moves AUC,
calibration decay moves ECE alone. Strong: adds the alert thresholds.
Flags: "low ECE means good selection". Rubric: 2 per rung, 16 total.
pass at 11. Remediation: lesson C10.

## A1
Min: first difference p(1-p)^(N-1) > 0 (increasing) and falling in N
(concave). For p = 0.2: 0.8^N <= 0.01 -> N >= ln(0.01)/ln(0.8) =
20.64 -> N = 21. Strong: verifies 0.8^20 = 0.01153 > 0.01 and 0.8^21
= 0.00922 < 0.01. Flags: off-by-one (answering 20). Rubric: proof 3,
computation 2. Remediation: lesson C01 items 5-6.

## A2
Min: true = 0.7 * mix term + 0.3 * mix term computed per difficulty:
easy pass@8 = 1 - 0.7^8 = 0.94235 * 0.7 = 0.65965, hard: same pass@8
* 0.55 = 0.51829. Mix: 0.7*0.65965 + 0.3*0.51829 = 0.46176 + 0.15549
= 0.61724. Single-number toy with a = 0.655 (the mix accuracy):
0.94235 * 0.655 = 0.61724. Equal here because p is shared, the gap
opens when p also varies with difficulty. Strong: states that
condition. Flags: averaging accuracies without weighting by traffic.
Rubric: per-difficulty 3, comparison 2. Remediation: lesson C05
item 11.

## I1
Min: (1) score-vs-length correlation on recent traffic, (2) verifier
accuracy on a labeled probe set, old vs new, (3) fixed-sample A/B:
score the same samples with both verifiers. Verifier implicated by
(2) dropping or (3) flipping picks, pipeline implicated if (1) and (2)
are flat but serving latency changed. Strong: cheapest is (3) on
logged samples, no new labels needed, sketch: load logged
(prompt, samples), score with both, compare argmax agreement and
flip direction. Flags: retraining the verifier before measuring.
Rubric: measurements 3, implication logic 3, code sketch 2, pass at 5.
Remediation: lesson C11, U02 C12.

## S1
Min: per-sample cost was 4 + 1 = 5 (cheap) vs 4 + 8.5 = 12.5
(strong), now verifier costs 40 and 85: unit costs 44 and 89. At
budget 100: cheap N = 2, strong N = 1. Cheap: pass@2 = 0.4375 * 0.7 =
0.30625. Strong: 0.25 * 0.9 = 0.225. Cheap wins now. Strong: notes the
general rule (expensive scoring favors fewer, cheaper-scored
samples). Flags: keeping N fixed while costs change. Rubric: re-
derivation 3, winner 1, rule 1. Remediation: lesson C05.

## S2
Min: best-of-N dies (no verifier), self-consistency dies (no discrete
answers). Survivors: repeated sampling with human pick, LLM-as-judge
with a rubric (needs the judge to be trusted), inference architecture
search over the survivors (needs a validation signal). Strong: names
the new assumption each survivor needs. Flags: proposing majority
vote on free text without a normalization rule. Rubric: 2 per
survivor, 1 per assumption, pass at 4. Remediation: lesson C04.

## R1
Min: strongest true part: weak verifiers do lift best-of-N over
single samples cheaply. Weakest assumption: that inference budgets
scale like training budgets in cost and latency. Decisive experiment:
matched-dollar comparison of (bigger model, 1 sample) vs (smaller
model, best-of-N) on latency-constrained serving. Strong: adds that
the claim confuses a real gap-shrink with a full substitute, cites
the verifier-accuracy ceiling (success <= a). Flags: accepting the
replacement claim without a cost model. Rubric: true part 2,
assumption 2, experiment 3, pass at 5. Remediation: lesson C05, C06.
