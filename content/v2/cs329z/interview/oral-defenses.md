# Oral defenses: cs329z (all 8 units)

Ten deep ladders, eight follow-ups each. Timed: ten minutes per ladder, closed book. The learner speaks. The examiner follows up. Keys in `keys-oral.md`, kept separate.

## D1: defend the system (U01)

"Your compound system scores 0.78 and the single model scores 0.74 at one quarter the cost. Defend shipping the system."

- F1: Define gain per extra cost and compute it for these numbers.
- F2: Toy: the eval has 200 items. Is the 0.04 gap real? Show the arithmetic.
- F3: Derive: why does cost-per-success beat raw accuracy for this decision?
- F4: Implement: write the comparison rig you would run. What does it cost?
- F5: Compare: when does the single model win this argument?
- F6: Debug: the system wins on the eval but users complain. Name two causes.
- F7: Critique: what assumption about the eval could make the whole defense collapse?
- F8: Design: the cheapest experiment that would change your mind.

## D2: defend the ranking (U02)

"Your hybrid search ranks A first. Dense-only ranks B first. A user complains B was right. Defend the fusion."

- F1: Define the fusion score and the role of normalization.
- F2: Toy: one exact-term query. Show how the lexical witness rescues it.
- F3: Derive: why does raw-score fusion collapse without normalization?
- F4: Implement: write the adjudication procedure for the complaint.
- F5: Compare: when would you set the fusion weight w = 0?
- F6: Debug: the complaint is valid. What does that imply about the eval?
- F7: Critique: one complaint is anecdote. When does anecdote become evidence?
- F8: Design: the labeling task that settles the weight question.

## D3: defend the retry (U03)

"Finance reports double charges after you enabled retries. Defend the retry policy."

- F1: Define idempotency and the key's role.
- F2: Toy: timeout rate 0.1, r = 3. Compute the all-fail rate and the expected doubles with and without keys.
- F3: Derive: why does the retry window interact with the key TTL?
- F4: Implement: write the diagnosis order (keys, TTL, store).
- F5: Compare: retries vs no retries on the finance report.
- F6: Debug: how do you prove zero doubles?
- F7: Critique: what breaks if the key store is in-memory?
- F8: Design: the chaos experiment that certifies the fix.

## D4: defend the team (U04)

"Your three-agent system loses to a single agent on the eval. Defend keeping the team."

- F1: Define gain per extra cost for the multi-agent comparison.
- F2: Toy: single 0.74 at 1x, multi 0.81 at 5x. Compute the verdict at bar 0.03.
- F3: Derive: why do errors compound multiplicatively across handoffs?
- F4: Implement: write the handoff envelope. What does each key prevent?
- F5: Compare: on which task families would you expect multi to win?
- F6: Debug: what is the first thing you would cut from the team?
- F7: Critique: the eval may lack clean handoffs. How would you test that claim?
- F8: Design: the 5-family measurement that would change your verdict.

## D5: defend the preference (U05)

"Your DPO-trained model is more verbose but judges rate it higher. Your users complain it rambles. Defend the training."

- F1: Define the preference pair and write the DPO loss.
- F2: Toy: beta = 0.1, m = 0.4 vs m = -0.6. Compute both losses.
- F3: Derive: what does beta control, and what happens at beta = 0?
- F4: Implement: write the check that distinguishes verbosity learning from quality learning.
- F5: Compare: DPO vs SFT-on-winners on what each learns from the pairs.
- F6: Debug: the pairs reward length. How do you prove it?
- F7: Critique: the judges and the users disagree. Which do you trust?
- F8: Design: the experiment that decides whether to keep the DPO model.

## D6: defend the number (U05/U06)

"Your team reports 0.91 from an LLM judge. The launch depends on it. Defend the number."

- F1: Define the calibration gap.
- F2: Toy: validator mean 0.65, human mean 0.50. Compute the gap and explain the risk.
- F3: Derive: why does the optimizer amplify validator errors?
- F4: Implement: write the audit (calibration, bias swap, seed spread, alignment receipt).
- F5: Compare: the calibrated number vs the 0.91 on launch risk.
- F6: Debug: name three ways the 0.91 could be a lie and the fastest check for each.
- F7: Critique: the alignment correlation is 0.31. What does that license?
- F8: Design: the cheapest audit that would change the launch decision.

## D7: defend the metric (U06)

"You report pass@10 = 0.97 for a single-shot product. Defend the metric choice."

- F1: Define pass@k and pass^k and the question each answers.
- F2: Toy: p = 0.3, k = 10. Compute both numbers.
- F3: Derive: P(at least one) = 1 - P(none). Show the steps.
- F4: Implement: write the table that would prevent this choice.
- F5: Compare: which metric for a code agent with 8 tries and a verifier?
- F6: Debug: measured pass@5 is 0.40, formula says 0.83. What broke?
- F7: Critique: the independence assumption. When does it fail silently?
- F8: Design: the measurement that gives the honest single-shot number.

## D8: defend the wall (U07)

"A poisoned tool output made your agent send a password. Defend the defenses you had."

- F1: Define the instruction hierarchy and the source tag.
- F2: Toy: 100 tool outputs, 5 poisoned. Your tagger blocked 4. Compute the miss rate and the consequence.
- F3: Derive: why does source-based tagging beat content filtering against paraphrase?
- F4: Implement: write the gate that should have caught the 5th.
- F5: Compare: tagging vs sandboxing on what each limits.
- F6: Debug: the 5th attack was pasted by the user. Which defense covers that?
- F7: Critique: your red-team ASR was 0.00. What do you suspect?
- F8: Design: the incident response: what you log, what you fix, what you tell the user.

## D9: defend the launch (U07/U08)

"Your refund agent's cost gate fails: $0.53 vs the $0.50 bar. The business wants to ship. Defend not shipping."

- F1: Define the acceptance gate and compute the cost decomposition.
- F2: Toy: 80.8 percent auto at $0.08, 19.2 percent escalated at $2.40. Show the $0.53.
- F3: Derive: why does the escalation rate dominate the cost?
- F4: Implement: write the three remediation options with their measurements.
- F5: Compare: shipping on a failed gate vs the shadow-mode alternative.
- F6: Debug: which measurement would most change the cost number?
- F7: Critique: the precision gate passes at 0.9988. Why is that not enough?
- F8: Design: the rollout plan with the gate checks at each step.

## D10: defend the horizon (U08)

"Your flat agent dies at step 60 of a 500-step task. Defend the hierarchical redesign."

- F1: Define planner, worker, checker, milestone.
- F2: Toy: per-step 0.99. Compute flat success over 500 steps.
- F3: Derive: why do checkers reset the error compounding?
- F4: Implement: write the milestone check predicate for one milestone.
- F5: Compare: hierarchy vs a longer context on what each buys.
- F6: Debug: milestone 6 keeps failing its check. Name the two suspects.
- F7: Critique: the planner's milestones are wrong. What fails first?
- F8: Design: the 20-task experiment comparing flat vs hierarchical.
