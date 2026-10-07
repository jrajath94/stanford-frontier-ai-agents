# U07 lab: safety, coding, and proactive agents

Environment: Python 3. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: privacy audit

Implement the C01 touch log on 20 toy tasks: 60 data touches, 2 of them secret without declared need. Report the violation rate. Apply the minimization filter (block secret touches without declared need) and report the new secret-touch count.

## Task 2: injection defense

Implement the C02 tagger on 100 tool outputs, 5 poisoned (2 direct commands, 3 paraphrased). Report naive-agent obedience (no tags) vs tagging-agent obedience. Verify 0 false positives on the 95 clean outputs.

## Task 3: red-team loop

Implement the C03 attack runner on 50 toy attacks: 12 succeed before the tagging fix, 3 after. Report ASR, SE per round, and the gap in SE units.

## Task 4: permission boundary

Implement the C04 capability checker with K = {read, write_tmp} on 20 toy tasks (14 read-only, 4 write_tmp, 2 send). Report the denial rate, the violation count, and the denial log contents.

## Task 5: approval tiers

Implement the C05 classifier on 100 toy actions: 60 auto, 30 approve (30 s each), 10 block/escalate (5 min each). Report human minutes per day. Recompute with the approve tier tightened to 10 items.

## Task 6: coding test rig and checkpoints

(a) Test rig loop: 20 toy tasks, passes per iteration 8, 12, 14. Report the gains. (b) SWE-bench toy scorer: 8 full fixes, 4 partial (FAIL_TO_PASS green but PASS_TO_PASS broken), 8 untouched. Report the score. (c) Checkpoint: 50 steps, crash at 47, checkpoint every 10 steps at 2 s each, step cost 60 s. Report lost steps with and without checkpoints and the seconds saved.

## Task 7: proactive stack

(a) User model: 5 preferences, 4 correct on the probe. Report accuracy. (b) Next-action: 100 predictions above the 0.7 gate, 62 correct. Correct saves 5 min, wrong costs 2 min. Report precision and net minutes. (c) Mixed initiative: 10 bookings. Report user minutes for the mixed policy (2 min each). (d) Consent gradient: 100 actions (60 implicit, 30 explicit-once at 10 s, 10 explicit-each-time at 30 s). Report friction vs flat ask-everything and the saving.
