# Interview key U02

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: thought, action, observation, in that order, thought plans,
action calls a tool, observation is the tool result. Strong: adds
that the next thought reads the observation. Flags: swapping action
and observation. Rubric: order 2, contents 3. Remediation: lesson
C01.

## B2
Min: execution feedback is computed by running the artifact, model
feedback is generated text. Strong: the causal link (change the code,
rerun, watch it change) is what makes repair possible. Flags:
"model feedback is always worse". Rubric: definition 2, causal link
3. Remediation: lesson C02.

## B3
Min: a critique judges output without changing weights, an update
changes weights. Strong: the trace/policy split (critique affects
this trace, update affects all future traces). Flags: expecting a
critique to fix the next task. Rubric: definition 3, split 2.
Remediation: lesson C05.

## B4
Min: write principles, model critiques its draft against them.
model revises, train on revisions. Strong: adds the drop rule for
twice-violating drafts and the human-review escape. Flags: skipping
the revision quality check. Rubric: 1 per step, 1 for the drop rule.
Remediation: lesson C06.

## B5
Min: test-pass rate (fails on gaming), keyword match (fails on
proxy), human vote (fails on cost/scale). Strong: adds when each is
the right choice. Flags: naming only one failure mode for all three.
Rubric: 1 per signal, 1 per failure, 1 for selection. Remediation:
lesson C07.

## B6
Min: a check with its own data, rules, and operator, separate from
the system it judges. Strong: the separation must be real (no shared
tuning/data/failure mode), else the validator is decor. Flags:
"more tests" without the independence argument. Rubric: definition
2, independence 3. Remediation: lesson C12.

## Ladder 1
D1.1 Min: (thought, action, observation) triples, max-steps or finish
stop, the trace is the list. Strong: states why the stop rule is
load-bearing.
D1.2 Min: the two-step trace from the lesson, answer 14. Strong:
checks the arithmetic.
D1.3 Min: observations carry new information that the plan could not
have, the loop lets the next thought use it. Strong: names the
condition (observations change the plan).
D1.4 Min: the loop code, one model call plus tool latency per step.
Strong: notes trace memory growth.
D1.5 Min: act-only for tiny action spaces, plan-then-execute for
known plans and reliable tools, ReAct when observations steer.
Strong: adds the cost axis.
D1.6 Min: missing retry budget / error classification, fixes: classify
then recover per class, cap retries. Strong: cites the retry-storm
mechanism.
D1.7 Min: a lying tool poisons the trace silently, no thought step
can detect it. Strong: the calculator-rounding-bug example.
D1.8 Min: task family with informative observations, matched model
calls, success plus cost metrics. Strong: adds the falsification
reading (equal scores mean thoughts add no value).
Flags: omitting the stop rule. Rubric: 2 per rung, 16 total, pass at
11. Remediation: lesson C01, C09.

## Ladder 2
D2.1 Min: a scalar training signal, Goodhart: optimization amplifies
whatever raises the reward, including proxies. Strong: the fence/
field image with the mechanism.
D2.2 Min: R1 = tests passed (trick scores 1.0), R2 = keyword
(trick scores 1.0), R3 = human (trick scores 0). Strong: explains why
R1 fails (suite too thin).
D2.3 Min: argmax over the proxy picks the max-proxy candidate, the
trick maximizes the proxy by construction. Strong: the 0.4-pick-
probability toy.
D2.4 Min: gap = visible - hidden > threshold, needs a locked hidden
suite. Strong: states the lock requirement.
D2.5 Min: fix the proxy when the flaw is known, hidden tests when the
flaw is unknown but guessable. Strong: adds the arms-race dynamic.
D2.6 Min: the policy games both suites, the threshold is too loose.
Strong: the memorized-both-suites counterexample.
D2.7 Min: the hidden suite must stay hidden and representative, leaks
and staleness break it. Strong: the rubber-stamp reviewer analogue.
D2.8 Min: rotate hidden tests each round, falsified if gaming speed is
unchanged vs a fixed suite. Strong: adds the cost accounting.
Flags: "the detector proves honesty". Rubric: 2 per rung, 16 total.
pass at 11. Remediation: lesson C07, C11, C12.

## A1
Min: timeouts 3*0.7 = 2.1, bad args 2*0.9 = 1.8, auth 0, server errors
2*0.7 = 1.4, malformed 0, empty 2, clean 9. Total 16.4. Strong: notes
these are expectations, not guarantees, and the quarantined/escalated
calls need a second round. Flags: counting escalated calls as usable.
Rubric: per-class 1 (7 total), total 1. Remediation: lesson C09.

## A2
Min: yield = 150 + 40 = 190 (95%). New: flagged 100, revised 20,
yield = 100 + 20 = 120 (60%). The fixed review budget prefers regime
1: 10 dropped drafts to review vs 80, and higher yield per draft.
Strong: notes the review budget binds on dropped count, not flag
count. Flags: preferring regime 2 for "more signal". Rubric:
computations 3, preference 2. Remediation: lesson C06.

## I1
Min: sketch: run tests -> if pass return, else propose fix from
failure -> repeat. Causes: (1) the two tests encode conflicting
requirements (or one test is wrong), (2) the fix operator is too
coarse (rewrites too much). Cheapest measurement: run each test
alone against each historical version to build the pass/fail matrix.
it shows whether any single version passes both. Fixes: (1) repair
or drop the wrong test, (2) shrink the edit scope / add regression
tests to the prompt. Strong: adds the stop rule (max rounds) to the
sketch. Flags: "run more rounds". Rubric: sketch 2, causes 2,
measurement 2, fixes 2, pass at 5. Remediation: lesson C02, C03.

## S1
Min: blind retry dies (side effects), retry-with-backoff dies.
Survivors: repair-once for request bugs (no side effect yet).
escalate for auth, quarantine for tool bugs. Replacement: check-
then-act (read state before acting), idempotency keys, and
human approval for the first execution of each action class. Strong:
adds the exactly-once vs at-least-once framing. Flags: keeping retry
for timeouts. Rubric: 2 per survivor/death, 2 for replacements, pass
at 5. Remediation: lesson C09, P20.

## S2
Min: hidden tests die (no secrecy). Survivors: behavioral checks the
policy cannot easily game (e.g., performance profiles, not just
correctness), human spot-check on a random sample (needs calibrated
judges), self-consistency across independent generations (needs
diverse errors). Strong: names each new assumption explicitly.
Flags: "use more visible tests". Rubric: 2 per survivor with
assumption, pass at 4. Remediation: lesson C12.

## R1
Min: strongest true part: execution feedback is computed from runs,
so it cannot flatter like a learned judge. Weakest assumption: tests
equal the goal (they rarely do). Decisive experiment: train RLEF on
a task family, then evaluate with fresh human judgment on held-out
tasks, a gap between test reward and human judgment kills the
claim. Strong: adds that the claim confuses grounding with
completeness. Flags: accepting "no human data" without asking who
wrote the tests. Rubric: true part 2, assumption 2, experiment 3.
pass at 5. Remediation: lesson C04, C07, C12.
