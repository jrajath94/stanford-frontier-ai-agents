---
page_id: cs329a-l02
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 2
nav: "L02 · Test-Time Compute Scaling"
title: "Lecture 2: Test-Time Compute Scaling"
summary: "Large Language Monkeys: coverage as a power law, the long tail of hard problems, the generation-verification gap. Then the optimal way to spend a test-time budget: when parallel sampling beats sequential revision, ORM versus PRM, and Archon, the architecture search that beat big models with small ones."
date: "Autumn 2025"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: -Ggc37xLj_Y
video_title: "Stanford CS329A Self-Improving AI Agents | Part 2 | Test-Time Compute Scaling"
video_caption: "Large Language Monkeys in full: repeated sampling, coverage curves, the long tail of hard problems, the generation-verification gap. Then Snell et al. on optimal test-time scaling and Archon, inference-time architecture search."
concepts: [test-time-compute, repeated-sampling, coverage, oracle-verifier, power-law, long-tail, generation-verification-gap, majority-voting, temperature, kernelbench, sequential-revision, orm, prm, process-reward-model, outcome-reward-model, beam-search, difficulty-binning, archon, inference-time-architecture-search, generator, fuser, critic, ranker, verifier, unit-test-generation, bayesian-optimization, model-stack, fusion]
sources:
  - tag: lecture
    label: "CS329A Part 2: Test-Time Compute Scaling (Autumn 2025, published 2026-08)"
    url: https://www.youtube.com/watch?v=-Ggc37xLj_Y
  - tag: paper
    label: "Brown et al., Large Language Monkeys: Scaling Inference Compute with Repeated Sampling (2024)"
    url: https://arxiv.org/abs/2407.21787
  - tag: paper
    label: "Snell et al., Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters (2024)"
    url: https://arxiv.org/abs/2408.03314
  - tag: paper
    label: "Saad-Falcon et al., Archon: An Architecture Search Framework for Inference-Time Techniques (ICML 2025)"
    url: https://arxiv.org/abs/2409.15254
---

## When one sample is not the budget

*Builds on: Lecture 1's test-time compute and the monkeys teaser.*

**Test-time compute** is computation spent when the model answers:
extra samples, longer chains, revisions, searches, verifier calls.
The weights stay fixed. The question of this lecture is the budget
question: with a fixed budget at answer time, what buys the most
accuracy.

The first answer is the simplest one: sample many times and keep
the best. **Repeated sampling** means asking the same question
over and over with randomness and selecting among the answers.
**Coverage** is the fraction of problems solved by at least one
sample. With an **oracle verifier**, a perfect checker that picks
the correct answer when it appears, coverage keeps rising with
the sample count on a smooth curve.

## Large Language Monkeys: the power law

*Builds on: The budget question, answered with the paper's full evidence.*

The **Large Language Monkeys** paper is the evidence the lecture
opens with. Same setup as the teaser in Lecture 1: hard problems,
many samples, an oracle verifier. Two findings.

First, coverage grows as a **power law** in the number of samples:
coverage equals A times K to the power B, where K is the sample
count. A **power law** means the relationship is linear on a
log-log plot: each doubling of samples buys a constant
multiplicative gain. A toy in the lecture's spirit: with A 0.15
and B 0.15, coverage rises 0.15 at 1 sample, 0.21 at 10, 0.30 at
100, 0.42 at 1,000. Smooth, predictable, and still rising.

Second, the **long tail of hard problems**: for some problems the
hit rate is tiny but nonzero. The lecture reports problems where
only 3 or 4 of 10,000 samples were correct. That is 0.03 to 0.04
percent. The model's knowledge has a tail that one shot never
reaches. The lecture states the condition that makes sampling
work: most problems need at least a moderate chance of success
(the necessary condition), and the model must also solve problems
that its base success rate says it cannot (the sufficient
condition, the long tail). Without the tail, sampling just
repeats what one shot already does.

![Coverage keeps rising](assets/plate-l02-coverage.svg "Coverage C = A x K^B. Toy A 0.15, B 0.15: 0.15 at 1 sample, 0.21 at 10, 0.30 at 100, 0.42 at 1,000. Shell 2. Source: paper, Large Language Monkeys. Project: Stanford Frontier AI.")

## The generation-verification gap

*Builds on: The monkeys power law, which assumed an oracle verifier.*

Knowing that a correct answer exists among the samples is not the
same as finding it. An oracle verifier is a fantasy. Real
selection has to pick the winner from the pile.

**Majority voting** picks the most common answer. It works when
the model is usually right. On hard problems it plateaus: with 10
to 50 samples the gains stop, because the most common answer is
confidently wrong. The gap between oracle coverage and majority
voting is the **generation-verification gap**. It is the same gap
Lecture 1 named from the Q&A: models generate plenty of good
attempts and cannot reliably tell which ones are good.

The paper's practical evidence: the models that benefited most
were the cheaper ones, so a small model sampled 10,000 times beat
a big model sampled once on the same benchmark. Small beats big
once the verifier is perfect.

![Small beats big with perfect verification](assets/plate-l02-small-beats-big.svg "Llama 3 8B at 10,000 samples beats GPT-4o at 1 sample with an oracle verifier. Same knowledge, more tries. Shell 2. Source: paper, Large Language Monkeys. Project: Stanford Frontier AI.")

## KernelBench: the verifier is a compiler

*Builds on: The generation-verification gap, with a verifier that has teeth.*

The lecture's applied stop is **KernelBench**: models write Compute Unified Device Architecture (CUDA)
kernels, and correctness is checked by running them. This is a
verifier with teeth, because execution is honest. A wrong kernel
fails its tests. The lecture frames it as AI as a compiler: the
model writes fast code and the hardware checks it. As of October
2026 the benchmark is live and active: it appeared at ICML 2025,
its dataset is on HuggingFace, and a Meta follow-up,
KernelBench-Verified, tightened the evaluation. The lesson the
lecture draws stands: where verification is automatic and
trustworthy, the generate-verify loop runs at full speed.

## The budget question: parallel versus sequential

*Builds on: the coverage power law, which says more samples help,
but not how a fixed budget should be split.*

Given a budget, is it better to draw many independent samples or
to revise one answer over and over? The **Snell et al.** paper
answers with a controlled study on math problems.

Two axes. **Parallel**: independent samples, then pick with a
verifier. **Sequential**: generate an answer, then revise it,
repeatedly, each revision conditioned on the last. Sequential
revisions are expensive: every step re-reads the whole chain, so
the token cost grows faster than the sample count.

## Difficulty binning: sort problems before spending

*Builds on: the parallel-versus-sequential budget question,
which needs a way to tell easy problems from hard ones.*

The paper's setup: 12,000 training problems, 500 test problems,
grouped by **difficulty binning** into five bins. The bins let
the study ask the budget question separately per difficulty,
because the right spend depends on how hard the problem is.

## Outcome reward models: score the answer

*Builds on: difficulty binning, which sets up the experiment in
which the two verifier types are compared.*

Two verifier types. An **outcome reward
model (ORM)** scores only the final answer. It sees whether the
answer is right and nothing about how the model got there.

## Process reward models: score the steps

*Builds on: outcome reward models, which show what scoring
answers alone can and cannot do.*

A **process reward
model (PRM)** scores the reasoning steps. It judges the trace,
not just the destination, so it can tell a lucky guess from a
sound derivation.

## Beam search with PRM: the winning mix

*Builds on: process reward models, whose step scores give the
search the signal it needs to choose branches.*

The search method that
beat both naive options was **beam search with PRM**: sample 4
candidates, keep the top 2 by PRM score, expand from those, and
keep the best final answer. Revising each candidate 4 times beat
the plain baseline but lost to beam search. And a telling detail:
ORM selection, which only sees final answers, converged to just
repeating the same answer, because without step information the
selection had nothing to work with.

The punchline the lecture stresses: the right mix depends on
difficulty. For easy and medium problems, more test-time compute
favored **sequential** compute: spend the budget on revisions.
For hard problems, spending the same budget on **pretraining**
still won. Small models can beat big models on easy problems by
thinking longer, but the hardest problems need the big weights.

## Archon: architecture search at inference time

*Builds on: The parallel-versus-sequential budget results, searching over combinations of techniques.*

If test-time techniques matter this much, which combination is
best? **Archon** answers by searching over inference-time
architectures the way neural architecture search (NAS) searched over networks. The search tool
is **ITAS**, an inference-time architecture search using
**Bayesian optimization**: try a configuration, measure it,
update a probabilistic model of what works, and let the model
choose the next configuration to try.

The components the search can assemble are operations on model
outputs. A **generator** produces candidate answers. A **fuser**
merges several candidates into one. A **critic** scores or
comments on candidates. A **ranker** orders them. A **verifier**
checks correctness. Two more for code: a **unit test generator** performs **unit test generation**, and a **unit test evaluator** runs the code against them. A **model stack** is one configuration: which models run at
each layer and which operations connect them.

![Archon stacks inference-time components](assets/plate-l02-archon.svg "Layers of generators, fusers, critics, rankers, verifiers. Bayesian optimization picks the stack. Average +14.1% pass@1 over GPT-4o and Claude 3.5 Sonnet with open-source models. Shell 2. Source: paper, Archon (v1). Project: Stanford Frontier AI.")

The findings, reported from the lecture: fusers beat generators
alone, and **fusion beats oracle selection**: merging candidates
outperforms even a perfect picker choosing among them. Deeper
layers help. The headline number: with open-source models,
Archon beats GPT-4o and Claude 3.5 Sonnet by an average of 14.1
percent pass@1. A worked sense of scale: a baseline at 0.60
pass@1 rises to about 0.685 under a 14.1 percent relative gain.

One honesty note from the paper's history: the first arXiv
version reports 14.1 percentage points of gain. The lecture
phrases it as 14.1 percent average improvement. The later paper
version reports 15.1. Numbers moved as the paper matured. Use the
v1 number with the lecture, and expect later versions to differ.

## What the lecture leaves out

*Builds on: Every verifier this lecture assumed, naming the missing piece.*

A note the course itself flags by its absence. The playlist's
Part 3, on reliable verification, has no transcript in the sources
this course was built from. The lectures covered here treat the
verifier as given: oracle, tests, or a judge. How to build a
verifier that resists gaming gets named as the bottleneck in
every lecture but is not covered as its own lecture. The auditor
should treat claims about verifier construction as the least
verified part of this chapter.

> [!QA]
> Q: Work a pass@k toy with real arithmetic.
> A: Suppose each sample solves a problem with probability 0.12,
> independently. Pass@25, the chance at least one of 25 succeeds,
> is 1 minus 0.88 to the 25th power. 0.88 to the 25th is about
> 0.0409. One minus that is 0.9591. A 12 percent per-shot model
> solves 96 percent of problems given 25 tries and a perfect
> picker.
> Follow-up: What breaks the independence assumption?
> A: The model repeats its own mistakes. Samples are correlated:
> if the model has a blind spot, all 25 samples share it. Then
> pass@k falls short of the formula. That is why the lecture
> stresses temperature diversity, and why the ceiling on
> temperature matters.

> [!QA]
> Q: Why does majority voting plateau on hard problems?
> A: Majority voting assumes the model is usually right, so the
> most common answer wins. On hard problems the model's per-shot
> success is low and its wrong answers cluster: many samples make
> the same plausible mistake. The vote then confidently picks the
> mistake. The lecture reports the plateau at 10 to 50 samples.
> More samples feed the same wrong consensus.
> Follow-up: What fixes it?
> A: A verifier with independent judgment: unit tests, a process
> reward model scoring steps, or an oracle. Anything that looks
> at the answer's content instead of its popularity. That is the
> generation-verification gap in one sentence.

> [!QA]
> Q: Explain the long tail of hard problems.
> A: For most problems the model succeeds at a moderate rate.
> Sampling multiplies those. The surprise is the tail: problems
> where 3 or 4 samples out of 10,000 are correct. At 0.03 percent
> per shot, one sample almost never finds them, yet they exist
> and the model can reach them. The lecture's condition: sampling
> pays when most problems are moderately solvable and the tail
> still contains problems the base rate says are out of reach.
> Follow-up: Why not just train until the tail disappears?
> A: The tail is where knowledge lives at low density. Training
> raises the base rate, which raises the tail with it. But at any
> fixed training budget some problems sit at the edge, and for
> those the marginal answer still comes cheaper from sampling.

> [!QA]
> Q: When should a budget go to sequential revision instead of parallel samples?
> A: The Snell et al. result: for easy and medium problems,
> sequential revision of a candidate wins. Each revision sees the
> previous attempt and its feedback, so the budget compounds. For
> hard problems, the same budget spent on pretraining wins:
> revisions of a weak candidate stay weak. The decision rule is
> difficulty: revise when the model is close, sample or scale the
> model when it is far.
> Follow-up: Why is sequential compute expensive?
> A: Every revision re-reads the whole chain. Tokens per step grow
> with the chain length, so the token cost grows faster than the
> number of revisions. Parallel samples cost a flat amount each.

> [!QA]
> Q: What is the difference between an ORM and a PRM?
> A: An outcome reward model scores the final answer only. A
> process reward model scores the reasoning steps. The paper
> found PRM-based beam search beats ORM-based selection, because
> step scores tell the search where the promising branches are.
> ORM selection on final answers alone converged to repeating the
> same answer: no signal, no search.
> Follow-up: What does a PRM cost that an ORM does not?
> A: Step-level labels. Someone or something must score each step
> of training traces, which is far more annotation than final
> answers. The PRM buys its advantage with that cost.

> [!QA]
> Q: How did Archon beat GPT-4o with open-source models?
> A: By stacking inference-time components: layers of generators,
> fusers, critics, rankers, and verifiers, with the configuration
> found by Bayesian optimization over the search space. Two
> findings matter: deeper layers help, and fusing candidates
> beats even an oracle picking among them. The lecture reports
> an average 14.1 percent pass@1 improvement over GPT-4o and
> Claude 3.5 Sonnet using open-source models.
> Follow-up: Is this just sampling with extra steps?
> A: No. Sampling feeds one verifier. Archon feeds candidates
> through a pipeline: generate, criticize, fuse, rank, verify,
> with each layer transforming the candidates. The search finds
> which pipeline fits the task. The gain is architectural, not
> just statistical.

> [!QA]
> Q: The lecture says inference is the new frontier. Where is the wall for inference scaling?
> A: Three walls. Cost: samples and revisions burn tokens and
> latency, and the trade-off is problem-dependent. Diversity:
> temperature caps near 1.2, after which outputs turn to
> gibberish, so samples correlate. Selection: without a good
> verifier, coverage is unreachable. Majority voting plateaus at
> 10 to 50 samples. The lecture's answer is that test-time
> compute is a real axis with real limits, and the verifier is
> the ceiling.
> Follow-up: So is test-time scaling just a patch for weak models?
> A: Partly, and the lecture is honest about it: on hard
> problems, pretraining still wins head-to-head. But test-time
> techniques also make strong models stronger, and they generate
> the training data the loop needs. It is both a patch and a
> path.

> [!QA]
> Q: Design the test-time compute strategy for a math tutoring product. Each question gets a fixed budget of 2,000 tokens. How do you spend it?
> A: Bin by difficulty first, then spend by bin. A cheap
> difficulty signal, the model's own confidence or a small
> classifier, routes the question. Easy question: sequential
> revision. Generate one candidate and revise it 3 to 4 times.
> Each revision re-reads the chain, so 4 revisions of a
> 400-token chain cost about 1,600 tokens plus verifier calls.
> Hard question: parallel sampling with PRM beam search. Draw 8
> candidates, score the steps with a process reward model, keep
> the top 2, expand from those. The verifier decides the
> ceiling: textbook problems with known answers get exact-match
> checking, which is free and honest. Open-ended problems fall
> back to majority vote, knowing it plateaus past 10 to 50
> samples on hard problems. Cap revisions at 4, because
> sequential token cost grows faster than the revision count,
> and spend the rest on parallel diversity.
> Follow-up: The product manager wants to cut the verifier to save cost. What breaks?
> A: Selection. Without a verifier the system cannot tell which
> sample is right, and the generation-verification gap swallows
> the budget: coverage rises but realized accuracy flatlines.
> The lecture's evidence: majority voting plateaus at 10 to 50
> samples on hard problems, and ORM-only selection converged to
> repeating the same answer. The verifier is the cheapest
> accuracy in the system. Cut it last.

## Recap: the whole lesson on one screen

1. **Coverage is a power law.** C equals A times K to the B.
   Toy: 0.15, 0.21, 0.30, 0.42 as samples go 1, 10, 100, 1,000.
2. **The tail matters.** Some problems solve at 0.03 percent per
   shot. Sampling reaches knowledge one shot cannot.
3. **Selection is the gap.** Oracle coverage rises. Majority
   voting plateaus at 10 to 50 samples on hard problems.
4. **Revise easy, scale hard.** Easy and medium problems favor
   sequential revision. Hard problems still reward pretraining.
5. **Steps beat answers for search.** PRM beam search wins.
   ORM-only selection converges to repeating itself.
6. **Architecture search at inference time.** Archon stacks
   generators, fusers, critics, rankers, verifiers and beats
   GPT-4o by 14.1 percent with open-source models.

## Used where, as of October 2026

- **Reasoning models (o1 from September 2024, o3, DeepSeek-R1
  from January 2025, Gemini thinking):** the commercial form of
  test-time scaling. Longer chains and more tokens at answer
  time, exactly the axis this lecture studies.
- **KernelBench** (Stanford, ICML 2025, arXiv 2502.10517): live
  and extended with a Meta verified variant. Execution as the
  honest verifier.
- **Best-of-n sampling in RLHF pipelines:** the production form
  of repeated sampling: draw several answers, keep the one the
  reward model scores highest. Documented as standard practice in
  the RLHF Book (Lambert, 2025), including use in the higher
  tiers of chat products.
- **Agentic coding systems:** parallel candidate patches with
  test-based selection, the Archon shape in industry form.
  Agentless (2024) generates candidate patches and selects among
  them with tests. Anthropic's Claude Sonnet 4.5 SWE-bench
  methodology (2025) samples parallel attempts, discards patches
  that break regression tests, and picks with a scoring model.

## Official sources and further reading

**Official:**
- CS329A Part 2: Test-Time Compute Scaling (Autumn 2025).
  https://www.youtube.com/watch?v=-Ggc37xLj_Y

**Further reading:**
- Brown et al., "Large Language Monkeys" (2024).
  https://arxiv.org/abs/2407.21787
- Snell et al., "Scaling LLM Test-Time Compute Optimally"
  (2024). https://arxiv.org/abs/2408.03314
- Saad-Falcon et al., "Archon" (ICML 2025).
  https://arxiv.org/abs/2409.15254
- Scale et al., "KernelBench" (ICML 2025).
  https://arxiv.org/abs/2502.10517

**Caveats from these sources.** The Archon number in the lecture
is 14.1 percent from the paper's v1. The paper's later version
reports 15.1. The lecture's pass@k figures assume an oracle
verifier unless stated. Part 3 of the playlist, on reliable
verification, has no transcript in this course's sources.

## Connections to the other courses

- **CS329Z:** covers test-time techniques from the builder side:
  prompting, sampling strategies, and evaluation of the outputs.
  This course adds the theory of the budget and the search over
  techniques.
- **CS229S:** the systems cost of test-time scaling: latency,
  throughput, and why sequential revision is expensive.
- **CS329H:** process reward models are trained with the
  preference machinery: reward models, human feedback, and the
  gap between a proxy and the goal.
