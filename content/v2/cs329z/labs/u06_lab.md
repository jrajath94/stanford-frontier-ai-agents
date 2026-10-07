# U06 lab: benchmark and evaluation infrastructure

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: eval tuple runner

Implement the C01 tuple as a dataclass (R, E, S, F) for the null-bug task. Run a stub agent under S = 10 steps (score 0.70) and S = 20 steps (score 0.78). Report the gap. Implement the canary leak test: write a canary file in task 1's world, reset, verify it is gone in task 2. Then inject a seeded fault schedule (4 of 20 tasks fail the tool): agent A gives up on all 4, agent B recovers on all 4. Report sunny-only scores and fault-slice recovery rates.

## Task 2: grading cascade and judge prompts

(a) Price the C03 cascade on 1000 traces: program $0.001 each on all, model $0.05 each on 200 unclear, human $2 each on a 50-item calibration sample. Report the total. (b) Judge prompts: vague-prompt agreement 0.70, rubric-prompt agreement 0.86 on 100 items. Report the gap in SE units.

## Task 3: pass@k versus pass^k table

Implement the C07 table for p = 0.3 and k in {1, 2, 5, 10}. Report both columns. Verify the two agree at k = 1 and diverge after.

## Task 4: judge bias and seed spread

(a) 100 tied pairs, judge picks the first-presented 62 times. Report the bias, its SE, and the z-score. (b) 5 seeds give scores [0.71, 0.68, 0.73, 0.70, 0.69]. Report the mean and sample std.

## Task 5: regression gate

Implement the C11 z-gate with SE 0.05 on n = 200. Report z for deltas +0.02, +0.12, -0.06 and the gate verdict for each (block below -2, celebrate above 2, rerun otherwise).

## Task 6: Bradley-Terry fit

(a) A beats B 7/10. Report d = log(7/3) and sigma(d). (b) Fit strengths for A beats B 7/10, B beats C 6/10, A beats C 8/10 by gradient ascent (seed 0, centered). Report strengths with B = 0 and the predicted P(A beats C).

## Task 7: tiny suite and alignment

(a) 500 tasks with 3 reference-model score vectors (seed 0). Rank by cross-model variance, keep the top 7. Report the contested share of the selection, the runtime (360 minutes for 500), and whether the tiny ranking matches the full ranking on 5 toy systems. (b) 30 items with human ratings. Metric A and B score vectors (seed 3). Report both Pearson correlations.
