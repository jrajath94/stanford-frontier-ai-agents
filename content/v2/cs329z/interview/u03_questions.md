# U03 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define the tool/result loop states and the halting conditions.
B2. Name the three MCP roles and the two transports.
B3. State the difference between authentication and authorization.
B4. What is a sandbox policy, and why default-deny?
B5. Define idempotency in one sentence.
B6. What does an approval gate bind, and to what?

## Deep ladders (2 x 5)

### Ladder 1: timeouts

L1.1 Define: write E[min(T, tau)] in words.
L1.2 Toy: compute expected wait with and without a 5s timeout on the C07 distribution.
L1.3 Derive: why does the tail dominate the expectation?
L1.4 Implement and complexity: write the timeout wrapper. State its cost.
L1.5 Compare: timeouts vs a step budget alone. What does each bound?

### Ladder 2: retries

L2.1 Define: write the all-fail probability and the expected-tries sum.
L2.2 Toy: p = 0.2, r = 3. Compute both.
L2.3 Derive: when is a retry never worth it?
L2.4 Implement and complexity: write the retry loop with backoff. State expected cost.
L2.5 Compare: retry vs failover. Which failure types suit each?

## Analytical/quantitative (2)

A1. A tool has p = 0.1 per-try failure and each try costs $0.02. Compare expected cost for r = 1 vs r = 3 with waits [1s, 2s] valued at $0.01/s.
A2. 1000 calls have error rates RATE_LIMIT 0.05, TIMEOUT 0.01, AUTH 0.001. A caller retries on the first two and aborts on AUTH. Compute expected successes.

## Implementation/debug (1)

I1. Your retry loop double-charges 2 percent of payments. The idempotency keys are enabled. Name two bugs and how you check each.

## Changed-constraint scenarios (2)

S1. The tool is a local pure function (no network, no side effects). Which of C05-C11 still matter?
S2. The approver goes on vacation for a week. The agent must keep running. What changes, and what is the risk?

## Research critique (1)

R1. "MCP makes custom tool integrations obsolete." State the strongest version, then give two reasons it fails and one experiment that would change your mind.
