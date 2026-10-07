# Lab U04 , Open-ended evolution and deep research

Run script: `runs/run_u04.py`. Deterministic. Status: executed
2026-10-07. Observed outputs are recorded below.

## Exercise 1 , truncation differential

Task: compute the selection differential for the lesson C03 toy.

Expected: mean 0.6167 -> 0.7067, differential +0.09.

Observed: mean_all=0.6167 mean_surv=0.7067 diff=0.0900.

Verdict: PASS. Matches lesson U04 C03 item 6.

Analysis questions (answers in `keys/u04_key.md`):
L1.1: why does truncation push harder than proportionate selection?

## Exercise 2 , evolution toy

Task: run 4 generations of mutate-select on 8-bit strings, fitness =
count of ones, seed 11.

Expected: mean fitness non-decreasing across generations.

Observed: 3.667 -> 4.500 -> 5.833 -> 6.833 -> 6.833.

Verdict: PASS. Fitness rises then plateaus, the classic shape.

Analysis questions:
L2.1: the plateau at 6.833 lasts one generation here. What two
different causes can a plateau have?
L2.2: what in this toy plays the role of locality (U04 C02)?

## Exercise 3 , holdout optimism

Task: predict the holdout score from the validation max with the
max-of-normals correction.

Expected: predicted about 0.71 against observed 0.69.

Observed: se=0.0324 optimism=0.0729 predicted_holdout=0.7071.

Verdict: PASS. Matches lesson U04 C09 item 6.

Analysis questions:
L3.1: the prediction uses 2.25. When is that constant wrong?

## Exercise 4 , evolution budget sheet

Task: compute the three-fuel sheet for the lesson U04 C10 toy.

Expected: money 600.0, time 1.67h, review 2.5h, money binds against a
$400 wallet.

Observed: money=600.0 time_h=1.67 review_h=2.5, binding fuel: money.

Verdict: PASS.

Analysis questions:
L4.1: name one way the sheet undercounts, and which fuel it hits.

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for self-improvement basics). They are
not the course homework and do not reproduce any assessed artifact.
