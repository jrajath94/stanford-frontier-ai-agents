# U03 capstone: retries under chaos (proposed, not executed)

Status: design only. No experiment has run. All numbers below are planned, not measured.

## Replication

Reproduce the C08/C09 result in a chaos rig: a stub payment tool with timeout rate 0.1 and crash rate 0.05, a client with r = 3 retries, backoff [1s, 2s], and idempotency keys. Run 1000 charges at seed 0. Success criterion: zero double charges and an all-fail rate within 0.02 of the predicted 0.1^3 plus crash term.

## Extension

Question: which breaks first under chaos: the retry policy (too few tries) or the key store (expiry shorter than the retry window)?

Falsifiable hypothesis: with key TTL 60s and max retry span 70s, double charges appear. With TTL 300s they vanish. Retry count r = 5 does not fix TTL expiry.

Literature: timeouts, retries, idempotency (S04, U03-C07 through C09).

Data: synthetic charge stream. No human data, no real money.

Baselines: no keys. Keys with TTL 60s. Keys with TTL 300s. R = 3 vs r = 5.

Matched budgets: same fault schedule across arms (seeded).

Metrics: double-charge count, all-fail count, total latency.

Controls: same stub, same seeds, same fault injection.

Ablations: crash faults on/off. Timeout faults on/off.

Seed variation: 5 seeds. Report means and ranges.

Uncertainty: exact counts (no sampling error on double charges. They must be zero).

Failure criteria: if the no-keys arm shows zero doubles, the fault injector is broken. Fix it before trusting any arm.

Reproducibility: fault schedule seeds and rig code committed.

Negative results: if TTL 300s still shows doubles, the dedupe logic has a bug. Report it as a finding.

Limitations: stub faults, not production failure modes. No claim about real payment systems.

Ethical considerations: none. No real charges, synthetic only.
