# Oral defense keys: cs329z

Minimum sufficient explanation, strong answer, red flags, rubric, remediation per ladder. Kept separate from `oral-defenses.md`.

## D1

- F1: (0.78-0.74)/3 = 0.0133 per unit extra cost.
- F2: SE near sqrt(0.5/200) = 0.05. The 0.04 gap is 0.8 SE: noise.
- F3: the decision is about money, not points. Cost-per-success prices the gain.
- F4: paired eval, same tasks, both systems, gain per cost with SE. Costs n x 4x calls.
- F5: when the gain is noise (it is) or the bar exceeds 0.013.
- F6: eval not representative. The system games the metric.
- F7: the eval mirrors deployment. If it does not, the 0.78 is theater.
- F8: rerun both on 200 more items, paired. Rubric: the ratio, the SE, the experiment. Red flag: defending on vibes. Remediation: U01-C11, U01-C12.

## D2

- F1: fused = w x lexical + (1-w) x dense on normalized scores. Normalization puts the witnesses on one scale.
- F2: the query has the exact code. Dense paraphrases past it. Lexical catches the code. Fusion ranks A.
- F3: raw dense scores live near 0.9, raw BM25 near 20. Without normalization dense always wins.
- F4: label the query (exact-term vs paraphrase), check the gold answer, score both rankings on the labeled set.
- F5: w = 0 when queries carry no exact terms (pure paraphrase load).
- F6: the eval underweights that query class. One valid complaint is a sampling signal.
- F7: anecdote becomes evidence at n with labels. One is a ticket, fifty is a slice.
- F8: label 200 queries by class, tune w per class. Rubric: the procedure, not the verdict. Red flag: changing w on one complaint. Remediation: U02-C05.

## D3

- F1: repeating a request has the same effect as doing it once. The key dedupes retries.
- F2: all-fail 0.1^3 = 0.001. Without keys: every retried timeout risks a double. With keys: zero.
- F3: a retry after the key expires looks like a new request. TTL must exceed the retry window.
- F4: log keys per attempt (per-attempt keys?), compare TTL vs window, check store durability.
- F5: retries without keys trade failures for doubles. The finance report prices the trade.
- F6: seeded chaos run, count doubles. Zero is the only passing count.
- F7: a restart wipes the store. Retries after the restart double-charge.
- F8: fault injector (timeouts, crashes), r = 3, TTL 300 s, 1000 charges, count doubles. Rubric: ordered diagnosis plus the proof. Red flag: blaming the retry concept. Remediation: U03-C08, C09.

## D4

- F1: (0.81-0.74)/4 = 0.0175 per unit extra cost. Below the 0.03 bar: single wins.
- F2: 0.0175 < 0.03. Verdict: single agent.
- F3: stage reliabilities multiply: 0.9^3 = 0.73. Each handoff is a multiplier below 1.
- F4: task (what), state (where), constraints (bounds), done (signal). Each prevents a handoff failure class.
- F5: families with clean handoffs and parallelizable subtasks.
- F6: the weakest handoff: merge two agents, re-measure.
- F7: run the eval items through a handoff-cleanliness judge. If most are single-agent-shaped, the eval is biased.
- F8: 5 families, paired, gain per cost vs the bar on each. Rubric: concedes the number, names the cut. Red flag: defending the team on principle. Remediation: U04-C11.

## D5

- F1: (x, y_w, y_l). Loss = -log sigma(beta m).
- F2: 0.673 and 0.724.
- F3: beta sets the distance from the reference. At 0 the loss is constant and nothing trains.
- F4: correlate the policy's length with its win rate on length-controlled pairs. If length predicts wins, it learned verbosity.
- F5: DPO learns the contrast (w beats l). SFT-on-winners learns the winners only, no contrast.
- F6: show that longer y_w wins regardless of content: length-controlled A/B.
- F7: trust the users on ramble (they live with it). Trust the judges on the rubric they graded.
- F8: length-controlled human eval, DPO vs SFT-on-winners. Rubric: the numbers plus the length control. Red flag: "judges rated it higher, ship it". Remediation: U05-C05.

## D6

- F1: mean(validator) - mean(human) on a calibration set.
- F2: gap 0.15. The optimizer will climb the 0.15 optimism.
- F3: every gradient step follows the validator. Errors in the validator become the objective.
- F4: 50 human labels (gap), 100 swapped pairs (bias), 5 seeds (spread), 30-item correlation (receipt).
- F5: the calibrated number is lower and honest. The 0.91 risks a launch on phantom gain.
- F6: uncalibrated optimism (check the gap), position bias (swap test), no human receipt (measure r).
- F7: 0.31 licenses nothing. The metric climbs alone.
- F8: the 50-label calibration: one day, kills or confirms the 0.91. Rubric: the audit list plus the verdict rule. Red flag: "the judge is strong". Remediation: U05-C11.

## D7

- F1: pass@k = 1-(1-p)^k (at least one). pass^k = p^k (all k).
- F2: 0.97175 and 0.0000059.
- F3: P(at least one passes) = 1 - P(all fail) = 1 - (1-p)^k under independence.
- F4: k in {1,2,5,10}, both columns, the two questions labeled.
- F5: the code agent gets pass@k (8 tries, verifier picks). Nothing gets pass^k except reliability claims.
- F6: the samples correlate (low temperature). True coverage is near p.
- F7: it fails when samples are near-identical. The formula then overstates coverage silently.
- F8: single-shot eval: one sample per task, no retries. That number is the product number. Rubric: both formulas plus the independence caveat. Red flag: "0.97 is the score". Remediation: U06-C07.

## D8

- F1: system > developer > user > tool output. Tags label the source.
- F2: miss rate 1/5 = 0.20. One password sent.
- F3: paraphrase changes content, not source. Source tagging is paraphrase-proof.
- F4: the gate blocks any plan whose instruction cites a tool/web span. The 5th needed the pasted-text rule too.
- F5: tagging limits what the agent tries. The sandbox limits what actions can do.
- F6: the user-paste case: the instruction hierarchy (user text still below system/developer) plus a confirmation for consequential actions from pasted content.
- F7: a 0.00 ASR on the first run means the attacks are weak, not the defense strong. Harden the attack set.
- F8: log the trace, rotate the credential, add the attack to the red-team set, tell the user what happened and what changed. Rubric: the hierarchy plus the incident steps. Red flag: "the tagger works". Remediation: U07-C02, C03.

## D9

- F1: the gate is a bar with a measurement. Cost = auto share x auto cost + escalation share x human cost.
- F2: 0.808 x 0.08 + 0.192 x 2.40 = 0.065 + 0.461 = 0.53.
- F3: escalations are 19 percent of volume but 87 percent of cost.
- F4: A: raise the cap (re-measure precision). B: cut flag noise (measure the false-escalation rate). C: renegotiate the bar (show the $1.87 saving vs baseline).
- F5: shadow mode keeps learning without the cost. Shipping on a failed gate spends the budget on hope.
- F6: the false-escalation rate: every point cut there drops cost 2.4 cents per request... precisely: 0.01 x (2.40-0.08) = $0.023 per request per point.
- F7: precision gates the quality, not the money. The business case needs both.
- F8: shadow 2 weeks, 10 percent with 5 green days, 50 percent, 100 percent. Roll back on any red day. Rubric: the arithmetic plus the no-ship-on-red rule. Red flag: "precision is high, ship it". Remediation: U08-C05, capstone B.

## D10

- F1: planner sets milestones, worker executes bounded subtasks, checker verifies, milestone a verifiable subgoal.
- F2: 0.99^500 = 0.0066.
- F3: each check catches errors before they compound into the next 50 steps.
- F4: predicate: milestone state matches the spec AND no constraint violated. Both must hold.
- F5: hierarchy buys reliability through verification. Longer context buys detail without checks.
- F6: the milestone is wrong (bad plan) or the worker is weak (bad execution). Check the predicate first.
- F7: the workers execute the wrong plan perfectly. The planner is the single point of failure.
- F8: 20 long tasks, flat vs hierarchical, completion rate and cost per completion. Rubric: the math plus the checker's role. Red flag: "more steps". Remediation: U08-C04.
