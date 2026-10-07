# U02 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define grounding and truth, and place "cited but wrong" in the 2x2.
B2. Write the cosine similarity formula. When does it equal the dot product?
B3. What does a vector store index trade for speed?
B4. Why does chunk overlap exist? State the guarantee.
B5. What are the two witnesses in hybrid search, and what does each catch?
B6. Define abstention and name its two triggers.

## Deep ladders (2 x 5)

### Ladder 1: late interaction

L1.1 Define: write the ColBERT score from the similarity matrix S.
L1.2 Toy: compute S for the 2x4 toy and the row maxes.
L1.3 Derive: show doc-token permutation leaves the score unchanged.
L1.4 Implement and complexity: write max-sim. State query-time cost per doc.
L1.5 Compare: how does the score differ from mean-pooled single-vector scoring?

### Ladder 2: the cascade

L2.1 Define: the retrieve-then-rerank pipeline and its two stages' jobs.
L2.2 Toy: first stage top-3 d2/d1/d5. Cross-encoder d2 0.30, d1 0.95, d5 0.60. Final top-1?
L2.3 Derive: total cost as a function of k1 and k2.
L2.4 Implement and complexity: write the pipeline. State the cost.
L2.5 Compare: when do you skip the reranker entirely?

## Analytical/quantitative (2)

A1. 10M docs, d = 768, 1000 partitions, probe 10. Compute exact vs approximate ops per query.
A2. A reranker costs 7.4e7 FLOPs per pair. Budget is 1e9 FLOPs per query after a 7.7e7 first stage. What is the max k2?

## Implementation/debug (1)

I1. Your fusion never changes the dense-only ranking no matter what w you set. Name two bugs and how you check each.

## Changed-constraint scenarios (2)

S1. The corpus is 500 docs. Which U02 machinery do you drop, and what stays?
S2. A new tenant joins with strict ACLs on half the corpus. What changes in the pipeline, and what is the first test?

## Research critique (1)

R1. "Dense retrieval makes BM25 obsolete." State the strongest version, then give two reasons it fails and one experiment that would change your mind.

## Concept-targeted supplements

CS1. (U02-C11) 100 questions, 70 answerable, 30 not. Your threshold answers 75 and abstains 25. Of the 75 answered, 65 are right. Of the 25 abstained, 20 were truly unanswerable. Compute precision on answered and abstention recall. What happens to precision if you lower the threshold?
