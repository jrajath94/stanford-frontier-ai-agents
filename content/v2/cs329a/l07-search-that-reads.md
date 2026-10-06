---
page_id: cs329a-l07
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 7
nav: "L07 · Search That Reads"
title: "Lecture 7: Search That Reads: Deep Research Agents"
summary: "Reasoning models have knowledge cutoffs and silent gaps. A deep research agent notices its own uncertainty, searches mid-thought, and reads the documents instead of dumping them into context."
date: "2025-10-22"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
concepts: [deep-research, agentic-rag, search-o1, knowledge-gap, uncertainty-trigger, reason-in-documents, retrieval]
sources:
  - tag: lecture
    label: "CS329A Lecture 5, second half: deep research agents (Autumn 2025)"
    url: https://www.youtube.com/watch?v=-Uni9dqyuuDM
  - tag: paper
    label: "Search-o1: Agentic Search-Enhanced Large Reasoning Models"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: the model does not know what happened yesterday

Large reasoning models are trained with a knowledge cutoff. If
something happened yesterday, it is not in the weights. Worse,
the model does not always admit the gap. The lecture points to a
telltale: on the GPQA science benchmark, reasoning traces fill
with uncertainty words, "perhaps", "alternatively", "wait". The
model is guessing past its knowledge, and the guesswork
propagates. One wrong guess early in a long chain cascades into
a wrong final answer.

A **knowledge gap** is a point in the reasoning where the model
needs a fact it does not reliably have. The naive fix is
retrieval-augmented generation (RAG): turn the question into a
search query, fetch documents, paste them into the prompt, and
generate. One retrieval, up front, before reasoning starts.

## First attempt, shown failing: retrieve once, reason once

The lecture's toy is a chemistry question: after a chain of
reactions, how many carbon atoms are in product 3? Watch three
approaches.

Approach 1, pure reasoning. The model hits an unfamiliar
intermediate compound, guesses its structure from the weights,
and counts 14 carbons. Wrong. The guess cascaded.

Approach 2, single-shot RAG. The model searches once, retrieves
10 documents about the compounds, pastes all of them into the
prompt, and reasons. Still wrong. The documents contain the
answer, but buried in noise: 10 long documents exceed what the
model can carefully reason over, and the relevant paragraph
drowns. Retrieval helped. Dumping hurt.

The failure is structural. A complex question needs different
facts at different reasoning steps. One retrieval at the start
cannot supply a fact the model only realizes it needs at step
7. And pasting raw documents treats the model's context as
infinite, which it is not.

## The key question

What if the model searches in the middle of thinking, whenever
it feels a knowledge gap, and reads what it finds instead of
filing it unread?

## The new idea: agentic search

The lecture builds the answer in two layers.

**Layer 1: agentic RAG.** The model emits special tokens when
its uncertainty spikes, triggering a search mid-reasoning. The
retrieved documents are inserted into the chain, and reasoning
continues with the new facts. Retrieval happens per gap, not
per question. A multi-part problem triggers several searches,
each aimed at the fact the current step needs.

**Layer 2: reason in documents (Search-o1).** Retrieved
documents are long and noisy. Instead of pasting them raw, a
dedicated step reads each document, judges relevance, and
extracts only the needed chunks. The lecture's human analogy:
you do not file every reference unread. You take notes. The
extracted notes, not the documents, join the prompt.

Now replay the chemistry toy with both layers. The model
reaches the unfamiliar compound, uncertainty spikes, and it
searches. It retrieves candidate pages, reads them, extracts
the one paragraph giving the compound's structure, and
continues. Final count: 10 carbons. Correct. The difference
from approach 2 is not the search. It is the reading.

```ascii
pure reasoning:      gap -> guess -> 14 (wrong, cascades)
single-shot RAG:     10 docs dumped -> noise -> still wrong
agentic search:      gap -> search -> read -> extract -> 10 (right)
```

## Where it breaks, part 1: knowing what to search

The hardest subproblem is the trigger. How does the model know
which terms it does not know? The lecture is honest that this is
partly heuristic: uncertainty in the trace, named entities that
look load-bearing, terms the model cannot define. Search the
wrong thing and you retrieve noise. Miss the gap and the guess
cascades. The trigger is doing real epistemic work, deciding
what the model does not know, and it is imperfect.

## Where it breaks, part 2: the context budget

Every retrieved chunk consumes context, and every search costs
latency. A deep research session that fires 20 searches and
extracts 20 chunks is 20 tool calls plus a long prompt. The
lecture frames this as context engineering: the binding
constraint is what the model can actually reason over well, not
the nominal context length. Dumping more documents past that
point degrades answers, as approach 2 showed. The agent must
budget: search where the gap matters, extract tightly, and stop.

## Mapping back

| Gap failure | Agentic search answer | How |
|---|---|---|
| Knowledge cutoff, silent guesses | Search mid-reasoning | Uncertainty triggers queries per gap, not one query per question. |
| Guesses cascade down the chain | Fill each gap when met | The fact arrives at the step that needs it. Later steps build on facts, not guesses. |
| 10 raw documents drown the reasoner | Reason in documents | Extract relevant chunks. Only the notes join the prompt. |
| One retrieval cannot serve step 7 | Iterate | Multiple search-read-reason rounds per session. |

## The honest price

Each search is latency and each chunk is context. The trigger
that decides what to look up is heuristic and can miss real
gaps or chase false ones. And the whole design assumes the
model's reasoning over long contexts is the bottleneck worth
engineering around. As long-context reasoning improves, the
optimal amount of extraction shifts. Deep research agents are
an applied form of the course's thesis: test-time compute,
spent on search and reading, buys capability the weights do
not have.

> [!QA]
> Q: How is agentic RAG different from regular RAG?
> A: Regular RAG retrieves once, up front: question in, documents out, answer generated. Agentic RAG retrieves during reasoning: the model detects a knowledge gap mid-trace, emits a trigger, searches, inserts the result, and continues. A complex question gets several targeted retrievals, one per gap, instead of one broad retrieval per question.
> Follow-up: What triggers the search?
> A: Uncertainty signals in the trace: hedging words like "perhaps" and "wait", entities the model cannot ground, terms it cannot define. The lecture is candid that the trigger is heuristic. It is the agent deciding what it does not know, which is genuinely hard and sometimes wrong in both directions.

> [!QA]
> Q: Why not just paste all retrieved documents into the prompt?
> A: Because the model cannot reason carefully over all of them. In the lecture's chemistry toy, 10 dumped documents still produced the wrong answer: the relevant paragraph drowned in noise. Search-o1's fix is a reading step that extracts only the relevant chunks. The prompt gets notes, not documents. Context length is not the same as reasoning capacity over that context.
> Follow-up: Is there a principled limit to how much to retrieve?
> A: The lecture frames it as a budget problem: retrieve where the gap is load-bearing, extract tightly, stop when marginal chunks stop changing the answer. There is no formula. It is context engineering, and the right budget moves as models' long-context reasoning improves.

> [!QA]
> Q: What does "knowledge gaps cascade" mean?
> A: One guessed fact early in a chain infects everything downstream. In the toy, guessing the intermediate compound's structure made the carbon count wrong, and no later reasoning step could recover because every step assumed the guess. Filling the gap at the moment it appears, before reasoning continues, is the entire point of searching mid-thought rather than after.
> Follow-up: Can the agent detect that its earlier step was a guess?
> A: Only imperfectly, which is why the lecture pairs search with memory of the reasoning state: a buffer tracking what is being answered and what was assumed. Detecting past guesses is an open problem. The current defense is to search at the first sign of uncertainty rather than after the damage.

## Recap: the whole lesson on one screen

1. **Yesterday is not in the weights.** Knowledge cutoffs plus
   silent guessing. Uncertainty words ("perhaps", "wait") mark
   the gaps.
2. **Single-shot RAG fails twice.** Pure reasoning guesses and
   cascades: 14, wrong. Dumping 10 documents drowns the
   reasoner: still wrong.
3. **The key question.** What if the model searches mid-thought
   and reads what it finds?
4. **Agentic RAG.** Uncertainty triggers searches per gap.
   Each reasoning step gets the fact it needs.
5. **Reason in documents.** Extract chunks, file notes, not
   documents. The chemistry toy: 10 carbons, correct.
6. **The trigger problem.** Deciding what you do not know is
   heuristic and sometimes wrong both ways.
7. **The context budget.** Searches cost latency. Chunks cost
   context. Budget both. Stop when chunks stop helping.
8. **The honest price.** Test-time compute buys what the
   weights lack, per question, forever.

## Official sources and further reading

**Official:**
- CS329A Lecture 5, second half (Autumn 2025): the lecture
  this chapter follows.
  https://www.youtube.com/watch?v=-Uni9dqyuuDM
- Search-o1 paper: agentic search with reason-in-documents.

**Further reading:**
- "Agentic Context Engineering" (2025): the context-budget
  framing the lecture cites.

**Caveats from these sources.** The chemistry toy is the
lecture's illustration with simplified numbers. GPQA
uncertainty-word observations are qualitative. The optimal
retrieval budget is presented as an open engineering question,
not a solved one.

## Connections to the other courses

- **CS329Z:** RAG pipelines in production: chunking,
  retrieval, and evaluation, the engineering under this
  chapter's agent.
- **CS329A L03:** the search call is a ReAct action. The gap
  trigger is the thought that precedes it.
- **CS329A L05:** the memory buffer of reasoning state is a
  small tree of what is known and assumed. Search fills its
  gaps.
- **CS224N:** retrieval and long-context reasoning from the
  language-model side.
