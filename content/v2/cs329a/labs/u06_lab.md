# Lab U06 , Memory, caches, and long-context representations

Run script: `runs/run_u06.py`. Deterministic. Status: executed
2026-10-07. Observed outputs are recorded below.

## Exercise 1 , KV cache memory

Task: compute the KV cache bytes for a 20,480-token corpus and a
512-slot cartridge (32 layers, 8 kv heads, d_head 128, fp16).

Expected: 2.684 GB vs 67.109 MB, ratio 40.0.

Observed: full=2.684 GB cart=67.109 MB ratio=40.0.

Verdict: PASS. Matches lesson U06 C04 item 6.

Analysis questions (answers in `keys/u06_key.md`):
L1.1: the ratio equals N/p exactly. Why does nothing else in the
formula matter for the ratio?

## Exercise 2 , CacheBlend saving

Task: compute the blend cost for 4 chunks of 512 tokens at
r = 0.15 with a 64-unit check.

Expected: 371 units vs 2,048, ratio 5.52.

Observed: full=2048 blend=371 (recomp 307 + check 64)
ratio=5.52.

Verdict: PASS. Matches lesson U06 C06 item 6.

Analysis questions:
L2.1: at what recompute ratio does the blend cost exceed half
the full prefill?
L2.2: why is the check cost counted separately from the
recompute?

## Exercise 3 , MemGPT paging

Task: page 20 turns through a capacity-8 main context.

Expected: 8 in main, 12 in archival, 0 lost.

Observed: main=8 archival=12 searches=5.

Verdict: PASS. Matches lesson U06 C01 item 6.

Analysis questions:
L3.1: which 8 stay, and what rule picks them?

## Exercise 4 , retrieval precision and recall

Task: compute precision and recall for 3 relevant of 5 returned,
8 relevant of 50.

Expected: precision 0.60, recall 0.375.

Observed: precision=0.60 recall=0.375.

Verdict: PASS. Matches lesson U06 C07 item 6.

Analysis questions:
L4.1: a second query returns 3 new relevant docs and no noise.
Recompute precision and recall over both queries combined.

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for self-improvement basics). They
are not the course homework and do not reproduce any assessed
artifact.
