# Oral defense keys , mse435

Keys for `oral-defenses.md`. Each ladder: sufficient
answer per rung, strong extension, red flags, rubric,
remediation.

## D1

1. Buyers and sellers trade tokens. The price where
   quantity supplied equals quantity demanded clears
   the market.
2. 100 - 2P = 20 + 3P gives P* = 16 dollars per unit,
   Q* = 68 units (68M tokens).
3. Set Qd = Qs, collect terms: 80 = 5P, P* = 16, back-
   substitute for Q*.
4. A bisection or closed-form solver. O(1) per clear.
5. Fast clearing passes the shock to price. Sticky
   supply rations by queue. Sellers with inventory pay
   in the fast market (margin compression). Buyers pay
   in the sticky market (wait or premium).
6. They used Qs = 20 + 3Q (quantity in the supply
   curve) or added instead of subtracting: check the
   algebra line by line.
7. Linear curves. Perfect competition. A single cloud
   provider with market power breaks linearity. A
   take-or-pay contract base breaks competition.
8. Post small test orders at varying prices for two
   weeks and measure fill times. Fast fills at varying
   prices mean fast clearing.
Red flags: confusing P* with Q*.
Rubric: 6 for rungs 1-6 correct, 2 for 7-8.
Remediation: U01-C02, U03-C04.

## D2

1. Training cost amortized over lifetime tokens plus
   inference cost per token.
2. 5,000,000 / 500,000 = 10 plus 4 = 14 per 1M.
3. Set C_train/V = c_inf: V = 5,000,000/4 x 1M = 1.25T
   tokens.
4. unit_cost = C_train/V + c_inf. Limit V -> inf is
   c_inf.
5. The reseller's margin is contract minus market. When
   utilization falls the fleet owner eats the fixed
   cost, the reseller renegotiates down. The fleet owner
   keeps the margin only at high utilization.
6. 504 = 500 + 4: they divided 5M by 10,000 blocks
   instead of 10B tokens. Fix: C_train/V with V counted
   in tokens.
7. One training run per lifetime. Quarterly retraining
   makes training cost recur: the true stack is
   n_runs x C_train/V + c_inf.
8. Meter actual tokens served, actual inference spend,
   actual retraining cadence and cost for one quarter.
Red flags: "training cost is sunk, ignore it".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U02-C02, U03-C05.

## D3

1. A contract trades a fixed price for the right to
   stop worrying about price spikes. The premium over
   the expected market price is the insurance cost.
2. Contract PV = 360 x 2.4869 = 895.27. Market PV =
   (480/1.1 + 360/1.21 + 240/1.331) = 914.20. Contract
   is smaller: sign it.
3. PV = sum_t C_t/(1+r)^t from the definition of
   discounting future cash flows.
4. Loop over years with (1+r)^t. Check: flat price p
   gives p x Q x a-angle-n.
5. Take-or-pay bills the full 120 blocks at 3.00 even
   at half usage (360). Pay-as-you-go bills 60 x market
   (~120-240). Pay-as-you-go wins under demand
   collapse. That is the optionality the contract
   sells away.
6. Discount each year's cash flow separately. The
   single-discount form understates the present value
   of early payments.
7. A fixed price for 3 years was bought. It was a bad
   buy if the expected market PV was lower: regret =
   contract PV minus market PV > 0.
8. A market-price reset clause, or a shorter term with
   renewal option: never lock the price in a falling
   market.
Red flags: "we beat the market price today".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U03-C08, U04-C05.

## D4

1. More usage corrects the index, corrections raise
   answer quality, quality raises usage.
2. Naive: 100,000 x 0.02 = 2,000 x 6 = 12,000
   corrections x 0.001 = 12.0. Decayed: month t gain =
   2.0 x 0.9^(6-t): 1.18098 + 1.3122 + 1.458 + 1.62 +
   1.8 + 2.0 = 9.371.
3. Each month's corrections decay for the remaining
   months. The linear sum applies full weight to stale
   corrections.
4. Cumulative sum of correction_rate x q x gain x
   decay^(D-t). Check decay = 1.0 reproduces the naive
   sum.
5. The flywheel is free but slow and noisy. Expert
   review is fast and clean but costly. The flywheel
   wins at scale, review wins when quality is safety-
   critical.
6. They added instead of decaying, or used decay > 1.
   Check: with decay = 1.0 the code must equal the
   naive sum exactly.
7. Corrections are assumed correct. Malicious or
   mistaken corrections poison the index. The loop
   amplifies bad corrections as happily as good ones.
8. A held-out question sample scored weekly (the a1
   instrument) plus a correction audit queue.
Red flags: "more data always helps".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U04-C02, U06-C04.

## D5

1. Faster answers are worth more. The tradeoff is the
   latency revenue loss against the compute saving.
2. Loss = 2,000,000 x 0.01 x 8 = 160,000 per month.
   Net = 160,000 - 30,000 = 130,000 loss. Do not
   batch.
3. 2,000,000 x 0.01 x (B-1) = 30,000 gives B - 1 =
   1.5, B = 2.5: batch beyond 2 loses money.
4. net = V x s x (L1 - L0) - saving. Check: L1 = L0
   gives net = -saving (the saving is pure gain, no
   latency loss).
5. Batching trades latency for throughput. Speculative
   decoding cuts latency directly. Speculative wins
   when latency is the binding constraint. Batching
   wins when throughput is.
6. p99 and p50 differ. Mixing them double-counts or
   under-counts. Use one percentile consistently.
7. Linear value decay per 100 ms. The abandonment cliff
   (users leave past 2 s) makes the loss superlinear.
   the formula underprices big slowdowns.
8. A/B latency on matched traffic for two weeks.
   regress conversion on latency. Read s off the
   slope.
Red flags: "latency is a tech problem, not a money
problem".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U04-C07.

## D6

1. Candidates enter discovery. Survivors move to the
   next stage. Each stage costs money. The total is the
   sum over stages of survivors x cost.
2. Discovery: 1,000. Assays: 1,000. Clinical entry:
   10M. Clinical: 100M. Total 111.002M.
3. Doubling survivors doubles n at every downstream
   stage. Cost scales with n, so the total rises by
   roughly the clinical cost of the extra survivors.
4. Sum n_i x c_i over stages. Check: doubling the
   stage-2 survivors raises the total by the downstream
   cost of those survivors.
5. AI discovery lowers the cost per candidate. Cheaper
   assays lower the cost per test. Invest in AI when
   discovery dominates. In assays when the funnel is
   wide downstream.
6. Units: n + c mixes counts with dollars. The doubling
   check catches it (total barely moves when survivors
   double).
7. Survival is assumed independent across candidates.
   A correlated failure (one bad scaffold family) kills
   the whole cohort. The expected total then
   understates risk.
8. A 200-candidate controlled AI-vs-human survival
   comparison, pre-registered, before any assay scale-
   up.
Red flags: "AI makes trials cheaper".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U05-C06.

## D7

1. An investment written so that a named measurement
   can kill it: threshold, duration, instrument, rule.
2. [13, 23], lower bound 13 < 15: reject. Insufficient
   evidence.
3. The decision must hold under the worst plausible
   truth. The lower bound is the conservative edge of
   the interval.
4. invest = L > Y. Check: L = Y exactly returns False
   (strict).
5. Gut feel is fast and wrong at the base rate of
   pilots (~half fail). The rule is slower and
   calibrated. The rule wins on error rate, gut wins
   on speed only.
6. Use the lower bound L. The boundary case (L = Y)
   catches the bug: with the upper bound the function
   invests when the interval straddles Y.
7. Moving Y down, or extending D, after seeing the
   data. Both void the pre-registration.
8. Half-width 0.04 at p ~ 0.2 needs n = (1.96/0.04)^2
   x 0.16 = 384 cases. At 100 per week, 4 weeks.
Red flags: "the point estimate cleared".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U06-C12.

## D8

1. The expected cost of getting one task done right,
   counting the retries the failures force.
2. Success = 1 - 0.4^2 = 0.84. Cost = 2 x 0.50 / 0.84
   = 1.19.
3. Failures are (1-s)^(r+1). Success is 1 minus that.
4. Cost = (r+1) x c / success. Check s = 1 gives c.
5. Retry: 1.19. Premium: 2.00/0.95 = 2.11. Retry the
   cheap model.
6. The failure probability compounds
   multiplicatively: (1-s)^(r+1), not (1-s) x (r+1)
   (which can exceed 1). The s = 0.5, r = 1 check
   catches it.
7. Retries are assumed independent draws. Hard
   questions fail every retry: the true success is
   lower and the formula is optimistic exactly where
   it matters.
8. Log per-task: attempts, success, cost. Compare
   predicted versus realized cost per success by
   difficulty bucket.
Red flags: "retries are free".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U04-C09.

## D9

1. Build plus run plus labor plus risk reserve over 3
   years, all in.
2. TCO = 400k + 3 x 450k + 100k = 1,850k. Build share =
   400/1,850 = 21.6 percent.
3. Build is paid once. Run and labor recur 3x. The
   reserve adds a cushion. A 400k build with 450k
   yearly run is 1.75M before the reserve: 4.4x the
   build.
4. tco(B, R, L, K) = B + 3(R+L) + K. Check B = R = L =
   K = 0 gives 0.
5. Hosted: 1,850k TCO versus 768k PV: reject. Lean:
   680k versus 768k: pilot. The build share drops from
   21.6 to 17.6 percent. The verdict flips on design,
   not on optimism.
6. Build is paid once: B + 3(R+L) + K, not 3B.
7. Run cost is assumed steady. A runaway (token price
   spike, review escalation) makes R grow. The 3-year
   TCO then understates badly.
8. A quarterly TCO review against the business case:
   recompute with actuals, flag 10 percent drift, kill
   or redesign at 25 percent.
Red flags: "the build is the budget".
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U06-C07.

## D10

1. We measured X, the design costs Y against Z
   savings, the risk is W, so we pilot for 4 weeks
   against pre-registered gates.
2. Net = 768k - 680k = 88k. Verdict: pilot the lean
   design.
3. PV = 0.20 x 642k/1.1 + 0.50 x 642k/1.21 + 0.80 x
   642k/1.331 = 116,727 + 265,289 + 385,876 =
   767,892.
4. case_value(adoption ramp, savings, TCO) = PV - TCO.
   check: full ramp [1,1,1] reproduces the naive
   642k x a-angle-3 minus TCO.
5. The hosted defense must justify 1.85M against 768k:
   impossible honestly. The lean defense justifies
   680k against 768k: thin but honest. The numbers
   that change the story are the design's build and
   run, not the savings.
6. 61.50 was the cost of 5,000 uncached pilot tasks,
   not the steady-state inference cost. Quoting it as
   the rate overstates cost ~35x and kills any honest
   case.
7. Adoption ramp (needs pilot measurement), success
   rate (needs production logs), review labor rate
   (needs time study). Each gets its instrument before
   the investment decision.
8. Week 1-2 shadow scoring. Week 3-4 1 percent canary, gates: cost <= 30, accuracy >= 0.90, escalation <=
   0.10. Kill on any guardrail breach two weeks
   running. Decision date: end of week 4.
Red flags: defending the design instead of the
numbers.
Rubric: 6 for rungs 1-6, 2 for 7-8.
Remediation: U06-C10, U06-C11, U06-C12.
