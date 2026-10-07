# Answer key U08 , Long-horizon evaluation and research projects

## C01

E1.1: the absolute drop from 0.25 h to 8 h is 0.90 - 0.35 =
0.55.
E1.2: compounding: each step can fail, so task success is
about q^n. Longer tasks have more steps, so success falls
even when per-step quality is constant.
E1.3: mixed-kind failure: the 8 h tasks are a different kind
(research) from the 15 min tasks (QA), so the curve mixes
kinds, not horizons.

## C02

E2.1: values: A $300, B $640, C $200. Ranking: B, A, C. The
A+C agent captures (300+200)/(300+640+200) = 500/1140 =
0.4386, about 0.44, while winning 2 of 3 tasks by count.
E2.2: value weighting: score the agent where the money is
(time saved times hourly rate), because an unweighted count
treats a 5-minute puzzle like an 8-hour analysis.
E2.3: review-cost failure: the agent's output needs hours of
expert review, so the "saved" hours are fiction.

## C03

E3.1: win rate: 660/1320 = 0.50. Gold SE:
sqrt(0.5*0.5/220) = sqrt(0.001136) = 0.0337, about 0.034.
E3.2: blinding: the judge does not know which deliverable is
the machine's, so the score measures the work, not the
source.
E3.3: unblinding failure: the judge spots machine tells and
grades the source, not the work.

## C04

E4.1: synthesis: (0.80+0.35)/2 = 0.575. Retrieval:
(0.60+0.25+0.10)/3 = 0.95/3 = 0.3167. Verifiability:
(0.70+0.55)/2 = 0.625.
E4.2: the nugget method: experts list the vital facts, the
grader checks what fraction the review covers. It makes
synthesis measurable instead of vibes.
E4.3: exemplar failure: the expert's vital facts are one
school's view, so nugget coverage measures conformity, not
quality.

## C05

E5.1: A: mean (0.90+0.55+0.85)/3 = 0.7667, min 0.55. B: mean
(0.72+0.74+0.70)/3 = 0.72, min 0.70. Mean picks A (wins by
0.047). Min picks B (wins by 0.15). The flip: A is spiky, B
is flat.
E5.2: tail argument: deployments fail at the minimum, not
the mean. The mean is for research progress, the minimum is
for shipping, because one bad task type is the incident.
E5.3: out-of-scope failure: the min task is one the agent
was never meant to do, so the minimum punishes honesty.

## C06

E6.1: marginal values: $200, $120, $60, $20 against $50
cost. Stop after h3. Nets: h2: $220, h3: $230, h4: $200.
The rule earns $30 more than running to h4.
E6.2: the stopping rule: continue while the next step's
expected value beats its cost. Gains shrink and costs do
not, so the crossing point is the answer.
E6.3: breakthrough failure: a big gain at h5 after small
ones. The rule stops before it.

## C07

E7.1: gap: 0.85 - 0.60 = 0.25. Reading: up to 25 points of
the 85 are judge-generator similarity. The honest score is
closer to 0.60.
E7.2: shared bias: the generator and the same-model judge
share training, so their errors correlate. Correlated errors
look like agreement.
E7.3: bad-far-judge failure: the far judge is incompetent,
and the gap measures the far judge's errors instead of
contamination.

## C08

E8.1: agent $400, judge $100, audit $600. Total $1,100.
Shares: 36%, 9%, 55%. Binding fuel: audit.
E8.2: the binding constraint: the fuel with the largest
share sets the re-run frequency. Cutting it changes the
design, cutting the others saves little.
E8.3: exploding-judge failure: the judge turns out to be
human at 10x the estimated cost, and the budget explodes.

## C09

E9.1: memory delta: 0.72-0.58 = 0.14. Search delta:
0.72-0.65 = 0.07. Joint delta: 0.72-0.50 = 0.22. Sum of
singles: 0.21 vs joint 0.22: interaction +0.01, near-
additive. Verdict: memory pulls twice the weight of search.
E9.2: controlled removal: the only difference between the
two runs is the component, so the delta is causal, not
correlational.
E9.3: broken-format failure: removing memory breaks the
prompt format, and the delta measures the breakage, not the
memory.

## C10

E10.1: gates: proposal (question, hypothesis, falsification),
midterm (baseline, first ablation), poster (results,
negatives, limitations). One exit criterion each: the
proposal needs the falsification written. The midterm needs
the baseline measured. The poster needs the negatives on
the poster.
E10.2: staged commitment: the value of information is highest
early, when killing is cheapest. Gates concentrate the hard
questions at the cheapest point.
E10.3: theater failure: every project passes every gate
because the kill rule never fires.

## C11

E11.1: predicted growth 0.15, measured growth -0.01 with CI
[-0.04, +0.02]. The prediction lies far outside the CI:
verdict rejected. The CI is tight enough that a real 0.08
growth would have shown, so the null is informative.
E11.2: preregistration: the falsification is written before
the run, so the measurement decides, not the author's hopes.
E11.3: underpowered failure: CI [-0.10, +0.10]. The null
result is uninformative, not negative.

## C12

E12.1: (1) 8 h reliability: 0.70 at 8 h on the duration
curve. (2) clean judging: gap under 0.05 at $0.10/task.
(3) compounding memory: delta grows with horizon. (4) prose
verifiers: a kernel for claims. (5) open envelope: zero
violations for a quarter.
E12.2: gap analysis: each unit ended with an extension and a
falsification. The open questions are the extensions nobody
falsified to date.
E12.3: metric-less failure: a question with no progress
metric is a wish, not a question.
