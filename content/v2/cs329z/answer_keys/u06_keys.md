# U06 answer keys

Kept separate from `lessons/u06_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: R = "fix the null-pointer bug in checkout.py". E = container with the repo at commit abc123. S = 10 steps or tests pass. F = fraction of 12 tests passing.
- E2: the same agent scores 0.70 under S = 10 and 0.78 under S = 20. The 0.08 is the stopping rule, not the agent.
- E3: no tuple, no benchmark. A task without E, S, F is a demo, not a measurement.

## C02

- E1: 0.74 - 0.61 = 0.13.
- E2: the mock auto-passes permission tasks. The 8 permission tasks explain the gap. The other 42 match within 0.02.
- E3: the scaffolding is part of the measurement. A mock measures the agent against the mock.

## C03

- E1: 1000 x 0.001 + 200 x 0.05 + 50 x 2 = 1 + 10 + 100 = $111.
- E2: the program grader trusts test passage, and the agent deletes the failing tests. The cascade trusts a gamed signal.
- E3: program first, model for the unclear, humans on a calibration sample.

## C04

- E1: 0.16/0.0574 = 2.78 SE.
- E2: malformed verdicts must be rejected, not silently kept. A kept malformed verdict is a missing grade.
- E3: criteria, level anchors, examples, fixed output format.

## C05

- E1: log(0.7/0.3) = log(2.333) = 0.847.
- E2: one strength per system cannot fit a cycle. A beats B beats C beats A needs matchup-specific terms.
- E3: at least 30 pairs per matchup. Ten pairs give a wide interval.

## C06

- E1: 0.12/0.05 = 2.4 SE. Real bias.
- E2: the pairs are not tied. The first answer is genuinely better 62 percent of the time. The "bias" is accuracy.
- E3: present every pair in both orders and average. Report seeds.

## C07

- E1: 1 - 0.7^5 = 0.83193. 0.3^5 = 0.00243.
- E2: low temperature makes the 5 samples near-identical. True coverage is near 0.3, the formula claims 0.83.
- E3: pass@k asks "at least one of k". pass^k asks "all k".

## C08

- E1: 0.70 - 0.40 = 0.30.
- E2: the container reuses a warm layer with a polluted cache. The canary checks /tmp but the cache leaks.
- E3: each task runs in a fresh world: fresh container, no shared mounts, reset between tasks.

## C09

- E1: sunny-only 0.80 vs 0.80, a tie. Fault-slice recovery 0.00 vs 1.00. The tie hides the robustness gap.
- E2: every call fails, so the agent learns to never call tools. Faults must resemble production.
- E3: at least 20 fault tasks for a stable robustness number. Four give a wide interval.

## C10

- E1: 360/500 = 0.72 min/task. 7 tasks = 5.0 minutes.
- E2: the 3 reference models share a blind spot, and the tiny suite drops the tasks that would expose it.
- E3: refresh the selection when models change. A stale tiny suite flatters everyone.

## C11

- E1: 0.02/0.05 = 0.4. Noise.
- E2: the suite refreshed between versions, so the delta measures the refresh, not the model.
- E3: block below -2, celebrate above 2, rerun otherwise.

## C12

- E1: r = 0.86 licenses treating the metric as a proxy for human-judged quality.
- E2: the metric cannot beat the raters' own agreement. Rater r = 0.40 caps the measurable alignment.
- E3: re-measure quarterly. Alignment decays as the task drifts.
