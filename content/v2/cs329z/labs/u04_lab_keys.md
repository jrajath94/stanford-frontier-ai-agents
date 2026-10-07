# U04 lab keys (execution-verified)

Seed 0 everywhere (fresh numpy default_rng(0) per RNG-consuming task). Numbers below are the actual outputs of labs/run_u04_lab.py. Re-verified 2026-10-07 (fixer run 1): empirical simulation rows now match the committed script. The builder-run values they replace differed only by RNG stream.

## Task 1

- Argmax: candidate 4 (index 3) at 0.78.
- Search cost: 4 x 20 = 80 scored calls.
- Gain over the hand-written baseline: 0.78 - 0.62 = 0.16.

## Task 2

- draft-then-translate -> prompt chaining. ticket triage -> routing. 5 code reviews -> parallelization. research brief -> orchestrator-workers. draft-critique-revise -> evaluator-optimizer. open-ended bug hunt -> agent.

## Task 3

- Trace alternation: True (7 steps, no two actions in a row).
- Chart run: valid path through start, plan, act, observe, reflect, done.
- Dropped observe->reflect edge: reflect unreachable (no incoming edge remains).

## Task 4

- Memory manager: summary 500 tokens, kept total 2500 tokens, compression 16x.
- File memory: 3 notes written. Fresh session reads them back. Grep for the step-3 fact: hit (True).

## Task 5

- Envelope keys: task, state, constraints, done. Size ratio 8000/200 = 40x.
- Bus: 30 sends total, 10 receives per agent (each agent reads its own 10).

## Task 6

- Pipeline simulation (10,000 runs): R without checks 0.734 (theory 0.729). R with checks 0.943 (theory 0.941).
- Comparison rig: gain per extra cost 0.0175. Verdict at bar 0.03: single agent.

## Task 7

- (a) answer at step 2: stops at step 2, rule answer.
- (b) 10 fruitless steps: stops at step 10, rule budget.
- (c) 3 identical observations at steps 4-6: stops at step 6, rule stall.
- (d) denial at step 3: stops at step 3, rule deny.
