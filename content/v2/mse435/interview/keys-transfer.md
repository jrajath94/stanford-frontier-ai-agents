# Transfer keys , mse435

Full keys for `transfer-sets.md`. Each set: sufficient
answer, strong extension, red flags, rubric, remediation.

## Set 1

1. Contract PV = 120 x 3.00 x a-angle-3 at 10 percent =
   360 x 2.4869 = 895.27. Market PV at 2.00 = 240 x
   2.4869 = 596.85. Regret = 298.42 (in block-dollars, scale to real units).
2. Q* = 30,000 / (2.00 - 1.50) = 60,000 = 60B tokens per
   month. The hosted fleet, sized for 12B, is stranded:
   at 15B the API costs 30,000 versus hosting 52,500.
   Verdict: shut the fleet or sublease.
3. Rule: in a falling-price market, never sign
   take-or-pay beyond the visible horizon. Buy optionality
   (short terms, volume flexibility), not price locks.
Red flags: "3.00 was a good price".
Rubric: 2 for the regret math, 2 for the rework, 1 for
the rule.
Remediation: U03-C08, U04-C05.

## Set 2

1. 800 x 50 x 0.85 x 86,400 = 2.9376T tokens per day =
   2,937,600 blocks, down from 3,672,000.
2. Supply falls 20 percent: Qs = 0.8 x (20 + 3P) = 16 +
   2.4P. 100 - 2P = 16 + 2.4P gives P* = 84/4.4 = 19.09,
   Q* = 61.82. Price rises from 16 to 19.09.
3. Spot power: the shortfall is 200 GPUs x 0.7 kW x 720 h
   x 3 x 0.10 = 30,240 per month (hypothetical rate).
   Shed load: forgone margin on 734,400 lost blocks per
   day x margin per block. Decide by comparing the two.
   the general rule is to shed the lowest-margin load
   first.
Red flags: assuming the fleet still serves 3.67T.
Rubric: 2 for the recompute, 2 for the shock, 2 for the
decision.
Remediation: U02-C05, U03-C04.

## Set 3

1. Value = 1,000 x (0.58 - 0.45) x 20 = 2,600 per month,
   down from 7,400.
2. 0.58 < 0.75: fail. No rollout, no expansion.
3. Cheapest fix: refresh the index from the live
   sources (the C02 refresh pipeline). Monitoring: track
   a1 on a fixed question sample monthly. Alert on a
   5-point drop.
Red flags: "the model got worse".
Rubric: 2 for the rework, 1 for the judgment, 2 for the
fix.
Remediation: U04-C01, U06-C04.

## Set 4

1. Per task = 2.00 + 1.0 x 150 = 152. Yearly = 50,000 x
   152 = 7,600,000.
2. The 500k upgrade bought e reduction that regulation
   voids: stranded 500k, write it off.
3. Governance: every model change now needs compliance
   sign-off. The rollout plan adds a regulatory gate
   before each stage, and the business case is rebuilt
   around 152 per task.
Red flags: "the AI still saves money".
Rubric: 2 for the rework, 1 for the write-off, 2 for
the governance change.
Remediation: U05-C11, U06-C08.

## Set 5

1. 0.7 x 9.5 + 0.15 x 5 + 0.15 x (-40) = 6.65 + 0.75 -
   6.0 = 1.40 per user per month.
2. Effective = 0.05 x 0.25 + 0.95 x 4.00 = 3.8125.
   Saving = 15,000 x 0.1875 = 2,812.50 against 3k
   infra: net -187.50. Kill the cache.
3. Move to usage-based pricing: 10 base + tokens at cost
   plus margin. At 50 usage the power user pays ~60 and
   the margin turns positive.
Red flags: keeping flat pricing "for simplicity".
Rubric: 2 for the blend, 2 for the cache math, 1 for
the recommendation.
Remediation: U05-C03, U04-C06.

## Set 6

1. Under the original rule (Y = 0.15, D = 4 weeks):
   interval [18, 26], lower bound 18 > 15: invest, BUT
   the 6-week duration voids the rule. Verdict: no
   valid decision. Rerun a clean 4-week pilot.
2. Breaks: (a) D moved from 4 to 6 weeks, (b) Y moved
   from 0.15 to 0.10 after seeing data.
3. Memo: "The pilot violated its pre-registered duration
   and threshold. No investment decision can be drawn.
   We rerun a 4-week pilot against the original rule."
Red flags: "22 percent beats 15 percent, invest".
Rubric: 2 for the judgment, 2 for the breaks, 1 for
the memo.
Remediation: U06-C12.

## Set 7

1. Before: 320/150 = 2.13 releases per month. After:
   80/150 = 0.53.
2. Labor = 10,000 x 0.25 x 10/60 x 40 = 16,666.67.
   Total = 5,000 + 16,666.67 + 8,000 = 29,666.67, or
   2.97 per task (was 1.97).
3. Hiring two experts (180k loaded) restores 320 hours:
   payback = 180,000 / (12 x 10,000) ... monthly saving
   = 29,666.67 - 19,666.67 = 10,000. Payback = 18
   months. Triage that cuts h to 80 doubles throughput
   per expert hour but does not replace the lost heads.
   Decide: hire one, invest in triage with the rest.
Red flags: "the AI can review itself".
Rubric: 2 for throughput, 2 for the rework, 2 for the
decision.
Remediation: U05-C09, U04-C08.

## Set 8

1. Q* = 30,000 / (8.00 - 1.50) = 4,615 = 4.6B tokens per
   month. At 15B: API = 120,000, hosting = 52,500.
   Hosting wins by 67,500 per month. Verdict: build the
   fleet (fast).
2. Saving = (8.00 - 5.00) x 15,000 = 45,000 per month.
   Payback = 250,000 / 45,000 = 5.6 months. Switch now,
   host in parallel.
3. A price-cap or most-favored-customer clause, or a
   90-day termination for convenience: the term that
   caps unilateral hikes.
Red flags: "we are locked in, pay it".
Rubric: 2 for the rework, 2 for the payback, 1 for the
term.
Remediation: U04-C05, U04-C11.

## Set 9

1. 200 assays at 5k = 1M spend. AI hits = 200 x 0.30
   = 60. Human hits = 200 x 0.50 = 100. The same 60 hits
   at human efficiency cost 600k. Excess spend
   attributable to the gap = 400,000 dollars.
2. 400 assays: cost 2M. Hits = 400 x 0.30 = 120 versus
   200 x 0.50 = 100 before. More hits (120 > 100) at
   double the cost: cost per hit rises from 10k to
   16.7k. The scale-up is value-destructive.
3. The falsifiable test: a 200-candidate controlled
   comparison of AI versus human survival BEFORE
   scaling assays (U05-C06 section 12).
Red flags: "more candidates is better".
Rubric: 2 for the waste math, 2 for the rework, 1 for
the test.
Remediation: U05-C06, U05-C08.

## Set 10

1. Year 1 hosted: 400k build + 450k run = 850k > 300k
   build cap and > 200k run cap. Violates both.
2. Lean fit: B = 120k, yearly = 170k, K = 50k. Year 1 =
   120k + 170k = 290k (build 120k < 300k, run 170k <
   200k). 3-year TCO = 680k.
3. "The hosted design breaks both caps in year 1, so we
   killed it. The lean design fits the caps with 680k
   3-year TCO against 768k savings PV. We pilot it for 4
   weeks against pre-registered gates."
Red flags: asking for a cap exception before trying the
lean design.
Rubric: 2 for the violation, 2 for the sizing, 1 for
the defense.
Remediation: U06-C07, U06-C12.
