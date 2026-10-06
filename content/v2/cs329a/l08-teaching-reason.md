---
page_id: cs329a-l08
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 8
nav: "L08 · Teaching Reason"
title: "Lecture 8: Teaching the Model to Reason: STaR"
summary: "Test-time tricks find answers but the model never learns. STaR closes the loop: generate rationales, keep the ones that reach right answers, and for failures, hand the model the answer and ask it to show its work."
date: "2025-10-29"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: yVnmHSAy3ck
concepts: [star, train-time-scaling, rationalization, bootstrapping, self-training, off-policy-rl, grpo, verifiable-rewards, deepseekmath]
sources:
  - tag: lecture
    label: "CS329A Lecture 6: train-time scaling, RL (Autumn 2025)"
    url: https://www.youtube.com/watch?v=yVnmHSAy3ck
  - tag: paper
    label: "Zelikman et al., STaR: Bootstrapping Reasoning With Reasoning (2022)"
  - tag: paper
    label: "Shao et al., DeepSeekMath (2024)"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: nobody wrote down how to think

Lecture 2 found answers by sampling. But the model never
learned: every question paid the sampling bill again. To move
answers from the tail into the first try, the model must train
on reasoning itself. Here is the blocker: the internet has
almost no step-by-step reasoning traces at scale. Human
annotation is slow and expensive. Prompting with a few examples
underperforms training on large data. The data the loop needs
does not exist.

## The key question

What if the model could manufacture its own reasoning data,
using known answers to sort its own attempts into good and bad?

## The loop, worked on a toy

**STaR** (Self-Taught Reasoner) is the answer. Start with two datasets. A small **prompt set**: a few problems
with human-written rationales, the worked examples. A large
**training set**: many problems with questions and correct
answers, but no rationales. Say 10,000 problems. The loop:

```ascii
round 1:
  few-shot prompt the model with the prompt set's rationales
  model attempts all 10,000 problems, writing rationales
  keep the 3,000 with correct answers  ->  new training data
  fine-tune the model on those 3,000

round 2:
  the better model attempts the 7,000 it missed
  keep the new winners, fine-tune again
  ...
```

Each round converts some failures into training data, and the
improved model converts more next round. That is the
**bootstrapping**: the model pulls itself up, with the correct
answers as the only outside supervision. The lecture calls it a
bare-bones off-policy RL: generate with the current policy,
keep what worked, train, repeat.

## The clever half: rationalization

Keeping winners handles the 3,000 the model could already solve.
What about the 7,000 it could not? Throwing them away wastes the
hardest problems, exactly the ones worth learning. STaR's second
move is **rationalization**: for a failed problem, give the model
the correct answer as a hint and ask it to produce the rationale.

```ascii
problem:   "A train travels... " (model answered 37, wrong)
hint:      "The correct answer is 42. Show your work."
model:     writes a rationale ending at 42
training:  fine-tune on (problem, rationale, 42) WITHOUT the hint
```

The hint is scaffolding, removed before training. The model
learns the problem as if it had solved it directly. This
expands the training set beyond what the model can solve alone,
into problems it can only solve with the answer in hand. Over
rounds, as the model improves, fewer hints are needed: the
frontier of solvable problems advances.

## The three assumptions, named

The lecture lists the assumptions STaR stands on, because each
is a place it can break:

1. **Correct answer implies good rationale.** Filtering keeps
   attempts that reached the right answer, assuming the
   reasoning was sound. A lucky guess with broken steps passes
   the filter and teaches broken reasoning.
2. **The model can rationalize from a hint.** Given the answer,
   the model must produce a valid path to it. If the problem is
   far beyond the model, the "rationale" is confabulation, and
   training on it teaches confabulation.
3. **The base model is strong enough to bootstrap.** Some
   fraction of problems must be solvable in round 1, or the
   loop never starts. The method cannot lift a model into a
   domain it cannot touch at all.

## Where it breaks, demonstrated

Assumption 1 is the live wire. The lecture's discussion
presses it: in step 3, rationalization, there is no filter on
the generated rationale's quality. A model handed the answer
42 can write steps that do not actually lead to 42, or lead
there by accident. Fine-tuning on those steps bakes the bad
reasoning into the weights. The lecture notes follow-up work
adding process-level filters, judging each step, but STaR
itself has none. Final-answer correctness is a proxy for
reasoning quality, and proxies leak.

Assumption 3 bounds the ambition. STaR hill-climbs within
reach of the base model. It does not invent new capabilities
from nothing. The iterative rounds extend the reach, but the
starting foothold must exist.

And the lecture's candid admission: learning from negative
examples is not nailed. Failed attempts without successful
rationalization are discarded. The loop learns from what
worked and ignores the rest.

## The industrial version: DeepSeekMath and GRPO

The lecture presents DeepSeekMath as the same idea at
industrial scale. Generate many reasoning traces, verify
against known answers, and train with RL rather than plain
fine-tuning. The algorithm named is **GRPO**, a policy-gradient
method that compares groups of sampled attempts and pushes the
policy toward the better ones. The core is unchanged from STaR:
verifiable rewards, the model's own generations as data, and
the loop turning test-time sampling into train-time capability.
The difference is scale and the RL machinery that squeezes
more from each verified batch.

## Mapping back: what closing the loop buys

| Test-time-only failure | Train-time answer | How |
|---|---|---|
| Every question pays the sampling bill | Train on verified attempts | Winners become training data. Pass@1 rises, so fewer samples needed later. |
| No reasoning data on the internet | Generate it | The model's own attempts, filtered by correct answers, are the dataset. |
| Hard problems never solved, never learned | Rationalization | Hand the model the answer as a hint, keep the rationale, train without the hint. |
| One round, then stall | Iterate | Each round's better model solves more. The frontier advances. |

## The honest price

STaR assumes the answer key exists: it needs problems with
known correct answers, which means verifiable domains, math
and code, again. It assumes correct answers imply good
reasoning, which leaks. It learns nothing from failures it
cannot rationalize. And it can regress: the lecture's Q&A notes
that training on broken reasoning chains, overthinking traces
that loop without progress, can infect the model. The loop is
powerful and blind. What it cannot check, it cannot help but
absorb.

That blindness is the next chapter's subject. If the verifier
is the loop's judge, and the judge is learned, who judges the
judge?

> [!QA]
> Q: What is STaR, in one paragraph?
> A: Self-Taught Reasoner. Start with a few human-written rationales and many problems with known answers but no rationales. Few-shot prompt the model to attempt all problems writing rationales. Keep the attempts with correct answers and fine-tune on them. For failures, give the model the correct answer as a hint, have it write the rationale, and fine-tune on those too, without the hint. Repeat. The model's own verified attempts become its reasoning training data.
> Follow-up: Why is it called off-policy RL?
> A: Because data generation and learning are decoupled. The current policy generates attempts, a filter keeps winners, and training updates the policy on that fixed dataset, like learning from someone else's experience. Then the new policy generates again. It is RL in the generate-filter-train loop sense, without online gradient steps per attempt.

> [!QA]
> Q: What is rationalization and why does it matter?
> A: Giving the model the correct answer as a hint and asking it to produce the reasoning that leads there, then training on the result as if the model solved it unaided. It matters because it rescues the hard problems: without it, training data is limited to what the model can already solve, and the loop can never reach beyond its current ability. With it, the frontier advances each round.
> Follow-up: What is the danger?
> A: Confabulated rationales. If the problem is too hard, the model writes steps that do not genuinely lead to the answer, and fine-tuning bakes that fake reasoning in. STaR has no filter on rationale quality beyond final-answer correctness. The lecture flags this as the method's weakest point and points to process-level judging as the fix.

> [!QA]
> Q: What are STaR's three assumptions?
> A: One, a correct final answer implies a good rationale, so filtering on answers filters for reasoning quality. Two, the model can generate a valid rationale when given the answer as a hint. Three, the base model is strong enough that some problems are solvable in round one, so bootstrapping starts. Break any one and the loop stalls or teaches bad reasoning.
> Follow-up: Which assumption fails most often in practice?
> A: The first. Correct answers with wrong reasoning are common: lucky guesses, flawed steps that cancel out, proofs with gaps. The lecture stresses that final-answer correctness is only a proxy for reasoning quality, and that building step-level judges, process reward models, is the active research direction aimed at this exact leak.

## Recap: the whole lesson on one screen

1. **No reasoning data exists.** The internet has answers, not
   step-by-step traces. Human annotation is too slow.
2. **STaR manufactures it.** Attempt 10,000 problems, keep the
   3,000 with correct answers, fine-tune, repeat.
3. **Rationalization.** For failures, give the answer ("42")
   as a hint, keep the rationale, train without the hint.
   Hard problems enter the training set.
4. **Bootstrapping.** Each round's better model solves more.
   The solvable frontier advances.
5. **Three assumptions.** Correct answer implies good
   rationale. The model can rationalize from hints. The base
   model can start the climb.
6. **The leak.** No filter on rationale quality. Broken steps
   that reach right answers get baked into the weights.
7. **Industrial form.** DeepSeekMath: same loop at scale,
   with GRPO pushing the policy toward better sampled groups.
8. **The honest price.** Needs answer keys. Learns nothing
   from un-rationalizable failures. Can absorb broken
   reasoning. Who judges the judge is next.

## Official sources and further reading

**Official:**
- CS329A Lecture 6 (Autumn 2025): the lecture this chapter
  follows. https://www.youtube.com/watch?v=yVnmHSAy3ck
- Zelikman et al., "STaR: Bootstrapping Reasoning With
  Reasoning" (2022): the algorithm.
- Shao et al., "DeepSeekMath" (2024): the industrial-scale
  version with GRPO.

**Further reading:**
- Zelikman et al. follow-ups on process filtering: judging
  rationale steps, not just final answers.

**Caveats from these sources.** The 10,000/3,000 numbers are
the lecture's representative illustration, not a reported
experiment. GRPO details are named, not derived, in the
lecture. The "learning from negatives not nailed" assessment
is the lecturers' summary of the field as of Autumn 2025.

## Connections to the other courses

- **CS329A L02:** the test-time half this chapter closes:
  sampling finds answers. STaR moves them into the weights.
- **CS329A L04:** the same keep-the-winners loop for code,
  with execution as the verifier instead of answer keys.
- **CS329A L09:** the leak this chapter leaves: judging
  reasoning steps, and the meta-verifier that judges judges.
- **CS336:** the training machinery underneath: fine-tuning
  and RL on language models.
