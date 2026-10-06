---
page_id: cs329a-cheatsheet
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 900
nav: "CS329A · Cheatsheet"
title: "CS329A Cheatsheet"
summary: "Every key fact from CS329A on one dense page: definitions, numbers, mechanisms, failure modes, interview lines, memory aids, and self-tests."
---

The whole course as a set of short stories. Each block tells one
idea the way the lesson tells it: the problem, the number, the
fix. Follow the links for the full derivations.

![The course on one plate](assets/plate-crash-flywheel.svg "Generate, verify, train. Each lecture strengthens one stage or names its price. Shell 4. Source: original. Project: Stanford Frontier AI.")

![The numbers that matter](assets/plate-crash-numbers.svg "Every number on this plate is computed or lecture-reported in the lessons. Shell 2. Source: lessons. Project: Stanford Frontier AI.")

<div class="cheat-cols" markdown="1">

<div class="cheat-block" markdown="1">

### The loop

Generate many attempts. Verify automatically. Train on winners.
Repeat. Test-time compute makes data. Train-time compute absorbs
it. The verifier is the bottleneck: it must be fast, automatic,
and honest. Slow or subjective domains stay outside the loop.
Mnemonic: **GVT**, generate, verify, train.
[L01](l01-self-improving-agents.html)

</div>

<div class="cheat-block" markdown="1">

### Test-time scaling

Coverage at k tries is 1-(1-p)^k. p=0.05: 10 tries give 40%,
100 give 99.4%. Log-linear in samples. Llama 3 8B with thousands
of verified samples beats GPT-4o-class at one try. DeepSeek v3
at 1,000 samples beats Claude 3.5 Sonnet and o1-preview on
SWE-bench-style tasks. Majority vote plateaus at 10-50 samples:
the generation-verification gap. Archon: generators, critic,
ranker, fuser, tuned by search, +14.1% average pass@1 over
frontier closed models, open models only. Price: pays per
question, needs the verifier at answer time.
[L02](l02-test-time-scaling.html)

</div>

<div class="cheat-block" markdown="1">

### ReAct

Thought, action, observation, repeat. Mnemonic: **TAO**. Tools
ground reasoning in facts from the world. Paper numbers:
ALFWorld +34 points absolute, WebShop +10, best trial 71%, from
1-2 examples. Price: compounding error. Ten 90%-reliable steps
give 0.9^10 = 35% task success. Poor tool choice grounds the
trace in wrong facts. Tool descriptions are prompts, not docs.
Overthinking stalls. Underthinking acts blind. Memory across
tasks is named and unsolved.
[L03](l03-agents-that-act.html)

</div>

<div class="cheat-block" markdown="1">

### RLEF

Code has a free teacher: run it. Inference-time loop: try, read
test failure, retry. Train-time: PPO on binary reward from
hidden private tests. Public tests guide iteration. Private
tests grade, blocking memorization. Turn-level value: one
advantage for all tokens in the program. PPO's clip caps each
update for stability. Price: sparse signal, needs executable
tests, failures teach nothing, never start from a model that
passes nothing.
[L04](l04-learning-from-execution.html)

</div>

<div class="cheat-block" markdown="1">

### LATS

ReAct walks one path. LATS grows a tree. Six stages, mnemonic
**SEESBR**: select by UCT, expand, evaluate, simulate,
backpropagate, reflect. Evaluate: LLM-judge 0-1 plus
self-consistency frequency. Toy: judge 0.6 + consistency 0.75
= 1.35. Backprop (1.35*3+1)/4 = 1.26. UCT = value +
c*sqrt(ln(parent visits)/node visits): exploit plus explore.
Toy: 2.13 beats 1.55. SPRINT: parallel plan-execute baked in.
SWiRL: process rewards before tools answer, transfers across
tools. Price: hundreds of model calls per task. The judge can
mislead the tree. Irreversible actions out of scope.
[L05](l05-planning-with-search.html)

</div>

<div class="cheat-block" markdown="1">

### AlphaCode to AlphaCode 2

10@k: generate k programs, submit at most 10. Example tests
remove ~95%. Clustering by behavior buys diversity: 41B plus
clustering beats 41B beats 9B. Log-linear in samples. Bigger
models steeper slopes. Selection bottleneck: unlimited pass@k
passes 40%, 10@k stalls near 30%. AlphaCode 2: fine-tune Gemini
Pro family for diversity, learned scoring model replaces
heuristic clustering. 100 samples matched AlphaCode's million.
~85% of Codeforces participants beaten. Price: diversity must
keep growing with samples. Loss is a poor proxy for solve rate.
Breadth for one-artifact problems, depth for dependent steps.
[L06](l06-sampling-at-scale.html)

</div>

<div class="cheat-block" markdown="1">

### Deep research agents

Knowledge cutoffs plus silent guessing. Uncertainty words
("perhaps", "wait") mark gaps. Single-shot RAG dumps 10
documents and still fails. Agentic RAG: search mid-reasoning
per gap, query the gap not the question. Search-o1: reason in
documents, extract chunks, file notes not documents. Chemistry
toy: guess 14 wrong, dump wrong, search plus read 10 right.
Context length is not reasoning capacity. Price: trigger
heuristics miss gaps both ways. Every search costs latency and
context. Stop when chunks stop changing the answer.
[L07](l07-search-that-reads.html)

</div>

<div class="cheat-block" markdown="1">

### STaR

No reasoning data on the internet, so manufacture it. Attempt
10k problems, keep the 3k with correct answers, fine-tune,
repeat. Rationalization: for failures, hand the model the
answer as hint, keep the rationale, train without the hint.
Construction is easier than search. Assumptions: correct answer
implies good rationale (the live wire), the model can
rationalize, the base can bootstrap. Price: unfiltered
rationales bake in bad reasoning. Needs answer keys. Negatives
teach nothing. Industrial form: DeepSeekMath (120B curated
tokens, 51.7% MATH at 7B) with GRPO (group-relative
advantages, majority@K not pass@K). DAPO: dynamic sampling,
watch entropy and response length.
[L08](l08-teaching-reason.html)

</div>

<div class="cheat-block" markdown="1">

### The verifier bottleneck

Outcome rewards approve right answers with broken reasoning.
LLM-as-judge certifies invalid proofs as valid. DeepSeek-Math
V2: meta-verifier judges the judge, generator and verifier lift
each other. 8 iterations climbing, best-of-32 reaches 42% proof
score on IMO 2024 shortlist. Absolute Zero: no answer keys,
model proposes its own tasks scored by learnability
(1 - success rate), verified by execution. Multi-agent debate:
generators plus critic keep chains diverse where single-agent
fine-tuning collapses. Gains transfer to adjacent domains.
Weaver: filter weak verifiers, weight on ~1% labels, distill
small. Price: human-seeded standards. Slow domains (chip sims,
wet labs) have no fast judge. Stand-in reward models invite
hacking.
[L09](l09-verifier-bottleneck.html)

</div>

<div class="cheat-block" markdown="1">

### Measuring agents

METR time horizon at 50% success doubles every 7 months: 2
seconds (GPT-2, 2019), 8 minutes (GPT-4, 2023), 59 minutes
(Claude 3.7, 2025). At 80% success the frontier drops to about
15 minutes. 50% is not deployable. Failure modes: poor
planning, poor tool choice, no error recovery, lost goal state
(the unsolved one). GDPval: instruction following fails on
expert tasks. DeepScholar: no system above 19%, fluency trades
off against verifiability. Open problems: diversity,
verifiers, curriculum, non-verifiable domains, cost of
intelligence. Intelligence per watt: local <=20B models cover
most chat queries.
[L10](l10-measuring-agents.html)

</div>

</div>

## One-glance decision tables

### Which method for which problem

| Your problem | Reach for | Why |
|---|---|---|
| Answers exist but one try misses them | Repeated sampling + verifier (L02) | Log-linear coverage, cheapest capability gain |
| Model cannot check facts or run code | ReAct (L03) | Grounds each step in tool observations |
| Coding agent must improve itself | RLEF (L04) | Execution is a free, honest teacher |
| One path keeps failing, need alternatives | LATS (L05) | Tree keeps untried branches alive |
| Competition coding, one program per problem | AlphaCode pattern (L06) | Breadth + learned selector |
| Knowledge cutoff, silent guesses | Agentic search (L07) | Fill gaps mid-thought, read the docs |
| No reasoning data, but answer keys exist | STaR (L08) | Manufactures rationales from answers |
| Verifier is weak or learned | Meta-verifier / Weaver / debate (L09) | Judge the judge, maintain diversity |
| "Is it ready to deploy?" | METR-style eval at 80% (L10) | 50% capability is not reliability |

### Test-time vs train-time, fast lookup

| | Test-time compute | Train-time compute |
|---|---|---|
| Weights | Fixed | Change |
| Examples | Sampling, traces, tools, search | Fine-tuning, RL on winners |
| Pays | Per question, forever | Once, up front |
| Needs | Verifier at answer time | Verifier during training |
| Fails when | No checkable answer | No training signal |

## Never-confuse pairs

- **Coverage vs pass@k.** Coverage: at least one of k solves it, oracle assumed. Pass@k: the same, verifier folded in. Same curve, different honesty about the judge.
- **Test-time vs train-time compute.** Test-time: weights fixed, answers improve per question. Train-time: weights change, answers get cheaper forever after.
- **Outcome vs process reward.** Outcome: checks the ending, cheap, blind to broken steps. Process: checks the steps, expensive, mostly does not exist yet.
- **ReAct vs chain of thought.** CoT: reasoning only, inside the box. ReAct: reasoning interleaved with tool actions, outside contact.
- **Generation vs selection.** Generation: is the winner in the set (coverage). Selection: can the filter pick it (10@k). The bottleneck moved from the first to the second.
- **Verifier vs reward model.** Verifier: any judge, including answer keys and tests. Reward model: a learned verifier, gameable, the hacking risk.
- **Majority@K vs pass@K.** Majority@K: the most common answer is right (consistency). Pass@K: any of K is right (capability). GRPO improves the first, not the second.
- **50% horizon vs 80% horizon.** 50%: capability trend, steep. 80%: deployability, lags years behind.

## If-this-then-that rules

- If samples are not diverse, then the effective k is the cluster count, not the sample count. Stop sampling, fix the generator.
- If the verifier is learned, then hold out a trusted check the loop cannot see. Rising loop scores with a flat held-out check means hacking.
- If the task has irreversible actions, then tree search is out. Simulate or do not search.
- If every training prompt is all-pass or all-fail, then the batch carries no gradient. Drop them (DAPO's rule).
- If entropy falls while loss falls, then the policy is collapsing. Stop, do not celebrate.
- If response length grows with flat scores, then the model is padding, not reasoning.
- If the question is easy, then spend 1-2 samples. If hard, then sequential revision beats parallel sampling.
- If the judge must be fast, then answer keys and tests qualify, learned judges risk honesty, humans do not qualify at all.
- If deploying, then measure at 80% success, not 50%. 50% is a research result.
- If the trigger fires constantly, then calibrate it: keep only searches that change answers.

## Interview lines

- "Test-time compute is a real axis: coverage is 1-(1-p)^k, log-linear in samples, and small models with verification beat giants at one try."
- "ReAct grounds reasoning in tool observations, but reliability compounds: 0.9^10 is 35 percent."
- "RLEF's two-tier tests block memorization: public tests for iteration, hidden tests for reward."
- "LATS replaces greedy trajectories with tree search: UCT balances exploiting good branches against exploring rare ones."
- "AlphaCode's binding constraint is selection, not generation: 10@k stalls near 30 percent while unlimited attempts pass 40."
- "Agentic search queries the gap, not the question, and files notes, not documents: context length is not reasoning capacity."
- "STaR bootstraps reasoning from answer keys, but correct answers do not imply correct reasoning, which is the leak process rewards must fix."
- "GRPO sharpens the distribution without widening it: majority@K up, pass@K flat. More consistent, not smarter."
- "The verifier is the bottleneck behind every loop: outcome checks are blind, model judges are gullible, and the meta-verifier judges the judge."
- "Capability doubles every 7 months. 80-percent reliability lags years behind 50-percent capability. 50% is not deployable."
