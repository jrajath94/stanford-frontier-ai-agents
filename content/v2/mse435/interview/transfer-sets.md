# Transfer sets , mse435 , changed scenarios

Ten sets. Each set changes one scenario constraint from the
lessons and asks what breaks, what to recompute, and what to
decide. Closed-book. Full keys in `keys-transfer.md`.

## Set 1 , token price collapse (U01, U03, U04)

A new entrant halves the token price from 4.00 to 2.00 per
1M overnight. Your firm holds a 3-year take-or-pay contract
at 3.00 for 120 blocks per year, and a hosted fleet sized
for the old price.

1. Price the contract's regret over 3 years at r = 10
   percent against the new market price.
2. Rework the API-versus-hosting break-even (F = 30k,
   p_h = 1.50) at the new price. What happens to the
   hosted fleet?
3. State the general rule for signing long contracts in a
   falling-price market.

## Set 2 , the data center loses power (U02, U04)

Your region's grid caps your data center at 80 percent of
planned power. The fleet was sized for 1,000 GPUs at full
power.

1. Recompute servable tokens per day at 50 tok/s/GPU,
   U = 0.85, with 800 effective GPUs.
2. The token market price jumps on the supply shock.
   Using Qd = 100 - 2P and Qs = 20 + 3P, and a 20 percent
   supply cut, find the new P*.
3. Decide: buy spot power at 3x, or shed load? Price
   both for one month.

## Set 3 , the corpus goes stale (U04, U06)

The document index behind the enterprise assistant is 18
months old. Measured a1 falls from 0.82 to 0.58.

1. Rework the access value (q = 1,000, a0 = 0.45, v = 20).
2. The quality gate needs a1 >= 0.75. Judge the system.
3. Name the cheapest fix and the monitoring that would
   have caught the decay.

## Set 4 , the regulator arrives (U05, U06)

A new rule requires human review of every AI clinical
recommendation (e = 1.0) at 150 dollars each. Compute was
2.00 per task.

1. Compute the new per-task cost and the yearly bill at
   50,000 tasks.
2. The model upgrade that cut e to 0.02 is now worthless.
   Price the stranded investment (500k).
3. State the governance change this forces in the
   rollout plan.

## Set 5 , the viral power user (U05, U04)

A viral template turns 15 percent of users into power
users at 50 dollars of usage each (seat 10 dollars).

1. Compute the blended margin (light 0.70 at 0.50,
   medium 0.15 at 5.00, power 0.15 at 50.00).
2. The cache hit rate for these users is 0.05. Price a
   cache (3k per month infra, 15B tokens) for this mix.
3. Recommend a pricing change with numbers.

## Set 6 , the pilot that proved too much (U06, U04)

The pilot ran 6 weeks instead of 4 and reports 22 percent
+/- 4 against a 15 percent target with Y moved to 10
percent after the fact.

1. Judge the pilot under the original rule.
2. Name the two pre-registration breaks.
3. Write the correct decision memo in three sentences.

## Set 7 , the expert quits (U05, U04)

The two domain experts leave. Review capacity falls from
320 to 80 hours per month. Releases need 150 hours with
triage.

1. Compute max releases per month before and after.
2. Escalation e rises from 0.10 to 0.25 (fewer reviewers,
   more rubber-stamping). Rework unit cost (10,000
   tasks, 0.50 compute, 10 min review at 40/hr, 8k
   fixed ops).
3. State the hiring-versus-triage decision with numbers.

## Set 8 , the vendor doubles the API price (U04, U03)

The API vendor raises p_a from 4.00 to 8.00 with 30 days
notice. Your volume is 15B tokens per month.

1. Recompute the hosting break-even (F = 30k,
   p_h = 1.50) and the verdict.
2. The switching cost to a new vendor is 250k. The new
   vendor charges 5.00. Compute the payback.
3. State what contract term stops this surprise.

## Set 9 , the wet lab fails the AI designs (U05)

AI-designed candidates show 0.30 assay survival versus
0.50 for human designs, at 5k per assay and 200 assays.

1. Price the wasted assay spend attributable to the
   survival gap.
2. Rework the funnel total if AI doubles candidates but
   halves survival (400 assays at 0.30 survival).
3. State the falsifiable test that should have run
   before scaling.

## Set 10 , the board says no to the budget (U06, U04)

The CFO caps the program at 300k build and 200k per year
run. The hosted design needs 400k build and 450k per
year.

1. Show the hosted design violates the cap in year 1.
2. Size the lean design to fit: pick B, yearly, and K
   under the caps and recompute 3-year TCO.
3. Write the stakeholder defense for the lean design in
   three sentences, naming the killed alternative.
