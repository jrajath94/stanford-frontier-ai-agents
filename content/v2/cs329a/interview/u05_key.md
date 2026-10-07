# Interview key U05

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: serial = more repair iterations per trajectory, parallel =
more trajectories per issue. Strong: ties each to its cost axis.
Flags: "more compute is always better". Rubric: 2 per axis, 1 for
the split. Remediation: lesson C01.

## B2
Min: sample K candidates, filter with generated tests, select with
a judge. Costs: generation, test runs, one judge call. Strong:
the cheap-then-expensive order. Flags: judging before filtering.
Rubric: 1 per stage, 2 for costs. Remediation: lesson C02.

## B3
Min: the share of problems both correct and at least p times
faster than the reference. Strong: adds that it is a
conjunction. Flags: "average of correctness and speed". Rubric:
5 for the one sentence. Remediation: lesson C04.

## B4
Min: silent wrongness costs more than slowness, so no speed weight
compensates for a wrong answer. Strong: the deployment-cost
argument. Flags: proposing a weighted sum. Rubric: 3 for the
ordering, 2 for the reason. Remediation: lesson C05.

## B5
Min: any four of: filesystem (data destruction), network
(exfiltration), process/time (resource exhaustion), audit log
(reviewability). Strong: the kernel-enforcement assumption.
Flags: prompt rules as a layer. Rubric: 1 per layer, 1 for
enforcement. Remediation: lesson C10.

## B6
Min: seed, version pins, inputs, environment capture. Strong:
adds the tolerance. Flags: "the code" as the whole receipt.
Rubric: 1 per field, 1 for tolerance. Remediation: lesson C11.

## Ladder 1
D1.1 Min: context (relevant files), generation (candidate edits),
selection (pick the winner). Strong: the cost axis of each.
D1.2 Min: 0.40 + 8 * 3 * 0.05 = $1.60, context share 25 percent.
Strong: shows the arithmetic.
D1.3 Min: context is paid once, trajectories divide it over K
samples, per-sample cost falls. Strong: the fixed-vs-variable
split.
D1.4 Min: context O(1) per issue, generation O(K * S), selection
O(K) test runs plus one judge. Strong: notes test runs dominate.
D1.5 Min: serial wins when one attempt is close, parallel wins
when attempts are cheap and diverse, mixed wins when the budget
allows. Strong: the saturation argument for each.
D1.6 Min: causes: generated tests are weak (pass wrong edits),
visible-hidden leak (tuned to visible). Separating measurement:
hidden-suite score of the chosen edits vs visible score.
D1.7 Min: the same model writes tests and edits, correlated
errors pass together. Strong: the precision-below-0.5 inversion.
D1.8 Min: fixed-test vs co-developed-test repair loops at equal
iteration budget, falsified by equal fix rates. Strong:
preregisters the issue set.
Flags: "more samples always fix selection". Rubric: 2 per rung,
16 total, pass at 11. Remediation: lesson C01-C03.

## Ladder 2
D2.1 Min: correctness (matches reference in tolerance), speedup
(T_ref / T_kernel), fast_p (share correct and >= p faster).
Strong: states the two gates.
D2.2 Min: fast_1 = 0.40, fast_2 = 0.10. Strong: names the
disqualified fast-but-wrong kernels.
D2.3 Min: each single gate is gameable (zeros are fast, the
wrapper is correct), the conjunction is not. Strong: the
economic argument.
D2.4 Min: the scorer code, timing needs repeated runs for
stability. Strong: the hardware-specificity caveat.
D2.5 Min: gate-then-rank wins whenever wrong outputs have real
cost, weighted scoring wins never for production kernels.
Strong: states the never.
D2.6 Min: causes: zeros under absolute tolerance, output buffer
barely written. Separating measurement: fraction of output
elements actually written plus a scale-invariant check.
D2.7 Min: a fixed tolerance is blind to scale, near-zero outputs
pass trivially. Strong: the tolerance-as-assumption point.
D2.8 Min: profile-guided vs unguided edits at fixed iterations,
falsified by equal speedups. Strong: preregisters the problem
set and the hardware.
Flags: quoting benchmark numbers from memory. Rubric: 2 per
rung, 16 total, pass at 11. Remediation: lesson C04, C05, C07.

## A1
Min: per-iteration cost 0.12. Runs: 30*1 + 25*2 + 20*3 + 10*4 +
15*4 = 30 + 50 + 60 + 40 + 60 = 240 iterations. Total: 240 *
0.12 = $28.80. Cap 2: runs = 30*1 + 25*2 + (20+10+15)*2 = 30 +
50 + 90 = 170, cost $20.40. Fixes lost: 20 + 10 = 30.
Strong: notes the never-pass issues still cost the full cap.
Flags: forgetting the never-pass cost. Rubric: cost 3, recompute
2, lost 1, pass at 4. Remediation: lesson C03.

## A2
Min: runs per pass: 90 * 1 + 10 * 3 = 120. False alarms per run
of a quarantined test: 0.10^3 = 0.001. Per 200 passes: 200 * 10
* 0.001 = 2. Quarantine beats nothing because reruns apply only
to the 10 known flakes, so the suite pays 20 extra runs instead
of 200, and false alarms fall from 200 * 10 * 0.10 = 200 to 2.
Strong: shows both arithmetic lines. Flags: applying reruns to
all 100 tests. Rubric: runs 2, alarms 2, argument 2, pass at 4.
Remediation: lesson C08.

## I1
Min: sketch: edit -> run tests -> repair, with logging of (edit
hash, test verdicts, pass-to-fail transitions) each iteration.
Causes: (1) flaky tests fail good code, the loop "repairs" it
into breakage. (2) the repair operator is destructive (edits
more than the trace justifies). Separating measurement:
pass-to-fail transition rate on rerun of the same tests without
any edit: high means (1), low means (2). Fixes: (1) quarantine
plus reruns, (2) minimal-diff repair constrained to the trace.
Strong: adds the edit-distance-per-iteration metric. Flags:
"run more iterations". Rubric: sketch 2, causes 2, measurement
2, fixes 2. Pass at 5. Remediation: lesson C03, C08.

## S1
Min: execution grounding survives (one careful run per edit),
reruns die (too expensive). Replacements: static analysis plus
one golden run, and a risk-ranked single run per edit instead of
iteration. Strong: the expected-value math of a $50 run.
Flags: "just run fewer tests" without changing the loop.
Rubric: 2 per survivor with replacement, pass at 4.
Remediation: lesson C03, C08.

## S2
Min: measure-first survives, hardware-specific tuning dies.
Replacement: portable optimizations (algorithmic, memory-access
patterns) plus a per-target autotune step at deploy time.
Strong: the split between portable and target-specific work.
Flags: tuning for one architecture and hoping. Rubric: survivor
2, replacement 3. Remediation: lesson C07.

## R1
Min: strongest true part: on well-specified tasks with strong
tests, sample-plus-select already beats median human patches.
Weakest assumption: that every task is well-specified with
honest tests (most real work is not). Decisive experiment:
random real-world issues with weak specs, blind comparison of
agent vs senior-engineer patches on hidden tests plus review
acceptance. Strong: adds that selection needs the tests the
claim assumes away. Flags: accepting "every task". Rubric: true
part 2, assumption 2, experiment 3. Pass at 5. Remediation:
lesson C01, C02.
