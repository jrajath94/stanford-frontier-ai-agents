# U07 answer keys

Kept separate from `lessons/u07_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: 2/20 = 0.10.
- E2: half the secrets are unlabeled, so the audit cannot see them. The 0 is a measurement failure.
- E3: touch only what the task needs. Log every touch.

## C02

- E1: naive 4/5, defended 0/5.
- E2: the pasted text carries the "user" tag, and the planner obeys user instructions. The tag lies about the true source.
- E3: data is never instructions. Tool and web spans are data.

## C03

- E1: 0.18/sqrt(0.060^2 + 0.034^2) = 0.18/0.069 = 2.6 SE.
- E2: one trick, fifty variants. The ASR measures that trick, not the attacker space.
- E3: attack, measure, fix, re-attack. Static tests guard the known attacks.

## C04

- E1: 2/20 = 0.10.
- E2: the agent writes to a shared file that another process emails. The boundary sees a write, not a send.
- E3: grant the minimum for the task. Enforce at the action layer.

## C05

- E1: 30 x 0.5 + 10 x 5 = 15 + 50 = 65 min/day.
- E2: the human approves in 2 seconds without reading. The tier adds latency and no safety.
- E3: no answer means deny. The queue must not fail open.

## C06

- E1: 12 - 8 = +4, 14 - 12 = +2.
- E2: the suite is weak, so the patch passes without fixing the issue. The test rig certifies broken code.
- E3: the test rig decides. The agent's confidence is not evidence.

## C07

- E1: 8/20 = 0.40.
- E2: the partial fix breaks a PASS_TO_PASS test. The test rig is strict: both sets must be green.
- E3: the score measures bug-fixing with tests. It does not measure design, taste, or vague issues.

## C08

- E1: 40 steps x 60 s = 2400 s saved for 10 s of checkpoint cost.
- E2: the state held an open transaction. Resume replays it and the effect applies twice.
- E3: verify the checkpoint by loading it. An unverified checkpoint is a hope.

## C09

- E1: 4/5 = 0.80.
- E2: "I love meetings" was sarcasm. The model stored a joke as a preference.
- E3: act above the confidence gate, ask below it. Corrections override.

## C10

- E1: 62 x 5 - 38 x 2 = 310 - 76 = +234 min.
- E2: the user changed teams. The table predicts the old routine and every prediction misses.
- E3: predict only above the precision gate. A wrong proactive action costs more than none.

## C11

- E1: 10 bookings x 2 min = 20 min.
- E2: each proposal costs the user 10 minutes of review. The mix costs more than manual.
- E3: route by confidence and stakes. The user can always interrupt.

## C12

- E1: 50 - 10 = 40 min/day saved.
- E2: "may I proceed?" names no risk. Consent to the unknown is void.
- E3: match the friction to the risk. High stakes need explicit consent.
