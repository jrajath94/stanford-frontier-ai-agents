# Notation and shapes: cs329z

One meaning per symbol across U01-U04. Shapes use (rows, cols) or named axes. Scalars are lowercase, vectors bold lowercase, matrices bold uppercase.

## General

| Symbol | Meaning | Units/shape |
| --- | --- | --- |
| x | input text or token sequence | sequence of token ids |
| y | model output text or token sequence | sequence of token ids |
| z | logits over the vocabulary | R^V |
| V | vocabulary size | count, e.g. 32000 |
| T | temperature | positive scalar, dimensionless |
| p_i | probability of token i | dimensionless, sums to 1 |
| n | context length in tokens | count |
| d | model width (embedding dimension) | count |
| L | number of transformer layers | count |
| h | number of attention heads | count |
| theta | model parameters | parameter vector |
| D | dataset or document collection | set |
| q | query (text or vector) | text. Or R^d as vector |
| d_i | document i (U02 uses d for document, not width. Lesson disambiguates) | text. Or R^d as vector |
| s(q, d) | retrieval score of document d for query q | scalar |

## Attention (U01)

Q, K, V: query, key, value matrices, each (n, d_k) per head with d_k = d / h.
Attention(Q, K, V) = softmax(Q K^T / sqrt(d_k)) V, output (n, d_k) per head.
KV cache: stored K and V for past tokens, shape (L, 2, n, d) across the model.

## Retrieval (U02)

e(x): embedding of text x, R^d.
cos(a, b) = (a . b) / (||a|| ||b||), dimensionless in [-1, 1].
Top-k: the k documents with the largest s(q, d).
BM25(q, d): scalar lexical score from term frequency and inverse document frequency.

## Tools and protocols (U03)

f: a tool, a named function with a schema.
args: tool arguments, a JSON object.
obs: tool result (observation), JSON or text.
s_t: agent state at step t.
a_t: action at step t (tool call or final answer).
pi: policy mapping state to action distribution.
tau: timeout in seconds. R: retry count (integer).

## Frameworks and memory (U04)

S: DSPy signature, an input-output contract.
M: DSPy module, a parameterized program step.
Phi: compiled program after optimization.
G: workflow graph (nodes = calls, edges = data flow).
H_t: conversation history up to step t.
mem_S: short-term memory (working context). Mem_L: long-term memory (persistent store).
B: step or token budget, integer.

## Probability and evaluation

P(A): probability of event A. E[X]: expectation. Var(X): variance.
pass@k: probability that at least one of k samples passes, given per-sample pass rate p: 1 - (1 - p)^k under independence.
