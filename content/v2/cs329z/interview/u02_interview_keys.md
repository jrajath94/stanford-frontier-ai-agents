# U02 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: grounding = tied to evidence. Truth = correct about the world. "Cited but wrong" is grounded and false (top-left). Red flag: "grounded means true". Rubric: both definitions plus the placement. Remediation: C01.
- B2: cos(a,b) = (a.b)/(||a|| ||b||). Equals the dot product on unit vectors. Red flag: "always". Rubric: formula plus the condition. Remediation: C02.
- B3: recall for speed (and build cost). Strong answer quantifies: 100x cheaper, 0.94 recall on the toy. Remediation: C03.
- B4: boundary insurance. Guarantee: any span shorter than the overlap survives uncut in some chunk. Remediation: C04.
- B5: lexical (exact terms: names, codes, quotes) and dense (paraphrase, synonyms). Red flag: "dense is always better". Remediation: C05.
- B6: abstention = refusing to answer without evidence. Triggers: empty filtered set, best score below threshold. Remediation: C11.

## Deep ladders

- L1.1: score = sum_i max_j S_ij.
- L1.2: S = [[1.00, 0.00, 0.20, 0.90], [0.90, 0.44, 0.61, 1.00]]. Row maxes 1.00, 1.00. Score 2.00.
- L1.3: the max over j is permutation-invariant, so column order does not matter.
- L1.4: S.max(axis=1).sum(). Cost O(m n d) per doc. Storage O(n d) per doc.
- L1.5: mean-pool gives 0.63 on the toy. It blurs exact matches that max-sim preserves. Red flag: "they are equivalent".
- L2.1: fast rough first stage (recall job), slow careful second stage (precision job).
- L2.2: d1 (0.95).
- L2.3: C1(k1) + k2 x C2.
- L2.4: dense top-k1, cross-encoder on k2, resort. Cost as in L2.3.
- L2.5: when the first stage already ranks well. The rerank buys nothing for its cost.

## Analytical/quantitative

- A1: exact 10M x 768 = 7.7e9 ops. Approximate: 7.7e9 x 10/1000 = 7.7e7 ops. Strong answer states both. Red flag: forgetting the probe factor.
- A2: (1e9 - 7.7e7) / 7.4e7 = 12.47, so k2 = 12. Red flag: ignoring the first-stage cost.

## Implementation/debug

- I1: bug 1: raw scores fused without normalization, so BM25 dominates at any w (check: print per-signal ranges). Bug 2: w applied to the wrong signal or the fused list never re-sorted (check: sort order before and after fusion). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: drop the approximate index (exact search on 500 docs is trivial), keep chunking, embeddings, fusion, citations. The reranker stays optional.
- S2: add pre-filtering by tenant ACL before scoring. First test: a query where the top hit is another tenant's doc. Assert its text never enters the context.

## Research critique

- R1: strong: steelman = "a good embedder captures everything BM25 does". Rebuttal 1: exact terms (part numbers, names) where lexical match is the signal. Rebuttal 2: the flip toy (dense-only ranks B first. Hybrid ranks A first). Experiment: sweep w on a labeled set with exact-term queries. Interior w beats w = 0.

## Concept-targeted supplements

- CS1: precision on answered = 65/75 = 0.87. Abstention recall = 20/30 = 0.67. Lowering the threshold answers more and lowers precision. It is one tradeoff curve, not two independent knobs. Rubric: both fractions plus the direction of the tradeoff.
