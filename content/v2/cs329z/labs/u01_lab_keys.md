# U01 lab keys (execution-verified)

Seed 0 everywhere (fresh numpy default_rng(0) per RNG-consuming task). Numbers below are the actual outputs of labs/run_u01_lab.py. Re-verified 2026-10-07 (fixer run 1): empirical simulation rows now match the committed script. The builder-run values they replace differed only by RNG stream.

## Task 1

- Model-only score: 3/10 (only the 3 weight-knowledge questions).
- Full pipeline score: 10/10 on the stub (retriever returns the gold chunk for every question).
- Token counts: 200 per question model-only, 800 per question with retrieval and tools. Cost ratio 4.

## Task 2

- Always-pass stage: outcome "done", 0 retries.
- Always-fail stage: outcome "abort", exactly 1 retry then abort.

## Task 3

- Scorer on 8/10: rate 0.8, standard error 0.1265.
- Bigram P("Paris" | "capital of France is") on corpus A: 6/10 = 0.6.

## Task 4

- Attention row sums: [1.0, 1.0, 1.0].
- Causal mask holds: row 0 sees only token 0, row 1 sees tokens 0-1.
- Output row 2: [3.5105, 4.5105].
- Cache bytes (L=32, d=4096, fp16): n=100 -> 52,428,800. N=1000 -> 524,288,000. N=8192 -> 4,294,967,296. Linear in n.

## Task 5

- T=0.2: theory p = [0.00, 0.01, 0.99]. Empirical (1000 draws) = [0.00, 0.01, 0.99].
- T=1.5: theory p = [0.15, 0.29, 0.56]. Empirical = [0.18, 0.30, 0.53].
- Top-k with k=1: argmax 2, identical to greedy argmax 2.

## Task 6

- Validator: good JSON -> (True, "ok"), `42 bucks` -> parse error, {"price": "42"} -> "price not number". Note: the quoted string '"42 bucks"' parses as JSON but fails with "not a JSON object". The unquoted form fails parsing.
- Masked sampler (1000 draws, seed 0): disallowed-token count 0. Empirical allowed distribution [0.48, 0.32, 0.20] vs theory [0.51, 0.31, 0.19].

## Task 7

- pass@k simulated vs formula (p=0.3, 10,000 trials): k=1: 0.301 vs 0.300. K=2: 0.498 vs 0.510. K=4: 0.759 vs 0.760. K=8: 0.943 vs 0.942. K=16: 0.998 vs 0.997.
- Decision table: tickets -> single call. Translate -> workflow or RAG. Qa10k -> workflow or RAG. Bug -> agent.
- Translate with "path known" flipped to unknown: -> agent with human check.
