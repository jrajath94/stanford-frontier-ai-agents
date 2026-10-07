# Capstone A (executed): test-time scaling vs prompt quality

Status: EXECUTED 2026-10-07. This report executes the design in `../u01_capstone.md`. All numbers below are measured outputs of `run_replication.py` (seed 0). All data synthetic. No claim about real LLMs.

## Replication

Question: does the measured pass@k curve match 1 - (1-p)^k on a synthetic QA set?

Method: 200 synthetic questions with checkable answers. Stub model: per-question pass rate drawn from Uniform(0.28, 0.32) (seed 0), Bernoulli draws per (question, sample, seed). k in {1, 2, 4, 8, 16}, 5 seeds. Success criterion: measured within 0.03 of theory at every k.

Result: PASS at every k.

| k | theory | measured | gap |
| --- | --- | --- | --- |
| 1 | 0.3000 | 0.2850 | 0.0150 |
| 2 | 0.5100 | 0.5070 | 0.0030 |
| 4 | 0.7599 | 0.7640 | 0.0041 |
| 8 | 0.9424 | 0.9290 | 0.0134 |
| 16 | 0.9967 | 0.9960 | 0.0007 |

Figure: `fig_passk.png`.

## Extension

Question: on the same set, does best-of-k with a verifier beat majority vote, and does either beat a better prompt at k = 1?

Falsifiable hypotheses:
- H1: best-of-k beats vote when p < 0.5. SUPPORTED.
- H2: a better prompt (p = 0.5) at k = 1 beats vote at k = 8 from the weak prompt. SUPPORTED.

Measured (5 seeds):

| arm | pass rate |
| --- | --- |
| weak prompt, k = 1 | 0.2850 |
| weak prompt, majority vote, k = 8 | 0.0660 |
| weak prompt, best-of-8, verifier 1.0 | 0.9290 |
| weak prompt, best-of-8, verifier 0.8 | 0.7480 |
| weak prompt, best-of-8, verifier 0.6 | 0.5780 |
| strong prompt, k = 1 (8x tokens via longer reasoning) | 0.4680 |

Matched budgets: vote k = 8 costs 8x tokens. The strong-prompt arm receives 8x tokens via longer reasoning. At matched budgets the ranking is best-of-8 (any verifier) > strong prompt > vote > weak k = 1.

Ablation (verifier accuracy): best-of-8 degrades gracefully from 0.9290 to 0.5780 as verifier accuracy falls from 1.0 to 0.6. Even the noisy verifier (0.6) beats voting (0.0660) by a wide margin. The verifier is the load-bearing component: at verifier 0.0 best-of-k would score 0.

Uncertainty: 200 questions x 5 seeds = 1000 draws per arm. Binomial SE on the vote arm: sqrt(0.066 x 0.934/1000) = 0.0079. The gaps (0.5+) are far outside noise.

Figure: `fig_extension.png`.

## Negative results

None on the hypotheses: both held. The honest negative: the weak prompt's measured k = 1 rate (0.2850) undershoots the nominal 0.3 by 0.015. The stub's per-question rates average 0.30 but the finite sample sits low. This is sample noise, not a finding, and it is reported rather than rounded away.

## Limitations

Synthetic stub, not a real model. Independent Bernoulli draws: real samples correlate, which would flatten the measured curve below theory (U01-C10 states the bound direction). The verifier model (pick-correct with probability v) is a crude stand-in for a real judge. No claim about real LLMs transfers without re-running on one.

## Reproducibility

`run_replication.py`, seed 0 (strong arm seed 99, verifier seeds 1000+10v). Re-run: `python3 run_replication.py`. Figures are metadata-stripped PNGs.

## Ethical considerations

None. Synthetic data, no human subjects, no real users.
