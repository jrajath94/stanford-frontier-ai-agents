# Interview key U04

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: a design is (prompt template, tool set, control flow, budget).
fitness is the validation success rate. Strong: adds the
enumerable-or-samplable requirement. Flags: "fitness is the loss".
Rubric: design 3, fitness 2. Remediation: lesson C01.

## B2
Min: a small stochastic edit of one design, locality says small edits
usually cause small fitness changes. Strong: the orphan problem (many
edits at once hide attribution). Flags: "mutation is random search".
Rubric: definition 2, locality 3. Remediation: lesson C02.

## B3
Min: truncation (top-k, strongest pressure), tournament (playoffs,
medium), proportionate (weighted lottery, weakest). Strong: ties
pressure to convergence speed vs diversity. Flags: "stronger is
always better". Rubric: 1 per rule, 2 for pressure. Remediation:
lesson C03.

## B4
Min: the holdout is locked before evolution starts and is reported
once, nothing selected or tuned on it. Strong: adds the reuse
failure (second use turns it into validation). Flags: long
explanations that miss "locked". Rubric: 5 for the one sentence.
Remediation: lesson C09.

## B5
Min: sample, filter (example tests), cluster by behavior, pick one
per large cluster. Strong: the diversity justification for
clustering. Flags: skipping the cluster step. Rubric: 1 per stage,
1 for the why. Remediation: lesson C06.

## B6
Min: any three of: no network, writes inside /task, read-only
outside, log everything, wall-clock kill, human approval for new
tools. Strong: states the enforcement assumption (kernel, not
prompt). Flags: rules that live in the prompt. Rubric: 1 per rule,
2 for enforcement. Remediation: lesson C12.

## Ladder 1
D1.1 Min: population (candidate set), fitness (scalar score),
mutation (stochastic edit), selection (who survives). Strong: gives
the shapes (M, f(c), m(c), top-k).
D1.2 Min: mean 0.6167 -> 0.7067, differential +0.09. Strong: shows
the arithmetic.
D1.3 Min: E[max] > max of means, the winner is the luckiest draw as
well as the best. Strong: the 2.25 * se estimate for n = 50.
D1.4 Min: truncation is O(M log M), the optimism estimate is O(1).
the real cost is fitness evaluation. Strong: notes the sort is not
the bottleneck.
D1.5 Min: truncation wins with reliable fitness and need for speed.
tournament wins with noisy fitness. Strong: the lucky-candidate
example.
D1.6 Min: causes: validation overfitting (selection optimism).
fitness noise. Separating measurement: the predicted-vs-observed gap
(optimism estimate vs actual holdout gap). Strong: adds a second
validation split as the check.
D1.7 Min: truncation trusts the measured ranking, a lucky candidate
(true 0.55, measured 0.73) gets kept and its children inherit
nothing. Strong: premature convergence as the second failure.
D1.8 Min: run evolution, record validation max and holdout each
generation, compare gaps with 2.25 * se, falsified by systematic
mismatch. Strong: preregisters the se estimator.
Flags: reporting validation as the result. Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C01-C03, C09.

## Ladder 2
D2.1 Min: the reasoner emits SEARCH(query), the retriever returns
(snippet, source), the reasoner continues with both in context.
Strong: adds the stop rule.
D2.2 Min: 20 * 0.8 * 0.9 = 14.4, about 14 (0.70). Strong: names the
two factors.
D2.3 Min: expected = P(retrieve right) * P(reason right | fact).
retrieval usually binds (0.8 < 0.9). Strong: notes the compounding
(the product, not the sum).
D2.4 Min: the loop code with (fact, text, source) appended, one
retrieval latency per unknown fact plus context growth. Strong: the
poisoned-snippet risk.
D2.5 Min: upfront RAG wins when needed facts are known before
reasoning, search-enhanced wins when reasoning discovers needs as it
goes. Strong: the dependency test design.
D2.6 Min: bad retriever (wrong facts), reasoner ignores facts (prior
override). Separating measurement: fact-use rate (does the trace cite
the snippet?) vs snippet accuracy. Strong: the lookalike-entity
example.
D2.7 Min: a wrong snippet poisons every later step, errors compound
down the trace. Strong: retrieval precision matters more than recall
here.
D2.8 Min: 50 claims, each needs (claim, source_id, retrieval_path,
date), verdict: pass rate on replayed checks, flag below threshold.
Strong: the fabricated-record counterexample.
Flags: "more retrieval is always better". Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C07, C08.

## A1
Min: money 600.0, time 1.67h, review 2.5h, money binds vs $400.
M = 30: money 360.0, time 1.0h, review 2.5h, money no longer binds
and review time is now the largest cost. Strong: notes the review
cost is unchanged (k fixed) and states the new tradeoff explicitly.
Flags: forgetting review in the recompute. Rubric: sheet 3, binding
1, recompute 2, pass at 4. Remediation: lesson C10.

## A2
Min: 25 -> 15 -> 10.5 -> about 9.45, so 9 or 10 survivors. The funnel
runs literature first because it is cheapest (a search), then
baselines (compute), then ablations (more compute), cheap filters run
first. Strong: adds that the order is also the falsification order.
Flags: multiplying kill rates against the original 25 at each stage.
Rubric: computation 3, order argument 2, pass at 3. Remediation:
lesson C11.

## I1
Min: sketch: propose (mutate) -> evaluate -> select, with logging of
(design signature, parent, fitness) each generation. Causes: (1)
premature convergence (selection too strong, one family takes over).
(2) mutation too weak (edits cannot reach other families).
Separating measurement: pairwise design distance over generations:
falling distance with flat fitness means (1), steady distance with
flat fitness means (2). Fixes: (1) weaken selection / add diversity
bonus, (2) widen the mutation distribution / add crossover. Strong:
adds the entropy-of-signatures metric. Flags: "run more
generations". Rubric: sketch 2, causes 2, measurement 2, fixes 2.
pass at 5. Remediation: lesson C02, C03.

## S1
Min: population search dies (too many destructive evals). Survivors:
single-candidate hill-climbing with tiny batches, Bayesian
optimization with a surrogate (needs a good prior over the design
space), offline evaluation on logged data (needs the log to cover the
space). Strong: the explore/exploit math under a hard eval budget.
Flags: "just use fewer designs" without changing the loop.
Rubric: 2 per survivor with replacement, pass at 4. Remediation:
lesson C01, C10.

## S2
Min: the (claim, source) link survives, the URL retrieval path does
not. Replacement: document IDs plus page/section pointers plus a
content hash, so the checker replays from the offline corpus.
Strong: the hash as the tamper check. Flags: dropping provenance
because "there are no links". Rubric: survivor 2, replacement 3.
Remediation: lesson C08.

## R1
Min: strongest true part: evolution already improves code and agent
designs on measurable tasks. Weakest assumption: that research taste
(choosing what to try) is automatable the same way. Decisive
experiment: blind comparison of machine-proposed vs human-proposed
research directions on novelty and impact rubrics, judged by outside
experts. Strong: adds that review-only humans still set the fitness,
so "automated" hides the human in the loop. Flags: accepting
timeline claims. Rubric: true part 2, assumption 2, experiment 3.
pass at 5. Remediation: lesson C04, C11.
