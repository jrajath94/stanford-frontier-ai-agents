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

The whole course as a set of short stories. Each block tells one
idea the way the lesson tells it: the problem, the number, the
fix. Follow the links for the full derivations.

<div class="cheat-cols" markdown="1">

<div class="cheat-block" markdown="1">

### The agent loop

Perceive, decide, act, observe, check. Reason-only hallucinates the
Apple Remote as "iPhone, iPad, iPod Touch". Act-only dies on the
first unexpected screen. ReAct interleaves: 4 acts, 3 observations,
Thought 3 recovers from the wrong remote. Four tool calls at 0.9
reliability survive at 0.9^4 = 0.66. The check step is the whole
difference between a demo and a system. [Lecture 1](l01-intro-agentic-systems.html)

</div>

<div class="cheat-block" markdown="1">

### Tool calling done right

Select, Arguments, Validate, Execute. The crack: an argument of
{"path": ["test.py"]} sails through and the tool fails late.
Validate before executing, never after. The 87% pop-up attack works
because the agent executes untrusted tool output as instruction.
Treat tool results as data, never as instructions. [Lecture 1](l02-compound-ai-systems.html)

</div>

<div class="cheat-block" markdown="1">

### The sampling math

Temperature rescales before the softmax. On [0.7, 0.2, 0.1]: T=0.5
sharpens to [0.91, 0.07, 0.02]; T=2 flattens to [0.52, 0.28, 0.20].
Training minimizes cross-entropy, which is negative log-likelihood:
the toy gives -log10(0.0124) = 1.907. Attention at n=4096 computes
16.7M scores: quadratic. Decode is bandwidth bound, so make the
model smaller, not the math different. [Lecture 2](l03-llms-for-builders.html)

</div>

<div class="cheat-block" markdown="1">

### Spend compute at inference

The jacket: +25% then -25% is not $80. $80 x 1.25 = $100, $100 x
0.75 = $75. Chain of thought is working memory, not intelligence:
each step is a checkable claim. Kimi K3's effort reward: +1
correct, 0 wrong, -1 wrong and over budget. The -1 teaches the
budget. Repeated sampling: at 0.3 success per sample, 1 - 0.7^10 =
0.97 coverage. The verifier is the scarce resource. [Lecture 2](l04-reasoning-and-context.html)

</div>

<div class="cheat-block" markdown="1">

### Constrain the shape, engineer the context

Constrained decoding masks forbidden tokens at generation time:
output always parses, but shape is not meaning. DSPy signatures
declare the contract; the compiled prompt implements it. Context
rot is measured: distractors degrade reasoning. Pi ships four
tools; fetch the rest on demand. The KV cache is positional, so
append, never edit. Compaction keeps goals, open loops, and key
facts; the keep-or-drop dilemma is empirical. [Lecture 2](l04-reasoning-and-context.html)

</div>

<div class="cheat-block" markdown="1">

### RAG in one formula

p(y|x) = sum p(z|x) p(y|x,z). The toy: 0.7 x 0.9 + 0.3 x 0.2 =
0.69; the trusted passage dominates. Training is a memory tax:
stale (retrain weekly?), no citation, lossy (reconstructions, not
rows). Retrieval is dynamic, exact, checkable. The retriever's
miss is the reader's ceiling. [Lecture 3](l05-rag-pipeline.html)

</div>

<div class="cheat-block" markdown="1">

### Chunking and indexing

200 to 400 tokens, 10 to 20% overlap, then measure. Too small
loses context; too large blurs topics. Read ten chunks by hand
before tuning. Contextual retrieval: an LLM writes a situating
prefix per chunk (one call each). Late chunking: embed the
document, pool per span (no LLM call, needs a long-context
encoder). RAPTOR builds a tree for spread-out answers; GraphRAG
indexes the relationships. [Lecture 3](l05-rag-pipeline.html)

</div>

<div class="cheat-block" markdown="1">

### The retriever zoo

BM25: IDF rewards rarity ("ACME" 5.65 vs "revenue" 2.93),
frequency saturates (10 mentions score 1.96, not 10). 62 ms, no
training. DPR: meaning as a dot product, beats BM25 on 4 of 5
datasets with 1,000 QA pairs, misses rare literals. ColBERT:
MaxSim over tokens, token-sized index, 458 ms. Cross-encoder:
10,700 ms per 1k passages, shortlists only. RRF fuses ranks:
0.0323 beats 0.0320, consensus wins. [Lecture 3](l06-retrieval-methods.html)

</div>

<div class="cheat-block" markdown="1">

### Agentic retrieval fails with numbers

Query 2 is born from observation 1: "CEO since 2019" arrives, then
"World Series host 2019" is written. The loop owns whether, what,
and when to stop. Nine failures: compounding error (0.95^20 =
0.36), no stopping rule (2,000 tokens x 25 rounds = 50,000),
injection (87%, steering the next hop), recall ceiling,
staleness, permission leaks, lost-in-the-middle, distraction,
evidence conflict. [Lecture 3](l07-agentic-retrieval-failure-modes.html)

</div>

<div class="cheat-block" markdown="1">

### Evaluate the other nine runs

Consistency 7/10, robustness 4/10 on rephrasing, legibility: run 6
called a refund tool it should never touch. SWE-bench: 2,294 real
GitHub issues; FAIL_TO_PASS must flip, PASS_TO_PASS must hold;
Claude 2 resolved 4.8% in 2023. GAIA: 466 questions, humans 92%,
GPT-4 with plugins 15%. The judge is wrong 15 times in 100;
humans cost 17 hours per 100 tasks. Goodhart: the metric becomes
the target. Sandbox the grader. [Lecture 4](l08-evaluating-agents.html)

</div>

</div>
