---
page_id: cs329a-cheatsheet
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 900
nav: "CS329A · Cheatsheet"
title: "CS329A Cheatsheet"
summary: "Every key fact from CS329A on one dense page: definitions, numbers, mechanisms, failure modes, interview lines."
---

The whole course as a set of short stories. Each block tells one
idea the way the lesson tells it: the problem, the number, the
fix. Follow the links for the full derivations.

<div class="cheat-cols" markdown="1">

<div class="cheat-block" markdown="1">

### The loop

Generate many attempts. Verify automatically. Train on winners.
Repeat. Test-time compute makes data. Train-time compute absorbs
it. The verifier is the bottleneck: it must be fast and honest.
Slow or subjective domains stay outside the loop.
[L01](l01-self-improving-agents.html)

</div>

<div class="cheat-block" markdown="1">

### Test-time scaling

Coverage at k tries is 1-(1-p)^k. p=0.05: 10 tries give 40%,
100 give 99.4%. Log-linear in samples. Llama 3 8B with thousands
of verified samples beats GPT-4o-class at one try. DeepSeek v3
at 1,000 samples beats Claude 3.5 Sonnet and o1-preview on
SWE-bench-style tasks. Archon: composed inference systems,
+14.1% average pass@1 over frontier closed models. Price: pays
per question, needs the verifier at answer time.
[L02](l02-test-time-scaling.html)

</div>

<div class="cheat-block" markdown="1">

### ReAct

Thought, action, observation, repeat. Tools ground reasoning in
facts from the world. Price: compounding error. Ten 90%-reliable
steps give 0.9^10 = 35% task success. Poor tool choice grounds
the trace in wrong facts. Overthinking stalls. Underthinking
acts blind. Memory across tasks is named and unsolved.
[L03](l03-agents-that-act.html)

</div>

<div class="cheat-block" markdown="1">

### RLEF

Code has a free teacher: run it. Inference-time loop: try, read
test failure, retry. Train-time: PPO on binary reward from
hidden private tests. Public tests guide iteration. Private
tests grade, blocking memorization. Turn-level value: one
advantage for all tokens in the program. Price: sparse signal,
needs executable tests, failures teach nothing.
[L04](l04-learning-from-execution.html)

</div>

<div class="cheat-block" markdown="1">

### LATS

ReAct walks one path. LATS grows a tree. Six stages: select by
UCT, expand, evaluate (LLM-judge 0-1 plus self-consistency
frequency), simulate, backpropagate running averages, reflect in
words. UCT = value + c*sqrt(ln(parent visits)/node visits):
exploit plus explore. Toy: judge 0.6 + consistency 0.75 = 1.35.
Backprop (1.35*3+1)/4 = 1.26. Price: hundreds of model calls per
task. The judge can mislead the tree.
[L05](l05-planning-with-search.html)

</div>

<div class="cheat-block" markdown="1">

### AlphaCode to AlphaCode 2

10@k: generate k programs, submit at most 10. Clustering by
behavior buys diversity: 41B+clustering beats 41B beats 9B.
Log-linear in samples. Bigger models steeper slopes. Selection
bottleneck: unlimited pass@k passes 40%, 10@k stalls near 30%.
AlphaCode 2: fine-tune Gemini Pro family for diversity, learned
scoring model replaces heuristic clustering. Price: diversity
must keep growing with samples. Loss is a poor proxy for solve
rate.
[L06](l06-sampling-at-scale.html)

</div>

<div class="cheat-block" markdown="1">

### Deep research agents

Knowledge cutoffs plus silent guessing. Uncertainty words mark
gaps. Single-shot RAG dumps 10 documents and still fails.
Agentic RAG: search mid-reasoning per gap. Search-o1: reason in
documents, extract chunks, file notes not documents. Chemistry
toy: guess 14 wrong, dump wrong, search plus read 10 right.
Price: trigger heuristics miss gaps. Every search costs latency
and context.
[L07](l07-search-that-reads.html)

</div>

<div class="cheat-block" markdown="1">

### STaR

No reasoning data on the internet, so manufacture it. Attempt
10k problems, keep the 3k with correct answers, fine-tune,
repeat. Rationalization: for failures, hand the model the
answer as hint, keep the rationale, train without the hint.
Assumptions: correct answer implies good rationale. The model
can rationalize. The base can bootstrap. Price: unfiltered
rationales bake in bad reasoning. Needs answer keys. Negatives
teach nothing. Industrial form: DeepSeekMath with GRPO.
[L08](l08-teaching-reason.html)

</div>

<div class="cheat-block" markdown="1">

### The verifier bottleneck

Outcome rewards approve right answers with broken reasoning.
LLM-as-judge certifies invalid proofs as valid. DeepSeek-Math
V2: meta-verifier judges the judge, generator and verifier lift
each other. 8 iterations climbing, best-of-32 reaches 42% proof
score on IMO 2024 shortlist. Multi-agent debate: generators
plus critic keep chains diverse where single-agent fine-tuning
collapses. Gains transfer to adjacent domains. Price:
human-seeded standards. Slow domains (chip sims, wet labs)
have no fast judge. Stand-in reward models invite hacking.
[L09](l09-verifier-bottleneck.html)

</div>

<div class="cheat-block" markdown="1">

### Measuring agents

METR time horizon at 50% success doubles every 7 months: 2
seconds (GPT-2, 2019), 8 minutes (GPT-4, 2023), 59 minutes
(Claude 3.7, 2025). At 80% success the frontier drops to about
15 minutes. Failure modes: poor planning, poor tool choice, no
error recovery, lost goal state. Open problems: diversity,
verifiers, curriculum, non-verifiable domains, cost of
intelligence.
[L10](l10-measuring-agents.html)

</div>

</div>

## Interview lines

- "Test-time compute is a real axis: coverage is 1-(1-p)^k, log-linear in samples, and small models with verification beat giants at one try."
- "ReAct grounds reasoning in tool observations, but reliability compounds: 0.9^10 is 35 percent."
- "RLEF's two-tier tests block memorization: public tests for iteration, hidden tests for reward."
- "LATS replaces greedy trajectories with tree search: UCT balances exploiting good branches against exploring rare ones."
- "AlphaCode's binding constraint is selection, not generation: 10@k stalls near 30 percent while unlimited attempts pass 40."
- "STaR bootstraps reasoning from answer keys, but correct answers do not imply correct reasoning, which is the leak process rewards must fix."
- "The verifier is the bottleneck behind every loop: outcome checks are blind, model judges are gullible, and the meta-verifier judges the judge."
- "Capability doubles every 7 months. 80-percent reliability lags years behind 50-percent capability."
