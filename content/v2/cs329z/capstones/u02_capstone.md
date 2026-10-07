# U02 capstone: hybrid fusion on exact-term queries (proposed, not executed)

Status: design only. No experiment has run. All numbers below are planned, not measured.

## Replication

Reproduce the C05 fusion flip on a synthetic corpus: 500 docs, 100 queries, half with exact terms (codes, names), half pure paraphrase. Dense-only, lexical-only, and fused (w = 0.5) rankings. Success criterion: the fused ranking reproduces the flip direction on the exact-term half (fused top-1 differs from dense-only top-1 on at least 20 percent of those queries).

## Extension

Question: does the optimal fusion weight differ between exact-term and paraphrase queries, and does a per-query weight rule beat a fixed w?

Falsifiable hypothesis: optimal w is above 0.6 on exact-term queries and below 0.4 on paraphrase queries. A rule setting w from the count of rare query terms beats fixed w = 0.5 on recall@10.

Literature: hybrid search concept (S03). Fusion from U02-C05.

Data: 500 synthetic docs, 100 synthetic queries with gold doc labels. No human data.

Baselines: dense-only, lexical-only, fixed w = 0.5, oracle per-query w (upper bound).

Matched budgets: same candidate depth k = 50 for all arms.

Metrics: recall@10, top-1 accuracy.

Controls: same corpus, same queries, same normalization.

Ablations: normalization on/off (does raw-scale fusion collapse as C05 predicts?).

Seed variation: 5 corpus shuffles. Report mean and standard error.

Uncertainty: binomial intervals on recall.

Failure criteria: if the replication shows no flips, the synthetic queries lack exact terms. Regenerate with more codes.

Reproducibility: corpus generator seed, query list, and fusion code committed.

Negative results: if per-query w ties fixed w, report it. The rule adds nothing.

Limitations: synthetic corpus. Real query distributions differ.

Ethical considerations: none. Synthetic data, no human subjects.
