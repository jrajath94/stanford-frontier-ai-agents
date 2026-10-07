# Transfer set keys: cs329z

Full keys with the decision each set tests, strong-answer elements, red flags, and remediation. Kept separate from `transfer-sets.md`.

## T1: the catering bot

- Tests: decomposition under a call budget (U01-C02, C10, C11, C12).
- Strong: 2-call design (call 1: retrieve this week's menu + date availability. Call 2: compose the answer with citations). Baseline: one call, no retrieval. Eval: 50 questions with checkable answers. Report the pass rate. Build first: the retrieval + one-call baseline. Stop rule: answer found or budget spent.
- Red flag: "fine-tune the model" on a weekly-changing menu. Remediation: U01-C11, C12.

## T2: the policy library

- Tests: retrieval with permissions and abstention (U02-C04 through C06, C10, C11).
- Strong: chunk by memo section, hybrid scoring, ACL filter before ranking (never after), citations per claim, abstain when the filtered set is empty or the ACL blocks the answer. Feared failure: a permission leak (the ACL applied after ranking, leaking snippets).
- Red flag: "rank then filter". Remediation: U02-C06.

## T3: the refund tool

- Tests: timeouts, retries, idempotency, approval (U03-C07 through C10).
- Strong: idempotency keys on every call, r = 3 with backoff, timeout 10 s, tiers (auto under $50, approve $50-500, block above), sandbox for the integration tests. Cost arithmetic: 1000 refunds, expected failures 0.1^3 per refund after retries, zero double charges by key dedupe.
- Red flag: "retry without keys". Remediation: U03-C09.

## T4: the research team

- Tests: handoffs, shared state, error compounding, stopping (U04-C08 through C12).
- Strong: envelopes (task, state, constraints, done) between agents, blackboard for the shared brief, per-stage checks (search quality, filing relevance, brief citations), stop on brief complete or budget. Errors compound multiplicatively: 0.9^3 = 0.73 without checks. Single-agent baseline compared on cost per success.
- Red flag: "shared soup with no envelopes". Remediation: U04-C08.

## T5: the prompt tuner

- Tests: knob choice under constraints (U05-C01, C02, C06-C12).
- Strong: prompt knob (no GPU, $500). Reflection-guided search on the 300 examples, synthetic expansion with code verification, three-tier eval (dev/test/sealed). Would not: fine-tune (no GPU), trust the judge without calibration, tune on the sealed set.
- Red flag: "buy GPU time" or "optimize on all 300". Remediation: U05-C02, C12.

## T6: the judge audit

- Tests: validator calibration, judge bias, human alignment (U05-C11, U06-C03, C04, C06, C12).
- Strong: calibration gap on 50 human labels, position-bias swap test, seed spread, alignment correlation. Three fastest lies: uncalibrated optimism (gap 0.15+), position bias inflating their own model, no human receipt (r unknown). Verdict rule: report the calibrated number with the receipt or reject the 0.91.
- Red flag: "re-run the judge". Remediation: U05-C11.

## T7: the benchmark fight

- Tests: the eval tuple, scaffolding, grading, regression gates (U06-C01 through C03, C08, C11).
- Strong: one tuple for both vendors (same E, S, F), real scaffolding, program-first grading cascade, paired delta with z-gate. Sample size for a 0.03 verdict at z = 2: SE = 0.015, n = 0.5/0.000225 = 2223 tasks. Refuse: vendor-run numbers, vendor-chosen tasks, mock scaffolding.
- Red flag: "average their reported scores". Remediation: U06-C01.

## T8: the inbox agent

- Tests: privacy, permissions, approval, injection, consent (U07-C01, C02, C04, C05, C12).
- Strong: zones (public/internal/secret), K = {read, draft} (no send), approve tier for sending, email bodies tagged as data (never instructions), consent gradient (draft implicit, send explicit-each-time). The project-ending incident: an email sent to the wrong person, or a secret leaked via a crafted email.
- Red flag: "send is fine, the model is careful". Remediation: U07-C04.

## T9: the night shift

- Tests: checkpoints, recovery, tracing, rollback, ownership (U07-C08, U08-C04 through C06, C10).
- Strong: checkpoint every invoice batch, recovery ladder (retry, rollback to last batch, escalate, compensate), cost/latency alerts, one-command rollback to manual, named owner with the runbook, morning handoff report (processed, paid, flagged, failed). Kill switch: the owner or the on-call may pull it. It drains the queue first.
- Red flag: "no kill switch, it works". Remediation: U08-C06.

## T10: the science loop

- Tests: hypothesis budgeting, oracles, kill criteria (U08-C03, C04, C11).
- Strong: $10,000 / $200 = 50 simulations max. Milestones: 10 sims per milestone with a hit-rate check. Cost per finding = 200/hit-rate. Kill criterion: hit rate below 0.1 after 20 sims, or cost per finding above $2000. Never unsupervised: changing the simulation code, spending beyond the budget, or declaring a finding without the oracle.
- Red flag: "let it run all 50". Remediation: U08-C03.
