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
concepts: [agentic-retrieval, multi-hop, self-rag, crag, search-r1, compounding-error, no-stopping-rule, injection, recall-ceiling, stale-index, permission-leak, lost-in-middle, distraction, evidence-conflict]
sources:
  - tag: slides
    label: "Lecture 3 slides: RAG + Agents (local: sources/agents/cs329z/lecture03.pdf)"
  - tag: supplement
    label: "Barnett et al., Seven Failure Points When Engineering a Retrieval Augmented Generation Solution (2024)"
    url: https://arxiv.org/abs/2401.05856
  - tag: supplement
    label: "Jin et al., Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning (2025)"
    url: https://arxiv.org/abs/2503.09516
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

Three frameworks from the slides. **Self-RAG** adds reflection tokens:
the model emits retrieve/no-retrieve, isRel/isSupp/isUse markers as it
goes, and a critic model trains those decisions with segment-level
scores. Retrieval is a generated decision, not a pipeline stage.
**CRAG** (corrective RAG) adds a correctness loop: an evaluator scores
the retrieved documents, triggers web search when they fail, and
refines them into knowledge strips. Retrieval can repair itself.
**Search-R1** trains the loop with reinforcement learning: the model
generates its own search queries mid-reasoning and learns from the
outcome reward. The query policy is learned, not hand-written.

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

## Mapping back: what the loop buys

| One-shot crack | The answer | How |
|---|---|---|
| No passage answers the full question | Multi-hop trace | Query 2 is written from observation 1 |
| Retrieval for its own sake | Whether to retrieve | Self-RAG's retrieve/no-retrieve decision |
| The question is not the query | Query rewriting | Each round targets the missing piece |
| Retrieval never stops | Stopping rule | Stop on answered, not on full |
| Bad retrieval is final | Correction | CRAG re-scores, re-searches, refines |

## The honest price: nine failure modes, priced

Agentic retrieval multiplies the moving parts, and each part fails
with numbers. Barnett et al. (2024) catalog the failure points; the
lecture organizes them. Worked one by one.

**1. Compounding error.** Each hop can fail, and the failures
multiply. If each step is right with probability 0.95:

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
loop burns 50,000 tokens before the budget does the stopping. The
stopping rule is a design decision, not an emergent behavior: stop
when the evidence answers the question, and say what "answers" means.

**3. Injection.** Retrieved text is untrusted input. The slides' case:
a pop-up window during web retrieval that hijacks the agent. Retrieved
passages can carry instructions ("ignore your task and do X"), and the
model reads them as part of its context. The builders lesson priced
this at 87 percent attack success. In an agentic loop the injected
text steers the next retrieval, so the corruption compounds across
hops. Treat retrieved content as data, never as instructions.

**4. Recall ceiling.** The reader cannot use what the retriever never
found. If the retriever's recall@10 is 0.8, the agent's end-to-end
accuracy is capped at 0.8 on questions needing that passage, no matter
how good the reasoning is. Agentic retrieval raises the ceiling with
rewritten queries and multiple rounds, but each round inherits the
same bound. Measure retriever recall separately: it is the ceiling of
the whole system.

**5. Stale index.** The index is a snapshot. Documents change, and the
agent answers from last month's rows with this month's confidence.
The RAG lesson's staleness argument returns: the fix is index refresh
discipline, and a freshness check on retrieved passages for
time-sensitive questions.

**6. Permission leak.** Retrieval crosses permission boundaries the
user cannot see. The agent retrieves a document the user is not
allowed to read, and the answer leaks it: a salary figure from a
private HR doc, summarized helpfully in a chat the user can quote.
The retriever must respect access control at retrieval time, not
filter at generation time: by the time the model sees the passage,
the leak is one paraphrase away.

**7. Lost in the middle.** Long retrieved contexts degrade: the model
attends to the start and the end and loses the middle. Ten passages
in, the key evidence at position 5 is effectively invisible. The
defense is the RAG lesson's defense: fewer, better passages, and
rerank so the critical evidence sits where the model looks.

**8. Distraction.** Irrelevant passages do not just waste tokens; they
mislead. A passage about the wrong year's World Series pulls the
answer off course. More retrieval is not more evidence: each added
passage is a chance to distract. This is context rot from the
reasoning lesson, wearing a retrieval costume.

**9. Evidence conflict.** Two retrieved passages disagree: one says
the CEO took office in 2019, another says 2018. The one-shot pipeline
picks by position. The agent must resolve the conflict: prefer the
newer source, prefer the primary source, or retrieve a tiebreaker.
Conflict resolution is a decision the pipeline never makes and the
loop must.

The pattern across all nine: retrieval failures are agent failures
now. In one-shot RAG the pipeline fails once, visibly. In agentic
retrieval the loop fails across hops, quietly, and each hop's error
feeds the next hop's query.

## Interview Q&A

> [!QA]
> Q: When does one-shot RAG fail but agentic retrieval succeed? Work an example.
> A: On multi-hop questions where no single passage contains the answer. "Which city hosted the World Series the year the current ACME CEO took office?" One-shot RAG retrieves for the full question and gets CEO biography chunks plus World Series history chunks, with no bridge between them. The agentic trace: search "ACME CEO took office year", observe "CEO since 2019", then search "World Series host 2019", observe "Washington Nationals", answer "Washington, D.C." The second query did not exist until the first observation arrived. Retrieval follows the reasoning instead of preceding it.
> Follow-up: What are the three retrieval decisions the loop owns?
> A: Whether to retrieve (some steps need no search; skipping saves a round trip), what to retrieve (rewrite the query for the missing piece, not the original question), and when to stop (stop when the evidence answers the question, not when the context fills). The stopping rule is the one teams forget: without it, the loop retrieves until the budget runs out.

> [!QA]
> Q: Work the compounding-error arithmetic for a retrieval chain.
> A: If each hop is right with probability 0.95, two hops give 0.90, five give 0.77, and twenty give 0.36. A twenty-hop chain is wrong two times in three even though every step looks reliable. The fixes: keep chains short, verify at each hop against evidence, and prefer fewer hops with stronger evidence. This is the same 0.9^4 = 0.66 survival math from the intro lesson, now applied to retrieval rounds instead of tool calls.
> Follow-up: Why is recall ceiling the most depressing of the nine?
> A: Because it caps the whole system below the retriever. If retriever recall@10 is 0.8, end-to-end accuracy on evidence-needing questions cannot exceed 0.8 no matter how good the reasoning is. Agentic retrieval raises the ceiling with rewritten queries and more rounds, but each round inherits the same bound. Teams that only benchmark the final answer never see the ceiling; measure retriever recall separately.

> [!QA]
> Q: A retrieved document contains instructions to ignore the user's task. Why is this worse in an agentic loop than in one-shot RAG?
> A: In one-shot RAG, the injected text influences one answer. In an agentic loop, it steers the next retrieval: the corrupted step writes the next query, fetches more corrupted content, and the corruption compounds across hops. The builders lesson priced prompt injection at 87 percent attack success for the pop-up case. The defense is architectural: treat retrieved content as data, never as instructions, and the permission check at retrieval time matters too, since a leaked private document is one paraphrase away from disclosure once the model has seen it.
> Follow-up: How do you handle two retrieved passages that disagree?
> A: Resolve, do not average. Prefer the newer source for time-sensitive facts, prefer the primary source over the secondary one, or retrieve a tiebreaker passage. The one-shot pipeline picks by position; the loop must make the conflict an explicit decision. Log which source won and why: the trace is the audit trail.

## Recap: the whole lesson on one screen

The story in eight steps. Each step answers the one before it.

1. **The job: no single passage answers.** The CEO's year lives in
   one chunk; the World Series host in another. One-shot retrieval
   finds both piles and guesses across the gap.
2. **The loop owns three decisions.** Whether to retrieve, what
   query to write, when to stop. Each was hard-coded before.
3. **The trace shows it.** "CEO since 2019" arrives; then "World
   Series host 2019" is written. Query 2 is born from observation 1.
4. **Frameworks name the machinery.** Self-RAG decides
   retrieve/no-retrieve with reflection tokens. CRAG repairs bad
   retrieval. Search-R1 learns the query policy by reward.
5. **Errors compound.** 0.95^20 = 0.36. Twenty reliable hops are
   wrong twice in three. Verify per hop, keep chains short.
6. **The loop has no brakes by default.** 2,000 tokens a round x
   25 rounds = 50,000 tokens. The stopping rule is a design
   decision.
7. **Retrieval is untrusted input.** Injection steers the next hop.
   Permission leaks happen at retrieval time. Stale indexes answer
   with last month's confidence.
8. **The reader is bounded by the retriever.** Recall ceiling caps
   the system. Lost-in-the-middle and distraction waste the good
   passages. Conflicts must be resolved, not averaged.

## Official sources and further reading

**Official:**
- Lecture 3 slides (local: sources/agents/cs329z/lecture03.pdf).
- Course site: http://web.stanford.edu/class/cs329z.

**Further reading:**
- Barnett et al. (2024), seven failure points of RAG.
- Jin et al. (2025), Search-R1: learning to search with RL.
- Self-RAG and CRAG papers: reflection tokens and corrective
  retrieval.

**Caveats from these sources.** The nine failure modes synthesize the
slides with Barnett et al.; the worked numbers (0.95^20, 2,000 tokens
x 25 rounds, 87 percent injection) are toy or cited-from-earlier
arithmetic, not new measurements. Framework details (Self-RAG tokens,
CRAG strips) are summarized from the slides' treatment. No video ID
is on record.

## Connections to the other courses

- **CS329A:** studies agentic retrieval as a research subject
  (learned search policies, retrieval for self-improvement). This
  course engineers the loop and prices its failures.
- **This course, intro lesson:** the agent loop that retrieval now
  lives inside; compounding error derived there, applied here.
- **This course, RAG pipeline:** the one-shot system this lesson
  upgrades; the retriever-reader handoff becomes a loop joint.
- **This course, retrieval methods:** the retriever zoo that the
  loop calls; recall ceiling is that lesson's metrics, weaponized.
- **This course, evaluation:** the next lesson scores these agents,
  including the failure modes priced here.
