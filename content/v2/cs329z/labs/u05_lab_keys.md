# U05 lab keys (execution-verified)

Seed 0 everywhere (each task starts with a fresh numpy default_rng(0)). Numbers below are the actual outputs of labs/run_u05_lab.py. Re-verified 2026-10-07 (fixer run 1): empirical simulation rows now match the committed script. The builder-run values they replace differed only by RNG stream.

## Task 1

- Argmax: candidate 4 (index 3) at 0.78.
- Search cost: 4 x 20 = 80 scored calls.
- SE per candidate: 0.1112, 0.1085, 0.1025, 0.0926 (candidate 3 at 0.70: 0.1025).
- 5-example dev: winner flips on 2/5 seeds.

## Task 2

- Bar 0.78: prompt rewrite. Bar 0.80: fine-tune.
- SE on 200 examples at 0.79: 0.0288.

## Task 3

- Full: 1,048,576. Adapter: 16,384. Ratio 64.
- Merge max abs diff: 7.11e-13 (exact merge).
- Rank of B A: 8.
- 7B memory: 14.0 GB fp16, 3.5 GB 4-bit.

## Task 4

- Distillation gain over scarce gold: 0.10. Labeling cost: 1000 teacher calls, once.
- Expected good synthetic labels: 722.5.
- Collapse variances: 1.00, 0.76, 0.56.

## Task 5

- Pair 1: m = 0.40, beta m = 0.040, loss 0.673.
- Pair 2: m = -0.60, beta m = -0.060, loss 0.724.
- Theta-equals-ref loss: 0.693 = log 2.

## Task 6

- Daily yield: 100 traces at $200/day. Weekly yield: 700 traces.
- Uncertainty vs random gap: 0.06. Duplicate filter saves 20 percent of any budget.

## Task 7

- Leakage rate: 0.06. Reported mean: 0.748. Inflation: 0.008.
- Validator gap: 0.15. Accuracy at 0.5: 0.60.
- Vault peek bias toy: 0.74 + 0.04 = 0.78.
