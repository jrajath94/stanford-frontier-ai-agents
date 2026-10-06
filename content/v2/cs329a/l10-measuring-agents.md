---
page_id: cs329a-l10
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 10
nav: "L10 · Measuring Agents"
title: "Lecture 10: Measuring Agents and the Road Ahead"
summary: "How long a task can an agent complete? The METR time-horizon doubles every 7 months, but 80 percent reliability lags years behind 50 percent capability. The course closes on the open problems."
date: "2025-11-12"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: 8JAqLnTaZu4
concepts: [agentic-evaluation, time-horizon, metr, reliability-gap, failure-modes, long-horizon-tasks, open-problems, capability-vs-reliability]
sources:
  - tag: lecture
    label: "CS329A Lecture 8: agentic evaluations and long-horizon tasks (Autumn 2025)"
    url: https://www.youtube.com/watch?v=8JAqLnTaZu4
  - tag: paper
    label: "METR, Measuring AI Ability to Complete Long Tasks (2025)"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: benchmarks say "better", users say "unreliable"

Every method in this course reports wins: higher coverage,
better pass rates, climbing proof scores. But ask anyone who
has delegated a real afternoon of work to an agent, and the
report is different: it sometimes works, sometimes wanders,
sometimes confidently finishes the wrong task. Benchmark
scores and lived reliability disagree. This chapter is about
measuring what actually matters: how long a task an agent can
complete, and how reliably.

An **agentic evaluation** differs from a question-answering
benchmark in one way: the task takes time. Not seconds, but
minutes to hours of skilled human work: debugging a real
repository, reproducing a machine learning result, planning
under constraints. The unit of difficulty is the **time
horizon**: how long the task would take a skilled human.

## The measurement, worked concretely

The METR methodology the lecture presents works like this.
Take a battery of tasks spanning seconds to many hours. For
each task, have skilled professionals, roughly five years of
experience, record how long successful completion takes, and
take the geometric mean as the task's difficulty rating. Then
run models on the tasks and record the success rate at each
horizon.

The headline numbers, read off the lecture's trend line:

```ascii
model (year)          task horizon at 50% success
GPT-2 (2019)          2 seconds
GPT-4 (2023)          8 minutes
Claude 3.7 (2025)     59 minutes
```

From 2 seconds to 59 minutes in six years. The doubling time
is about 7 months: every 7 months, the task length the model
handles half the time doubles. That is the capability trend,
and it is steep.

Now the number that matters for deployment. Redo the
measurement at 80 percent success instead of 50:

```ascii
Claude 3.7 (2025):    59 minutes at 50% success
                      ~15 minutes at 80% success
```

An intern who completes hour-long tasks half the time, and
15-minute tasks most of the time. The lecture's gloss: there
is always uncertainty. Capability at 50 percent is years
ahead of reliability at 80 percent. The gap between the two
curves is the headroom the field has not closed, and it is
large.

The lecture is also honest about the methodology's weak
point. Experts underestimate task difficulty: people fluent
in a field are conditioned to what success looks like, and
their times do not reflect how hard the task feels to a
model. Human difficulty and model difficulty are different
rulers.

## Where agents fail: the failure modes

The lecture walks through a failure-mode analysis comparing
a non-reasoning model (GPT-4) with a reasoning model (o1).
The categories recur across the field:

- **Poor planning.** The model does not break the task into
  steps, or breaks it wrongly. It acts before it has a plan,
  or plans at the wrong granularity.
- **Poor tool choice.** Wrong tool, or right tool with a bad
  query. The trajectory grounds itself in the wrong facts.
- **No error recovery.** Something goes wrong mid-task, as it
  always does in an hour-long task, and the agent cannot
  detect it or replan. It repeats the failing behavior.
- **Lost goal state.** Over a long horizon the agent forgets
  what it is optimizing: no memory of the final goal, no
  sense of progress. It optimizes a subtask as if it were
  the task.

Read these against the earlier chapters. Poor planning is
what Lecture 5's tree search addresses. Poor tool choice is
Lecture 3's failure mode. No error recovery is the
compounding-error arithmetic of Lecture 3, now measured.
Lost goal state is the memory problem the lectures keep
naming and never fully solving: the agent needs a notion of
where it is and what remains.

The lecture notes what has been driving the gains anyway:
better reasoning, better code generation, tool use, less
repetitive behavior, and crucially, **context engineering**,
structuring what the agent sees across steps so the tools
work better. Reliability engineering around the model, not
just the model, moves the curves.

## The key question

If capability doubles every 7 months but reliability lags
years behind, what are the actual open problems?

## The road ahead, from the recap lecture

The course's closing lecture names the frontier explicitly.
Each item is a research problem, not a solved one:

1. **Diversity of reasoning chains.** Self-improvement feeds
   on varied attempts. Keeping them diverse, across rounds
   of training, is unsolved. Multi-agent debate is a start.
2. **Breaking the verifier bottleneck.** Everything needs
   fast, honest judges. Outcome checks are blind, model
   judges are gullible, and slow domains have no judges at
   all. Better verifiers improve everything downstream.
3. **Data selection.** Only so much can be curated by humans.
   Which problems go into the loop, in which order, a
   **curriculum**, matters enormously and is barely studied.
4. **Non-verifiable domains.** Creative writing, open-ended
   design, science with slow experiments. The loop does not
   reach them today. Learned reward stand-ins invite hacking.
5. **The cost of intelligence.** Test-time scaling burns
   compute per question. Demand is exploding: the lecture
   cites Google's served tokens jumping from 160 trillion to
   1.3 quadrillion in months, and data-center energy demand
   in the hundreds of gigawatts. Efficiency is not optional.

And the through-line the lecturers keep returning to: the
self-improvement loop, generate, verify, train, is the
engine. Every open problem is a way the engine stalls.
Fix the stall, turn the crank again.

## Mapping back: the whole course in one table

| Chapter | Engine part | Core result | Honest price |
|---|---|---|---|
| L01 | The loop | Generate, verify, train | Needs fast honest verifiers |
| L02 | Generate | Log-linear coverage. Small beats big | Pays per question. Needs the check |
| L03 | Act | ReAct grounds thought in tools | Errors compound: 0.9^10 = 0.35 |
| L04 | Train on doing | RLEF: execution feedback to RL | Sparse binary signal. Tests required |
| L05 | Plan | LATS: tree search over plans | Hundreds of calls. Judge can mislead |
| L06 | Scale | AlphaCode: 10@k. Learned selectors | Selection bottleneck. Diversity engineered |
| L07 | Know | Agentic search fills gaps mid-thought | Trigger heuristics. Context budget |
| L08 | Learn | STaR: bootstrap reasoning from answers | Unfiltered rationales. Needs answer keys |
| L09 | Judge | Meta-verifier. Multi-agent debate | Human-seeded. Slow domains excluded |
| L10 | Measure | 7-month doubling. Reliability lags | 50% is not deployable |

## The honest price, final

The course's own measurement says the field is far from done.
An agent that handles hour-long tasks half the time is a
research result, not a coworker. The reliability gap, the
verifier bottleneck, and the cost curve are the three walls.
The doubling trend says the walls are moving. Nothing in the
lectures says they fall on their own.

> [!QA]
> Q: What is the METR time-horizon result?
> A: The task length a model completes 50 percent of the time doubles roughly every 7 months: GPT-2 in 2019 managed 2 seconds, GPT-4 in 2023 managed 8 minutes, Claude 3.7 Sonnet in 2025 manages 59 minutes. Task difficulty is rated by the geometric mean of skilled professionals' completion times. It is a capability trend, not a reliability claim.
> Follow-up: Why is not 50 percent enough?
> A: Because deployment needs reliability. At 80 percent success, Claude 3.7's horizon drops from 59 minutes to about 15. The gap between the 50-percent curve and the 80-percent curve is years of headroom. An agent that finishes half its hour-long tasks is a demo. One that finishes 80 percent of 15-minute tasks is a tool. The field has the first, not the second.

> [!QA]
> Q: What are the main failure modes of long-horizon agents?
> A: Four, from the lecture's analysis. Poor planning: the task is not broken into workable steps. Poor tool choice: wrong tool or bad query grounds the trace in wrong facts. No error recovery: mid-task failures go undetected and un-replanned. Lost goal state: over long horizons the agent forgets the objective and optimizes a subtask. Every one of them compounds with trajectory length.
> Follow-up: Which of these did the course's methods address?
> A: Planning: LATS tree search. Tool choice: ReAct grounding, plus learned selectors in AlphaCode 2. Error recovery: reflection in LATS, retry loops in RLEF. Lost goal state: named repeatedly, never fully solved. Memory structures for agents remain an open research area. The honest scorecard is three partials and one open.

> [!QA]
> Q: What are the open problems the course leaves?
> A: Five from the recap lecture. Keeping reasoning chains diverse across training rounds. Building fast honest verifiers, especially process-level ones. Data selection and curriculum: which problems feed the loop in which order. Reaching non-verifiable domains: creativity, slow science, where no fast judge exists. And the cost of intelligence: test-time scaling's compute demand against exploding usage.
> Follow-up: Which one helps the most downstream?
> A: The lecturers' framing points at verification. Every loop, sampling, RL, debate, meta-verification, consumes verifier judgments. A breakthrough in fast, trustworthy, process-level verification would speed up all of them at once.

## Recap: the whole lesson on one screen

1. **Benchmarks vs reliability.** Scores climb. Users still
   see flakiness. Measure task horizons, not just accuracy.
2. **The trend.** 50%-success horizon doubles every 7 months:
   2 seconds (2019), 8 minutes (2023), 59 minutes (2025).
3. **The gap.** At 80% success, the 2025 frontier drops to
   about 15 minutes. Capability is years ahead of
   reliability.
4. **Failure modes.** Poor planning, poor tool choice, no
   error recovery, lost goal state. All compound with length.
5. **What drove gains.** Reasoning, code, tools, less
   repetition, and context engineering around the model.
6. **The key question.** Capability doubles. Reliability
   lags. What are the real open problems?
7. **Five opens.** Diversity, verifiers, curriculum,
   non-verifiable domains, cost of intelligence.
8. **The engine.** Generate, verify, train. Every open
   problem is a stall in the engine. Fix the stall, turn
   the crank.

## Official sources and further reading

**Official:**
- CS329A Lecture 8 (Autumn 2025): the lecture this chapter
  follows. https://www.youtube.com/watch?v=8JAqLnTaZu4
- METR, "Measuring AI Ability to Complete Long Tasks"
  (2025): the time-horizon methodology and doubling trend.

**Further reading:**
- The recap lecture's open-problems discussion (Lecture 7):
  https://www.youtube.com/watch?v=AyO6wyu4DEg

**Caveats from these sources.** Horizon numbers are the
lecture's readings from METR plots, approximate. The 7-month
doubling is a fitted trend, not a law. Expert time estimates
underestimate difficulty, per the lecture itself. Model names
are Autumn 2025 snapshots.

## Connections to the other courses

- **CS329Z:** evaluation engineering: building the
  benchmarks this chapter critiques, and doing it well.
- **CS336:** the pretraining side of the capability trend:
  where the base models come from.
- **CS229S:** the cost side of the road ahead: what
  exploding inference demand means for systems.
- **CS329A L01:** the full circle: the loop this chapter's
  open problems are all trying to unstall.
