# Interview key U08

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: success rate vs task duration in hours. It measures how the
agent degrades with horizon. Strong: adds the compound-failure
note. Flags: "it measures speed". Rubric: 5. Remediation:
lesson C01.

## B2
Min: value = hours times hourly rate. 3 * 120 = $360. Strong:
adds the substitution assumption. Flags: confusing value
with duration. Rubric: definition 2, computation 3.
Remediation: lesson C02.

## B3
Min: Knowledge Synthesis (Nugget Coverage), Retrieval Quality
(Reference Coverage), Verifiability (Citation Precision).
Strong: adds all seven metrics. Flags: "ROUGE". Rubric: 2
per dimension. Remediation: lesson C04.

## B4
Min: the mean picks one agent, the minimum picks the other.
Strong: adds the spiky-vs-flat reading. Flags: "the mean is
always right". Rubric: 5 for the one sentence.
Remediation: lesson C05.

## B5
Min: continue while the next step's expected value beats its
cost. Strong: adds the diminishing-gains note. Flags:
"run to the budget". Rubric: 5 for the one sentence.
Remediation: lesson C06.

## B6
Min: same-model agreement minus independent-model agreement.
the part of the score that is similarity, not quality.
Strong: adds the shared-bias mechanism. Flags: "judges are
neutral". Rubric: 3 for the definition, 2 for the reading.
Remediation: lesson C07.

## Ladder 1
D1.1 Min: x duration in hours, y success rate, decreasing.
Strong: the per-step compounding note.
D1.2 Min: drop 0.55. Per doubling past 1 h about 0.15-0.20.
Strong: shows the arithmetic.
D1.3 Min: q^n with n growing in duration. Strong: the
non-extrapolation point.
D1.4 Min: the grouping code. Cost is agent compute per task
times tasks per point. Strong: the CI note.
D1.5 Min: single number wins never for agents. Step count
wins when steps are countable. Duration wins when wall time
is the cost. Strong: states the never.
D1.6 Min: causes: the 8 h tasks are easier (mixed kinds),
the agent was tuned on long tasks. Separating measurement:
per-step success vs duration: flat per-step means tuning,
falling means compounding stopped.
D1.7 Min: binary success hides partial credit and quality
differences. Strong: the shipping counter (binary is fine
for the min).
D1.8 Min: matched task kinds across horizons, falsified by
a non-exponential fit. Strong: preregisters the step count.
Flags: inventing benchmark numbers. Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C01.

## Ladder 2
D2.1 Min: value = h * r. Fuels: agent compute, judge cost,
human audit. Strong: the binding-constraint preview.
D2.2 Min: agent $400, judge $100, audit $600, total $1,100,
binding audit. Strong: shows the shares.
D2.3 Min: the binding fuel is the largest share, so it caps
how often you can re-run. Strong: the cut-the-binding-fuel
rule.
D2.4 Min: the budget code. Lock-in cost is the unit prices
before the eval. Strong: the drift note.
D2.5 Min: no budget wins never. Agent-only wins never (the
judge bill surprises). Three-fuel wins always. Strong:
states both nevers.
D2.6 Min: causes: the judge is human not model, the judge
prompt is long (context cost). Separating measurement: cost
per judged task vs the estimate sheet.
D2.7 Min: too small misses rare failures, too big wastes the
budget. Strong: ties the sample to the incident rate.
D2.8 Min: survey of published eval budgets, falsified by
agent compute binding most often. Strong: preregisters the
sample frame.
Flags: "budgets are mere accounting". Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C08.

## A1
Min: A mean (0.62+0.88+0.70)/3 = 0.7333, min 0.62. B mean
(0.73+0.75+0.74)/3 = 0.74, min 0.73. Mean picks B (by
0.0067). Min picks B (by 0.11). The min ships: B's worst
task (0.73) beats A's worst (0.62) by a mile, and failures
cost. Strong: notes the mean race is noise (0.0067).
Flags: shipping on the mean. Rubric: numbers 3, winners 1,
argument 2, pass at 4. Remediation: lesson C05.

## A2
Min: agent 500*1.20 = $600, judge 500*0.30 = $150, audit
25*40 = $1,000. Total $1,750. Binding: audit (57%). Halving
the audit: 12.5 -> 12 or 13 audits. At 12, saves $520. The
cut is unsafe if rare failures matter. The audit CI widens
and the binding fuel is the truth-check. Safe only with a
power argument that 12 audits still catch the failure rate
you care about. Strong: does the 12-vs-13 rounding.
Flags: "cut the judge instead". Rubric: total 2, binding 1,
savings 2, argument 2, pass at 5. Remediation: lesson C08.

## I1
Min: sketch: same tasks, three judges (same-model, different-
lab model, human sample). Metric is the agreement gap per
pair. Causes: (1) shared-bias contamination (the judge
rewards its own style). (2) the human audit sample is hard
(the spot check picked hard tasks). Separating measurement:
gap on matched easy tasks: persists means (1), vanishes
means (2). Fixes: (1) switch the official judge to the
different-lab model plus human audit, report the gap.
(2) stratify the audit sample to match the task mix.
Strong: adds the matched-tasks control. Flags: "drop the
eval". Rubric: sketch 2, causes 2, measurement 2, fixes 2.
Pass at 5. Remediation: lesson C07.

## S1
Min: survives: the task set, the duration curve, the budget
sheet (two fuels now). Dies: paid judging, human audit.
Replacement: a verifier where one exists (U07 C02:
contamination zero by construction), else a different-lab
open model as judge with the contamination gap reported, or
self-consistency checks. Strong: the verifier-first rule.
Flags: "the generator judges itself". Rubric: survivor 2,
death 1, replacement 3. Remediation: lesson C07, C08.

## S2
Min: survives: the curve's shape idea. Dies: 4 clean points
(10 tasks give one noisy 24 h point). Changes: report the
single 24 h point with a wide CI, add intermediate
checkpoints (success at 6 h, 12 h within the 24 h runs) to
recover the curve, and lean on the 1-8 h points from cheaper
runs. Strong: the checkpoint trick. Flags: "10 tasks is
enough". Rubric: survivor 2, changes 3. Remediation: lesson
C01.

## R1
Min: strongest true part: the mean is the right research
target (average progress). Weakest assumption: that the
deployment sees the average (it sees the tail. One bad type
is the incident). Decisive experiment: ship both agents and
compare incident rates: if the higher-mean agent has more
incidents, the min was the right number. Strong: adds the
research-vs-shipping split. Flags: accepting "summarizes
everything". Rubric: true part 2, assumption 2, experiment
3. Pass at 5. Remediation: lesson C05.
