# U01 lab: from a model to a system

Environment: Python 3 with NumPy. No installs beyond the standard scientific stack. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: three-step pipeline on stub data

Stub a retriever (returns fixed chunks for 10 toy questions), a calculator (evaluates arithmetic strings), and an answer formatter. Score the model-only path (formatter with no evidence) and the full pipeline on the 10 questions. Report both scores and the token counts.

## Task 2: gated runner

Implement the (function, gate) runner from C02: a list of (stage, gate) pairs, one retry per failed stage, abort after the retry fails. Test with: (a) a stage that always passes, (b) a stage that always fails. Report the retry counts and final outcomes.

## Task 3: scorer and bigram mixer

(a) Implement the scorer: given a list of 0/1 outcomes, report the rate and the standard error. Check it on 8/10. (b) Implement the bigram mixer: fit counts on corpus A, continue on corpus B, report P("Paris" | "capital of France is") before and after.

## Task 4: attention and cache simulator

(a) Implement masked attention in NumPy on the 3x2 toy from C04. Verify rows sum to 1 and the causal mask holds. (b) Implement the cache simulator: report bytes at n = 100, 1000, 8192 for L = 32, d = 4096, fp16. Verify linear growth.

## Task 5: sampler

Implement greedy, temperature sampling, top-k, and top-p on logits [1.0, 2.0, 3.0]. Draw 1000 samples at T = 0.2 and T = 1.5 with seed 0. Report the empirical frequencies. Verify top-k with k = 1 equals greedy.

## Task 6: validator and masked sampler

(a) Implement the JSON validator from C07. Test the three cases from the lesson. (b) Implement the masked sampler from C08 on the 5-token toy. Draw 1000 samples at seed 0. Report disallowed-token count and the empirical allowed distribution.

## Task 7: pass@k simulator and decision table

(a) Simulate pass@k for p = 0.3, k in {1, 2, 4, 8, 16} over 10,000 trials at seed 0. Compare with 1 - (1-p)^k. (b) Implement the C12 decision function and map the four toy tasks. Flip "path known" to "unknown" on the translation task and report the new mapping.
