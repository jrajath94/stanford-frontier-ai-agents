# U04 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: signature = input-output contract. Module = parameterized pipeline of signatures. Optimizer = search over prompts/demos maximizing a metric. Red flag: "DSPy is a prompt library". Remediation: C01.
- B2: chaining (sequence), routing (categories), parallelization (independent subtasks or votes), orchestrator-workers (unpredictable subtasks), evaluator-optimizer (clear criteria). Remediation: C03.
- B3: in a workflow the code path is fixed. In an agent the model directs its own steps. Red flag: "agents are smarter workflows". Remediation: C03.
- B4: short-term = recent trace in context. Long-term = summaries plus indexed records outside the window. Remediation: C06.
- B5: the state passed between agents: task, state, constraints, done. Remediation: C08.
- B6: answer found, budget reached, stall detected, approval denied. Remediation: C12.

## Deep ladders

- L1.1: t = thought text, a = tool call with args, o = tool result.
- L1.2: thought, action(multiply), observation(42), thought, action(is_prime), observation(false), answer.
- L1.3: each thought sees all prior observations, so the plan updates on surprises instead of following a fixed script.
- L1.4: loop appending (t, a, o). Cost per step = one model call plus one tool call.
- L1.5: ReAct 7.78, planning 6.67 steps per success. Planning cheaper, ReAct more adaptive. Rubric: both numbers plus the tradeoff.
- L2.1: r_i per stage. Effective r_i + (1 - r_i) c_i with catch rate c_i.
- L2.2: 0.729 without, 0.941 with.
- L2.3: at the least reliable stage. That is where the product loses most.
- L2.4: runs x stages loop, O(runs x stages).
- L2.5: per-stage checks localize failures and allow partial retry. End-to-end only says pass/fail.

## Analytical/quantitative

- A1: ratio 8000/500 = 16x. SE = sqrt(0.7 x 0.3/10) = 0.145. Red flag: quoting recall without an interval.
- A2: (0.90 - 0.74)/4 = 0.16/4 = 0.04 per unit extra cost. Above the 0.03 bar: multi-agent ships.

## Implementation/debug

- I1: bug 1: exact-match on observations that differ trivially each time (check: log consecutive observations and diff them). Bug 2: k compared against step count instead of consecutive identical observations, or the detector resets on every thought (check: unit-test with 3 planted identical observations). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: drop the two-tier memory (C06) and file memory (C07). Keep handoffs (C08) only if multiple agents remain. The window holds everything, so eviction machinery buys nothing.
- S2: messages (least privilege. The blackboard leaks to all readers). First test: an agent without clearance never receives the secret's bytes.

## Research critique

- R1: strong: steelman = "specialization plus parallelism beats one generalist". Rebuttal 1: coordination price (handoff tokens, 0.729 pipeline reliability). Rebuttal 2: the toy where multi scores 0.81 at 5x vs single 0.74 at 1x and loses the cost-benefit. Experiment: paired comparison across 5 task families. Multi wins only with clean handoffs.
