# U08 lab keys (execution-verified)

Seed 0 everywhere (each task starts with a fresh numpy default_rng(0)). Numbers below are the actual outputs of labs/run_u08_lab.py. Re-verified 2026-10-07 (fixer run 1).

## Task 1

- Action space: click, type, scroll, keypress.
- Open-loop prediction: 0.3164. Observed: 0.60 (12/20).
- Grounding errors: 5 of 8 failures.

## Task 2

- Vision premium: 0.15. SE 0.0984. z = 1.5 (suggestive).
- Vision-only arm: 0.55 (worse than table-only).

## Task 3

- Mean task cost: $0.48. p99: $1.60.
- Retry step: $0.05 to $0.15 (3x). Alert at 2 SE above baseline.
- Probe: 4 extra runs. Removing the cited 3 flips the decision. Removing random 3 does not.
- Cost per finding: $500/3 = $167.

## Task 4

- Flat: 0.99^500 = 0.0066. Hierarchical with checks: near 0.90.
- Recovery counts: retry 12, rollback 4, escalate 3, compensate 1.
- Total cost units: 202. Escalation share: 0.743.

## Task 5

- All-to-all: 999,000. Hub: 2,000. Ratio 499.5.
- Per round at 1 ms/msg: 999 s vs 2 s.

## Task 6

- Drill: 25 min with runbook vs 4 h without. Saves 3.5 h.
- Proposal A: 7/10 ships. Proposal B: 4/10 returns.

## Task 7

- Run budget: 16.7 h. Fits weeks 7-8.
- Open gap rows: S10 (26 Oct), S16 (16 Nov).
