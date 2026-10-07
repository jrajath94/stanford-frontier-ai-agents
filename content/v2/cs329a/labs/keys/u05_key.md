# Lab key U05

Keep separate from the lab. Test-mode answers live here only.

## L1.1
The context cost is fixed per issue, paid once. More trajectories
divide that fixed cost over more samples, so its share of the
total falls. The trajectory cost grows with K, the context cost
does not.

## L2.1
False positives: 7 * 0.60 = 4.2. Shortlist: 2.7 + 4.2 = 6.9,
about 7. The judge now sees 7 instead of 4, and most of the
shortlist is wrong. Precision below 0.5 inverts the filter.

## L2.2
The judge is the expensive step. Running it on the full pile
wastes judge calls on candidates the cheap tests could have
dropped. Filter first, judge the survivors.

## L3.1
Kernels 3 (F, 2.1x) and 8 (F, 1.8x). They prove that a
speed-only score rewards wrong code and a correctness-only
score ignores speed. fast_p is the conjunction for a reason.

## L4.1
The 0.40 is the unoptimized share: parse, softmax, norm, copy.
It forbids any single-part optimization from beating 2.5x. To go
further, optimize more parts or change the pipeline.
