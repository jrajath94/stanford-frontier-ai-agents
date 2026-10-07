# Answer key , U04 , Enterprise knowledge and inference cloud

Answers for the assessments in
`lessons/u04_enterprise_knowledge_inference_cloud.md`, item 13
per concept. Keep separate from the lesson.

## C01 , internal knowledge access

Breadth:

1. The documents exist, are current, and are reachable with
   permission checks.
2. Vendor demos use generic questions. The firm's value
   depends on its own questions, so a1 must be measured
   there.

Ladder:

1. Internal knowledge access connects the model to the
   firm's documents before it answers, so firm-specific
   questions get firm-specific facts.
2. 500 x (0.75 - 0.40) x 30 = 5,250 dollars per month.
3. Each question is independent, so total value is the
   per-question gain times count.
4. access_value(1000, 0.45, 0.45, 20) = 0.0. The zero-delta
   check guards the formula.
5. Access wins where answers depend on internal facts. The
   bigger model wins where they depend on general reasoning
   and internal facts add little.

Transfer: value = 500 x (0.63 - 0.40) x 30 on covered half
only, roughly half the full-corpus value. Cheapest fix:
interview the experts and write the tribal knowledge into
the corpus before buying more model.

## C02 , integration costs

Breadth:

1. Per-source build, yearly maintenance per source, and the
   one-time permission filter.
2. Build dominates year one. Maintenance dominates by year
   four.

Ladder:

1. Integration cost is the one-time plus recurring spend to
   connect internal sources to the AI system with correct
   permissions.
2. 2 x 40k + 30k + 2 x 2 x 5k = 130k dollars.
3. Build is paid once, maintenance every year, so the
   recurring term eventually passes the one-time term.
4. integration_cost(0, 40_000, 5_000, 30_000) = 30_000. The
   n = 0 check guards the filter term.
5. Custom connectors win with many stable sources. Curation
   wins when few high-value documents matter.

Transfer: filter 60k raises the two-year total to 210k.
Payback = 210k / 7.4k = 28.4 months. Rule: proceed only if
the value stream covers the full stack, not just tokens.

## C03 , experience/data feedback

Breadth:

1. Usage generates corrections, corrections improve the
   system, improvement grows usage.
2. Later corrections overlap earlier ones, so marginal gain
   decays.

Ladder:

1. A data flywheel turns usage into logged corrections that
   improve quality, which brings more usage.
2. Gains: 1.0, 0.9, 0.81. Cumulative = 2.71 recall points.
3. The decay factor models overlap between corrections.
4. flywheel(100_000, 0.02, 0.001, 6, decay=1.0) sums to
   12.0. The decay = 1.0 check guards the linear case.
5. The flywheel wins with high usage and cheap errors.
   Expert review wins where errors are expensive.

Transfer: effective gain per correction falls 30 percent,
so multiply g by 0.7. Guard: sample corrections for
correctness before they enter the index.

## C04 , custom versus generic models

Breadth:

1. Q* = F / (p_g - p_c), in 1M-token units.
2. Vendor benchmarks flatter the custom model. The firm's
   value depends on its own task mix.

Ladder:

1. Custom trades a fixed monthly floor and cheaper tokens
   for better domain quality against a generic API priced
   purely per token.
2. 30,000 / 2.50 = 12,000 units = 12B tokens per month.
3. Quality value = 13 x 2,000 = 26k per month. Custom =
   30k + 7.5k - 26k = 11.5k vs generic 20k. Custom wins at
   5B once quality has a price.
4. custom_wins(0) returns (30000, 0, False). The Q = 0
   check guards the floor term.
5. Full custom wins at high volume with valuable quality.
   Generic plus retrieval wins at low volume or a small
   gap.

Transfer: F = 60k moves Q* to 24B tokens per month. The
contract term that prevents the surprise: a price lock or
cap on F for the full term.

## C05 , API versus hosting

Breadth:

1. Q* = F / (p_a - p_h), in 1M-token units. F is the fixed
   hosting cost, p_a the API price, p_h the hosted variable
   cost.
2. Forecasts are wrong. The low end is the conservative
   case that protects against a stranded fleet.

Ladder:

1. API is pay per token with no fixed cost. Hosting is a
   fixed fleet plus cheaper variable tokens.
2. 30,000 / 2.50 = 12,000 = 12B tokens per month.
3. At 8B the API wins by 9k per month. Advise the API: the
   range straddles the break-even and the downside is a
   stranded fleet.
4. compare(0) = (0, 30000, "api"). The Q = 0 check guards
   the floor.
5. Committed-use discounts win where volume is moderate and
   commitment is safe. Hosting wins where volume is high
   and steady.

Transfer: idle half the time doubles effective p_h to
3.00. Q* = 30,000 / 1.00 = 30B tokens per month. Hosting
loses at any realistic volume.

## C06 , batching/caching

Breadth:

1. Effective = h x c_c + (1 - h) x c_m, dollars per 1M.
2. Requests wait for the batch to fill, so latency rises.

Ladder:

1. Batching shares one model pass across requests. Caching
   answers repeats from memory.
2. 0.6 x 0.25 + 0.4 x 4.00 = 1.75 dollars per 1M.
3. Each query is a hit with probability h or a miss with
   probability 1 - h, so the expected cost is the weighted
   average.
4. effective_cost(0.0) = 4.0. The h = 0 check guards the
   miss term.
5. Caching wins where queries repeat. The smaller model
   wins where queries are novel but easy.

Transfer: saving = 15,000 x (4.00 - 3.8125) = 2,812.50 per
month against 3k infra. Net -187.50. Advise: skip the
cache.

## C07 , latency/quality

Breadth:

1. Latency cost = V x s x L / 100. V is value at stake, s
   is share lost per 100 ms, L is latency in ms.
2. Sensitivity is behavioral and product-specific. An
   assumed s makes the whole tradeoff fiction.

Ladder:

1. Faster serving costs more compute. Slower serving loses
   users. The optimum balances the two in dollars.
2. Latency cost = 1M x 0.01 x 8 = 80k. Net = 30k - 80k =
   -50k per month.
3. The internal tool has s = 0.001, so latency is cheap
   and compute saving dominates.
4. latency_tradeoff(V, s, 400, 400, X) = (0, X). The
   L1 = L0 check guards the delta.
5. Batching wins where s is low. Speculative decoding wins
   where s is high and latency must fall without batching.

Transfer: past 2 s the linear model breaks. Recompute with
s = 0.10 past the cliff: the batch-8 case loses far more.
Rule: cap batch size so p99 stays under the cliff.

## C08 , operational labor

Breadth:

1. Labor per task = e x t / 60 x w, dollars.
2. Labor is often 2-3x the token cost, so token-only math
   overstates margin badly.

Ladder:

1. Operational labor is the human review, prompt
   maintenance, and on-call work that remains after
   automation.
2. 0.10 x 10 / 60 x 40 = 0.67 dollars per task.
3. It scales with task count and escalation rate, not with
   every token, so it is semi-fixed.
4. unit_cost(10_000, 0.50, 0, 10, 40, 8_000) has zero labor
   term. The e = 0 check guards the formula.
5. Reviewers win where errors are expensive and e is
   irreducible. Prompt investment wins where e is high and
   fixable.

Transfer: slip cost = 10,000 x 0.02 x 200 = 40,000 per
month. True unit cost = (5,000 + 6,667 + 8,000 + 40,000)
/ 10,000 = 5.97 dollars per task. The rubber-stamping
destroys the case.

## C09 , cost per successful task

Breadth:

1. The business buys successes, not attempts. Retries and
   failures make attempts cheap and successes expensive.
2. c x (1 + (1 - s)) / (1 - (1 - s)^2) dollars per success.

Ladder:

1. Cost per successful task is total spend divided by
   successful tasks, counting retries.
2. 0.50 x 1.4 / 0.84 = 0.83 dollars.
3. The cheap model's low attempt cost survives the retry
   penalty until s falls near 0.25.
4. cost_per_success(0.50, 1.0) = 0.50. The s = 1 check
   guards the formula.
5. Retrying wins where s is moderate. The premium model
   wins where s is low and failures cost.

Transfer: retry success 0.2 changes expected successes:
first-try 0.6 plus retry 0.4 x 0.2 = 0.68. Cost = 0.70 /
0.68 = 1.03 dollars per success. Still below premium 2.11,
but the gap narrows.

## C10 , fixed cost floor

Breadth:

1. Average = F / Q + v, dollars per 1M.
2. The pilot runs at low volume, so the floor dominates the
   average and the number does not transfer to rollout.

Ladder:

1. The fixed cost floor is the spend that remains at zero
   usage: reservations, licenses, minimum staff.
2. 30,000 / 500 + 1.50 = 61.50 dollars per 1M.
3. Dividing F by a small Q gives a huge term that shrinks
   as Q grows.
4. avg_cost(10**12) is approximately v. The large-Q check
   guards the limit.
5. Floored hosting wins at high certain volume. Serverless
   wins at low or uncertain volume.

Transfer: Q = 2,000 gives 15 + 1.50 = 16.50 per 1M, 4x
the API price. Diagnosis: forecast error, not a serving
failure. Re-decide at realized volume.

## C11 , vendor lock-in

Breadth:

1. Re-integration labor, re-validation, data egress, and
   retraining.
2. After lock-in the vendor prices against your switching
   cost. Before it, competition disciplines the price.

Ladder:

1. Vendor lock-in is the cost of leaving once systems
   depend on a vendor, which sets the vendor's pricing
   power.
2. 250,000 / 5,000 = 50 months.
3. The vendor can raise prices up to roughly the switching
   cost before you move.
4. switch_payback(S, 0) raises ZeroDivisionError. The
   d = 0 guard names the never-switch case.
5. Accept lock-in where the vendor edge is large and
   durable. Build portability where the market is
   competitive.

Transfer: quality penalty = 5 x 100k = 500k per year =
41.7k per month, which exceeds the 12k saving. Do not
switch. The price saving is negative after quality.

## C12 , workload break-even

Breadth:

1. Break-even tasks = F / (w x s - v), tasks per month.
2. It is usually "soft" saved time that is never
   redeployed, so the break-even can be fiction.

Ladder:

1. Workload break-even is the task volume where total
   value covers fixed plus variable cost.
2. 38,000 / (5 x 0.8 - 1.17) = 13,427.6 tasks per month.
3. The assert is the honest "never" answer: negative
   contribution means no volume pays.
4. workload_breakeven with w x s <= v raises AssertionError.
   The never-case check guards the economics.
5. Break-even decides go/no-go on volume. NPV decides the
   investment size over time.

Transfer: w = 2 hard gives contribution 2 x 0.8 - 1.17 =
0.43. Break-even = 88,372 tasks against 18k actual.
Verdict: do not proceed. The case needs real redeployment
or a lower F.
