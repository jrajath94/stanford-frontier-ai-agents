---
page_id: cs329a-index
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 0
nav: "CS329A · Overview"
title: "CS329A: Self-Improving AI Agents"
summary: "The research course on agents that improve themselves: test-time scaling, acting with tools, planning with search, training on execution, and the verifier bottleneck."
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
---

One argument, eight lessons. A language model can improve itself.
It generates many attempts, checks them with a verifier, and
trains on the winners. Each lesson adds one piece of that loop,
demonstrates it with numbers, and names its price.

## The arc

The course opens with the loop itself: one-shot answers waste
what the model knows, and a generate-verify-train cycle recovers
it. Then it scales each stage. Sampling thousands of times makes
small models beat giants, and architecture search stacks
inference-time components to beat them further. Giving the model
tools grounds its reasoning in the world, execution feedback
trains code models, and constitutions replace human labelers.
Searching over plans instead of walking one path fixes greedy
commitment, interleaved planning parallelizes execution, and
step-level RL beats imitation. Sampling a million programs
exposes the selection bottleneck, and agentic search fills
knowledge gaps mid-thought. Bootstrapping rationales from answer
keys teaches reasoning, GRPO normalizes advantages by group, and
the DAPO ladder writes down the stable RL recipe. Measuring
long-horizon tasks shows how far capability has come and how far
reliability lags. The close looks forward: agents debating,
verifiers checking verifiers, self-play with zero human data,
and the open problems of non-verifiable domains,
intelligence per watt, and continual learning.

## The lessons

1. [L01 · The Self-Improving Agent](l01-course-overview.html): scaling laws and the wall, chain of thought as emergence, instruction tuning and RLHF, the monkeys teaser, reasoning models, and the generate-verify-train loop.
2. [L02 · Test-Time Compute Scaling](l02-test-time-scaling.html): Large Language Monkeys, the coverage power law, the generation-verification gap, parallel versus sequential budgets, and Archon.
3. [L03 · Learning from Feedback with Tools and Code](l03-feedback-tools-code.html): ReAct, RLEF with two-tier tests, and Constitutional AI.
4. [L04 · Planning and Multi-Step Reasoning](l04-planning-multistep-reasoning.html): LATS tree search, SPRINT interleaved planning, and SWiRL multi-step RL.
5. [L05 · Self-Improvement and Deep Research Agents](l05-search-at-scale.html): AlphaCode to AlphaCode 2, the selection bottleneck, and Search-o1.
6. [L06 · Train-Time Scaling and Scaling RL](l06-train-time-scaling.html): STaR, DeepSeekMath and GRPO, DAPO, and SFT versus RL.
7. [L07 · Agentic Evaluations and Long-Horizon Tasks](l07-agentic-evaluations.html): METR time horizons, GDPval against professionals, and DeepScholar-Bench.
8. [L08 · Future Research Areas](l08-future-directions.html): multi-agent fine-tuning, DeepSeekMath-V2 meta-verification, Absolute Zero, and the open problems.

## How this differs from CS329Z

CS329Z is the engineering course: how to build agents with
tools, function calling, ReAct, memory, evaluation, and
infrastructure. CS329A is the research course: the frontier
questions behind those systems. Can agents improve themselves?
What does scaling test-time compute buy? How do you verify the
verifier? The two courses meet in the middle: everything CS329A
studies becomes something CS329Z has to build.

## Sources

Eight lecture transcripts from the Autumn 2025 offering, taught
by Azalia Mirhoseini and Aakanksha Chowdhery, plus the papers
each lecture cites: Large Language Monkeys, Snell et al.,
Archon, ReAct, RLEF, Constitutional AI, LATS, SPRINT, SWiRL,
AlphaCode, Search-o1, STaR, DeepSeekMath, DAPO, METR, GDPval,
DeepScholar-Bench, multi-agent fine-tuning, DeepSeekMath-V2,
Absolute Zero, and AlphaEvolve. Full citations close every lesson.

Note: the playlist's Part 3, on reliable verification, has no
transcript in the course sources. Verification is covered from
what the other eight lectures say about verifiers.
