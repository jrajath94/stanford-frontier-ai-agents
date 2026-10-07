# U03 interview keys

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per item.

## Breadth

- B1: states think, call, observe, done. Halting: answer emitted or budget B reached. Red flag: "it stops when done" with no budget. Remediation: C03.
- B2: host, client, server. Transports: stdio, Streamable HTTP. Remediation: C04.
- B3: authentication proves identity. Authorization grants permission. 401 vs 403. Red flag: merging them. Remediation: C05.
- B4: the allow/deny list plus resource limits. Default-deny fails closed: a forgotten entry blocks a feature instead of allowing an attack. Remediation: C06.
- B5: repeating a request has the same effect as doing it once. Rubric: the effect clause, not just "safe to retry". Remediation: C09.
- B6: binds the approval to the exact (tool, args) pair executed. Red flag: "approval to proceed". Remediation: C10.

## Deep ladders

- L1.1: expected value of the smaller of the latency and the timeout.
- L1.2: 0.66s without, 0.41s with.
- L1.3: 1 percent of calls at 30s contribute 0.30 of the 0.66 total. The tail carries nearly half the expectation.
- L1.4: thread plus join(tau). Cost is one thread and the false-error rate above tau.
- L1.5: the timeout bounds each step's wait. The budget bounds the number of steps. Red flag: "they do the same thing".
- L2.1: all-fail p^r. Expected tries 1 + p + ... + p^{r-1}.
- L2.2: 0.008 and 1.24.
- L2.3: when the failure is permanent (4xx, auth) or the operation is non-idempotent and already ran.
- L2.4: loop with sleep(w_i). Expected cost = expected tries x tool cost + expected wait.
- L2.5: retry suits transient failures of the same tool. Failover suits dead tools with a live alternative.

## Analytical/quantitative

- A1: r = 1: expected cost 1 x 0.02 = $0.0200, success 0.90. r = 3: expected tries 1.11 x 0.02 = $0.0222 plus expected wait 0.12s x 0.01 = $0.0012, total $0.0234, success 0.999. Strong answer gives both cost and success and notes the tradeoff.
- A2: 1000 x (1 - 0.001) = 999 expected successes, assuming retried calls succeed. Red flag: forgetting the abort class.

## Implementation/debug

- I1: bug 1: keys generated per attempt instead of per operation (check: log keys for a retried charge. Two different keys means the bug). Bug 2: the key store expires before the retry window or is in-memory across restarts (check: restart the server mid-retry and see if the dedupe holds). Rubric: two distinct mechanisms plus a check each.

## Changed-constraint scenarios

- S1: still matter: schemas (C02), the loop (C03), output contracts (C11), tool design (C12). Mostly moot: auth (C05), sandbox (C06), timeouts (C07), retries (C08), idempotency (C09), approval (C10) for side-effect-free local calls.
- S2: move approve-tier actions to deny or to a deputy approver. Or widen auto for reversible actions only. Risk: unattended high-risk actions, or a week of blocked work if everything needs approval.

## Research critique

- R1: strong: steelman = "one protocol for all tools kills N x M integration work". Rebuttal 1: local single-app toolsets pay protocol overhead for nothing. Rebuttal 2: version drift and proxy chains break the discovery promise. Experiment: measure integration time for N apps x M tools with MCP vs hand-rolled across small and large N x M.
