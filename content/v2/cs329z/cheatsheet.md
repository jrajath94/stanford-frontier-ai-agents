---
page_id: cs329z-cheatsheet
course_slug: cs329z
course_name: "CS329Z: Engineering AI Agents"
course_order: 7
order: 900
nav: "CS329Z · Cheatsheet"
title: "CS329Z Cheatsheet"
summary: "Every key fact from CS329Z on one dense page: definitions, numbers, decisions, mistakes, interview lines."
---

The whole course as one-glance tables. Each block holds the numbers
and the decision rules. Follow the links for the derivations.

<div class="cheat-cols" markdown="1">

<div class="cheat-block" markdown="1">

### The agent loop

| Step | Does | Skipped means |
|---|---|---|
| Perceive | read task + world state | acts on stale state |
| Plan | Thought: choose the next step | no recovery from failure |
| Act | tool call, message, answer | nothing touches the world |
| Observe | read what came back | blind next step |
| Check | named test: goal met? | runs until budget dies |

0.9^4 = 0.66: four steps at 90% each. Termination: check passes,
budget dies, or the model declares done. ReAct: Thought/Act/Observe.
Thought 3 diagnoses, extracts, replans. [Lecture 1](l01-intro-agentic-systems.html)

</div>

<div class="cheat-block" markdown="1">

### Loop patterns

| Pattern | Edit to the loop | Wins when |
|---|---|---|
| ReAct | Thought between acts | facts live in the world |
| Plan-and-execute | plan is a document | task decomposes up front |
| Handoff | delegate = tool call | one prompt would need two jobs |
| Reflexion | failure becomes text hint | repeated tries, verbal feedback |
| Debate | N agents argue, judge picks | errors uncorrelated |
| Self-consistency | many paths, majority vote | no tools, no verifier |

</div>

<div class="cheat-block" markdown="1">

### Tool calling done right

Select, Arguments, Validate, Execute. Validate is load-bearing:
{"path": ["test.py"]} dies there, not in the sandbox. Errors return
as data, never as exceptions: the model routes around what it can
read. Retry transient failures only: backoff 1s/2s/4s, max 3, then
dead-letter. The 87% pop-up attack works on untrusted tool output
read as instruction. MCP: 5 x 8 = 40 integrations become 5 + 8 = 13.
Transport, not trust. [Lecture 1](l02-compound-ai-systems.html)

</div>

<div class="cheat-block" markdown="1">

### Tool design rules

One job per tool. Typed narrow arguments. Errors as data. Idempotent
where possible. Names the model can spell. Few sharp tools (Pi: read,
write, edit, bash) beat fifty dull ones. The description is a prompt:
it says when to reach for this tool.

</div>

<div class="cheat-block" markdown="1">

### The sampling math

| Setting | [0.7, 0.2, 0.1] becomes | Use for |
|---|---|---|
| T = 0.5 | [0.91, 0.07, 0.02] | acting: tool calls steady |
| T = 1 | unchanged | default |
| T = 2 | [0.52, 0.28, 0.20] | thinking: plans need variety |

Logits -> scale by T -> softmax -> truncate (top-k/top-p) -> sample.
Set T and top-p as a pair. Loss = -log p(true token): the toy gives
-log10(0.0124) = 1.907. [Lecture 2](l03-llms-for-builders.html)

</div>

<div class="cheat-block" markdown="1">

### The cost model

Attention O(n^2): 16.7M scores per layer per head at n = 4096. KV
cache = 2 x layers x tokens x dims x bytes: 2.0 GiB at 32 layers,
4096 tokens, fp16. Prefill: parallel, compute-bound. Decode: one
token at a time, memory-bound. Every context token is bandwidth per
step. Speculative decoding: draft cheap, verify in one pass. Wins on
predictable structured output.

</div>

<div class="cheat-block" markdown="1">

### Training ladder

| Rung | Teaches | Trap |
|---|---|---|
| Pretrain | next-token on web text | the corpus is the ceiling |
| Midtrain | domain mix (code, math) | - |
| SFT | format: follow instructions | format, not judgment |
| RLHF/DPO | human preferences | sycophancy: annotators like confident agreeable answers |
| RLVR | verifiable rewards (tests) | weak verifier teaches reward hacking |
| Agent train | synthesized tasks + sandbox | - |

</div>

<div class="cheat-block" markdown="1">

### Spend compute at inference

The jacket: +25% then -25% is not $80. $80 x 1.25 = $100, $100 x
0.75 = $75. Chain of thought is working memory, not intelligence.
Effort dial: low/medium/high per step. Kimi K3: +1 correct, 0 wrong,
-1 wrong and over budget. Repeated sampling: 1 - 0.7^10 = 0.97
coverage at 0.3 per sample. Sampling is cheap. The verifier is the
scarce resource. Outcome reward checks the answer. Process reward
checks each step (needs step labels). [Lecture 2](l04-reasoning-and-context.html)

</div>

<div class="cheat-block" markdown="1">

### Constrain the shape, engineer the context

Constrained decoding: grammar masks forbidden tokens. Output always
parses. Shape, not meaning. DSPy: signature declares, compiled prompt
implements. Context rot: distractors degrade reasoning (OOLONG).
Defenses: few tools, retrieve on demand, compact. KV cache is
positional: append, never edit. Compaction keeps goal, open loops, key
facts. The keep-or-drop dilemma is empirical. [Lecture 2](l04-reasoning-and-context.html)

</div>

<div class="cheat-block" markdown="1">

### RAG in one formula

p(y|x) = sum p(z|x) p(y|x,z). Toy: 0.7 x 0.9 + 0.3 x 0.2 = 0.69. The
trusted passage dominates. RAG-Sequence: one passage per answer.
RAG-Token: re-pick per token. Chunk: 200-400 tokens, 10-20% overlap.
read ten chunks by hand. Embeddings: 768 numbers per chunk. The
retriever measures distances. Vector store: embed offline, query live.
Contextual retrieval: LLM prefix per chunk (one call each). Late
chunking: embed doc, pool per span (no call, needs long encoder).
RAPTOR: tree for spread-out answers. GraphRAG: index relationships.
[Lecture 3](l05-rag-pipeline.html)

</div>

<div class="cheat-block" markdown="1">

### The retriever zoo

| Retriever | Latency | Wins on | Breaks on |
|---|---|---|---|
| BM25 | 62 ms | exact terms, no training | paraphrase |
| DPR | tens of ms | semantic, 1k pairs beats BM25 | rare literals |
| ColBERT | 458 ms | token-level evidence | token-sized index |
| Cross-encoder | 10,700 ms / 1k | accuracy on shortlist | cannot scan corpus |
| HNSW | ms | ANN at billions of vectors | a little recall |

BM25: IDF 5.65 ("ACME") vs 2.93 ("revenue"). 10 mentions score 1.96
not 10. RRF: 0.0323 beats 0.0320. Fuse ranks not scores. MRR for
one-passage readers. Recall for synthesizers. Failed@k for empty
queries. [Lecture 3](l06-retrieval-methods.html)

</div>

<div class="cheat-block" markdown="1">

### Agentic retrieval fails with numbers

Query 2 is born from observation 1. The loop owns whether, what, and
when to stop. Nine failures: compounding (0.95^20 = 0.36), no
stopping rule (2,000 x 25 = 50,000 tokens), injection (87%, steers the
next hop), recall ceiling (0.8 caps all), stale index, permission
leak (fix at retrieval time), lost-in-the-middle, distraction,
evidence conflict (resolve: newer, primary, or tiebreaker).
[Lecture 3](l07-agentic-retrieval-failure-modes.html)

</div>

<div class="cheat-block" markdown="1">

### Evaluate the other nine runs

Consistency 7/10. Robustness 4/10 on rephrasing. Legibility: run 6
called a refund tool it should never touch. SWE-bench: 2,294 issues.
FAIL_TO_PASS must flip, PASS_TO_PASS must hold. Claude 2 4.8% (2023).
GAIA: 466 questions. Humans 92%, GPT-4 + plugins 15%. Judge wrong 15
times in 100: calibrate on humans first. Never claim a 2-point win.
Humans cost 17 hours per 100 tasks. Goodhart: the metric becomes the
target. Sandbox the grader. Score the trace. Print cost, latency,
safety next to every score. [Lecture 4](l08-evaluating-agents.html)

</div>

<div class="cheat-block" markdown="1">

### Never-confuse pairs

| Do not confuse | Because |
|---|---|
| Observation vs check | observation is raw; check is the verdict |
| RAG-Sequence vs RAG-Token | one passage per answer vs re-pick per token |
| Outcome vs process reward | answer check vs step check |
| Recall vs MRR | find all vs first rank |
| BM25 vs DPR failure | paraphrase vs rare literals |
| Self-RAG vs CRAG | decide to retrieve vs repair retrieval |
| Consistency vs robustness | same task twice vs rephrased task |

</div>

<div class="cheat-block" markdown="1">

### If-this-then-that

- If the answer needs no external facts -> chain-of-thought, not ReAct.
- If {"path": ["test.py"]} -> it dies at validate, before the sandbox.
- If a tool fails transiently -> append as result, backoff, max 3.
- If the context fills -> compact to goal + open loops + key facts.
- If the retriever's recall is 0.8 -> the system caps at 0.8.
- If two passages disagree -> resolve (newer, primary, tiebreaker).
- If no verifier exists -> vote (self-consistency), do not sample blind.
- If the judge is uncalibrated -> its scores are stories, not numbers.

</div>

</div>

<div class="cheat-block" markdown="1">

### Go deeper

- Yao et al., ReAct (2022): https://arxiv.org/abs/2210.03629 : the Thought/Act/Observe loop and its measurements.
- Shinn et al., Reflexion (2023): https://arxiv.org/abs/2303.11366 : verbal reinforcement from failed runs.
- Lewis et al., RAG (2020): https://arxiv.org/abs/2005.11401 : the original retrieve-then-generate recipe.
- Barnett et al. (2024): https://arxiv.org/abs/2401.05856 : seven failure points of RAG engineering.
- Asai et al., Self-RAG (2023): https://arxiv.org/abs/2310.11511 : retrieve, generate, and critique through self-reflection.
- Brown et al., Large Language Monkeys (2024): https://arxiv.org/abs/2407.21787 : inference compute keeps helping far past intuition.
- Wei et al., Chain-of-Thought (2022): https://arxiv.org/abs/2201.11903 : the scratch pad that started it all.
- HarnessAudit: https://harnessaudit.github.io : agent scaffold auditing.

</div>
