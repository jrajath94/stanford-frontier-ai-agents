---
page_id: cs329z-l07
course_slug: cs329z
course_name: "CS329Z: Engineering AI Agents"
course_order: 7
order: 7
nav: "L07 · Agentic Retrieval"
title: "Lecture 3C: Retrieval Inside the Loop and Nine Failure Modes"
summary: "Multi-hop questions need retrieval inside the agent loop. The loop makes three decisions: whether, what, and when to stop. Nine failure modes, each priced with numbers."
date: "[uncertain: Fall 2026]"
instructor: "Diyi Yang"
offering: "Fall 2026"
concepts: [agentic-retrieval, multi-hop, self-rag, crag, search-r1, flare, ircot, compounding-error, no-stopping-rule, injection, recall-ceiling, stale-index, permission-leak, lost-in-middle, distraction, evidence-conflict]
sources:
  - tag: slides
    label: "Lecture 3 slides: RAG + Agents (local: sources/agents/cs329z/lecture03.pdf)"
  - tag: supplement
    label: "Barnett et al., Seven Failure Points When Engineering a Retrieval Augmented Generation Solution (2024)"
    url: https://arxiv.org/abs/2401.05856
  - tag: supplement
    label: "Jin et al., Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning (2025)"
    url: https://arxiv.org/abs/2503.09516
  - tag: supplement
    label: "Asai et al., Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection (2023)"
    url: https://arxiv.org/abs/2310.11511
---

## The job: a question no single passage answers

"Which city hosted the World Series the year the current ACME CEO took
office?" One passage holds the CEO's start year. A different passage
holds the World Series host for that year. No chunk contains both
facts. A one-shot RAG pipeline fetches passages for the full question,
finds chunks about the CEO and chunks about the World Series, and the
reader guesses across the gap.

## First attempt: retrieve once, then answer

The standard pipeline from the RAG lesson: one retrieval round for the
whole question, then the reader writes the answer from whatever came
back.

## Where one-shot retrieval breaks

The retriever scores passages against the full question. "Which city
hosted the World Series the year the current ACME CEO took office?"
has no passage-shaped answer. The top-K returns CEO biography chunks
and World Series history chunks, and neither mentions the bridge: the
year. The reader must find the year in the CEO chunks, then search
World Series hosts for that year, but the pipeline has no second
round. It answers from the gap.

## The key question

What if the agent decides, mid-loop, what to search for next?

## Three retrieval decisions move inside the loop

In **agentic retrieval** the agent plans the retrieval strategy. Three
decisions that the one-shot pipeline hard-codes become choices.

**Whether to retrieve.** Some questions need no search. The agent
decides per step: is external information required, or is this
reasoning I can do from context? Skipping retrieval saves a round
trip and the decode tokens of K passages.

**What to retrieve.** The query is rewritten for the missing piece.
Not the original question, but "ACME CEO took office year", then
"World Series host 2019" once the year is known. The loop from the
intro lesson: perceive the partial answer, decide the next search.

**When to stop.** Each round costs tokens and latency. The agent needs
a stopping rule: stop when the evidence answers the question, not
when the context is full. Without one, the loop retrieves until the
budget runs out.

```ascii
agentic trace, the 2-hop question:

Thought 1: Need the CEO's start year first.
Action 1:  search("ACME CEO took office year")
Obs 1:     "CEO since 2019."
Thought 2: Now the World Series host for 2019.
Action 2:  search("World Series host 2019")
Obs 2:     "Washington Nationals."
Thought 3: Both facts found. Answer.
Final:     "Washington, D.C."
```

The second query did not exist until the first observation arrived.
That is the whole difference: retrieval follows the reasoning instead
of preceding it.

![Agentic retrieval](assets/l07-agentic-trace.svg "Query 2 is born from observation 1. Retrieval follows the reasoning instead of preceding it. Project: Stanford Frontier AI. Source: original.")

### Self-RAG: the model decides to retrieve

**Self-RAG** (Asai et al., 2023) makes retrieval a generated decision.
As the model writes, it emits reflection tokens: `[Retrieve]` yes or
no at each segment, then `isRel` (is the passage relevant?), `isSupp`
(is the answer supported?), `isUse` (is the segment useful overall?).
A critic model trains those tokens with segment-level scores.

![Self-RAG](assets/l07-selfrag.svg "The model emits retrieve or no-retrieve as it writes. A critic trains those calls. Project: Stanford Frontier AI. Source: original.")

Read what changes. In one-shot RAG, retrieval is a pipeline stage
that runs once, always. In Self-RAG, retrieval is a choice the model
makes per segment: retrieve for the CEO's start year, skip for the
arithmetic that follows. The price is the critic's labels:
segment-level supervision (relevant? supported? useful?) is expensive
to write, and the quality of the reflection tokens is bounded by the
quality of those labels.

### CRAG: repair the retrieval

**CRAG** (corrective RAG) adds a correctness loop around retrieval. An
evaluator scores the retrieved documents: correct, incorrect, or
ambiguous. Correct documents go to the reader. Incorrect ones trigger
web search as a fallback. Ambiguous ones are decomposed and refined
into knowledge strips: short, filtered statements with the noise cut.

The idea is repair, not retry. A failed retrieval is not just tried
again. It is diagnosed (which documents failed and why), escalated
(web search when the corpus has nothing), and refined (strips instead
of raw chunks). The cost is the evaluator and the fallback: every
correction is latency and tokens. The decision rule: add the
correctness loop when retrieval misses are the dominant failure on
your eval set. If the reader is the problem, CRAG buys nothing.

### Search-R1 and FLARE: retrieve mid-reasoning

**Search-R1** (Jin et al., 2025) trains the loop with reinforcement
learning. The model generates its own search queries mid-reasoning and
learns the query policy from the outcome reward: did the final answer
come out right? No hand-written query templates, no heuristics. The
query policy is learned, not designed.

**FLARE** (forward-looking active retrieval) takes a different angle:
predict the next sentence, and retrieve when the model's confidence in
the prediction is low. **IRCoT** interleaves retrieval with
chain-of-thought: each reasoning step can trigger a retrieval for the
fact it needs. The family shares one idea: retrieval fires when the
reasoning needs it, not on a schedule. The price is control: the
retrieval pattern is learned or confidence-gated, which makes it
harder to bound the token budget than a fixed pipeline.

## Mapping back: what the loop buys

| One-shot crack | The answer | How |
|---|---|---|
| No passage answers the full question | Multi-hop trace | Query 2 is written from observation 1 |
| Retrieval for its own sake | Whether to retrieve | Self-RAG's retrieve/no-retrieve decision |
| The question is not the query | Query rewriting | Each round targets the missing piece |
| Retrieval never stops | Stopping rule | Stop on answered, not on full |
| Bad retrieval is final | Correction | CRAG re-scores, re-searches, refines |
| The query policy is hand-written | Search-R1 | Learn it from the outcome reward |

## What is used where: agentic retrieval in production

| System | The loop it runs | The check |
|---|---|---|
| Perplexity | retrieve, read, cite, repeat; answers carry sources | citations: every claim points at a page |
| ChatGPT Deep Research | plans a research outline, browses dozens of pages, synthesizes | the report: sections map to the plan |
| Devin-style code search | search the repo, read, test, repeat | the tests: green means done |
| Claude Agent SDK | subagents retrieve with isolated context | the parent's synthesis over subagent outputs |

The pattern: every production system pairs the retrieval loop with an
artifact the user can check. Citations, reports, green tests. The loop
is trusted exactly as far as its artifact is checkable.

## The honest price: nine failure modes, priced

Agentic retrieval multiplies the moving parts, and each part fails
with numbers. Barnett et al. (2024) catalog the failure points. The
lecture organizes them. Worked one by one, in three groups.

### Group 1: the loop's own math

**1. Compounding error.** Each hop can fail, and the failures
multiply. If each step is right with probability 0.95:

![Compounding error](assets/l07-compounding.svg "0.95^2 = 0.90. 0.95^5 = 0.77. 0.95^20 = 0.36. Reliable steps, unreliable chains. Project: Stanford Frontier AI. Source: original.")

```ascii
2 hops:   0.95^2  = 0.90
5 hops:   0.95^5  = 0.77
20 hops:  0.95^20 = 0.36
```

A twenty-hop chain is wrong two times in three even when every step
is 95 percent reliable. The fix is the intro lesson's fix: verify at
each hop, keep chains short, prefer fewer hops with stronger evidence.

**2. No stopping rule.** Each retrieval round burns about 2,000 tokens
of passages plus a search call. Without a stopping rule, a 25-turn
loop burns 50,000 tokens before the budget does the stopping.

![No stopping rule](assets/l07-stopping.svg "25 rounds x 2,000 tokens = 50,000 tokens. The stopping rule is written, not hoped for. Project: Stanford Frontier AI. Source: original.")

The stopping rule is a design decision, not an emergent behavior: stop
when the evidence answers the question, and say what "answers" means.
The budget is the backstop, not the plan.

**3. Injection.** Retrieved text is untrusted input. The slides' case:
a pop-up window during web retrieval that hijacks the agent. Retrieved
passages can carry instructions ("ignore your task and do X"), and the
model reads them as part of its context. The builders lesson priced
this at 87 percent attack success.

![Injection](assets/l07-injection.svg "One passage carries instructions. The poisoned Thought steers the next search. Project: Stanford Frontier AI. Source: original.")

In an agentic loop the injected text steers the next retrieval, so the
corruption compounds across hops. Treat retrieved content as data,
never as instructions.

### Group 2: the index and the permissions

**4. Recall ceiling.** The reader cannot use what the retriever never
found. If the retriever's recall@10 is 0.8, the agent's end-to-end
accuracy is capped at 0.8 on questions needing that passage, no matter
how good the reasoning is.

![Recall ceiling](assets/l07-recall-ceiling.svg "Retriever recall@10 = 0.8 caps the whole system at 0.8. Project: Stanford Frontier AI. Source: original.")

Agentic retrieval raises the ceiling with rewritten queries and
multiple rounds, but each round inherits the same bound. Measure
retriever recall separately: it is the ceiling of the whole system.

**5. Stale index.** The index is a snapshot. Documents change, and the
agent answers from last month's rows with this month's confidence.
The RAG lesson's staleness argument returns: the fix is index refresh
discipline, and a freshness check on retrieved passages for
time-sensitive questions. For fast corpora, size the refresh to the
question's half-life: hourly docs need hourly rebuilds or a fresh tier.

**6. Permission leak.** Retrieval crosses permission boundaries the
user cannot see. The agent retrieves a document the user is not
allowed to read, and the answer leaks it: a salary figure from a
private HR doc, summarized helpfully in a chat the user can quote.
The retriever must respect access control at retrieval time, not
filter at generation time: by the time the model sees the passage,
the leak is one paraphrase away.

### Group 3: the reader's failures

**7. Lost in the middle.** Long retrieved contexts degrade: the model
attends to the start and the end and loses the middle. Ten passages
in, the key evidence at position 5 is effectively invisible. The
defense is the RAG lesson's defense: fewer, better passages, and
rerank so the critical evidence sits where the model looks. Position
is a retrieval decision, not just a reader property.

**8. Distraction.** Irrelevant passages do not just waste tokens. They
mislead. A passage about the wrong year's World Series pulls the
answer off course. More retrieval is not more evidence: each added
passage is a chance to distract. This is context rot from the
reasoning lesson, wearing a retrieval costume. The fix is the same:
retrieve less, but better.

**9. Evidence conflict.** Two retrieved passages disagree: one says
the CEO took office in 2019, another says 2018. The one-shot pipeline
picks by position. The agent must resolve the conflict: prefer the
newer source, prefer the primary source, or retrieve a tiebreaker.

![Evidence conflict](assets/l07-conflict.svg "Same fact, two values. Resolve: prefer newer, prefer primary, or retrieve a tiebreaker. Project: Stanford Frontier AI. Source: original.")

Conflict resolution is a decision the pipeline never makes and the
loop must. Log which source won and why: the trace is the audit trail.

The pattern across all nine: retrieval failures are agent failures
now. In one-shot RAG the pipeline fails once, visibly. In agentic
retrieval the loop fails across hops, quietly, and each hop's error
feeds the next hop's query.

## Interview Q&A

> [!QA]
> Q: When does one-shot RAG fail but agentic retrieval succeed? Work an example.
> A: On multi-hop questions where no single passage contains the answer. "Which city hosted the World Series the year the current ACME CEO took office?" One-shot RAG retrieves for the full question and gets CEO biography chunks plus World Series history chunks, with no bridge between them. The agentic trace: search "ACME CEO took office year", observe "CEO since 2019", then search "World Series host 2019", observe "Washington Nationals", answer "Washington, D.C." The second query did not exist until the first observation arrived. Retrieval follows the reasoning instead of preceding it.
> Follow-up: What are the three retrieval decisions the loop owns?
> A: Whether to retrieve (some steps need no search. Skipping saves a round trip), what to retrieve (rewrite the query for the missing piece, not the original question), and when to stop (stop when the evidence answers the question, not when the context fills). The stopping rule is the one teams forget: without it, the loop retrieves until the budget runs out.

> [!QA]
> Q: Self-RAG versus CRAG: what does each add, and what does each cost?
> A: Self-RAG makes retrieval a generated decision: the model emits retrieve/no-retrieve reflection tokens per segment (isRel, isSupp, isUse), trained by a critic with segment-level scores. It buys selective retrieval: no search where none is needed. CRAG adds a correctness loop: an evaluator scores retrieved documents, triggers web search when they fail, and refines them into knowledge strips. It buys repair: bad retrieval is diagnosed and fixed, not just retried. Self-RAG costs segment-level labels for the critic. CRAG costs the evaluator plus the fallback on every correction.
> Follow-up: When would you pick Search-R1 over hand-written query templates?
> A: When the query policy is the bottleneck and you have outcome rewards to learn from. Search-R1 learns the query policy with RL from final-answer success: no templates, no heuristics. It wins where human query intuition is weak: novel domains, adversarial corpora. It loses where the budget must be bounded tightly, because a learned policy's retrieval count is harder to cap than a fixed pipeline's.

> [!QA]
> Q: Work the compounding-error arithmetic for a retrieval chain.
> A: If each hop is right with probability 0.95, two hops give 0.90, five give 0.77, and twenty give 0.36. A twenty-hop chain is wrong two times in three even though every step looks reliable. The fixes: keep chains short, verify at each hop against evidence, and prefer fewer hops with stronger evidence. This is the same 0.9^4 = 0.66 survival math from the intro lesson, now applied to retrieval rounds instead of tool calls.
> Follow-up: Why is recall ceiling the most depressing of the nine?
> A: Because it caps the whole system below the retriever. If retriever recall@10 is 0.8, end-to-end accuracy on evidence-needing questions cannot exceed 0.8 no matter how good the reasoning is. Agentic retrieval raises the ceiling with rewritten queries and more rounds, but each round inherits the same bound. Teams that only benchmark the final answer never see the ceiling. Measure retriever recall separately.

> [!QA]
> Q: A retrieved document contains instructions to ignore the user's task. Why is this worse in an agentic loop than in one-shot RAG?
> A: In one-shot RAG, the injected text influences one answer. In an agentic loop, it steers the next retrieval: the corrupted step writes the next query, fetches more corrupted content, and the corruption compounds across hops. The builders lesson priced prompt injection at 87 percent attack success for the pop-up case. The defense is architectural: treat retrieved content as data, never as instructions, and the permission check at retrieval time matters too, since a leaked private document is one paraphrase away from disclosure once the model has seen it.
> Follow-up: How do you handle two retrieved passages that disagree?
> A: Resolve, do not average. Prefer the newer source for time-sensitive facts, prefer the primary source over the secondary one, or retrieve a tiebreaker passage. The one-shot pipeline picks by position. The loop must make the conflict an explicit decision. Log which source won and why: the trace is the audit trail.

> [!QA]
> Q: Your agentic RAG agent retrieves 10 passages per round for 5 rounds. The answers are getting worse as you add rounds. Diagnose.
> A: Two suspects from the nine. Distraction: each added passage is a chance to mislead, and a passage about the wrong year's World Series pulls the answer off course. More retrieval is not more evidence. Lost in the middle: with 50 passages across rounds, the key evidence sits where the model does not look. The fix is fewer, better passages per round, a rerank so critical evidence sits at the edges, and a stopping rule so the loop stops when the evidence answers instead of when the budget dies.
> Follow-up: How do you tell distraction from a recall problem?
> A: Check whether the right passages were retrieved at all. If the evidence is in the retrieved set and the answer is still wrong, it is distraction or lost-in-the-middle: a reader-side failure. If the evidence never arrived, it is recall ceiling: a retriever-side failure. The fix lives on opposite sides of the handoff, so measure each side separately.

> [!QA]
> Q: The agent has a private HR document in its corpus. A user asks about salaries. What is the failure, and where is the fix?
> A: Permission leak: retrieval crosses a permission boundary the user cannot see, and the answer leaks a salary figure the user is not allowed to read. The fix is at retrieval time, not generation time: the retriever must respect access control when it searches, so the private document never enters the candidate set. Filtering at generation time is too late: by the time the model sees the passage, the leak is one paraphrase away. This is failure mode 6, and it is an architecture decision, not a prompt.
> Follow-up: The permission system is per-document but the chunks are shared. What now?
> A: Then the chunking broke the permission boundary. Re-chunk along permission lines, or tag each chunk with its document's ACL and filter at retrieval. A chunk that mixes public and private text is unretrievable safely: split it. Permissions are a property of the index, not just the documents.

> [!QA]
> Q: Design the stopping rule for a research agent. What does "answers the question" mean, concretely?
> A: Three parts. First, the evidence test: every claim the answer will make has a retrieved passage supporting it, checked by an entailment pass or a critic. Second, the coverage test: the question's sub-questions (from the plan) each have at least one supporting passage. Third, the budget backstop: max 10 rounds, max 20,000 tokens of passages, whichever comes first. The rule is written before the loop runs: stop when the evidence answers, not when the context is full. Log the stop reason per run: answered, budget, or model-declared-done.
> Follow-up: The agent stops early with a confident wrong answer. What failed?
> A: The evidence test. The agent declared "answered" without supporting passages for each claim: the stopping rule checked the model's confidence instead of the evidence. The fix: the stop decision reads the retrieved set, not the model's tone. Confidence is not evidence, and a stopping rule that trusts confidence is a loop that stops at the first plausible answer.

## Recap: the whole lesson on one screen

The story in nine steps. Each step answers the one before it.

1. **The job: no single passage answers.** The CEO's year lives in
   one chunk. The World Series host in another. One-shot retrieval
   finds both piles and guesses across the gap.
2. **The loop owns three decisions.** Whether to retrieve, what
   query to write, when to stop. Each was hard-coded before.
3. **The trace shows it.** "CEO since 2019" arrives. Then "World
   Series host 2019" is written. Query 2 is born from observation 1.
4. **Frameworks name the machinery.** Self-RAG decides
   retrieve/no-retrieve with reflection tokens. CRAG repairs bad
   retrieval. Search-R1 learns the query policy by reward. FLARE
   retrieves when confidence drops.
5. **Errors compound.** 0.95^20 = 0.36. Twenty reliable hops are
   wrong twice in three. Verify per hop, keep chains short.
6. **The loop has no brakes by default.** 2,000 tokens a round x
   25 rounds = 50,000 tokens. The stopping rule is a design
   decision: evidence test, coverage test, budget backstop.
7. **Retrieval is untrusted input.** Injection steers the next hop.
   Permission leaks happen at retrieval time. Stale indexes answer
   with last month's confidence.
8. **The reader is bounded by the retriever.** Recall ceiling caps
   the system. Lost-in-the-middle and distraction waste the good
   passages. Conflicts must be resolved, not averaged.
9. **Every production loop pairs with an artifact.** Perplexity's
   citations, Deep Research's report, Devin's green tests. The loop
   is trusted as far as its artifact is checkable.

## Go deeper

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:16px 0;">
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%;" src="https://www.youtube-nocookie.com/embed/hwxmYqh_ykY" title="Agentic RAG: Query Planning, Iterative Retrieval, and Knowledge Graphs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
- Agentic RAG: Query Planning, Iterative Retrieval, and Knowledge Graphs (the embed above): https://www.youtube.com/watch?v=hwxmYqh_ykY, the one-shot limit, retrieval as a tool, the agentic loop, query decomposition, and knowledge-graph RAG.

Further:
- Asai et al., Self-RAG (2023): https://arxiv.org/abs/2310.11511, retrieve, generate, and critique through self-reflection.
- Jin et al., Search-R1 (2025): https://arxiv.org/abs/2503.09516, learning to search with RL.
- Barnett et al. (2024): https://arxiv.org/abs/2401.05856, seven failure points of RAG engineering.

## Official sources and further reading

**Official:**
- Lecture 3 slides (local: sources/agents/cs329z/lecture03.pdf).
- Course site: http://web.stanford.edu/class/cs329z.

**Further reading:**
- Self-RAG and CRAG papers: reflection tokens and corrective
  retrieval.
- FLARE and IRCoT: confidence-gated and interleaved retrieval.

**Caveats from these sources.** The nine failure modes synthesize the
slides with Barnett et al.. The worked numbers (0.95^20, 2,000 tokens
x 25 rounds, 87 percent injection) are toy or cited-from-earlier
arithmetic, not new measurements. Framework details (Self-RAG tokens,
CRAG strips) are summarized from the slides' treatment. No lecture
video is on record. The embed above is a third-party explainer,
verified live.

## Connections to the other courses

- **CS329A:** studies agentic retrieval as a research subject
  (learned search policies, retrieval for self-improvement). This
  course engineers the loop and prices its failures.
- **This course, intro lesson:** the agent loop that retrieval now
  lives inside. Compounding error derived there, applied here.
- **This course, RAG pipeline:** the one-shot system this lesson
  upgrades. The retriever-reader handoff becomes a loop joint.
- **This course, retrieval methods:** the retriever zoo that the
  loop calls. Recall ceiling is that lesson's metrics, weaponized.
- **This course, evaluation:** the next lesson scores these agents,
  including the failure modes priced here.
