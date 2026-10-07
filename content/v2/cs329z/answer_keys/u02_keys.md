# U02 answer keys

Kept separate from `lessons/u02_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: grounded rate 30/40 = 0.75. Truth rate 32/40 = 0.80.
- E2: true but ungrounded (bottom-right of the 2x2). No pointer, but the claim is correct.
- E3: the cited page was wrong. The pointer existed, so the answer looked checked, but the source was a forum post with the wrong window.

## C02

- E1: d2 = [0.70, 0.71]. Norm = sqrt(0.49 + 0.5041) = sqrt(0.9941) = 0.997. cos = 0.70 / 0.997 = 0.702, about 0.70.
- E2: u = [1.8, 0.88], norm = sqrt(3.24 + 0.7744) = sqrt(4.0144) = 2.004. cos = 1.8 / 2.004 = 0.898, about 0.90, tied with d1.
- E3: antonyms share context words ("refund", "money", "back"), so the embedder places them near each other. Geometry follows co-occurrence, not logic.

## C03

- E1: 10,000,000 x 768 = 7.68e9 multiply-adds, about 15 GFLOPs counting multiply plus add.
- E2: p / w = 1000 / 10 = 100. Cost falls from 7.7e9 to 7.7e7 ops.
- E3: every stored vector is stale. Distances are computed against the old geometry, so the ranking is wrong at any w. Rebuild the index.

## C04

- E1: starts at 0, 150, 300, 450, 600, 750, 850. That is 7 chunks (last chunk 850-1000).
- E2: a span [x, x+L] is cut only if a boundary falls strictly inside it. Boundaries repeat every s - o = 150. With o > L, every window of length L sits whole inside some chunk of length s = L + o... precisely: chunk starts are spaced 150 apart and each chunk is 200 long, so any span of length under 50 is contained in the chunk whose start is the largest multiple of 150 at or below x.
- E3: each cell loses its column header. The chunks are numbers without meaning, so the embedder matches on noise.

## C05

- E1: A = 0.5 x 1.00 + 0.5 x 0.82 = 0.91. B = 0.5 x 0.336 + 0.5 x 0.91 = 0.623.
- E2: w = 1 gives s = s_lex only: A 1.00 > B 0.336. Lexical order.
- E3: raw BM25 ranges 0-30 while cosine ranges -1 to 1. At w = 0.5 the BM25 term dominates the sum and the dense scores barely move the total.

## C06

- E1: d2 at 0.80 (d1 removed by the filter).
- E2: the text of d1 entered the context before the filter ran. The model read it and paraphrased it. Dropping the citation does not un-read the text.
- E3: re-resolve ACLs on every index write and on a schedule. A stale ACL is a leak. Treat it as an incident.

## C07

- E1: 2 x 220^2 x 768 = 2 x 48,400 x 768 = 74,342,400, about 7.4e7 FLOPs.
- E2: the cross-encoder reads query and doc together, so it sees that d2's high dense score came from a spurious match. The joint read reverses the ranking.
- E3: keep k small (10-100). The per-pair cost is quadratic in length. K = 1000 makes the reranker dominate the pipeline.

## C08

- E1: policy row = [0.90, 0.44, 0.61, 1.00]. Max = 1.00 (the "policy" column).
- E2: query mean [0.95, 0.22], doc mean [0.525, 0.605]. Dot = 0.95 x 0.525 + 0.22 x 0.605 = 0.499 + 0.133 = 0.632, about 0.63.
- E3: each query token takes the max over doc tokens, so four copies of "refund" give the same maxes as one. The score cannot tell one mention from four.

## C09

- E1: 7.7e7 + 10 x 7.4e7 = 7.7e7 + 7.4e8 = 8.17e8, about 8.2e8 FLOPs.
- E2: the gold doc is outside the candidate set. The second stage only reorders what the first stage returned, so it can never recover the gold.
- E3: when the first stage already ranks well. The rerank cost buys no accuracy and the pipeline is slower for nothing.

## C10

- E1: coverage 16/20 = 0.80. Precision 13/16 = 0.8125, about 0.81.
- E2: the pointer exists but aims at a span that does not support the claim. It looks checked and is not.
- E3: chunk ids must be stable across rebuilds. If a rebuild renumbers chunks, old citations point at wrong text.

## C11

- E1: precision 65/75 = 0.867, about 0.87. Abstention recall 20/30 = 0.667, about 0.67.
- E2: no doc mentions 2+2, so the evidence rule fires. The fix is a fast path: computable or definitional answers bypass the retrieval requirement.
- E3: re-tune the threshold on each new corpus. Score distributions shift. A fixed t drifts.

## C12

- E1: ranking failures fall from 50 to 20. New total = 20 + 20 + 30 = 70.
- E2: the gold label is wrong, so staged elimination blames the reader for ignoring a bad chunk. The diagnosis punishes the stage that was right.
- E3: re-diagnose after every component fix. Buckets migrate as the system changes. A stale diagnosis misdirects the next fix.
