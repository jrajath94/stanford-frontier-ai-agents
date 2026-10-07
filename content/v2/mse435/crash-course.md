# mse435 crash course , AI economics and infrastructure

All six units, every concept, condensed to the one-line
definition, the key formula, and the toy number that
proves it. Numbers are TOY unless marked observed.
Details live in `lessons/u0N_*.md`.

## U01 , AI economics and the full value chain

- C01 supply/demand. Price clears where quantity supplied
  equals quantity demanded. Toy: Qd = 100 - 2P, Qs = 20 +
  3P gives P* = 16, Q* = 68.
- C02 complements/substitutes. Cheaper complements raise
  demand. Cheaper substitutes steal it. Model: Qd shifts
  with the substitute price.
- C03 fixed/variable costs. Fixed costs are paid once.
  Variable costs scale with output. Average cost =
  F/Q + v.
- C04 capex/opex. Capex buys the asset, opex rents the
  flow. Depreciation turns capex into a yearly cost.
- C05 value capture. Value created is not value kept.
  Capture goes to the scarcest layer: margin =
  price minus cost at the bottleneck.
- C06 layers from chips to applications. Chips,
  infrastructure, models, applications. Each layer taxes
  the next.
- C07 consumer versus enterprise. Consumers buy delight,
  enterprises buy ROI. Enterprise sales cycles are long
  but contracts are sticky.
- C08 productivity versus adoption. Productivity gains
  need adoption first. Output = productivity x adoption.
- C09 forecasts versus observations. Forecasts are
  guesses with error bars. Trust observations, derate
  forecasts.
- C10 two-year comparison. Compare the same metric at
  t and t + 2 years. Growth compounds, costs decay.
- C11 uncertainty. Every input has a range. The case
  must hold at the bad end of the range, not the
  middle.
- C12 source claims. Speaker forecasts carry the label
  [SPEAKER CLAIM, EVIDENCE PENDING]. Never build a
  business case on an unlabeled claim.

## U02 , silicon, power, and data centers

- C01 GPU economy. GPUs are the scarcest input. Rent =
  purchase price divided by lifetime tokens plus margin.
- C02 custom accelerators. Custom silicon beats general
  GPUs only at sustained high utilization: the crossover
  is utilization x volume.
- C03 memory/interconnect bottlenecks. FLOPs are cheap,
  moving data is expensive. Roofline: throughput =
  min(compute, bandwidth x intensity).
- C04 infrastructure lifecycle. Hardware lives 3-5
  years. TCO = buy + power + cooling + refresh.
- C05 power constraints. Power, not silicon, caps the
  data center. Tokens per day = GPUs x tok/s x U x
  86,400.
- C06 cooling. Every watt of compute needs ~0.3 watts
  of cooling. PUE = total power / IT power.
- C07 gigawatt scale. A gigawatt campus serves ~20M
  concurrent users at 50 W each. Power is the new
  moat.
- C08 build/lease tradeoffs. Build for steady base
  load, lease for peaks. The crossover is utilization
  x duration.
- C09 utilization. An idle GPU earns nothing. Effective
  cost = sticker cost / utilization.
- C10 depreciation. Hardware loses ~40 percent of
  value per year. Book value = purchase x 0.6^t.
- C11 supply concentration. One foundry, one GPU
  vendor, few grids. Concentration = pricing power
  upstream.
- C12 scenario analysis. Run base, good, bad. The
  decision must survive the bad case.

## U03 , enterprise infrastructure and token markets

- C01 service-as-software thesis. Software margins with
  service costs. The thesis holds only if delivery cost
  per token keeps falling.
- C02 enterprise integration. Integration cost is
  3-10x the license. Budget the integration, not the
  subscription.
- C03 open/closed stacks. Open stacks trade control
  for cost. Closed stacks trade cost for speed.
- C04 compute supply. Supply = GPUs x utilization x
  time. Shocks shift supply left and price up.
- C05 token demand. Demand = users x tokens per user.
  Demand is elastic: price cuts raise volume.
- C06 capacity bottlenecks. The scarcest input sets
  output. Find the bottleneck before buying anything.
- C07 inference versus training economics. Training is
  capex-like, inference is opex-like. Unit cost =
  C_train/V + c_inf.
- C08 long contracts. A contract is insurance against
  price spikes. Regret = contract PV minus market PV.
- C09 ownership. Owning the stack keeps the margin.
  Renting keeps the optionality. Own the bottleneck.
- C10 data governance. Data has owners, lineage, and
  retention rules. Governance cost is real and rising.
- C11 unit prices. Quote everything per 1M tokens.
  The unit price is the only comparable number.
- C12 sensitivity. Vary each input 20 percent. The
  inputs that move the verdict get measured first.

## U04 , enterprise knowledge and inference cloud

- C01 knowledge access value. Value = q x (a1 - a0) x
  v. Toy: 1,000 x 0.37 x 20 = 7,400 per month.
- C02 integration costs. Connectors cost 40k to build,
  5k per year to maintain, plus a 30k one-time permission
  filter. Toy: three sources (20k, 35k, 80k docs),
  two-year bill = 180k, payback in month 25.
- C03 experience/data feedback. Usage corrects the index,
  corrections raise quality, quality raises usage. Toy
  6-month decayed gain = 9.371 (naive 12.0).
- C04 quality value. Each quality point is worth
  w dollars. Value = w x points x volume.
- C05 hosting/API break-even. Q* = F / (p_a - p_h).
  Toy: 30,000 / 2.50 = 12,000 = 12B tokens per month.
- C06 cache economics. Effective = h x c_c + (1 - h) x
  c_m. Toy: 0.6 x 0.25 + 0.4 x 4.00 = 1.75 per 1M.
  Replication (capstone 1) measured H1 FAIL at small
  caches: analytic models overstate h by ~12 percent.
- C07 latency/quality tradeoff. Net = V x s x dL -
  saving. Toy: 2M x 0.01 x 0.8 - 30k = 130k loss, do
  not batch.
- C08 review labor. Labor = tasks x e x minutes/60 x
  wage. Toy: 10k x 0.10 x 10/60 x 40 = 6,666.67 per
  month.
- C09 cost per success. (r+1) x c / success. Toy: 2 x
  0.50 / 0.84 = 1.19 with one retry at s = 0.6.
- C10 enterprise pricing. Price the seat for access,
  the token for usage. Blended margin must stay
  positive.
- C11 switching costs. Migration cost amortized over
  the contract. Payback = switching / monthly saving.
- C12 inference ROI. Net = savings PV - TCO. Toy:
  767.9k - 680k = 87.9k, pilot the lean design.

## U05 , coding/application and life-science economics

- C01 verify gap. Verification is cheaper than
  generation. The gap is the business: v - c > 0.
- C02 software 2.0 economics. Code is written by
  models, reviewed by humans. Cost = generation +
  review.
- C03 distribution cost. Serving cost per user falls
  with scale. Margin = price - c_serve(user).
- C04 build/buy/license. License wins when the vendor
  amortizes build over many buyers. Compare 3-year
  TCOs, not year 1.
- C05 Amdahl for AI. Speedup is capped by the
  non-automatable share: 1 / ((1-p) + p/s).
- C06 discovery funnel. Total = sum n_i x c_i. Toy:
  111.002M from discovery to clinical.
- C07 clinical trials. Trials dominate cost: the
  funnel's tail wags the dog. Price the tail first.
- C08 assay economics. Cost per hit = assays x cost /
  (assays x survival). Halving survival doubles cost
  per hit.
- C09 expert review. Experts are the bottleneck: 320
  hours per month at 2 experts. Triage multiplies
  expert hours.
- C10 adoption PV. Gate savings by the ramp:
  [0.20, 0.50, 0.80] at r = 10 percent gives 767.9k,
  not 1.93M naive.
- C11 life-science quality bar. Accuracy >= 0.90 and
  full audit trails. The bar is regulatory, not
  technical.
- C12 OOD limits. Out-of-distribution inputs break
  silently. Monitor the input distribution, not just
  the output.

## U06 , capstone evidence and stakeholder defense

- C01 baseline. Measure the current cost before
  proposing anything. No baseline, no business case.
- C02 objectives. One primary metric, guardrails for
  the rest. Pre-register all of them.
- C03 constraints. Budget, latency, compliance: the
  box the design must fit in.
- C04 quality gates. a1 >= 0.75 or the system does not
  ship. Gates are binary.
- C05 trust boundaries. Data crosses boundaries only
  under contract. Mask PII before egress.
- C06 alternatives. Always price the status quo and
  the hire-more-humans option. The AI design must
  beat both.
- C07 TCO reckoning. TCO = B + 3(R + L) + K. Toy:
  1,850k, build share 21.6 percent. Build-only cases
  understate 3-4x.
- C08 acceptance gates. Cost <= 30, accuracy >= 0.90,
  escalation <= 0.10, 90 percent confidence. Kill on
  two consecutive breaches.
- C09 monitoring. Dashboard the five vitals: cost,
  accuracy, escalation, latency, hit rate. Alert on
  drift.
- C10 cost/latency assumptions. 1.75 per 1M cached,
  0.67 review labor, p99 1.8 s. Mark each for pilot
  measurement.
- C11 rollout. Shadow, 1 percent, 10 percent, 100
  percent. 15-minute rollback, game-day tested.
- C12 falsifiable investment. L > Y on the pilot
  interval or reject. Toy: [13, 23] vs Y = 15:
  reject. Never move Y or D after seeing data.

## The ten numbers to memorize

1. Q* = F / (p_a - p_h): 12B tokens per month.
2. Effective cached price: h x c_c + (1 - h) x c_m.
3. Cost per success: (r + 1) x c / (1 - (1 - s)^(r+1)).
4. Adoption-gated PV: ramp each year, then discount.
5. TCO = B + 3(R + L) + K: build is ~22 percent.
6. Break-even volume: 30k / (p_a - p_h).
7. Review labor: tasks x e x min/60 x wage.
8. Flywheel: decay each month's corrections by
   0.9^(remaining).
9. Falsifiable rule: invest iff L > Y, pre-registered.
10. Stakeholder line: measured X, costs Y, saves Z,
    risk W, pilot 4 weeks, kill criteria named.
