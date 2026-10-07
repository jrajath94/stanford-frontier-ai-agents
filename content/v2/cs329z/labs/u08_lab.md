# U08 lab: frontiers, production, and project artifacts

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: computer-use loop

Name the 4 base UI ops. Implement the C01 observe-ground-act-verify loop on 20 toy web tasks with per-step grounding accuracy 0.75 and 4 steps per task. Report the open-loop prediction 0.75^4, the observed success (12/20), and the grounding share of the 8 failures.

## Task 2: modality ablation

Implement the C02 paired ablation on 40 toy chart tasks: vision+table 32/40, table-only 26/40, vision-only (report the toy value). Report the premium, its SE, and the z-score.

## Task 3: cost dashboard and probes

(a) Implement the C05 span logger on 100 toy task costs (seed 0). Report mean and p99. Model the retry-step spike ($0.05 to $0.15) and report the alert rule. (b) Implement the C08 counterfactual probe: 40 docs, decision cites 3. Report the extra runs needed and the flip results. (c) Price the C03 hypothesis loop: 10 hypotheses at $50, 3 verify. Report cost per finding.

## Task 4: long-horizon and recovery

(a) Compute the C04 flat-vs-hierarchical math: per-step 0.99 over 500 steps vs 10 milestones with checks. Report both. (b) Implement the C06 recovery dispatcher on 20 toy failures (12 transient, 4 state corruption, 3 judgment, 1 partial effects). Report the level counts, total cost units (1/5/50/20), and the escalation share.

## Task 5: scalability

Implement the C07 message counter for n = 1000: all-to-all vs hub. Report both counts, the ratio, and the per-round seconds at 1 ms per message.

## Task 6: runbook and proposals

(a) Write the C10 runbook for the cost-spike incident (5 steps). Run the drill: report diagnose time with the runbook (25 min) vs without (4 h) and the hours saved. (b) Score two C09 proposals with the 5-criterion rubric: A = (2,2,1,1,1), B = (1,0,1,1,1). Report both totals and the verdicts.

## Task 7: capstone scoping and gap log

(a) Run the C11 scoping checklist on the retry-ladder capstone: 100 failures, 2 arms, 5 min per run. Report the run-hours budget and the week fit. (b) Maintain the C12 gap log: list the open rows for S10 and S16 with evidence and next steps.
