# U01 capstone: test-time scaling vs prompt quality (EXECUTED)

Status: EXECUTED 2026-10-07. The design below ran as `capstones/research_replication/run_replication.py`. Results in `capstones/research_replication/results.md`. All numbers in this file were planned. The measured numbers live in the results report.

## Replication

Reproduce the pass@k curve from C10 on a synthetic QA set: 200 questions with checkable answers, a stub model with per-sample pass rate p near 0.3 (seeded). Measure pass@k for k in {1, 2, 4, 8, 16} over 5 seeds. Success criterion: measured curve within 0.03 of 1 - (1-p)^k at every k.

## Extension

Question: on the same set, does best-of-k with a verifier beat majority vote, and does either beat a better prompt at k = 1?

Falsifiable hypothesis: best-of-k beats vote when p < 0.5. A better prompt (p = 0.5) at k = 1 beats vote at k = 8 from the weak prompt.

Literature: the course's test-time scaling concept (S02). Pass@k definition from U01-C10.

Data: 200 synthetic questions, fixed. No human data.

Baselines: weak prompt k = 1. Weak prompt vote k = 8. Weak prompt best-of-k = 8. Strong prompt k = 1.

Matched budgets: token budgets equated across arms (vote k = 8 costs 8x. The strong prompt arm gets 8x tokens via longer reasoning).

Metrics: pass rate, tokens per question.

Controls: same questions, same seeds, same verifier.

Ablations: verifier accuracy at {1.0, 0.8, 0.6} (does a noisy verifier kill best-of-k?).

Seed variation: 5 seeds. Report mean and standard error.

Uncertainty: binomial intervals on pass rates.

Failure criteria: if the replication misses the curve by more than 0.05, the stub model's p is miscalibrated. Fix the stub before the extension.

Reproducibility: seed list, stub code, and the exact 200 questions committed.

Negative results: if the strong prompt does not beat vote, report it. The hypothesis is wrong.

Limitations: synthetic stub, not a real model. No claim about real LLMs.

Ethical considerations: none. Synthetic data, no human subjects.
