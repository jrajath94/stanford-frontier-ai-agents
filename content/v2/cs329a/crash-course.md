---
page_id: cs329a-crash
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 901
nav: "CS329A · Crash course"
title: "CS329A Crash Course"
summary: "Interview-speed review of CS329A: the full self-improvement story in 30 minutes, with links into the deep lessons."
---

<span class="crash-timer">30 minutes · interview speed</span>

This page tells the whole self-improvement story fast. Each
section gives you the working version: enough to answer
interview questions with confidence. Links at the end of each
section take you into the full lesson when you want the
derivations and the follow-ups.

<div class="crash-section" markdown="1">

### 1. The loop that defines the course

One-shot answers waste what the model knows. A small model
sampled 10,000 times with a verifier solves IMO-level problems
it fails at one try. The course's engine: generate many
attempts, verify automatically, train on the winners, repeat.
Test-time compute manufactures data. Train-time compute absorbs
it. The verifier is the load-bearing wall: it must be fast and
honest, and slow or subjective domains stay outside the loop.

<ul class="crash-links">
<li><a href="l01-self-improving-agents.html">Lecture 1: the self-improving agent</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 2. Ask again and again

Coverage at k tries is 1-(1-p)^k. A 5-percent-per-try model
reaches 40 percent at 10 tries and 99.4 at 100. The curve is
log-linear in samples. Llama 3 8B with thousands of verified
samples outperforms GPT-4o-class models at one attempt.
DeepSeek v3 at 1,000 samples beats Claude 3.5 Sonnet and
o1-preview on SWE-bench-style tasks. Archon goes further:
compose generators, critics, and fusers into a tuned
inference-time system, +14.1% average pass@1 over frontier
closed models with open models only. The price: the model
never improves, so every question pays the sampling bill
again.

<ul class="crash-links">
<li><a href="l02-test-time-scaling.html">Lecture 2: test-time scaling</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 3. Give the model hands

A closed-box model cannot check facts or run code. ReAct
interleaves thought, action, and observation: the model
reasons, calls a tool, reads the result, and continues. Each
step is grounded in what the world says back. The price is
compounding error: ten 90-percent steps give 0.9^10 = 35
percent task reliability. Wrong tool choice grounds the trace
in wrong facts, and current models overthink simple tasks.

<ul class="crash-links">
<li><a href="l03-agents-that-act.html">Lecture 3: agents that act</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 4. Learn from running code

Code has a free teacher: execution. RLEF runs an inference-time
loop, try, read the test failure, retry, and a train-time loop,
PPO on binary rewards. The two-tier test design is the key
honesty mechanism: public tests guide iteration, hidden private
tests decide the reward, so the model cannot memorize answers.
Credit is turn-level: one advantage value for every token in
the program. The price: sparse signal, tests required, and
failures teach nothing.

<ul class="crash-links">
<li><a href="l04-learning-from-execution.html">Lecture 4: learning from execution</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 5. Search the plan space

ReAct walks one path with no way back. LATS grows a tree of
plans and searches it: select by UCT, expand, evaluate, simulate,
backpropagate, reflect. Node value mixes an LLM-judge score with
self-consistency frequency. UCT adds an exploration bonus for
rarely visited nodes. Reflection appends verbal lessons from
failed runs to context. The price: hundreds of model calls per
task, and a miscalibrated judge misdirects the whole tree.

<ul class="crash-links">
<li><a href="l05-planning-with-search.html">Lecture 5: planning with search</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 6. Sample at massive scale, then select

AlphaCode generates up to a million programs per problem but may
submit 10: the 10@k metric. Clustering by behavior buys
diversity so the 10 submissions cover 10 approaches. Solve rates
rise log-linearly. 41B plus clustering beats 41B beats 9B. The
binding constraint is selection: unlimited attempts pass 40
percent, 10 submissions stall near 30. AlphaCode 2 learns the
selector, a reward model trained to predict correctness, and
fine-tunes a diverse family of base models. The price: gains
continue only while new samples stay diverse.

<ul class="crash-links">
<li><a href="l06-sampling-at-scale.html">Lecture 6: sampling at scale</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 7. Search in the middle of thinking

Reasoning models have knowledge cutoffs and silent gaps, marked
by hedging words like "perhaps" and "wait". Single-shot RAG
retrieves once and dumps documents. In the lecture's chemistry
toy it still fails. Agentic RAG searches mid-reasoning whenever
a gap appears. Search-o1 adds a reading step: extract the
relevant chunks, put notes in the prompt, not documents. Result:
the right carbon count. The price: heuristic triggers that miss
gaps, and a context budget that every search spends.

<ul class="crash-links">
<li><a href="l07-search-that-reads.html">Lecture 7: search that reads</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 8. Manufacture reasoning data

The internet has no step-by-step reasoning traces at scale, so
STaR makes them: attempt 10,000 problems, keep the 3,000 with
correct answers, fine-tune, repeat. Rationalization rescues the
failures: hand the model the answer as a hint, keep the
rationale, train without the hint. Three assumptions: correct
answers imply good rationales, the model can rationalize, the
base can bootstrap. The leak: no filter on rationale quality,
so broken steps that reach right answers get baked in. The
industrial form is DeepSeekMath with GRPO.

<ul class="crash-links">
<li><a href="l08-teaching-reason.html">Lecture 8: teaching the model to reason</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 9. Judge the judge

Outcome rewards approve right answers with broken reasoning.
LLM-as-judge certifies invalid proofs as valid. DeepSeek-Math
V2 adds a meta-verifier that audits the verifier: do the
claimed proof issues exist, does the score follow? Generator
and verifier then lift each other, 8 iterations climbing,
best-of-32 reaching 42% on the IMO 2024 shortlist. Separately,
multi-agent debate fine-tuning keeps reasoning chains diverse
where single-agent training collapses, and the gains transfer
to new domains. The price: human-seeded standards, multiplied
cost, and no answer for domains with slow verifiers.

<ul class="crash-links">
<li><a href="l09-verifier-bottleneck.html">Lecture 9: the verifier bottleneck</a></li>
</ul>

</div>

<div class="crash-section" markdown="1">

### 10. Measure what matters

The METR time horizon at 50% success doubles every 7 months: 2
seconds in 2019, 8 minutes in 2023, 59 minutes in 2025. But at
80% success the frontier is about 15 minutes: capability is
years ahead of reliability. Failure modes: poor planning, poor
tool choice, no error recovery, lost goal state. The open
problems: reasoning diversity, verifiers, curriculum,
non-verifiable domains, and the cost of intelligence.

<ul class="crash-links">
<li><a href="l10-measuring-agents.html">Lecture 10: measuring agents</a></li>
</ul>

</div>
