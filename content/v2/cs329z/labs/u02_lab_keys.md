# U02 lab keys (execution-verified)

Seed 0 everywhere (fresh numpy default_rng(0) per RNG-consuming task). Numbers below are the actual outputs of labs/run_u02_lab.py. Re-verified 2026-10-07 (fixer run 1): empirical simulation rows now match the committed script. The builder-run values they replace differed only by RNG stream.

## Task 1

- Verdicts (naive stemming overlap, threshold 3): "The refund window is 30 days" -> supported. "Refunds are instant" -> insufficient. "Refunds take 90 days" -> contradicted.
- Citation for the supported claim: (doc7, chunk2, span 150-350).

## Task 2

- Raw dot-product order: trap, d1, d2, d3, d4. The trap vector wins by length.
- Cosine order: d1, trap, d2, d3, d4. The trap ties d1 at 0.90 after normalization.
- Partitioner recall of true top-10 (200 points, 4 clusters, seed 0): w=1 -> 0.80, w=2 -> 1.00, w=4 -> 1.00. Recall rises monotonically with w.

## Task 3

- (s=200, o=0): 5 chunks. Span 190-210 cut: intact = False.
- (s=200, o=50): 7 chunks. Span 190-210 intact = True.

## Task 4

- Fusion w=0.5: A = 0.910, B = 0.623. Winner: A (flip from dense-only).
- w=0: A = 0.820, B = 0.910. Winner: B (dense order).
- w=1: A = 1.000, B = 0.336. Winner: A (lexical order).
- Rerank final top-1: d1 (cross-encoder 0.95 beats d2's 0.30).

## Task 5

- Bob top-1: d2 at 0.80 (d1 filtered). Alice top-1: d1 at 0.95.
- Query with best permitted score 0.70 and threshold 0.75: abstain.

## Task 6

- S = [[1.00, 0.00, 0.20, 0.90], [0.90, 0.44, 0.61, 1.00]].
- Row maxes: 1.00, 1.00. Score: 2.00.
- Permuted doc tokens: score still 2.00.
- Mean-pooled baseline: 0.632, about 0.63.

## Task 7

- Buckets: coverage 3, ranking 4, generation 3. Fix priority: ranking (largest bucket).
