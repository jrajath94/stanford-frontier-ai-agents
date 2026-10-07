# Lab U05 , Software-engineering and kernel agents

Run script: `runs/run_u05.py`. Deterministic. Status: executed
2026-10-07. Observed outputs are recorded below.

## Exercise 1 , CodeMonkeys budget

Task: compute the per-issue cost and context share at K = 8 and
K = 32 for the lesson C01 toy (context $0.40, $0.05 per serial
iteration, S = 3).

Expected: $1.60 at 25.0 percent context share. $5.20 at 7.7
percent. Coverage 0.9719.

Observed: cost_k8=1.60 share_k8=0.2500 cost_k32=5.20
share_k32=0.0769 coverage=0.9719.

Verdict: PASS. Matches lesson U05 C01 item 6.

Analysis questions (answers in `keys/u05_key.md`):
L1.1: why does the context share fall as K grows?

## Exercise 2 , test-time code search

Task: compute coverage for K = 10, p = 0.30, and the expected
shortlist from generated tests with precision 0.80, recall 0.90
on 3 correct of 10 candidates.

Expected: coverage 0.9718, shortlist about 4 (2.7 true, 1.4
false positives).

Observed: coverage=0.9718 tp=2.7 fp=1.4 shortlist=4.1.

Verdict: PASS. Matches lesson U05 C02 item 6.

Analysis questions:
L2.1: what happens to the shortlist when test precision drops to
0.40?
L2.2: why does the judge run after the filter, not before?

## Exercise 3 , KernelBench fast_p

Task: score the 10-kernel toy table from lesson U05 C04.

Expected: correctness 0.60, fast_1 0.40, fast_2 0.10.

Observed: correct=0.60 fast_1=0.40 fast_2=0.10.

Verdict: PASS. The fast-but-wrong kernels score 0.

Analysis questions:
L3.1: which two kernels are fast but wrong, and what do they
prove about single-axis scores?

## Exercise 4 , Amdahl bound

Task: compute the speedup for a 60 percent hotspot at 2x and 3x.

Expected: 1.4286 and 1.6667.

Observed: speedup_2x=1.4286 speedup_3x=1.6667.

Verdict: PASS. Matches lesson U05 C07 item 6.

Analysis questions:
L4.1: the bound at infinite factor is 2.5x. What does the
remaining 0.40 represent, and what does it forbid?

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for self-improvement basics). They
are not the course homework and do not reproduce any assessed
artifact.
