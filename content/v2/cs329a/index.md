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

One argument, ten chapters. A language model can improve itself.
It generates many attempts, checks them with a verifier, and
trains on the winners. Each chapter adds one piece of that loop,
demonstrates it with numbers, and names its price.

## The arc

The course opens with the loop itself: one-shot answers waste
what the model knows, and a generate-verify-train cycle recovers
it. Then it scales each stage. Sampling hundreds of times makes
small models beat giants. Giving the model tools grounds its
reasoning in the world. Searching over plans instead of walking
one path fixes greedy commitment. Training on execution feedback
turns tries into weights. Sampling a million programs exposes
the selection problem. Searching mid-thought fills knowledge
gaps. Bootstrapping rationales from answer keys teaches
reasoning. Judging the judge attacks the verifier bottleneck.
Measuring long-horizon tasks shows how far capability has come
and how far reliability lags.

## The lessons

1. [L01 · The Self-Improving Agent](l01-self-improving-agents.html): the generate-verify-train loop, chain of thought, and why the verifier is the bottleneck.
2. [L02 · Test-Time Scaling](l02-test-time-scaling.html): repeated sampling, the log-linear coverage law, and Archon's inference-time architectures.
3. [L03 · Agents That Act](l03-agents-that-act.html): ReAct, grounding thought in tool calls, and compounding error.
4. [L04 · Learning from Execution](l04-learning-from-execution.html): RLEF, two-tier tests, and binary rewards from running code.
5. [L05 · Planning with Search](l05-planning-with-search.html): LATS, tree search over plans, UCT, and reflection.
6. [L06 · Sampling at Scale](l06-sampling-at-scale.html): AlphaCode to AlphaCode 2, the 10@k metric, and the selection bottleneck.
7. [L07 · Search That Reads](l07-search-that-reads.html): deep research agents, agentic RAG, and reading documents instead of dumping them.
8. [L08 · Teaching the Model to Reason](l08-teaching-reason.html): STaR, rationalization, and bootstrapping reasoning from answer keys.
9. [L09 · The Verifier Bottleneck](l09-verifier-bottleneck.html): outcome vs process rewards, the meta-verifier, and multi-agent debate.
10. [L10 · Measuring Agents](l10-measuring-agents.html): METR time horizons, the reliability gap, and the open problems.

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
each lecture cites: Large Language Monkeys, ReAct, RLEF, LATS,
AlphaCode, Search-o1, STaR, DeepSeekMath, DeepSeek-Math V2, and
the METR long-task study. Full citations close every chapter.
