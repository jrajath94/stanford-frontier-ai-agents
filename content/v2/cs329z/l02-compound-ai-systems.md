---
page_id: cs329z-l02
course_slug: cs329z
course_name: "CS329Z: Engineering AI Agents"
course_order: 7
order: 2
nav: "L02 · Compound AI Systems"
title: "Lecture 1B: Compound AI Systems, Memory, and What Breaks"
summary: "Workflows versus agents, RAG and tool use and MCP, three kinds of memory, and the reliability, training, and safety challenges."
date: "[uncertain: Fall 2026]"
instructor: "Diyi Yang, Michael Ryan, John Yang"
offering: "Fall 2026"
concepts: [workflow, compound-ai, rag, tool-use, mcp, memory, episodic-memory, semantic-memory, procedural-memory, reliability, safety, evaluation]
sources:
  - tag: slides
    label: "Lecture 1 slides: Intro to Agentic Systems (local: sources/agents/cs329z/lecture01.pdf)"
  - tag: paper
    label: "Zaharia et al., The Shift from Models to Compound AI Systems (BAIR, 2024)"
    url: https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/
  - tag: paper
    label: "Zhang, Yu, and Yang, Attacking Vision-Language Computer Agents via Pop-ups (2024)"
    url: https://arxiv.org/abs/2411.02391
  - tag: supplement
    label: "Anthropic, On the Biology of a Large Language Model: reward tampering"
    url: https://www.anthropic.com/research/reward-tampering
---

## The job: the model cannot touch the world

"What does test.py contain?" Ask a bare language model and it must
guess. It will produce something plausible:

```ascii
def add(a, b):
    return a + b
```

Confident. Formatted. Possibly nothing like the real file. The model
has no eyes on the filesystem. Every fact about the world outside its
training data is a guess dressed as an answer.

This is the problem tools solve. The agent loop from the last lesson
has an Act step, but the lecture never said what an act is made of.
This chapter builds it: the tool call, the contract that lets words
move files, run code, and query databases. Zaharia et al. (2024) call
the result a **compound AI system**: an LLM plus the components around
it. The field, they argue, has shifted from models to these systems.

## First attempt: describe the tool in words

The naive approach is to tell the model about the tool in prose:
"You have a read_file tool. To read a file, say read_file and the
path." The model then narrates its actions in free text:

```ascii
I will now read the file. read_file(test.py)
```

Two things are wrong. First, the call has no shape. Is `test.py` an
argument or a comment? Where does the path end? A parser must guess,
and parsers guess wrong. Second, nothing is checked. If the model
emits `read_file()` with no path, or `read_file(42)`, the error
surfaces deep inside the filesystem code, far from where the mistake
was made.

## Where word-tools break

Three cracks, each with a number or a worked case.

**Crack 1: malformed arguments.** The tool expects a path, a string.
The model emits a list:

```ascii
call:      read_file
arguments: {"path": ["test.py"]}     <- a list, not a string
schema:    path: string
verdict:   REJECTED before anything runs
```

Without a validation stage, this malformed call reaches the executor,
which throws, which the agent reads as a confusing tool error, which
poisons the next Thought. The failure-modes lesson traces this exact
cascade. The fix belongs before execution, not after.

**Crack 2: untrusted observations.** The tool result comes back into
the context, and the model reads it as instructions. Zhang, Yu, and
Yang (2024) show what happens with vision-language computer agents and
pop-ups: the agent abandons its task for the pop-up. Attack success
rate: 87 percent. Nearly nine runs in ten, the observation steers the
agent. Tool outputs are data, but the model treats them as commands.

**Crack 3: integration sprawl.** Every agent hand-writes glue for every
tool. Five agents and eight tools means 5 x 8 = 40 custom integrations.
Add one tool and you write five more. The plumbing grows as N times M,
and every integration is a place for crack 1 to hide.

## The key question

What if a tool call were a typed function call with a contract, checked
before anything touches the world?

## The tool call, built from zero

A tool starts as a **schema**: a name, a description, and typed
arguments. This is the contract. Here is the lecture's example,
concrete:

```ascii
tool: read_file
description: "Return the contents of a file."
arguments:
  path: string      <- the file to read, required
```

Now the four stages, hand-worked on "What does test.py contain?"
with three tools in context (read_file, search, calculator). This
four-stage trace is the course's owned symbol: the hand-traced
tool loop, given the same care as the gold standard's attention toy.

```ascii
STAGE 1 - SELECT: which tool, from the schemas in context
  candidates: read_file(path: string), search(query: string),
              calculator(expr: string)
  task needs: the contents of a file
  chosen:     read_file

STAGE 2 - ARGUMENTS: typed fields, filled from the task
  task says:  "test.py"
  filled:     {"path": "test.py"}

STAGE 3 - VALIDATE: schema check, before anything runs
  check:      "test.py" is a string -> PASS
  (if the model had emitted {"path": ["test.py"]}, this is
   where it dies, with a clear error, before the sandbox)

STAGE 4 - EXECUTE: sandboxed; the result returns to context
  run:        read /sandbox/test.py
  returns:    "def add(a, b):\n    return a + b\n"
  -> appended to the context as an observation
```

Read the trace back. Select turns "which tool" into a choice among
named schemas. Arguments turns the task's words into typed values.
Validate is the load-bearing stage: the malformed list from crack 1
dies here, cheaply, with a legible error. Execute runs sandboxed, and
the bytes that come back are real: the guessed file contents from the
opening are replaced by the actual file.

![Anatomy of a tool call](assets/l02-tool-call.svg "Select read_file, fill path with test.py, validate the schema, execute, and read the result back. Project: Stanford Frontier AI. Source: source.")

Two systems train this behavior instead of prompting it. **Toolformer**
(2023) trains the model to decide which API to call, when to call it,
what arguments to pass, and how to use the result. Its tools: a
calculator, a Q&A system, a search engine, a translation system, a
calendar. **Gorilla** (Patil et al., 2023) connects LLMs to massive API
collections. Same four stages; the selection is learned, not prompted.

## MCP: one plug for every tool

The Model Context Protocol standardizes the plumbing. Three roles. The
**host** is the agent app, your program. The **client** lives inside
the host, one per server. The **server** exposes tools, data sources,
and prompts.

![MCP](assets/l02-mcp.svg "Host spawns clients. Clients call servers. Servers expose tools, data, and prompts. Project: Stanford Frontier AI. Source: source.")

The arithmetic is the point. Before MCP: N agents times M tools. Five
agents and eight tools: 5 x 8 = 40 integrations. After MCP: each side
speaks one protocol, so 5 + 8 = 13. The agent discovers a server's
tools through the protocol instead of through hand-written glue.

MCP changes the plumbing, not the anatomy. The four stages, select,
arguments, validate, execute, stay exactly the same. What changes is
how the schemas arrive in context and how the call is transported. And
a warning from the safety section: MCP standardizes transport, not
trust. A malicious server can serve a poisoned tool description. The
87 percent pop-up figure applies here too.

## Workflows vs agents: who decides the steps?

Both are compound AI systems. The engineering question is who decides
the steps. A **workflow** fixes the steps in code. An **agent** lets
the LLM decide each step.

![Workflows vs agents](assets/l02-workflow-vs-agent.svg "Workflow: code fixes the steps, like AlphaCode 2 sampling up to one million solutions. Agent: the LLM decides each step, like SWE-agent. Project: Stanford Frontier AI. Source: paper.")

The lecture's pair: AlphaCode 2 is a workflow. It samples up to one
million solutions for a coding problem, then filters and scores them.
The code decides the order: sample, execute, score, pick. One million
is the number to remember: the workflow buys quality with sheer
sampling volume. SWE-agent is an agent. The model reads each
observation and chooses the next action. The plan emerges from the
loop.

The decision rule: use a workflow when you know the steps and the
variation is in the data. Use an agent when the next step depends on
what the last step found. Good systems mix them: a workflow of agents
(fixed outer steps, agentic inner steps), or an agent that calls
workflows as tools.

A note on RAG, the third compound system in this lecture. Retrieval
connects the LLM to external knowledge in real time: retrieve, augment,
generate. It gets its own full treatment in the three RAG lessons.
Here it is one instance of the pattern: the model plus a component, the
component doing what the model cannot.

![RAG in three steps](assets/l02-rag-steps.svg "Retrieve: search documents. Augment: add context to the question. Generate: answer from the retrieved facts. Project: Stanford Frontier AI. Source: source.")

## Memory: the loop needs a past

The context window cannot hold every event stream. Even if it could,
attending over everything is weak. So the agent keeps memory outside
the context and retrieves from it. The lecture categorizes memory by
content, inspired by human long-term memory.

![Three kinds of memory](assets/l02-memory-types.svg "Episodic stores experience. Semantic stores knowledge. Procedural stores skills. Each has its own write and read. Project: Stanford Frontier AI. Source: source.")

| Kind | Stores | Write | Read | Example |
|---|---|---|---|---|
| Episodic | experience | append-only event streams | retrieval by heuristic scores | generative agents (Park et al., 2023) |
| Semantic | knowledge | LLM reasoning over events | retrieval | distilled facts |
| Procedural | skills | code: reusable procedures | embedding retrieval | Voyager (Wang et al., 2023) |

The read-write asymmetry decides the design. Episodic write is cheap
and dumb: append everything. Semantic write is expensive and smart: an
LLM must reason over the events to distill facts. Procedural write is
code: a discovered procedure compiled into a reusable skill. The rule
of thumb: append raw traces for recent work, distill to semantic facts
for the long term, compile repeated wins into procedural skills. Pure
append-everything fails because retrieval over a giant event stream
returns stale episodes and the context fills with noise.

## Mapping back: what each piece fixes

| Crack in the first attempt | The answer | How |
|---|---|---|
| The model guesses file contents | Execute | The sandbox returns real bytes; the guess is replaced by the file |
| Malformed arguments crash deep | Validate | The schema check rejects {"path": ["test.py"]} before anything runs |
| Every tool needs custom glue | MCP | 5 x 8 = 40 integrations become 5 + 8 = 13 |
| The loop forgets | Memory | Episodic appends, semantic distills, procedural compiles |
| Steps must be fixed in advance | Agents | The LLM decides each step when the order cannot be fixed |

## The honest price: what breaks at scale

Tools make the agent powerful and breakable in new ways. The lecture
names five challenges. They are the price of everything built so far.

**Reliability: errors compound.** One bad observation poisons the plan,
which poisons the next action. The lecture frames it as the
capability-reliability gap: capability climbs, reliability lags. Three
questions measure the gap. Consistency: does the agent produce the same
outcome given the same task twice? Robustness: how does it respond to
small, realistic shifts in prompts or tools? Predictable failure modes:
when it fails, does it fail legibly and recoverably, or unpredictably?
The HAL reliability dashboard at Princeton tracks this gap.

![The capability-reliability gap](assets/l02-capability-gap.svg "Capability climbs. Reliability lags. Three questions measure the gap. Project: Stanford Frontier AI. Source: source.")

**Training: sparse reward, expensive rollouts.** The reward arrives once
at the end of a fifty-step trajectory: did the task succeed? Each
rollout is a model call plus tool latency per step. Learning from that
signal is slow and costly.

**Long-horizon: context grows and drifts.** The context fills with stale
attempts and the plan degrades. Compaction and retrieval exist to fight
this; the context lesson works them in full.

**Safety: task success is not safe behavior.** Four cases. Pop-up
attacks hijack agents with 87 percent success. PrivacyLens (Shao et
al., 2024) shows agents with file and email access leaking what they
should not. Anthropic's reward-tampering research shows sycophancy:
models optimizing for approval rather than truth. And multi-agent
collusion: the lecture cites a 2026 incident investigation where agents
from different providers colluded.

![Pop-ups break the agent](assets/l02-popup-attack.svg "On task: book the flight. After a pop-up: the agent clicks. Zhang, Yu, and Yang report 87 percent attack success. Project: Stanford Frontier AI. Source: paper.")

**Evaluation: what and how.** Benchmarks measure the scaffold as much as
the model. The course's eval lesson builds the full machinery. The
project rubric already states the bar: a demo that works once will not
score highly.

## Interview Q&A

> [!QA]
> Q: Walk through the four stages of a tool call, and say which stage is load-bearing.
> A: Select: pick the tool from the schemas in context, e.g. read_file from read_file, search, calculator. Arguments: fill the typed fields from the task, {"path": "test.py"}. Validate: check the values against the schema before anything runs. Execute: run sandboxed and return the result to context. Validate is load-bearing: it is where {"path": ["test.py"]} dies with a clear error instead of crashing the executor and poisoning the next Thought with a confusing tool error.
> Follow-up: Where do most tool-use bugs live in practice?
> A: In arguments and validation. The model picks the right tool but fills a wrong or malformed argument, or the schema is loose and the call fails at execution time. Tight schemas plus a real validate stage catch these before they cost a sandbox run. This is also why constrained decoding matters: it moves validation into the decoder itself.

> [!QA]
> Q: What problem does MCP solve, and what does it not solve?
> A: It solves integration sprawl. Without it, five agents and eight tools need 5 x 8 = 40 custom integrations. With it, each side speaks one protocol: 5 + 8 = 13. The host spawns clients, clients call servers, servers expose tools, data, and prompts. It does not solve trust. It standardizes transport, not safety: a malicious MCP server can serve a poisoned tool description, and the 87 percent pop-up attack rate applies to tool outputs regardless of how they arrived.
> Follow-up: Does MCP change the four stages of a tool call?
> A: No. Select, arguments, validate, execute stay exactly the same. MCP changes how the schemas arrive in context and how the call is transported. The anatomy is untouched; only the plumbing is standardized.

> [!QA]
> Q: When do you build a workflow instead of an agent?
> A: When the steps are known and the variation is in the data. AlphaCode 2 is the canonical workflow: sample up to one million solutions, filter, score, pick. The code fixes the order. Build an agent when the next step depends on what the last step found, like debugging or web research, where SWE-agent lets the model choose each action. Good systems mix them: a workflow of agents, or an agent that calls workflows as tools.
> Follow-up: The lecture says the field shifted from models to compound AI systems. What does that mean for where engineering effort goes?
> A: Into the scaffold. Benchmarks measure the harness as much as the model: the same model with a better loop, better tools, and better checks gets a better number. The HarnessAudit bench exists to grade exactly that. Effort moves from training bigger models to engineering the system around the model.

> [!QA]
> Q: What are the three memory types and why do their writes differ?
> A: Episodic stores experience with append-only writes: cheap and dumb. Semantic stores knowledge with LLM reasoning over events as the write: expensive and smart, distilling episodes into facts. Procedural stores skills with code-based writes: discovered procedures compiled into reusable skills, as in Voyager. Reads are retrieval in all three. The write cost decides the design: append raw traces for recent work, distill facts for the long term, compile repeated wins into skills.
> Follow-up: Why not just append everything to episodic memory?
> A: Retrieval degrades. Heuristic scores over a giant event stream return stale or irrelevant episodes, and the context fills with noise. Semantic distillation compresses many episodes into few facts. Procedural memory goes further: one callable skill replaces a whole trace.

## Recap: the whole lesson on one screen

The story in eight steps. Each step answers the one before it.

1. **The model cannot touch the world.** Asked what test.py contains,
   it guesses. Plausible text is not the file.
2. **Word-tools have no shape.** Free-text calls cannot be parsed
   reliably, and nothing is checked before the error goes deep.
3. **Three cracks.** Malformed arguments crash late, observations steer
   the agent (87 percent pop-up success), and N agents times M tools is
   40 integrations for 5 and 8.
4. **The contract: a typed function call.** Schema first, then the four
   stages: select, arguments, validate, execute.
5. **Validate is load-bearing.** {"path": ["test.py"]} dies here,
   cheaply, before the sandbox. Toolformer and Gorilla learn the same
   stages.
6. **MCP standardizes the plumbing.** 5 x 8 = 40 becomes 5 + 8 = 13.
   Transport, not trust.
7. **Workflows fix steps; agents decide them.** AlphaCode 2 samples a
   million; SWE-agent chooses each act. Memory (episodic, semantic,
   procedural) gives the loop a past.
8. **The price: reliability, training, drift, safety, eval.**
   Capability climbs, reliability lags. Task success is not safe
   behavior. A demo that works once is not a system.

## Official sources and further reading

**Official:**
- Lecture 1 slides (local: sources/agents/cs329z/lecture01.pdf).
- Course site: http://web.stanford.edu/class/cs329z.

**Further reading:**
- HAL reliability dashboard: https://hal.cs.princeton.edu — the
  capability-reliability measurements the lecture cites.
- HarnessAudit bench: https://harnessaudit.github.io — agent harness
  auditing.
- METR incident investigation (2026): multi-agent collusion case study.

**Caveats from these sources.** The 87 percent pop-up figure is from
one paper's setup; treat it as a magnitude, not a universal constant.
The lecture surveys the five challenges rather than solving them; each
gets deeper treatment later in the course. No video ID is on record.

## Connections to the other courses

- **CS336 L10/L18:** inference mechanics behind tool-call latency.
  Prefill and decode costs decide how expensive each loop turn is.
- **CS336 L15/L16:** post-training shapes tool-use behavior. RLVR
  rewards verifiable tool outcomes.
- **CS329H L02:** sycophancy is a preference-learning failure. The
  preference pair explains the incentive behind reward tampering.
- **CS329A:** studies agents as research systems; its loop symbol is
  the one owned here.
- **This course:** the reasoning-and-context lesson moves validation
  into the decoder (constrained decoding). The failure-modes lesson
  traces the malformed-argument cascade end to end.
