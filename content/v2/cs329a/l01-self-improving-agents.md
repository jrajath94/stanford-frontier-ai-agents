---
page_id: cs329a-l01
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 1
nav: "L01 · The Self-Improving Agent"
title: "Lecture 1: The Self-Improving Agent"
summary: "One-shot answers waste what the model knows. The course opens with the loop that fixes it: generate many attempts, check them with a verifier, and train on the winners."
date: "2025-09-24"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: 6YnLB0XbTnI
concepts: [agent, self-improvement, scaling-laws, chain-of-thought, reasoning-model, verifier, test-time-compute, train-time-compute]
sources:
  - tag: lecture
    label: "CS329A Lecture 1: course introduction and LLM overview (Autumn 2025)"
    url: https://www.youtube.com/watch?v=6YnLB0XbTnI
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: one shot is not enough

You ask a chatbot a hard math question. It answers in one try. The
answer is wrong. You ask again, phrased a little differently. This
time it is right. The model knew the answer all along. It just did
not say it the first time.

This gap, between what a model can say once and what it knows, is
the subject of this course. A **language model** is a machine that
predicts the next word, over and over, until a full answer appears.
An **agent** is a language model that does more than answer: it
reasons, takes actions with tools, reads the results, and keeps
going until a task is done. Fixing a bug, planning a trip, proving
a theorem: these are agent tasks. None of them fits in one shot.

The lectures build one argument across the quarter. The model can
improve itself. It can try many times and keep the good tries. It
can check its work with tools. It can search over plans. It can
train on its own best attempts. Each lecture adds one piece of
that loop. This chapter opens the loop and names its parts.

## How we got here: scaling, then a wall

From 2018 to 2024 the field had one reliable recipe: make the
model bigger. The **scaling laws** say that as you raise compute,
data, and parameter count, the test loss falls in a predictable
curve. BERT had 340 million parameters. GPT-2 had 1.5 billion.
GPT-3 had 175 billion. PaLM had 540 billion. Each step brought
better scores on language and reasoning benchmarks.

Bigger models also gained abilities nobody trained directly.
**Few-shot learning** means the model follows a task from a few
examples in the prompt, with no retraining. Show it two English to
French pairs, then ask for a third, and it translates. These
abilities appear only past a size threshold. They are called
**emergent** because no one predicted them from the small models.

Then the recipe started to saturate. Around 2024, throwing more
pretraining compute at the same data stopped buying as much. The
field needed a new axis of improvement. The lectures argue the new
axis is the model improving itself: better answers at test time,
and better models from those answers at train time.

## First tool: thinking out loud

Before the loop, the model needs one skill: showing its work. A
**chain of thought** is a step-by-step trace the model writes
before the final answer. The lecture's toy is almost insultingly
simple, which is the point: the mechanism is visible.

```ascii
prompt:  Roger has 5 tennis balls. He buys 2 cans.
         Each can has 3 tennis balls. How many total?

model:   Roger started with 5 balls.
         2 cans of 3 balls is 6 balls.
         5 + 6 = 11.
answer:  11
```

The model does not jump to 11. It writes the steps, and each step
is easy on its own. The lecture reports a striking fact: small
models, around 8 billion parameters, gain nothing from chain of
thought. Larger models gain a lot. The ability to use a reasoning
trace is itself emergent. It appears only at scale.

Watch what the trace buys. The steps are checkable. A wrong step
can be spotted. The model can also correct itself mid-trace: start
down a path, write "wait, that is wrong", and backtrack. This
**self-correction** is a small thing in a toy. In hard problems it
is the difference between a dead end and a solution. Reasoning
models, the o1 series, Gemini thinking, DeepSeek, are built on
this: long traces of analysis, decomposition, trial, correction.

## Where one shot breaks

Now put the model on a hard problem, say an olympiad-level math
question. One attempt, one answer. The model fails. This is
expected: a single forward pass is a single draw from the model's
distribution over answers, and hard problems sit in the tail.

Here is the fact that opens the whole course. The Large Language
Monkeys result, which the lectures return to again and again:
sample the same problem many times, and small models solve
problems far above their apparent level. A Llama 3 8B model, asked
ten thousand times with a way to check which answers are right,
solves IMO-level problems from the F2F benchmark. The knowledge
was in the weights. One shot could not reach it. Ten thousand
shots could.

Two lessons fall out. First, the model's single-attempt score
understates what it knows. Second, reaching the knowledge needs
two things: many attempts, and a way to tell the good ones from
the bad. The checker has a name in this course: the **verifier**.

## The key question

What if the model generates many attempts, keeps the ones a
verifier approves, and trains on them to get better?

## The self-improvement loop

A **verifier** is any procedure that judges an answer without a
human in the loop. For math, it can be the known correct answer.
For code, it can be unit tests: the program passes or it fails.
The verifier must be fast and automatic, because the loop will
call it thousands of times.

The loop has three stages, and the lecture names them plainly:

```ascii
1. generate    the model tries the problem many times
                  (test-time compute: more tries, no new training)
                  |
2. verify      a verifier scores every attempt
                  keep the winners, drop the losers
                  |
3. train       fine-tune the model on the winners
                  (train-time compute: the weights change)
                  |
               repeat: the better model generates better attempts
```

**Test-time compute** is effort spent answering: more samples,
longer reasoning traces, tool calls. The weights do not change.
**Train-time compute** is effort spent learning: gradient updates
on the winners. The weights change. The DeepSeek and o1 breakthrough
the lecture describes was joining the two: use test-time scaling
to manufacture high-quality training data, then train on it, then
scale test time again. Each turn of the crank lifts the next.

A concrete instance from the lecture: for math problems with known
answers, generate many candidate solutions, keep the ones that
reach the right answer, and fine-tune on them. For coding, generate
many programs, keep the ones that pass the tests, and fine-tune on
those. The model's own outputs become its training set. That is
what "self-improving" means here: no new human labels, just the
model, the verifier, and the loop.

## Mapping back: what the loop fixes

One-shot answering fails in two ways, and the loop answers both:

| One-shot failure | Loop answer | How |
|---|---|---|
| The model knows more than one try shows | Generate many attempts | Test-time sampling surfaces answers that live in the tail of the distribution. |
| No signal tells good tries from bad | Verify automatically | A fast verifier (answer match, unit tests) selects winners with no human in the loop. |
| Winners are thrown away after use | Train on the winners | Fine-tuning on verified attempts moves the knowledge from the tail into the first try. |

## The honest price: the verifier is the bottleneck

The loop has one load-bearing part, and it is not the model. It is
the verifier. Every turn of the crank needs thousands of fast,
trustworthy judgments. Math with known answers qualifies. Code
with unit tests qualifies. Creative writing does not: there is no
fast automatic judge of a good essay, and a learned judge can be
gamed by the model, a failure called **reward hacking**.

Speed matters as much as correctness. The lectures stress that
verifiers must be near-instant. A chip-design simulation that takes
days to return one score cannot sit inside a training loop that
needs thousands of iterations. Domains with slow verification are,
for now, outside the loop's reach. The price of self-improvement
is a fast, honest judge. Where no such judge exists, the loop does
not turn.

That price shapes the whole course. Lecture 2 scales the
generate step. Lectures 3 through 5 add tools, planning, and
search to make attempts stronger. Lecture 6 turns attempts into
training data. Lecture 7 asks who verifies the verifier. Lecture
8 measures whether any of it works on long tasks.

> [!QA]
> Q: What does "self-improving" mean in this course?
> A: A loop with no new human labels. The model generates many attempts at problems, a fast automatic verifier picks the winners, and the model trains on those winners. The improved model then generates better attempts. Test-time compute makes the data. Train-time compute absorbs it.
> Follow-up: Why not just train on more human-written data?
> A: Human labels are slow and expensive, and for hard reasoning there are few sources with step-by-step traces on the internet. The loop manufactures its own supervision. Its limit is the verifier: it only works where answers can be checked automatically and fast.

> [!QA]
> Q: What is the difference between test-time compute and train-time compute?
> A: Test-time compute is effort spent producing an answer: sampling many candidates, writing long reasoning traces, calling tools. The model's weights stay fixed. Train-time compute is effort spent updating the weights: fine-tuning or reinforcement learning on data. The lectures' key move is joining them: test-time scaling manufactures training data, which train-time scaling absorbs, which makes the next round of test-time scaling stronger.
> Follow-up: Which one mattered more in the DeepSeek and o1 results?
> A: The combination. Test-time scaling alone needs a verifier at answer time and pays per question. Training on the verified attempts raises the single-attempt accuracy, so you pay less per question later. The lecture presents them as one flywheel, not two alternatives.

> [!QA]
> Q: Why is chain of thought a big deal if the toy is just tennis balls?
> A: The toy shows the mechanism, not the power. Writing steps turns one hard leap into many easy steps, and each step can be checked or corrected. The striking fact is that only large models benefit: at around 8 billion parameters, chain of thought does nothing. At larger sizes it unlocks reasoning. The ability itself is emergent.
> Follow-up: Does the model ever correct itself?
> A: Yes, and the lecture calls this out as a core reasoning-model behavior. Mid-trace the model writes that something looks wrong and backtracks. That self-correction, plus task decomposition and trying alternatives, is what the long thinking traces of o1-style models consist of.

## Recap: the whole lesson on one screen

1. **One shot wastes knowledge.** A model can know an answer it
   will not give on the first try. Agent tasks, multi-step work
   with tools and feedback, never fit in one shot.
2. **Scaling hit a wall.** Bigger models, more data, more compute
   drove a decade of gains, then saturated around 2024. The new
   axis is the model improving itself.
3. **Thinking out loud.** Chain of thought breaks one hard leap
   into checkable steps. Roger has 5 balls, buys 2 cans of 3:
   5 + 6 = 11. Only large models can use it.
4. **The monkeys result.** Sampled 10,000 times with a verifier,
   a small 8B model solves IMO-level problems. The knowledge is
   in the weights. One shot cannot reach it.
5. **The key question.** What if the model generates many
   attempts, keeps the verified winners, and trains on them?
6. **The loop.** Generate many tries, verify automatically, train
   on winners, repeat. Test-time compute makes data. Train-time
   compute absorbs it.
7. **Map back.** Sampling surfaces tail knowledge. The verifier
   selects without humans. Training moves winners into the first
   try.
8. **The honest price.** The verifier is the bottleneck. It must
   be fast and honest. Slow or subjective domains stay outside
   the loop.

## Official sources and further reading

**Official:**
- CS329A Lecture 1 (Autumn 2025): the lecture this chapter
  follows, in its order. https://www.youtube.com/watch?v=6YnLB0XbTnI
- CS329A course site: https://cs329a.stanford.edu

**Further reading:**
- Brown et al., "Large Language Monkeys" (2024): the repeated
  sampling result the lecture leans on.
- OpenAI o1 release notes (Sept 2024): log-linear test-time
  scaling on hard math, cited in lecture.

**Caveats from these sources.** The lecture dates are Autumn
2025. Model names and benchmark numbers are snapshots from then.
The "ten thousand samples" monkeys figure is for coverage with an
oracle verifier, not single-attempt accuracy. Saturation of
pretraining scaling is the lecturers' framing of 2024, not a
measured constant.

## Connections to the other courses

- **CS329Z:** the engineering counterpart. This course asks how
  agents can improve themselves. CS329Z covers how to build them:
  tool use, function calling, ReAct, evaluation, infrastructure.
- **CS336:** where the base models come from: pretraining,
  scaling laws, and the transformer the agents are built on.
- **CS229S:** the systems view of the compute the loop burns:
  training cost, inference cost, and why test-time scaling is a
  systems problem too.
