# Crash course , cs329a Agentic AI and Frontier Research

The whole course in one pass: 8 units, 96 concepts, the mechanisms
that matter and the numbers that anchor them. Detail lives in
`lessons/u01`-`u08`. Practice in `labs/`, `interview/`,
`capstones/`.

## The arc

U01 spends compute at test time. U02 grounds the agent with tools
and feedback. U03 plans and searches. U04 evolves agents. U05
builds software-engineering and kernel agents. U06 gives them
memory. U07 reasons formally and bounds autonomy. U08 evaluates
long-horizon work and turns the course into research projects.

## U01 , Test-time compute and verification

More tries help when tries differ. pass@N = 1-(1-p)^N: with
p=0.25 and N=5, the set wins 0.76 of the time while one ticket
wins 0.25. Best-of-N samples N and keeps the verifier's top
pick. Self-consistency samples N and takes the majority. The
generator/verifier gap: verification is cheaper than generation,
which is why selection works. Weak verifiers help only above
0.60 pairwise accuracy (below 0.55 the method is untestable).
Selection bias is the failure: a verifier that rewards length
selects for length. The cost-success curve is concave: each new
sample adds less. Read it to allocate a fixed budget.

## U02 , Feedback and tools

ReAct: thought, action, observation, repeat. Execution feedback is
ground truth from the world. Self-critique is the model's
opinion and shares its blind spots. Code and tests are the
tightest loop: the test suite is a semi-trusted judge. Critique
is not a learning update: a comment changes the next try, a
gradient changes the weights. Constitutional feedback is critique
with principles. Reward signals shape behavior. Constraints bound
it. Tool errors are data: read the traceback, do not repeat the
call. Shortcut exploitation is the agent doing the wrong thing
correctly (editing the test). Independent validation is the
separate judge that execution feedback cannot be.

## U03 , Planning and search

Tree search: state (reasoning so far), action (next step),
reward (right answer). A perfect verifier makes search tractable:
every node is labeled free, so only the policy is learned.
Adaptive branching spends compute where it matters. Decomposition
splits the problem. Parallel planning runs branches together.
Multi-step credit is the hard part: which step caused the win.
Synthetic traces, STaR, and reasoning RL all manufacture training
signal from search. DAPO/GRPO are the reading pointers. Stay
on-policy: train on what you deploy. The budget binds everything.
Reward validity is the last word: a high reward that does not mean
a right answer is a hack, not a reward.

## U04 , Open-ended evolution

Vary a population of agent architectures, select the fittest,
inherit with mutation. Novelty search escapes deceptive
landscapes by rewarding difference. Selection is Goodhart in a
population: it selects on the proxy, so the proxy is what grows.
Holdout separation is the law: the champion is scored on data the
search never saw, with the true metric. Evidence provenance
tracks where every number came from. Resource budgets bound the
search. Novelty claims need the holdout gap. Safe iteration means
the kill rule is real: a project that cannot pass a gate dies at
the gate.

## U05 , Software-engineering and kernel agents

CodeMonkeys: serial iterations S raise coverage (0.832 at S=1 to
0.997 at S=5 with K=8), parallel width K amortizes the shared
context (context share 25.0 percent at K=8, 7.7 percent at K=32).
Selection has three stages: generate, vote with model-generated
tests, and a final selection trajectory. KernelBench: the model
rewrites a PyTorch reference as a GPU kernel. fast_p counts
kernels that are both correct AND at least p times faster
(correctness 0.60 but fast_1 0.40 on the toy: speed without
correctness scores zero). Amdahl: 2x on 60 percent gives 1.43x,
never more than 2.5x. Profile first: the biggest share sets the
ceiling.

## U06 , Memory, caches, and long-context

The KV cache is the working memory of inference. CacheBlend
reuses non-prefix chunk caches and recomputes only high-
deviation tokens: 2,048 prefill units become 307 recomputed
plus 64 of deviation check, a 5.52x saving. MemGPT pages its
own memory: hot facts stay in main context (8 slots), cold
facts are evicted to archival storage (12 in the toy) and return
via search. 20 turns, 27 memory actions, nothing lost. A
Cartridge trains a small KV cache per corpus by self-study:
20,480 tokens distill into 512 trained slots, 40x fewer per
query. Training amortizes over queries.

## U07 , Reasoning, formal systems, and autonomy

Formal proof search: goal (what remains), tactic (a step), kernel
(the checker). The kernel is the free verifier: every node is
labeled right/wrong for free. AlphaGeometry's split: the neural
net proposes constructions (ideas are cheap), the symbolic
engine closes by deduction (deduction decides). Report search and
proof separately: 13 nodes searched, 4-step proof. Sim-to-real:
domain randomization narrows the reality gap (0.25 to 0.12 on
the toy). The autonomy envelope: authority must not exceed
verified capability, with margin. 3 of 4 configs admitted. The
low-capability high-authority cell rejected. Traces: a trace is
faithful iff flipping the cited fact changes the behavior.
30 percent of plausible traces are stories.

## U08 , Long-horizon evaluation and research projects

Duration is difficulty in disguise: 0.90 at 15 minutes, 0.35 at
8 hours on the toy. Short-task scores do not extrapolate.
Value = hours times hourly rate: weight tasks by value, not
count. GDPVal: experts from 44 occupations write real
deliverables. Blinded pairwise comparison gives the win rate.
220 gold tasks anchor it. DeepScholar-Bench grades research
synthesis in three dimensions: synthesis, retrieval quality,
verifiability. The split diagnoses the system (fluent 0.80 but
thin 0.35). Ship on the minimum, not the mean: A means 0.767
but mins 0.55, B means 0.72 and mins 0.70. Stop when the next
hour's value falls below its cost. The contamination gap:
same-model judge 0.85 minus independent judge 0.60 = 0.25 of
similarity, not quality. Budget three fuels: agent, judge,
audit. The audit binds. Ablate: the delta is causal. Gates with
kill rules. Negative results with power. Five open questions.

## How the units connect

U01's verifier is U07's kernel pushed to the limit (infallible)
and U08's judge pushed to the real world (fallible). U02's
execution feedback is U03's reward signal grounded. U04's
holdout separation is U08's eval hygiene at population scale.
U05's selection stage is U01's best-of-N with tests as the
verifier. U06's paging is U03's search over memory. The course
is one idea restated eight ways: generate candidates, verify
cheaply, select honestly, and report what the verifier cannot
see.
