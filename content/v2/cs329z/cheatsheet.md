# CS329Z cheatsheet

One page per theme. Formulas, counts, decision rules. All numbers from the course toys unless noted.

## Core formulas

| formula | meaning | where |
| --- | --- | --- |
| pass@k = 1-(1-p)^k | coverage: at least one of k passes | U01, U06 |
| pass^k = p^k | reliability: all k pass | U06 |
| gain per extra cost = delta/(cost multiple - 1) | ship rule vs the bar | U01, U04 |
| SE(diff) = sqrt(p1(1-p1)/n + p2(1-p2)/n) | noise on a comparison | U06 |
| z = delta/SE. |z| > 2 is actionable | regression gate | U06 |
| LoRA params = r(d + k) | adapter count | U05 |
| DPO loss = -log sigma(beta m) | preference training | U05 |
| P(i beats j) = sigma(s_i - s_j) | Bradley-Terry | U06 |
| flat H steps = p^H | compounding without checks | U08 |
| messages all-to-all = n(n-1), hub = 2n | coordination topology | U08 |
| cost = auto share x auto cost + esc share x esc cost | FDE cost model | capstone B |

## Counts to memorize

- LoRA 1024x1024, r = 8: 16,384 trainable (64x fewer).
- 7B params: 14 GB fp16, 3.5 GB 4-bit.
- Grading per 1000: program $1, model $50, human $2000.
- Timeout 0.1, r = 3: all-fail 0.001.
- p = 0.3, k = 5: pass@k 0.83, pass^k 0.0024.
- 1000 agents: 999,000 vs 2,000 messages per round.
- 0.99^500 = 0.0066.

## Decision rules

| decision | rule |
| --- | --- |
| workflow vs agent | path known: workflow. Steps unpredictable: agent |
| knob order | prompts, then weights, then compute |
| optimizer trust | gaps above 2 SE only |
| grader order | program, then model, then human sample |
| regression | block below -2 SE, celebrate above 2 SE, rerun otherwise |
| approval tier | auto (reversible), approve (costly), block (irreversible) |
| consent | implicit < explicit-once < explicit-each-time, by stakes |
| recovery | retry, rollback, escalate, compensate, cheapest first |
| eval tiers | dev (touch), test (schedule), sealed (once) |
| rollout | shadow, 10%, 50%, 100%, gates green 5 days each |

## Failure pairs (confused concepts)

- Grounding vs truth (U02).
- pass@k vs pass^k (U06).
- Retry vs idempotency (U03).
- Workflow vs agent (U04).
- Temperature vs top-k vs top-p (U01).
- Point vs pairwise judging (U06).
- Validator score vs human quality (U05).
- Demo vs production (U08).

## Provenance shorthand

- S01-S04: released, schedule-title level.
- S05-S20, finals: PLANNED / SOURCE ATTRIBUTION PENDING.
- S10, S16 guests: TBA, logged in GAP-08.
- Everything else: independent theory, labeled.
