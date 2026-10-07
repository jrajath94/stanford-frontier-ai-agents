# U02 lab: the evidence pipeline

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: verdicts and citations

Implement the support verdict function from C01 on three claim/chunk pairs (supported, contradicted, insufficient). Extend it to emit a citation (doc id, chunk id, span) for the supported claim. Report the three verdicts and the citation.

## Task 2: ranker and toy partitioner

(a) Implement the cosine ranker on the C02 toy (query plus 4 docs plus the trap vector). Report the ranking before and after normalization. (b) Implement the 4-cluster partitioner on 200 random 2D points at seed 0. Report recall of the true top-10 for w in {1, 2, 4}.

## Task 3: chunker

Implement the sliding-window chunker with (s, o). On a 1000-token toy doc, report chunk counts for (200, 0) and (200, 50). Verify the span 190-210 sits whole in one chunk at o = 50.

## Task 4: fusion and rerank

(a) Implement score fusion on the C05 toy. Report fused scores and the winner at w = 0.5. Verify w = 0 and w = 1 reproduce the single-signal orders. (b) Implement the two-stage rerank on the C09 toy scores. Report the final top-1.

## Task 5: permissions and abstention

Implement the ACL filter on the C06 toy (Bob and Alice). Then add the abstention rule with threshold t = 0.75: report what Bob gets for a query whose best permitted score is 0.70.

## Task 6: max-sim

Implement max-sim on the C08 toy matrix. Report the 2x4 matrix, the row maxes, and the score 2.00. Verify doc-token permutation leaves the score unchanged. Report the mean-pooled baseline 0.63.

## Task 7: diagnoser

Implement the staged diagnoser on a toy set of 10 failures with known buckets (3 coverage, 4 ranking, 3 generation). Report the bucket counts and the fix priority.
