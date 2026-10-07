# CS329Z crash course: compound AI systems and agents (all 8 units)

One-pass review of the full course. Each unit: the ideas, the key numbers, the decision rules. Detail lives in `lessons/u0N_lesson.md`.

## U01: Compound systems and LLM foundations

A model is a function. A system is components with interfaces and per-interface failure modes. Decompose the task, then pick the architecture: the simple baseline first, the compound system only when the gain per cost clears the bar. Decoding: temperature, top-k, top-p are three different controls. Test-time scaling: pass@k = 1-(1-p)^k measures coverage (at least one of k). Structured I/O plus constrained decoding make outputs machine-readable. Context engineering decides what fills the window.

Key numbers: pass@k at p = 0.3, k = 8: 0.94. Gain per extra cost = delta/cost-multiple.

## U02: Retrieval and evidence engineering

Grounding is not truth: a cited claim can still be false. The stack: chunk, embed, store, hybrid score (lexical + dense, normalized before fusion), rerank, cite, abstain. ColBERT keeps token vectors and scores with max-sim at query time. Cross-encoders read query and doc together (accurate, slow). Permissions filter before ranking, never after. Abstain when the evidence is insufficient.

Key numbers: fusion needs normalization (raw BM25 near 20 vs dense near 0.9). Leakage: ACLs applied after ranking leak snippets.

## U03: Tools, protocols, and runtime safety

The tool/result loop is a state machine: thought, call, result. MCP: host/client/server, JSON-RPC 2.0, stdio (local trust) vs Streamable HTTP (network auth). Timeouts cut the tail. Retries need idempotency keys, or they double-charge. TTL must exceed the retry window. Approval tiers sort by reversibility. Sandboxes bound blast radius.

Key numbers: timeout 0.1, r = 3: all-fail 0.001. Zero doubles is the only passing count.

## U04: Frameworks, workflows, memory, coordination

Five workflow patterns (chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer) plus the agent: fixed code path vs model-directed. ReAct interleaves thought, action, observation. Memory: working context vs persistent store. Files for exact facts. Handoffs carry envelopes (task, state, constraints, done). Errors compound multiplicatively: 0.9^3 = 0.73. Stopping rules: answer, budget, stall, denial.

Key numbers: gain per extra cost at bar 0.03 decides single vs multi.

## U05: Optimization and agent data

Three knobs in spend order: prompts (words), weights (LoRA: W + BA, r << d), compute (bigger models, more calls). Prompt optimizers search wordings with sentence-shaped feedback. DPO trains on preference pairs with -log sigma(beta m), no RL. Data: traces (cheap, noisy), demos (expensive, clean), feedback (weak signal). Synthetic data needs an independent verifier. The flywheel compounds deployment data. Hygiene: quarantine train from eval, calibrate the validator before the optimizer trusts it, three tiers (dev/test/sealed).

Key numbers: LoRA 1024x1024 r = 8: 16,384 vs 1,048,576 (64x). Trust gaps above 2 SE only.

## U06: Benchmark and evaluation infrastructure

A benchmark is a tuple: request, environment, stopping, scorer. No tuple, no benchmark. The scaffolding is part of the measurement (mock vs real: 0.13 gap on the toy). Graders: program ($0.001), model ($0.05), human ($2). Cascade cheap-first. Judge prompts need criteria, anchors, examples, format. Point vs pairwise: Bradley-Terry turns wins into strengths. Judge biases: position, verbosity, self-preference. Swap and average, report seeds. pass@k (coverage) vs pass^k (reliability). Isolate the test rig (fresh world per task). Inject faults to grade recovery. Tiny suites for speed, z-gates for regressions (|z| > 2), human alignment as the receipt.

Key numbers: p = 0.3, k = 5: pass@k 0.83, pass^k 0.0024. Delta 0.02 on n = 200 is noise (z = 0.4).

## U07: Safety, coding, and proactive agents

Privacy: minimize, log, audit. Instruction hierarchy: system > developer > user > tool output (data, never instructions). Tag sources. The planner obeys tags, not content. Red-team: attack, measure ASR, fix, re-attack. Permission boundary: capabilities enforced at the action layer. Approval tiers: auto/approve/block by reversibility. Coding agents: the test rig decides (tests), SWE-bench provenance (FAIL_TO_PASS + PASS_TO_PASS, strict). Checkpoints bound crash losses. Proactive: user model with confidence, next-action prediction above a precision gate, mixed initiative by confidence and stakes, consent gradient matching friction to risk.

Key numbers: ASR 0.24 to 0.06 (z = 2.6). Consent gradient: 10 min/day vs 50 flat.

## U08: Frontiers, production, and project artifacts

Computer use: observe, ground, act, verify. Multimodality: ablate before you pay. Science agents: the oracle is the world. Cost per finding = c/hit-rate. Long horizon: planner/worker/checker. 0.99^500 = 0.0066 flat vs 0.90 with checks. Production: trace every span, attribute every dollar, p99 budgets, recovery ladder (retry, rollback, escalate, compensate), hub topology (2n vs n^2), interpretability by counterfactual probe. Project: reviewable proposal (question, baseline, budget, metric, kill criterion), named owner, runbook, scoped capstone, honest gap log.

Key numbers: 1000 agents: 999,000 vs 2,000 messages per round. No trace, no production.

## The twelve rules (one per course theme)

1. Name the interfaces before the system.
2. Baseline first, compound only on gain per cost.
3. Grounding is not truth.
4. Filter permissions before ranking.
5. Retries without idempotency double-charge.
6. Workflows when the path is known. Agents when it is not.
7. Spend words, then weights, then compute.
8. Calibrate the validator before the optimizer trusts it.
9. No tuple, no benchmark.
10. Data is never instructions.
11. Match the friction to the risk.
12. No trace, no production.
