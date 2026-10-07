# Lab key , U06

Verified outputs from `u06_lab_run.py`, executed 2026-10-07.

## Task 1

- Baseline: cost 1,900,000 dollars per year, 37,500 hours,
  2,140,000 with errors.
- December uplift (22 days at 1.4x): 66,880 dollars.

## Task 2

- Plan PV: 767,891.81 dollars.
- Stalled PV: 444,721.26 dollars.
- Verdict: replan the driver before spending.

## Task 3

- (28, 0.87, 4.2): True (pass).
- (28, 0.79, 4.2): False (resolution guardrail).
- With the CSAT floor moved to 3.8: still False. The
  breach is resolution, not CSAT: moving the wrong
  goalpost is theater twice over.

## Task 4

- A (0.91, 1.8, 0.08): pass.
- B (0.89, 1.8, 0.08): fail (accuracy).
- C (0.93, 2.3, 0.08): fail (latency).

## Task 5

- Honest: E = 475,000, downside 200,000.
- Advocacy: E = 587,500, downside 200,000.
- The advocacy weights add 112,500 of pure desire.

## Task 6

- Base ranking: adoption 500k, labor cost 250k, volume
  180k, quality 120k.
- After the pilot narrows adoption: labor cost 250k,
  volume 180k, adoption 150k, quality 120k.
- Re-run the tornado after every de-risking step.

## Task 7

- TCO: 1,850,000 dollars. Build share: 0.216.
- R doubling in year 2: 2,450,000 dollars.

## Task 8

- Low-stakes tier: board cost 5,000, risk 2,000 per
  change. Verdict: lighten.
- High-stakes tier: board cost 20,000, risk 250,000 per
  change. Verdict: board.
- Tiered governance: friction proportional to blast
  radius.

## Task 9

- [0.05, 0.09, 0.10]: trigger True, max 0.10.
- [0.05, 0.06, 0.05]: no trigger, max 0.06.
- 4-hour rollback at 1 percent traffic: 21,600 dollars
  of damage. Rollback must be minutes, not hours.

## Task 10

- On-call cost 104,000, value 36,000, net -68,000 per
  year: honest insurance.
- 6 missing checklist items: 1,500 dollars on the first
  incident alone.

## Task 11

- Team scores: build 7.8, vendor 7.4, hire 5.8. Build
  wins by 0.4 (noise).
- Blind scores: build 6.4, vendor 7.4, hire 5.8. Vendor
  wins.
- Verdict: the team scores were advocacy. The blind
  re-score flips the winner.

## Task 12

- (0.18, 0.05): lower bound 0.13, kill.
- (0.22, 0.04): lower bound 0.18, invest.
- Moving Y to 0.10 after seeing the pilot breaks
  pre-registration. The rule is void. The decision was
  already made.
