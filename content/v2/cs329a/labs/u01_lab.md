# Lab U01 , Test-time compute and verification

Run script: `runs/run_u01.py`. Seed: 7. Status: executed 2026-10-07.
Observed outputs are recorded below next to the expected values.

## Exercise 1 , pass@N Monte Carlo

Task: estimate pass@N for p = 0.25, N = 1..8, with 40,000 trials per N.
Compare with the analytic table in lesson C01 item 6.

Expected: estimates within 0.01 of analytic at every N.

Observed:

| N | analytic | estimate | diff |
|---|---|---|---|
| 1 | 0.2500 | 0.2535 | 0.0035 |
| 2 | 0.4375 | 0.4373 | 0.0002 |
| 3 | 0.5781 | 0.5825 | 0.0044 |
| 4 | 0.6836 | 0.6847 | 0.0011 |
| 5 | 0.7627 | 0.7625 | 0.0001 |
| 6 | 0.8220 | 0.8231 | 0.0011 |
| 7 | 0.8665 | 0.8686 | 0.0020 |
| 8 | 0.8999 | 0.9007 | 0.0008 |

Verdict: PASS. All diffs below 0.01. The diminishing-returns shape is
visible in both columns.

Analysis questions (answers in `keys/u01_key.md`):
L1.1: why does the diff shrink and grow irregularly across N?
L1.2: how many trials would you need for diff < 0.001 at N = 8?

## Exercise 2 , best-of-N with a noisy verifier

Task: 20,000 rounds of 8 samples at p = 0.25. Perfect verifier scores
1.0/0.0. Noisy verifier adds N(0, 0.35) noise to correctness.

Expected: perfect-verifier rate near pass@8 = 0.8999, noisy rate below
it but above p = 0.25.

Observed: perfect 0.9044, noisy 0.8671, analytic pass@8 0.8999.

Verdict: PASS. Perfect-verifier best-of-8 matches pass@8 within noise.
The noisy verifier keeps most of the gain (0.8671 vs 0.9044).

Analysis questions:
L2.1: why is the noisy rate above pass@8 * 0.5?
L2.2: what happens to the noisy rate as the noise std goes to 0? To
infinity?

## Exercise 3 , cost-success crossing

Task: find the first budget (steps of 5) where the strong-verifier plan
beats the cheap-verifier plan, with the lesson C05/C12 numbers.

Expected: crossing between 60 and 65.

Observed: 65. cheap@50 = 0.6606, strong@50 = 0.6152, cheap@100 =
0.6978, strong@100 = 0.8099.

Verdict: PASS. Matches the lesson table to four decimals.

Analysis questions:
L3.1: why does the crossing move if p rises to 0.4?
L3.2: the script steps by 5. What does the step size hide?

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for self-improvement basics). They are
not the course homework and do not reproduce any assessed artifact.
