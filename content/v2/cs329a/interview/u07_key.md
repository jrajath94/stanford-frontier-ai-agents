# Interview key U07

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: 15 Denny Zhou LLM Reasoning, 16 Thang Luong AlphaProof/
AlphaGeometry, 18 Misha Laskin autonomy, 19 Danny Driess
robotics. Evidence: schedule-line only for all four. Strong:
adds the dates. Flags: describing talk content. Rubric: 1 per
session, 1 for the level. Remediation: lesson C01.

## B2
Min: goal (what remains to prove), tactic (a proof step),
kernel (the checker that accepts or rejects). Strong: adds
that the kernel is the free verifier. Flags: "the tactic is
the proof". Rubric: 1 per term, 2 for the kernel. Remediation:
lesson C02.

## B3
Min: the neural net proposes constructions, the symbolic engine
closes the proof by deduction. Strong: adds why the split
works (ideas are the bottleneck, checking is cheap). Flags:
"the net proves". Rubric: 5 for the one sentence.
Remediation: lesson C03.

## B4
Min: a conjecture is a guess, search tries guesses, a proof
is the verifier-accepted artifact. Strong: the reporting rule
(proof size and search cost are different numbers). Flags:
calling the search tree a proof. Rubric: 2 per distinction,
1 for the rule. Remediation: lesson C04.

## B5
Min: authority must not exceed verified capability, with margin.
Strong: adds the two failure modes (danger, waste). Flags:
"more autonomy is always better". Rubric: 5 for the one
sentence. Remediation: lesson C06.

## B6
Min: change the fact the trace cites and hold the rest. Faithful
iff the behavior changes. Strong: adds the sampling note.
Flags: "plausible traces are valid". Rubric: 3 for the test,
2 for the verdict. Remediation: lesson C11.

## Ladder 1
D1.1 Min: state (goal stack), action (tactic), reward (1 iff
the kernel accepts). Strong: the sparse-reward note.
D1.2 Min: random (1/12)^4 = 1/20736 about 0.00005, guided
(1/3)^4 = 1/81 about 0.012. Strong: the 250x ratio.
D1.3 Min: every node is labeled right/wrong for free, so
scoring and stopping are solved. Strong: the credit-
assignment point.
D1.4 Min: the search code, node cost is one kernel check.
Strong: notes training is the real cost.
D1.5 Min: neural-guided wins for hard goals, uniform wins as
the baseline, pure symbolic wins when the space is small.
Strong: the baseline-always requirement.
D1.6 Min: causes: the tactic space lacks the needed tactic,
the policy never proposes the right sequence. Separating
measurement: human-written proof replay (replays mean the
space is fine, the policy is the problem).
D1.7 Min: the tactic set bounds what is provable. A missing
tactic is an unfixable blind spot. Strong: the granularity
tradeoff.
D1.8 Min: neural vs uniform proposals at fixed node budget,
falsified by equal proof rates. Strong: preregisters the
theorem set.
Flags: inventing prover internals. Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C02, C05.

## Ladder 2
D2.1 Min: capability (measured success), authority (unsupervised
action set), envelope (authority <= capability + margin).
Strong: the margin rationale.
D2.2 Min: admits (0.95, low), (0.95, high), (0.60, low).
rejects (0.60, high). Strong: names the danger cell.
D2.3 Min: expected harm = (1 - c) times harm per failure,
raising authority without capability raises it. Strong: the
drift argument for the margin.
D2.4 Min: the check code, cost is honest measurement of c.
Strong: the re-measurement schedule.
D2.5 Min: full autonomy wins never without measured c,
human-in-loop wins when c is unknown, envelope wins when
authority grows. Strong: states the never.
D2.6 Min: causes: capability was measured on easy tasks,
authority grew faster than capability. Separating measurement:
incident rate per authority level vs per capability bucket.
D2.7 Min: too big wastes useful autonomy, too small admits
drift risk. Strong: ties margin to measurement noise.
D2.8 Min: gated vs ungated rollouts, falsified by equal
incident rates. Strong: preregisters the incident definition.
Flags: "autonomy is a single dial". Rubric: 2 per rung, 16
total, pass at 11. Remediation: lesson C06, C10.

## A1
Min: success rate 3/40 = 0.075. Mean length: (4+6+9)/3 =
6.33. Search cost per step for the shortest: 40/4 = 10 checks
per step. Keep the shortest because shorter proofs replay
faster, are easier to audit, and usually generalize better.
length is a cost with no benefit. Strong: adds the audit
argument. Flags: reporting 40 as the proof size. Rubric:
rate 2, mean 1, cost 2, argument 2, pass at 5. Remediation:
lesson C04.

## A2
Min: independent: 0.20 * 0.10 * 0.30 = 0.006. Shared failure
mode: vision and force miss together, so the pair counts once
at 0.20, times proprioception: 0.20 * 0.30 = 0.06. Comparison:
the miss rate is 10x worse (0.06 vs 0.006). It proves the
product rule needs real independence. Correlated channels
echo. Strong: shows both lines. Flags: multiplying all three
in the shared case. Rubric: independent 2, shared 2, argument
2, pass at 4. Remediation: lesson C08.

## I1
Min: sketch: sample traces -> run intervention (flip cited
fact) -> verdict (faithful/story) -> dashboard of the rate.
Causes: (1) the model rationalizes after acting (the trace is
written to sound good, not to record causes). (2) the task is
hard and the model is uncertain, so it confabulates.
Separating measurement: story rate vs task difficulty: flat
across difficulty means (1), rising with difficulty means
(2). Fixes: (1) train with intervention-tested traces,
penalize stories. (2) allow "I do not know" traces, reward
honesty. Strong: adds the sampling plan. Flags: "ban long
traces". Rubric: sketch 2, causes 2, measurement 2, fixes 2.
Pass at 5. Remediation: lesson C11.

## S1
Min: the search loop survives, the kernel's certainty dies.
The 5 percent error means accepted proofs need re-checking.
Replacement: a second independent verifier (or human audit)
on accepted proofs, plus confidence-weighted search.
Strong: the error-compounding math. Flags: "5 percent is
fine". Rubric: survivor 2, death 1, replacement 3.
Remediation: lesson C02.

## S2
Min: the veto rules survive (they need no human). What dies:
approval-gated actions. Added before the first run: a full
envelope check (capability measured on the exact task),
a dead-man's switch (stop on sensor fault or timeout), and a
remote kill channel. Strong: the pre-flight checklist.
Flags: "the veto is enough". Rubric: survivor 2, additions 3.
Remediation: lesson C06, C10.

## R1
Min: strongest true part: for code with formal specs, proofs
catch what tests miss. Weakest assumption: that specs exist
(most code has no formal spec, and writing one is the hard
part). Decisive experiment: real-world codebases, blind
comparison of proof-based vs test-based pipelines on escaped
defects per engineer-hour. Strong: adds the spec-writing
cost. Flags: accepting "replace". Rubric: true part 2,
assumption 2, experiment 3. Pass at 5. Remediation: lesson
C02, C05.
