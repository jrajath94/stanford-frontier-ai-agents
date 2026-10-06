---
page_id: cs329a-l06
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 6
nav: "L06 · Sampling at Scale"
title: "Lecture 6: Sampling at Scale: AlphaCode to AlphaCode 2"
summary: "One program will not solve a hard coding problem, but a million might contain the answer. AlphaCode's lesson: generate at massive scale, then solve the selection problem. AlphaCode 2's lesson: learn the selector."
date: "2025-10-22"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: -Uni9dqyuuDM
concepts: [alphacode, large-scale-sampling, ten-at-k, clustering, diversity, selection-bottleneck, reward-model, scoring-model]
sources:
  - tag: lecture
    label: "CS329A Lecture 5: search in code models (Autumn 2025)"
    url: https://www.youtube.com/watch?v=-Uni9dqyuuDM
  - tag: paper
    label: "Li et al., Competition-Level Code Generation with AlphaCode (2022)"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: one shot cannot solve competition coding

Competitive programming problems are brutal. A problem statement
describes a puzzle. The solution is a program that must pass
hidden tests on correctness and efficiency. A single generated
program almost never passes. The lecture's question: can scale
succeed where cleverness fails?

The setup matters. In the AlphaCode evaluation, the model may
generate up to a million candidate programs per problem, but it
may submit only 10 for grading against the hidden tests. This is
the **10@k metric**: generate k samples, submit at most 10. It
measures two things at once: the raw search power of sampling,
and the quality of the filtering that picks the final 10.

## First attempt: sample blindly, submit randomly

Suppose you generate 1,000 programs and submit 10 at random.
Most of the 1,000 are variations of the same few ideas: the
model's distribution has favorite patterns, and blind sampling
repeats them. Your 10 random submissions are likely 10 versions
of the same wrong approach. The million samples are wasted
because they are not a million different ideas.

This is the **diversity** problem, and the lecture hammers it:
sampling more only helps if the new samples are different. Ten
copies of one wrong program are one wrong program.

## The key question

If we generate at massive scale and select a diverse, promising
few, how far does sampling alone go, and what limits it?

## AlphaCode: scale plus clustering

AlphaCode's pipeline has three stages. Generate a huge number of
samples. Filter out the ones that fail the problem's example
tests. Then **cluster** the survivors: group programs that behave
the same on generated test inputs, and submit one representative
per cluster. Clustering is a heuristic for diversity: programs in
different clusters do different things, so 10 submissions cover
10 genuinely different approaches instead of 10 copies.

The numbers, from the lecture's validation results. Three
systems, submitting 10 programs out of 1,000 generated:

```ascii
model                    10@1K solve rate
9B parameters            lowest
41B parameters           higher
41B + clustering         highest of the three
```

Two trends. Larger models do better at every sample count, and
clustering helps at every model size. Now scale the samples.
Going from 10@1K to 10@1M, the solve rate climbs log-linearly,
the same straight line against log samples from Lecture 2.
Bigger models have steeper slopes: the 41B curve rises faster
than the small model at the bottom.

Then the sobering comparison. With unlimited submissions,
**pass@k**, the solve rate at large k passes 40 percent. With
only 10 submissions, **10@k**, it stalls near 30 percent. The gap
is the **selection bottleneck**: the right program is usually
somewhere in the million, but the filter cannot always find it.
Sampling solved generation. Selection is now the binding
constraint.

The lecture adds two honest observations from the paper. First,
the model was trained on loss, and loss is a poor proxy for
solve rate: many different programs solve a problem, and the
training objective does not know that. The model was notably
weak on dynamic programming and constructive algorithms.
Second, the approach was verified to generalize: the generated
code showed novelty against the training data, not memorization.
It was reasoning, expensively.

## AlphaCode 2: learn the selector

AlphaCode 2 attacks the bottleneck directly, with three changes
the lecture walks through.

First, stop pretraining your own model. Fine-tune an existing
strong model, Gemini Pro in the paper's case, on competitive
programming data. Better base, fewer samples needed for the same
coverage.

Second, manufacture diversity instead of hoping for it.
Fine-tune not one model but a family of variants, with different
hyperparameters, difficulty tags, and data mixes. Each variant
has different favorite patterns, so massive sampling across the
family covers genuinely different approaches. Diversity becomes a
design choice, not a sampling accident.

Third, and most important, replace the heuristic filter with a
**learned scoring model**. Instead of clustering by behavior and
hoping the representatives are good, train a reward model to
predict which candidates are actually correct, and submit its
top picks. The selector is now learned from data rather than
hand-designed.

The lecture's summary of the effect: better models need fewer
samples for the same performance, and at a million samples the
learned selector reaches much higher. The pipeline is the same
shape, generate then select, but both stages got smarter.

## Where it breaks: diversity must keep growing

The method has one fragile assumption, and the lecture states it
plainly. The log-linear gains continue only if new samples keep
being different. If you sample 10 times more but the model
repeats its favorite patterns, the extra samples add nothing.
Clustering and model families are patches over a deeper issue:
the model's output distribution has limited true diversity, and
no selection method can submit a good program that was never
generated.

There is also the domain limit. One-shot massive sampling works
for problems solvable in one program. For problems needing many
dependent steps, where step 2 depends on step 1's result, the
lecture notes that multi-step approaches do better. Sampling is
breadth. Some problems need depth.

## Mapping back

| Problem | AlphaCode answer | AlphaCode 2 upgrade |
|---|---|---|
| One program rarely passes | Generate up to 1M candidates | Fine-tuned Gemini Pro family: better base, fewer samples needed |
| 10 random submissions repeat one idea | Cluster by behavior, submit per-cluster representatives | Family of diverse model variants: diversity by design |
| Heuristic filter misses winners | 10@k still log-linear, but capped near 30% vs 40%+ unlimited | Learned scoring model predicts correctness. Submits its top picks |
| Loss does not measure solving | Honest gap: weak on DP and constructive algorithms | Better data (CodeContests v2) plus the scoring model |

## The honest price

A million samples per problem is a research demonstration, not a
product. The selection bottleneck means most of the generation
budget is wasted on programs never submitted. Diversity is not
free: it must be engineered through clustering, model families,
or better base models. And the whole pipeline assumes cheap,
automatic checking: example tests to filter on, hidden tests to
grade against. No verifier, no AlphaCode.

The deeper lesson the lecture draws: sampling and selection are
two separate problems. Lectures 2 and 6 scaled the first. The
second, picking winners well, is where learned reward models
enter, and where the next chapter's troubles begin: who verifies
the verifier.

> [!QA]
> Q: What does 10@k actually measure?
> A: Generate k candidate programs, submit at most 10 for grading on hidden tests. It measures generation and selection together: whether the right program appears among the k, and whether the filter picks it. In the lecture's numbers, 10@1M beats 10@1K log-linearly, but 10@k stalls near 30 percent while unlimited pass@k passes 40 percent. The gap is the selection bottleneck.
> Follow-up: Why not just submit all k?
> A: Because grading is the expensive, trusted step: hidden tests run by the benchmark. The 10-submission limit models reality, where you cannot try a million things against the real world. The limit is what makes selection a problem worth solving.

> [!QA]
> Q: Why does clustering help?
> A: Blind sampling repeats the model's favorite patterns, so 10 random submissions may be 10 versions of one wrong idea. Clustering groups behaviorally identical programs and submits one per cluster, so the 10 submissions cover 10 genuinely different approaches. In the lecture's table, 41B with clustering beats 41B without it at every sample count. It is a heuristic: cheap, no training, and consistently useful.
> Follow-up: What replaced clustering in AlphaCode 2?
> A: A learned scoring model, a reward model trained to predict which candidates are correct. Clustering says "these programs differ". The scoring model says "this one is likely right". Learning the selector beats the heuristic, at the cost of needing scored training data.

> [!QA]
> Q: What is the selection bottleneck, exactly?
> A: The gap between what sampling can find and what the filter can pick. At large k, the correct program is usually somewhere in the generated set: unlimited-attempt solve rates pass 40 percent. But with only 10 submissions allowed, the rate stalls near 30 percent. The missing 10 points are programs that were generated and then not chosen. Better generation cannot fix this. Only better selection can.
> Follow-up: Does this generalize beyond code?
> A: Yes. Anywhere you generate many candidates and keep few, math proofs, agent trajectories, the picker is the binding constraint once generation is strong enough. The lecture's framing is general: scale the generator, then the selector becomes the research problem.

## Recap: the whole lesson on one screen

1. **One shot fails.** Competition coding needs programs that
   pass hidden tests. Single generations almost never do.
2. **10@k.** Generate k programs, submit at most 10. Measures
   search power and filtering together.
3. **Diversity or waste.** Blind sampling repeats favorite
   patterns. Ten copies of one wrong program are one wrong
   program.
4. **AlphaCode.** Generate up to 1M, filter on examples,
   cluster by behavior, submit per-cluster picks. 41B plus
   clustering beats 41B beats 9B. Log-linear in samples.
5. **The bottleneck.** Unlimited submissions pass 40 percent.
   10 submissions stall near 30. The winners are generated but
   not picked.
6. **AlphaCode 2.** Fine-tune Gemini Pro, not from scratch. A
   family of diverse variants. A learned scoring model replaces
   heuristic clustering.
7. **The fragile assumption.** Gains continue only if new
   samples stay diverse. Sampling is breadth. Some problems
   need depth.
8. **The honest price.** A million samples per problem is a
   demo, not a product. No verifier, no pipeline.

## Official sources and further reading

**Official:**
- CS329A Lecture 5 (Autumn 2025): the lecture this chapter
  follows. https://www.youtube.com/watch?v=-Uni9dqyuuDM
- Li et al., "Competition-Level Code Generation with
  AlphaCode" (2022): the 10@k setup, clustering, the scaling
  curves.

**Further reading:**
- AlphaCode 2 technical report (2023): the Gemini fine-tune,
  model family, and learned scoring model.
- CodeContests dataset: the open benchmark both papers build
  on.

**Caveats from these sources.** The 40-vs-30 percent figures
are the lecture's validation-set readings, approximate. Model
sizes (9B, 41B) and the Gemini Pro base are 2022-2023
snapshots. The novelty-over-memorization check is the paper's
own analysis.

## Connections to the other courses

- **CS329A L02:** the same log-linear sampling law, now with
  a submission limit that exposes the selector.
- **CS329A L04:** the same hidden-test discipline: RLEF's
  private tests are AlphaCode's hidden tests, used as reward.
- **CS329A L07:** the selector's next form: learned verifiers,
  and what happens when they err.
- **CS329Z:** running this pipeline in practice: sandboxed
  execution at scale and submission infrastructure.
