# Prerequisites: cs329z

Shared bridges P01-P24 live at `~/workspace/stanford-frontier-ai/v2-pack/shared/prerequisites/`. Link, do not rebuild. Each unit below names its parent-level prerequisites from the inventory and the local remediation this course adds. Every lesson also opens with a local self-contained remediation section.

## Prerequisite graph for U01-U08

| Unit | Inventory prerequisites | Bridge content | Shared bridge files |
| --- | --- | --- | --- |
| U01 | P10, P14, P20 | ML foundations and evaluation. Transformer mechanics. Tools, APIs, and agent state | p10_ml_foundations.md, p14_transformer.md, p20_tools.md |
| U02 | P19, P21 | Retrieval and information access. Security, privacy, and safety | p19_retrieval.md, p21_security.md |
| U03 | P16, P20, P21 | Distributed systems and networking. Tools, APIs, and agent state. Security, privacy, and safety | p16_distributed.md, p20_tools.md, p21_security.md |
| U04 | P16, P20 | Distributed systems and networking. Tools, APIs, and agent state | p16_distributed.md, p20_tools.md |
| U05 | P09, P14, P17, P22 | Optimization. Transformer mechanics. Reinforcement learning. Experiments | p09_optimization.md, p14_transformer.md, p17_rl.md, p22_experiments.md |
| U06 | P07, P10, P22 | Statistical estimation. ML foundations and evaluation. Experiments | p07_estimation.md, p10_ml_foundations.md, p22_experiments.md |
| U07 | P20, P21, P24 | Tools, APIs, and agent state. Security, privacy, and safety. Production ML (P24 is a composite of P10/P16/P21/P22/P23, no dedicated file) | p20_tools.md, p21_security.md |
| U08 | P16, P22, P24 | Distributed systems and networking. Experiments. Production ML and economics (P24 is a composite, no dedicated file) | p16_distributed.md, p22_experiments.md, p23_economics.md |

Deep chain used inside lessons: P01 numeracy, P02 Python, P03 vectors, P06 probability, P07 estimation, P08 information, P10 ML foundations, P13 language, P14 transformer, P15 hardware, P16 distributed, P20 tools, P21 security, P22 experiments.

## Local remediation per unit

- U01: Bernoulli and softmax refresher (logits, temperature, normalization). Attention cost counting (O(n^2 d) with n context length, d model width). Train versus inference. Likelihood as a training objective. Taught inside `lessons/u01_lesson.md`.
- U02: cosine/dot/L2 refresher with a 2D toy, BM25 intuition (term frequency saturation, inverse document frequency). Precision and recall for retrieval. Ranking as sorting by score. Taught inside `lessons/u02_lesson.md`.
- U03: JSON and HTTP refresher. State machines (states, transitions, halting). Exponential backoff arithmetic. Authentication versus authorization split. Taught inside `lessons/u03_lesson.md`.
- U04: graphs and DAGs refresher.
- U05: averages as expectations, parameter counting, matrix rank, preference pairs, overfitting. Taught inside `lessons/u05_lesson.md`.
- U06: means, standard errors, correlations, win rates, nondeterminism. Taught inside `lessons/u06_lesson.md`.
- U07: trust boundaries, instruction hierarchy, capabilities, consent. Taught inside `lessons/u07_lesson.md`.
- U08: action spaces, spans, percentiles, ownership. Taught inside `lessons/u08_lesson.md`. The LLM call as a pure function of (prompt, parameters). Summary as lossy compression. Fixed-point iteration intuition for loops. Taught inside `lessons/u04_lesson.md`.

## Diagnostic (closed book, 20 minutes)

Answer in `diagnostics/diagnostic_keys.md`, kept separate.

D1. Write the softmax of logits [1.0, 2.0, 3.0] at temperature 1. Give each probability to two decimals.
D2. A transformer reads 4096 tokens with model width 1024. Estimate the attention FLOPs up to a constant factor.
D3. Two unit vectors have dot product 0.8. What is the angle between them in degrees, roughly?
D4. Define precision and recall for a retrieval system in one sentence each.
D5. Name the three MCP participant roles and the two transport mechanisms.
D6. A tool call fails with probability 0.2 per try, independently. After 3 tries with no backoff, what is the probability all three fail?
D7. Sketch the ReAct loop as three boxes with arrows. Label the arrows.
D8. What breaks first when an agent loop has no stopping rule? Name one concrete failure.

## How to use the diagnostic

Score each item 0/1. A score below 5 means: read the local remediation of the failed unit first, then the shared bridge, then the lesson. A score of 5 or above means: start the lessons and use remediation on demand. Do not infer mastery from reading. The diagnostic measures entry state only.
