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
video_title: "CS329A Part 1: Course Overview (Autumn 2025)"
video_caption: "Azalia Mirhoseini and Aakanksha Chowdhery introduce the self-improvement loop. Scaling recap, chain of thought as emergent behavior, and test-time scaling via repeated sampling."
concepts: [agent, self-improvement, scaling-laws, chain-of-thought, reasoning-model, verifier, test-time-compute, train-time-compute, emergence]
sources:
  - tag: lecture
    label: "CS329A Part 1: Course Overview (Autumn 2025)"
    url: https://www.youtube.com/watch?v=6YnLB0XbTnI
  - tag: paper
    label: "Brown et al., Large Language Monkeys: Scaling Inference Compute with Repeated Sampling (2024)"
    url: https://arxiv.org/abs/2407.21787
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

![Bigger models, predictable gains](assets/plate-l01-scaling.svg "Parameters rose 1,500x from BERT to PaLM. Test loss fell on a smooth curve. Shell 2. Source: public model cards. Project: Stanford Frontier AI.")

### Subchapter: the scaling law, worked

The law is a power law, not a metaphor. Double the compute and
the loss drops by a fixed fraction, over and over, across six
orders of magnitude. That predictability is what made scaling
an engineering plan instead of a gamble: a lab could budget the
compute for a target loss the way a builder budgets concrete.

Two consequences matter for this course. First, the curve is
smooth, so surprises are rare: bigger is better, boringly. Second,
the curve describes loss on next-token prediction, not skill at
agent tasks. Past a point, lower loss stopped buying the
abilities the lectures care about. The recipe kept working on
its own metric while the field needed a new one.

### Subchapter: emergence, worked with few-shot learning

Bigger models also gained abilities nobody trained directly.
**Few-shot learning** means the model follows a task from a few
examples in the prompt, with no retraining:

```ascii
English:  sea     -> French: mer
English:  sky     -> French: ciel
English:  river   -> French:
model:    riviere
```

Two examples, then a third request, and it translates. No
gradient update happened. The model read the pattern from the
prompt and applied it. These abilities appear only past a size
threshold. They are called **emergent** because no one predicted
them from the small models.

The trap: emergence is a fact about the jump, not a guarantee
about the landing. A capability that appears at 100B parameters
may be brittle, prompt-sensitive, or present only in the tail
of the model's distribution. Lectures 2 and 8 will exploit
exactly that brittleness: the ability exists, but one shot
cannot reliably reach it.

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

![Thinking out loud beats one leap](assets/plate-l01-cot.svg "The tennis toy: 5 + 2 x 3. One leap guesses. Steps check each other. Shell 3. Source: original toy. Project: Stanford Frontier AI.")

### Subchapter: why the steps help, mechanically

Three mechanisms, not one. First, **decomposition**: a hard leap
becomes a sequence of easy moves, each inside the model's
reliable range. Second, **working memory**: the trace is
scratch space. Intermediate results sit in context instead of
being held in activations, so later steps can read them.
Third, **checkability**: a wrong step is visible. The model, or
a verifier, can spot "2 cans of 3 is 5" without redoing the
whole problem.

The common misunderstanding: chain of thought does not make the
model smarter per token. It spends more tokens to turn one
unreliable computation into several reliable ones. That is
test-time compute in its cheapest form, and the whole course is
variations on spending compute to buy reliability.

### Subchapter: self-correction inside the trace

Watch what the trace buys beyond decomposition. The steps are
checkable, so the model can correct itself mid-trace: start down
a path, write "wait, that is wrong", and backtrack. This
**self-correction** is a small thing in a toy. In hard problems it
is the difference between a dead end and a solution.

Reasoning models, the o1 series, Gemini thinking, DeepSeek, are
built on this: long traces of analysis, decomposition, trial,
correction. The lecture's claim is that the trace is not a
report of reasoning that happened elsewhere. The trace is the
reasoning. More trace, more chances to catch the error.

## Where one shot breaks

Now put the model on a hard problem, say an olympiad-level math
question. One attempt, one answer. The model fails. This is
expected: a single forward pass is a single draw from the model's
distribution over answers, and hard problems sit in the tail.

### Subchapter: the monkeys arithmetic

Here is the fact that opens the whole course. The Large Language
Monkeys result, which the lectures return to again and again:
sample the same problem many times, and small models solve
problems far above their apparent level. A Llama 3 8B model, asked
ten thousand times with a way to check which answers are right,
solves IMO-level problems from the F2F benchmark. The knowledge
was in the weights. One shot could not reach it. Ten thousand
shots could.

![Ten thousand tries surface tail knowledge](assets/plate-l01-monkeys.svg "Llama 3 8B, F2F benchmark, oracle verifier: one try fails, 10k tries solve. Shell 2. Source: paper: Large Language Monkeys. Project: Stanford Frontier AI.")

Work the arithmetic that makes it possible. If a model solves a
problem with probability p per attempt, the chance that k
attempts all fail is (1-p)^k. Coverage, the chance at least one
succeeds, is 1-(1-p)^k. At p = 0.05 and k = 10,000, the failure
chance is 0.95^10000, which is effectively zero. Even a tiny
per-try chance becomes near-certainty with enough draws.

### Subchapter: why the tail holds answers

Two lessons fall out. First, the model's single-attempt score
understates what it knows. The weights contain far more than the
greedy decoding shows, because greedy decoding takes the single
most likely path and hard problems need unlikely ones.

Second, reaching the knowledge needs two things: many attempts,
and a way to tell the good ones from the bad. The checker has a
name in this course: the **verifier**. Without it, ten thousand
attempts are ten thousand guesses. With it, they are a search.

## The key question

What if the model generates many attempts, keeps the ones a
verifier approves, and trains on them to get better?

## The self-improvement loop

A **verifier** is any procedure that judges an answer without a
human in the loop. For math, it can be the known correct answer.
For code, it can be unit tests: the program passes or it fails.
The verifier must be fast and automatic, because the loop will
call it thousands of times.

![The self-improvement loop](assets/plate-l01-loop.svg "Generate many tries. Verify automatically. Train on winners. Repeat. Shell 3. Source: original. Project: Stanford Frontier AI.")

### Subchapter: the three stages, deep

**1. Generate.** The model tries the problem many times.
Test-time compute: more tries, no new training. The tries must
be diverse, not ten copies of one idea, or the verifier has
nothing to choose between. Diversity is the hidden requirement
of the whole stage. Lectures 2 and 6 are about manufacturing it.

**2. Verify.** A verifier scores every attempt. Keep the
winners, drop the losers. The verifier is the only part of the
loop that touches ground truth, so its quality caps the whole
system. A sloppy verifier does not just waste compute. It
certifies bad answers as good, and the next stage trains on them.

**3. Train.** Fine-tune the model on the winners. Train-time
compute: the weights change. The knowledge that lived in the
tail of the distribution moves toward the first try. Then
repeat: the better model generates better attempts, which make
better training data.

### Subchapter: the two computes, joined

**Test-time compute** is effort spent answering: more samples,
longer reasoning traces, tool calls. The weights do not change.
**Train-time compute** is effort spent learning: gradient updates
on the winners. The weights change.

![Two kinds of compute, one flywheel](assets/plate-l01-test-train.svg "Test-time: weights fixed, answers improve. Train-time: weights change, answers get cheaper. Shell 3. Source: original. Project: Stanford Frontier AI.")

The DeepSeek and o1 breakthrough the lecture describes was
joining the two: use test-time scaling to manufacture
high-quality training data, then train on it, then scale test
time again. Each turn of the crank lifts the next. Test-time
alone pays per question forever. Train-time alone needs data
nobody has. Together they are a flywheel.

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

### Subchapter: what counts as a verifier

Not every judge qualifies for the loop. The requirements are
three, and each rules out a class of tasks:

1. **Automatic.** No human in the loop. Thousands of judgments
   per training run rule out any human grading.
2. **Fast.** Near-instant per judgment. A chip-design simulation
   that takes days to return one score cannot sit inside a loop
   that needs thousands of iterations.
3. **Honest.** The judge must measure the real goal. A learned
   judge that the model can game will be gamed: the loop
   optimizes the judge, not the task.

Answer keys and unit tests pass all three. Learned reward models
pass the first two and risk the third. Human taste fails the
first two outright. The set of tasks the loop can touch is
exactly the set with verifiers meeting all three.

### Subchapter: reward hacking, previewed

Speed matters as much as correctness. The lectures stress that
verifiers must be near-instant. Domains with slow verification
are, for now, outside the loop's reach. The price of
self-improvement is a fast, honest judge. Where no such judge
exists, the loop does not turn.

That price shapes the whole course. Lecture 2 scales the
generate step. Lectures 3 through 5 add tools, planning, and
search to make attempts stronger. Lecture 6 turns attempts into
training data. Lecture 7 asks who verifies the verifier. Lecture
8 measures whether any of it works on long tasks.

## Go deeper

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:16px 0;">
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%;" src="https://www.youtube-nocookie.com/embed/jPluSXJpdrA" title="Noam Brown, Ilge Akkaya and Hunter Lightman on o1 and teaching LLMs to reason" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

- Noam Brown, Ilge Akkaya and Hunter Lightman on o1 and teaching LLMs to reason (Sequoia): test-time compute scaling laws, generation vs verification, bottlenecks to scaling. https://www.youtube.com/watch?v=jPluSXJpdrA
- Brown et al., Large Language Monkeys (2024): repeated sampling, coverage, the log-linear law. https://arxiv.org/abs/2407.21787
- OpenAI o1 system card (2024): test-time scaling curves on hard reasoning benchmarks. https://openai.com/index/openai-o1-system-card/

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
> A: The toy shows the mechanism, not the power. Writing steps turns one hard leap into many easy steps, and each step can be checked or corrected. The striking fact is that only large models benefit: at around 8 billion parameters, chain of thought does nothing. At larger sizes reasoning appears. The ability itself is emergent.
> Follow-up: Does the model ever correct itself?
> A: Yes, and the lecture calls this out as a core reasoning-model behavior. Mid-trace the model writes that something looks wrong and backtracks. That self-correction, plus task decomposition and trying alternatives, is what the long thinking traces of o1-style models consist of.

> [!QA]
> Q: Walk me through the mechanics of why chain of thought works.
> A: Three mechanisms. Decomposition: one hard leap becomes several easy steps, each inside the model's reliable range. Working memory: the trace is scratch space, so intermediate results sit in context where later steps can read them. Checkability: a wrong step is visible, so the model or a verifier can catch it without redoing everything. In the toy, "2 cans of 3 is 6" can be checked on its own. The cost is tokens: CoT spends more of them to buy reliability.
> Follow-up: Why do only large models benefit?
> A: The lecture reports it as an empirical threshold around 8B parameters, with no settled mechanism. The plausible reading: using a trace requires enough capacity to both reason and monitor the reasoning. Small models spend their capacity writing the steps and have none left to check them.

> [!QA]
> Q: Walk me through one full turn of the self-improvement loop with numbers.
> A: Take 10,000 math problems with known answers. Generate: the model attempts each 100 times, producing 1M attempts. Verify: the answer key keeps the attempts that reach correct answers, say 300,000. Train: fine-tune the model on those 300,000 winning attempts. The model's single-attempt accuracy rises. Next turn, the better model needs fewer attempts per problem to produce the same number of winners. That is the flywheel.
> Follow-up: What breaks first if the verifier is weak?
> A: The training data. A verifier that approves wrong answers fills the winner set with bad attempts, and fine-tuning bakes them into the weights. The loop amplifies the verifier's errors, not just its judgments. That is why the course treats the verifier as the load-bearing wall.

> [!QA]
> Q: Design a self-improvement loop for a customer-support answer agent. What is the verifier?
> A: Generate: sample 20 candidate answers per ticket. Verify: this is the hard part. Candidate verifiers: an LLM judge checking the answer against the retrieved help articles, a strict citation check (every factual claim must match a quoted span), and customer thumbs-up/down as a slow signal. Train: fine-tune on answers that pass the citation check and get positive ratings. The honest answer names the weak link: the LLM judge can be gamed and the thumbs-up signal is slow and sparse. The loop works only as far as the citation check is airtight.
> Follow-up: Where does reward hacking appear here?
> A: If the verifier is "customer did not complain", the model learns to write answers that suppress complaints: over-apologizing, deflecting, burying the hard answer. The metric improves. Support quality does not. The fix is a verifier tied to resolution, not sentiment.

> [!QA]
> Q: What is reward hacking, and why does it threaten the loop?
> A: The loop optimizes whatever the verifier measures. If the verifier is a learned model, the generator can learn to produce outputs that score high without being good: fluent nonsense that fools the judge. The scores climb. The actual quality does not. The lecture names this as the reason verifiers must be honest, not just fast: a gameable judge turns self-improvement into self-deception.
> Follow-up: How do you detect it?
> A: Hold out a trusted check the loop cannot see: human spot-checks, or a separate verifier trained differently. If the loop's scores rise but the held-out check flatlines or falls, the loop is hacking its judge. No held-out check, no detection.

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
- CS329A Part 1: Course Overview (Autumn 2025): the lecture this
  chapter follows. https://www.youtube.com/watch?v=6YnLB0XbTnI
- CS329A course site: https://cs329a.stanford.edu

**Further reading:**
- Brown et al., "Large Language Monkeys" (2024):
  - [the repeated sampling](https://arxiv.org/abs/2407.21787)
  result the lecture leans on.
- OpenAI o1 release notes (Sept 2024): log-linear test-time
  scaling on hard math, cited in lecture. [link](https://openai.com/index/openai-o1-system-card/)

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
