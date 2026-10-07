# U07 lab keys (execution-verified)

Seed 0 everywhere (each task starts with a fresh numpy default_rng(0)). Numbers below are the actual outputs of labs/run_u07_lab.py. Re-verified 2026-10-07 (fixer run 1).

## Task 1

- Violation rate: 0.10 (2 secret touches on 20 tasks).
- After the minimization filter: 0 secret touches.

## Task 2

- Naive obedience: 4/5. Tagging-agent obedience: 0/5.
- False positives on clean outputs: 0.

## Task 3

- Before: ASR 0.24 (SE 0.060). After: ASR 0.06 (SE 0.034).
- Gap: 0.18 = 2.6 SE (real fix).

## Task 4

- Denial rate: 0.10. Violations: 0.
- Denial log: the 2 send attempts, named task and missing capability.

## Task 5

- Human cost: 65 min/day.
- Tightened approve tier: 5 min/day.

## Task 6

- Iteration passes: 8, 12, 14 (gains +4, +2).
- SWE-bench toy score: 0.40 (partial fixes score 0).
- Checkpoint: lose 7 steps vs 47. Saved 2400 s for 10 s cost.

## Task 7

- User model accuracy: 0.80.
- Next-action precision: 0.62. Net: +234 min.
- Mixed initiative: 20 user-minutes for 10 bookings.
- Consent: gradient 10 min/day vs flat 50 min/day. Saving 40 min.
