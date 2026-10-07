# Transfer sets: cs329z (all 8 units)

Unfamiliar transfer tasks. Closed book. No recognition cues from the lessons. Keys in `keys-transfer.md`, kept separate.

## T1: the catering bot (U01)

A catering company wants a bot that answers "can you serve 200 guests on date X with a vegan menu". The menu changes weekly. The budget allows 2 model calls per question. Design the system: name the components, the interfaces, the eval, and the baseline. State what you would build first and what the stop rule is.

## T2: the policy library (U02)

A law firm has 50,000 memos. Associates need answers with citations. Half the memos are client-confidential with per-client ACLs. A query is usually "what did we advise client X on topic Y". Design the retrieval pipeline: chunking, scoring, permissions, citations, abstention. Name the failure you fear most.

## T3: the refund tool (U03)

An agent must issue refunds up to $500 through a flaky payments API (timeout rate 0.1, occasional 500s). Design the tool integration: schema, timeout, retry policy, idempotency, approval tiers, sandbox needs. Show the expected cost arithmetic for 1000 refunds.

## T4: the research team (U04)

Three agents research a market: one searches, one reads filings, one writes the brief. Design the coordination: handoff envelopes, shared state choice, per-stage checks, stopping rules, and the single-agent baseline comparison. State where errors compound and what you measure.

## T5: the prompt tuner (U05)

A startup's support bot scores 0.72 and the bar is 0.80. They have $500, no GPU, and 300 labeled examples. The task is checkable by code. Design the optimization plan: which knob (prompt, weights, compute), the optimizer loop, the data plan, and the eval hygiene. State what you would not do.

## T6: the judge audit (U05/U06)

A team uses an LLM judge to grade their agent and reports 0.91. You are asked to audit the number. Design the audit: the calibration check, the bias checks, the human-alignment receipt, and the verdict rule. State the three fastest ways the 0.91 could be a lie.

## T7: the benchmark fight (U06)

Two vendors claim 0.85 and 0.88 on their own benchmarks for a code agent. Your company must pick one. Design the independent evaluation: the tuple, the scaffolding, the grader cascade, the regression gate for the decision, and the sample size for a 0.03 verdict. State what you refuse to accept from the vendors.

## T8: the inbox agent (U07)

An agent reads email and drafts replies. The CEO wants it to "just handle it". Design the safety case: privacy zones, the permission boundary, approval tiers, the injection defense for email content, and the consent gradient for sending. Name the one incident that ends the project if it happens.

## T9: the night shift (U07/U08)

An agent runs unattended overnight: it processes invoices, pays the approved ones, and flags the rest. Design the production system: checkpoints, the recovery ladder, tracing and cost alerts, the rollback plan, ownership, and the morning handoff. State the kill switch and who may pull it.

## T10: the science loop (U08)

A lab wants an agent to propose battery materials and run simulations. Each simulation costs $200 and takes 2 hours. The budget is $10,000. Design the loop: the hypothesis budget, the oracle rules, the cost-per-finding math, the milestone checks for the long horizon, and the kill criterion. State what the agent may never do unsupervised.
