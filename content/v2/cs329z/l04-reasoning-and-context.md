---
page_id: cs329z-l04
course_slug: cs329z
course_name: "CS329Z: Engineering AI Agents"
course_order: 7
order: 4
nav: "L04 · Reasoning and Context"
title: "Lecture 2B: Inference-Time Scaling, Structured I/O, Context Engineering"
summary: "Spend compute after training: chain of thought, reasoning effort, repeated sampling. Force output shape with constrained decoding. Engineer the context: rot, KV-cache placement, compaction."
date: "[uncertain: Fall 2026]"
instructor: "Diyi Yang, Michael Ryan, John Yang"
offering: "Fall 2026"
concepts: [inference-time-scaling, chain-of-thought, reasoning-effort, repeated-sampling, structured-io, constrained-decoding, dspy, context-engineering, context-rot, compaction, kv-cache, recursive-lm]
sources:
  - tag: slides
    label: "Lecture 2 slides: LLMs for Builders (local: sources/agents/cs329z/lecture02.pdf)"
  - tag: paper
    label: "Wei et al., Chain-of-Thought Prompting Elicits Reasoning in Large Language Models (2022)"
    url: https://arxiv.org/abs/2201.11903
  - tag: paper
    label: "Brown et al., Large Language Monkeys: Scaling Inference Compute with Repeated Sampling (2024)"
    url: https://arxiv.org/abs/2407.21787
  - tag: supplement
    label: "Anthropic Engineering: Effective context engineering for AI agents"
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
---

## The job: training is frozen, queries are not

Training happens once. Queries arrive forever, and they vary in
difficulty. "What is 2+2" and "debug this race condition" should not
cost the same. **Inference-time scaling** spends compute after
training, per query: more tokens for the hard ones, fewer for the easy
ones.

The lecture's toy makes the case. A jacket costs $80. The store raises
its price by 25 percent, then offers a 25 percent discount on the new
price. What is the final price?

## First attempt: answer directly

The direct answer pattern-matches: adding 25 percent and subtracting 25
percent looks like no change. So $80.

```ascii
+25% then -25%  ->  looks like cancellation  ->  $80
```

Wrong. The two percentages use different bases. The increase applies
to $80. The discount applies to the increased price. The pattern
"cancels out" is a mirage, and the direct answer walks into it with
full confidence.

## Where direct answers break

Work the arithmetic the direct answer skipped:

```ascii
increase:  $80 x 1.25 = $100   (25% of $80 is $20)
discount:  $100 x 0.75 = $75   (25% of $100 is $25)
check:     $80 + $20 - $25 = $75
```

The true answer is $75. The direct answer is off by $5, a 6.25 percent
error from a confident pattern match. The mistake is invisible without
the intermediate numbers. Each step of the worked version is a small,
checkable claim: $80 to $100, $100 to $75. The direct answer has no
steps to check.

## The key question

What if the model writes the steps, and we spend compute on the steps
that need it?

## Chain of thought: working memory, not smarts

**Chain of thought** (Wei et al., 2022) elicits the reasoning steps
before the answer. The model writes the intermediate math, and the
intermediate math is checkable. The jacket trace above is the whole
idea: $80 x 1.25 = $100, $100 x 0.75 = $75, check the bases.

The misunderstanding: chain of thought does not make the model
smarter. It gives the model working memory. Each step is a small claim
the model commits to in text, where a verifier or a human can catch it.
And the failure mode: long traces on ambiguous questions accumulate
confident-sounding errors. The steps are in the open, but open errors
are still errors. The fix is the same as in agents: verify the steps,
do not just admire them.

## The effort dial

Reasoning models expose an **effort** setting: low, medium, high. Low
is cheap and fast for simple lookups. High spends many tokens on hard
math and deep bugs. The system prompt sets it per query.

![Reasoning effort](assets/l04-reasoning-effort.svg "Low, medium, high: cost rises with effort. Kimi K3 trains the dial with a budget-aware reward. Project: Stanford Frontier AI. Source: source.")

Kimi K3 trains the dial explicitly with a budget-aware reward:

```ascii
correct answer:               reward = +1
wrong answer:                 reward =  0
wrong AND over the budget:    reward = -1
```

Read what the -1 teaches. A wrong answer already scores 0. A wrong
answer that also burned the budget scores -1: worse than being wrong
cheaply. The model learns two lessons at once: be right, and do not
spend effort where it does not pay. That is the dial, learned.

The agent lesson: set effort per step, not per agent. A file lookup
gets low effort. A tricky bug gets high effort. The loop already knows
which steps are hard: the ones that failed before.

## Repeated sampling: the verifier is the scarce resource

Sample the same prompt N times. With a verifier, pick the best.
**Coverage**, the chance that at least one sample is right, keeps
rising with more samples. Large Language Monkeys (Brown et al., 2024)
shows inference compute keeps helping far past intuition. The math of
coverage, worked on a toy: if each sample succeeds with probability
0.3, ten samples give 1 - 0.7^10 = 0.97. Ninety-seven percent coverage
from a thirty-percent model, provided the verifier can spot the winner.

![Repeated sampling](assets/l04-repeated-sampling.svg "One sample: low coverage. Ten samples: rising. A thousand samples with a verifier: high. Project: Stanford Frontier AI. Source: paper.")

Without a verifier, vote. **Self-consistency** is the no-verifier
version: sample many reasoning paths, take the majority answer. The
cost is linear in samples either way. The agent version: sample three
candidate plans, execute the best-scoring one. Sampling is cheap.
Checking is dear. The verifier is the scarce resource, which is why
the builders lesson spent so long on verifier design.

## Mapping back I: what inference-time compute buys

| Direct-answer crack | The answer | How |
|---|---|---|
| Pattern-match says $80 | Chain of thought | The steps $80 to $100 to $75 expose the base change |
| Every query costs the same | Effort dial | Low for lookups, high for hard bugs; Kimi K3's -1 teaches the budget |
| One shot, one chance | Repeated sampling | 1 - 0.7^10 = 0.97 coverage from a 0.3 model, with a verifier |

The honest price of this half: tokens are money and latency. A small
model with a big inference budget can beat a big model with none, but
the budget is real. Spend it where the errors are.

## The second contract: structured output

Agents are programs, and programs need contracts. The model's output
goes to a parser, a tool, or another agent. Free text breaks the
contract: plausible-looking JSON with a missing field, a wrong type, a
trailing comma. The parser fails downstream and the loop burns a turn.

**Constrained decoding** enforces the contract at generation time. The
decoder may only emit tokens the grammar allows. SGLang implements this
with finite state machines built into decoding. Every token is checked
against the grammar as it is generated. The output always parses.

![Constrained decoding](assets/l04-constrained-decoding.svg "Free text breaks the schema. Grammar-constrained output always parses. Project: Stanford Frontier AI. Source: source.")

This is the validate stage of the tool call, moved into the decoder
itself. The cost: the grammar must be written, and constrained decoding
adds overhead per step. The benefit for agents is decisive: tool
arguments must parse every time. What constrained decoding cannot fix
is semantics. The output parses but can still be wrong: a valid tool
call with the wrong arguments, a well-formed plan that misunderstands
the goal. The grammar constrains shape, not meaning. Meaning needs the
check step.

**DSPy** declares the contract one level up. A **signature** names the
input and output fields of a model call, and DSPy compiles the prompt
that implements it. The lecture's example extracts contact info:

```ascii
input:  "I'm Sarah (sarah@acme.co). Meet Thursday?"
output fields:
  name:   str
  email:   Union[str, None]     <- must match the JSON schema
  intent:  Literal['meeting',
            'intro', 'follow-up']  <- exact match, no extra chars
```

The compiled prompt wraps each field in markers and states the type
constraints in prose. The signature is the contract; the compiled
prompt is the implementation. Two lighter constraining tools: a small
classifier head on embeddings for fixed label sets (cheap, fast, no
generation), and the Toolformer pattern, where the tool's argument
schema is the structured output.

## The third contract: the context

**Context engineering** is the design of what the model sees. Five
ingredients: the system prompt, the message history, memories, tool
call results, and attached files.

![What goes in the context](assets/l04-context-parts.svg "System prompt, message history, retrieved memories, tool results, attached files. Every token costs bandwidth per decode step. Project: Stanford Frontier AI. Source: source.")

Three practical rules from the lecture. **Avoid bloat:** a few tools
beat fifty. Pi ships with four: read, write, edit, bash. **Retrieve on
demand:** fetch the relevant memories and files when needed instead of
stuffing them in. **Evaluate empirically:** set up a small eval set and
test each context choice. There is no one right context. The context is
a design surface, not a dumping ground.

### Where stuffing breaks: context rot

More context is not more understanding. OOLONG (2025) measures long
context reasoning and aggregation: as the context fills with
distractors, the model's reasoning degrades. The lecture calls this
**context rot**.

![Context rot](assets/l04-context-rot.svg "Stuff everything: reasoning degrades. Curate and retrieve: the signal survives. Project: Stanford Frontier AI. Source: paper.")

The before state: fifty tool schemas when the task needs three, full
chat history gone stale, ten retrieved documents with two relevant.
The after state: three schemas, compacted history, top-k documents.
Same task, less rot, better answers. The mechanism is attention
dilution plus the decode cost from the builders lesson: every
distractor token is bandwidth spent on noise and a chance to mislead
the next step.

### The KV-cache placement rule

The KV cache is positional. Appending tokens at the end keeps every
existing position unchanged, so the cache stays valid. Inserting or
editing in the middle shifts positions: every token after the edit gets
new position embeddings, and their cached keys and values are wrong.

![Append, do not edit](assets/l04-kv-append.svg "Append at the end: cache stays valid. Insert in the middle: positions shift, cache invalidates. Project: Stanford Frontier AI. Source: source.")

The design rule: the loop appends. Tool results go at the end of the
context, never spliced into history. Rewriting history is not just
confusing for the model; it is expensive, forcing recomputation of the
whole suffix.

### Compaction: the keep-or-drop dilemma

Long trajectories fill the context. **Compaction** summarizes it: the
model compresses the trace into a summary plus key facts, and the new
context starts from there.

![Compaction](assets/l04-compaction.svg "Full context compresses to a summary. The new context keeps the summary and the open loops. Project: Stanford Frontier AI. Source: source.")

The decision is what to keep, and the lecture names the two failure
modes without resolving them. Keep too much and you compact again
soon: no savings. Drop too much and you lose critical context: the
task fails for lack of a fact you had. Resolution is empirical: test
what the summary must contain for your task class. In practice, keep
the goal, the open loops (what is still undone), the key facts
discovered, and the current plan. Drop stale tool outputs, superseded
plans, and dead-end attempts. The summary is a new perceive step for a
fresh loop.

### Recursive LMs: a different philosophy

**Recursive language models** (2025) reject the giant context. Instead
of stuffing the document into one context, the model calls itself on
chunks: summarize this part, then the top call reasons over the
summaries.

![Recursive LMs](assets/l04-rlm.svg "The top call delegates chunks to sub-calls. Each call sees a small context. Depth replaces width. Project: Stanford Frontier AI. Source: paper.")

Each call sees a small context, so there is no rot and no quadratic
blowup. The tradeoff: detail is lost in the summaries, and errors in a
sub-call propagate silently upward. Compare with RAG: RAG retrieves
chunks into one context; RLM recurses over chunks with separate calls.
Both fight the same enemy, the O(n^2) context. RAG is retrieval plus
one reader. RLM is divide and conquer with the model as the divider.

## Mapping back II: what the contracts fix

| Context crack | The answer | How |
|---|---|---|
| Parser chokes on free text | Constrained decoding | The grammar masks every forbidden token; output always parses |
| Fifty schemas, three needed | Avoid bloat | Pi's four tools; retrieve memories and files on demand |
| Distractors degrade reasoning | Curation | Three schemas, compacted history, top-k docs; OOLONG measures the rot |
| Mid-context edits kill the cache | Append-only loop | Tool results go at the end; positions never shift |
| The trace outgrows the window | Compaction or RLM | Summarize to goals plus open loops, or recurse over chunks |

## The honest price

Inference-time compute costs tokens, and tokens are latency and money.
Chain of thought gives working memory, not intelligence, and long
traces accumulate confident errors in the open. Context rot is
measured, not hypothetical. Compaction's keep-or-drop dilemma has no
principled answer: the lecture leaves it empirical. Recursive LMs dodge
the quadratic context but let sub-call errors propagate silently. Every
contract here, shape and context both, is a bet placed per task. The
lecture's final word on context stands: experiment, and measure.

## Interview Q&A

> [!QA]
> Q: Why does chain of thought help on the jacket problem, and what does that tell you about what CoT actually is?
> A: The naive answer pattern-matches: plus 25 minus 25 looks like zero change, so $80. Writing the steps forces the model to compute each stage: 80 to 100, then 100 to 75, exposing that the discount applies to a different base. The check, $80 + $20 - $25 = $75, closes it. What this tells you: CoT is working memory, not intelligence. Each step is a small, checkable claim committed to text. It does not make the model smarter; it gives errors a place to be caught.
> Follow-up: When does chain of thought hurt?
> A: When the steps are uncheckable and the model is confident anyway. Long reasoning traces on ambiguous questions accumulate confident-sounding errors, each step building on the last. The fix is the agent's fix: verify the steps against the world or a verifier. Open errors are still errors.

> [!QA]
> Q: You have a verifier and a fixed budget. One careful high-effort sample or 50 quick samples?
> A: Usually the 50 quick samples with the verifier picking. Coverage grows fast: at 0.3 success per sample, ten samples give 1 - 0.7^10 = 0.97 coverage. High effort wins when the task needs deep sequential reasoning that quick samples never stumble into: a proof with a 20-step dependency chain, a bug that needs sustained attention. Spend the budget where the errors are: breadth when solutions are scattered, depth when they are buried.
> Follow-up: What breaks repeated sampling?
> A: A bad verifier. If the check accepts wrong answers, more samples just find more ways to be wrong. This is the verifier-design warning from the builders lesson, applied at inference time. Sampling is cheap; checking is dear; a cheap check is worse than none because it certifies garbage.

> [!QA]
> Q: Why does constrained decoding matter more for agents than for chatbots?
> A: A chatbot's output goes to a human who tolerates a malformed sentence. An agent's output goes to a parser, a tool, or another agent. One bad token breaks the tool call and burns a loop turn. Constrained decoding turns "usually valid JSON" into "always valid JSON" by masking every token the grammar forbids, as it is generated. It is the validate stage of the tool call moved into the decoder itself.
> Follow-up: What can constrained decoding not fix?
> A: Semantics. The output parses but can still be wrong: a valid tool call with the wrong arguments, a well-formed plan that misunderstands the goal. The grammar constrains shape, not meaning. Meaning needs the check step of the agent loop. Shape guarantees are cheap; meaning guarantees are the whole hard problem.

> [!QA]
> Q: What is context rot, and what are the three practical defenses?
> A: Context rot is the measured degradation of reasoning as the context fills with distractors (OOLONG, 2025). More context is not more understanding: every distractor token is decode bandwidth spent on noise and a chance to mislead the next step. Three defenses from the lecture. Avoid bloat: a few tools beat fifty, as Pi's four tools show. Retrieve on demand: fetch memories and files when needed instead of stuffing them in. Compact: summarize the trace to goals, open loops, and key facts before the window fills.
> Follow-up: Why must the loop append rather than edit the context?
> A: The KV cache is positional. Appending at the end keeps every existing position unchanged, so the cache stays valid. Editing in the middle shifts positions: every token after the edit gets new position embeddings and its cached keys and values are wrong. Rewriting history forces recomputation of the whole suffix. The rule is append-only, with compaction as the one expensive rewrite.

## Recap: the whole lesson on one screen

The story in eight steps. Each step answers the one before it.

1. **Training is frozen; queries vary.** "What is 2+2" and "debug this
   race condition" should not cost the same. Spend compute per query.
2. **Direct answers pattern-match.** +25% then -25% looks like
   cancellation. $80. Wrong by $5.
3. **The steps expose the base.** $80 x 1.25 = $100, $100 x 0.75 =
   $75. Each step is a checkable claim. CoT is working memory, not
   smarts.
4. **Effort is a dial.** Low, medium, high, set per step. Kimi K3's
   reward: +1 correct, 0 wrong, -1 wrong and over budget. The -1
   teaches the budget.
5. **Sample many, verify once.** 1 - 0.7^10 = 0.97 coverage from a
   0.3 model. Without a verifier, vote (self-consistency). Checking
   is the scarce resource.
6. **Force the shape.** Constrained decoding masks forbidden tokens;
   output always parses. DSPy signatures declare the contract. Shape,
   not meaning.
7. **Engineer the context.** Five ingredients. Defenses against rot:
   few tools, retrieve on demand, compact. Append, never edit: the KV
   cache is positional.
8. **The price is tokens.** Latency and money per step. Compaction's
   keep-or-drop dilemma is empirical. RLM dodges the quadratic
   context but propagates sub-call errors silently.

## Official sources and further reading

**Official:**
- Lecture 2 slides (local: sources/agents/cs329z/lecture02.pdf).
- Course site: http://web.stanford.edu/class/cs329z.

**Further reading:**
- SGLang paper: constrained decoding with finite state machines.
- DSPy documentation: signatures and compilation.
- OOLONG paper (2025): long-context reasoning and aggregation.
- Recursive Language Models paper (2025): the recursion philosophy.
- Anthropic, "Effective context engineering for AI agents": the five
  ingredients in production form.

**Caveats from these sources.** The slides cite blog and paper figures
for several claims; the plates here are original. Effort-level
mechanics differ across providers; the Kimi K3 reward numbers are the
lecture's. The coverage arithmetic is a worked toy, not a measured
rate. No video ID is on record.

## Connections to the other courses

- **CS336 L10/L18:** the inference cost model behind every choice
  here. Decode bandwidth is the tax.
- **CS336 L15/L16:** reasoning models and RLVR: where the effort dial
  comes from.
- **CS329A:** studies inference-time scaling as a research subject
  (test-time compute, verifiers, search). This lesson is the
  engineering interface to the same ideas.
- **This course, intro lesson:** self-consistency and the agent loop.
  Inference-time methods plug into the plan and check steps.
- **This course, builders lesson:** verifier design, which repeated
  sampling depends on.
- **This course, RAG lessons:** retrieval is the main weapon against
  context rot. Compaction and RLM are the alternatives.
