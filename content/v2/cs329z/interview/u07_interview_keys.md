# U07 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: touch only what the task needs. Violation rate = needless touches per task. Remediation: C01.
- B2: system, developer, user, tool output. Tool output is data. Red flag: "the user outranks the system". Remediation: C02.
- B3: ASR = successful attacks / total attacks. Loop: attack, measure, fix, re-attack. Remediation: C03.
- B4: a named permission. Least privilege = the smallest set that completes the task. Remediation: C04.
- B5: auto, approve, block. Sort by reversibility and blast radius. Remediation: C05.
- B6: none, implicit, explicit-once, explicit-each-time. Red flag: "one consent covers all". Remediation: C12.

## Deep ladders

- L1.1: untrusted span = text from tools/files/web. Instruction = text with an obey-me claim. Tag = the source label.
- L1.2: the naive agent reads content and obeys. The tagging agent sees the tool source and refuses instructions from data.
- L1.3: paraphrase changes content but not source. Source-based tagging is paraphrase-proof by construction.
- L1.4: wrap spans with tags, gate plans that cite tool/web spans as instructions. O(tokens).
- L1.5: tagging limits what the agent tries. The sandbox limits what actions can do. Rubric: both limits plus the depth argument.
- L2.1: tiers auto/approve/block. Levels none/implicit/explicit-once/explicit-each-time.
- L2.2: 30 x 0.5 + 10 x 5 = 65 min/day. Rubric: the arithmetic.
- L2.3: the gradient spends friction where the risk is: 10 min vs 50 min flat. Saving 40 min.
- L2.4: classify by reversibility and cost rules, queue with timeout, deny by default. O(1) per action.
- L2.5: the boundary encodes crisp rules at the action layer. Tiers handle judgment calls. Rubric: the crisp-vs-judgment split.

## Analytical/quantitative

- A1: ASR 0.24 (SE 0.060) and 0.06 (SE 0.034). Gap 0.18 = 2.6 SE. Real fix. Red flag: "ASR fell, ship it" without the SE.
- A2: precision 0.62, net +234 min. Zero at 700p = 200, p = 0.286. Below 0.29 the predictor destroys value. Rubric: both numbers plus the breakeven.

## Implementation/debug

- I1: bug 1: the gate checks only the first plan, not replans (check: log every plan's instruction sources and find the ungated one). Bug 2: the tag is stripped when the span is summarized (check: trace one poisoned span through the summarizer and confirm the tag survives). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: allowlist the recipe tool as a trusted instruction source, keep tagging for everything else. The gate checks the allowlist before blocking. First test: a poisoned recipe step from a non-allowlisted tool is still blocked.
- S2: the model approver inherits judge biases (C06) and may approve its own style. The backstop becomes a rubber stamp with latency. First test: measure the model approver's catch rate on a labeled set of bad actions before it touches the queue.

## Research critique

- R1: strong: steelman = "each guardrail removes a failure class". Rebuttal 1: guardrails compose badly (the 2-second approver, the 200-item queue) and add latency without safety. Rebuttal 2: the toy where the fix breaks legitimate tasks (recipe API blocked, password reset denied). Experiment: measure task success and ASR across 0, 1, 2, 3 guardrail layers. Safety rises then task success falls. The optimum is interior.

## Concept-targeted supplements

- CS1: stop at 3 iterations. Gains are +4 then +2: diminishing returns, the 4th buys little. The rig is the judge: the test suite decides pass/fail, not the agent's confidence. Guarantee rests on the assumption that the tests capture the issue. Weak tests certify broken code. Rubric: the stopping rule from the gains plus the judge-vs-confidence distinction.
