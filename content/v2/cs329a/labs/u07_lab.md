# Lab U07 , Reasoning, formal systems, and autonomy

Run script: `runs/run_u07.py`. Deterministic. Status: executed
2026-10-07. Observed outputs are recorded below.

## Exercise 1 , proof search

Task: run the toy tactic search from lesson U07 C02 (6 sequences,
2 close).

Expected: rate 1/3, kernel judges all 6 for free.

Observed: tried=6 closed=2 rate=0.3333.

Verdict: PASS. Matches lesson U07 C02 item 6.

Analysis questions (answers in `keys/u07_key.md`):
L1.1: why is the kernel check "free" while the policy training
is expensive?

## Exercise 2 , AlphaGeometry loop

Task: run the toy propose-and-close loop from lesson U07 C03 (5
constructions, 2 close).

Expected: hit rate 0.40.

Observed: proposed=5 closed=2 hit_rate=0.40.

Verdict: PASS. Matches lesson U07 C03 item 6.

Analysis questions:
L2.1: which side of the loop would you scale first to raise the
solve rate, and why?

## Exercise 3 , conjecture/search/proof split

Task: classify the toy run from lesson U07 C04 (13 nodes, 4-step
proof).

Expected: 9 dead ends, ratio 3.25.

Observed: nodes=13 proof=4 dead=9 ratio=3.25.

Verdict: PASS. Matches lesson U07 C04 item 6.

Analysis questions:
L3.1: a run reports "13-step proof". What is wrong with the
report, in one sentence?

## Exercise 4 , sim-to-real gap

Task: compute the reality gap before and after domain
randomization for the lesson U07 C09 toy.

Expected: 0.25, then 0.12.

Observed: gap_plain=0.25 gap_randomized=0.12.

Verdict: PASS. Matches lesson U07 C09 item 6.

Analysis questions:
L4.1: the sim number fell from 0.95 to 0.88. Why is that good
news, not bad?

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for self-improvement basics). They
are not the course homework and do not reproduce any assessed
artifact.
