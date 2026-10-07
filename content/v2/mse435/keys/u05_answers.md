# Answer key , U05 , Coding/application and life-science economics

Answers for the assessments in
`lessons/u05_coding_lifescience_economics.md`, item 13 per
concept. Keep separate from the lesson.

## C01 , vibe coding versus verified software

Breadth:

1. Vibe = L/100 x d_v x f. Verified = r + L/100 x d_f x f.
   Verify when r is below the gap.
2. Vibe wins where the fix cost is near zero: throwaway
   prototypes and demos nobody uses.

Ladder:

1. Vibe coding trades review time for defect risk: fast now,
   expensive tail later.
2. Vibe = 10,000, verified = 4,000 dollars.
3. Tie at r = 10,000 - 1,000 = 9,000 dollars.
4. vibe_vs_verified(1000, 40, 4, 0, 3000) = (0.0, 3000.0).
   The f = 0 check guards the tail term.
5. Tests-only wins where tests catch most defects cheaply.
   Full verification wins where defects are subtle or
   expensive.

Transfer: vibe = 10 x 40 x 100 = 40,000. Verified = 3,000
+ 10 x 4 x 100 = 7,000. Tie at r = 36,000. Expensive
defects make verification nearly always right.

## C02 , Software 2.0

Breadth:

1. The dataset plus the training recipe: data is the
   source code.
2. The dataset is the moat when it is proprietary. It is
   not when anyone can replicate it.

Ladder:

1. Software 2.0 learns weights from data instead of
   hand-writing logic. The dataset is the asset.
2. D = 50,000, total = 250,000 dollars.
3. Compute rents by the hour from any cloud. Proprietary
   labeled data cannot be rented.
4. software2_cost(0, 0.50, 200_000) = (0.0, 200000,
   200000.0). The n = 0 check guards the dataset term.
5. The rules engine wins where logic is simple and stable.
   Software 2.0 wins where data is proprietary and the
   task repeats.

Transfer: D = 100k x 5 = 500k. Total = 700k. The moat
argument strengthens: expert labels are even harder to
replicate.

## C03 , product distribution

Breadth:

1. Every user carries variable inference cost, so heavy
   users can cost more than a flat price covers.
2. Blended = sum over cohorts of share x (p - usage).

Ladder:

1. AI distribution has marginal cost per user, so flat
   pricing subsidizes power users with light users.
2. 0.8 x 9.5 + 0.15 x 5 + 0.05 x (-15) = 7.60 dollars per
   user per month.
3. The blend averages the loss away: 95 percent of users
   hide the 5 percent who lose money.
4. cohort_margin(10, [(1.0, 0.0)]) = 10.0. The zero-usage
   check guards the formula.
5. Flat wins where usage is uniform. Usage-based wins
   where usage is skewed.

Transfer: blended = 7.6 + 0.75 - 2.0 = 6.35. Advise:
move to usage-based pricing before the power cohort
grows.

## C04 , software-service boundary

Breadth:

1. When the product needs the model on every use, it is a
   service no matter what the contract calls it.
2. Service margin = retained months x (p - i), with
   retained months = sum of (1 - churn)^t.

Ladder:

1. A license sells a copy once. A service sells outcomes
   monthly and pays inference monthly.
2. License 500, service 36 x 17 = 612. Service wins.
3. 3 percent churn: 22.2 retained months, margin 377.38.
   The license wins.
4. license_vs_service(500, 20, 20, 36) = (500, 0). The
   i >= p check guards the margin.
5. Hybrid pass-through wins where usage is heavy or
   unpredictable. Pure service wins where usage is light
   and steady.

Transfer: 10 percent churn gives 9.77 months, margin
166.17. The license wins by a wide margin.

## C05 , science workflows

Breadth:

1. AI speeds the design step only. The wet-lab step is
   unchanged and dominates the cycle.
2. Design quality: extra failed cycles erase the speedup.

Ladder:

1. Workflow speedup is limited by the slowest unchanged
   step.
2. T' = 2/7 + 4 = 4.29 weeks. Speedup = 6 / 4.29 = 1.40x.
3. 1.3 x 4.29 / 6 = 0.93: still 7 percent faster, barely.
4. cycle_speedup(2, 4, 1) = (1.0, 1.0). The k = 1 check
   guards the formula.
5. AI design wins where design is the binding step. Lab
   automation wins where the wet lab binds.

Transfer: the metric becomes throughput (cycles per
quarter), not cycle time. Overlapped steps hide design
time inside wet-lab time.

## C06 , discovery versus clinical evidence

Breadth:

1. The funnel's cost lives at the bottom: assays,
   preclinical, clinical. A cheaper top does not move it.
2. Triage quality: fewer, better candidates reaching the
   expensive stages.

Ladder:

1. Discovery is a funnel from many cheap candidates to few
   expensive proofs. AI cheapens the wide top.
2. 1,000 + 1,000,000 + 10,000,000 + 100,000,000 =
   111,001,000 dollars.
3. 400 assays: 2M assay cost, total 112,001,000. The
   "saving" costs an extra million.
4. Doubling the assay count adds exactly 1M. The doubling
   check guards the sum.
5. AI discovery wins for triage quality. Cheaper assays
   win for cost per candidate.

Transfer: 400 correlated assays waste 2M. Guard: diversify
scaffolds before scaling assays, and measure per-scaffold
survival.

## C07 , privacy/IP

Breadth:

1. Buy protection when C < p x L, dollars per year.
2. Leak probability is a guess. A 10x error flips most
   decisions.

Ladder:

1. Proprietary data in shared models is a small chance of
   a large loss. Price it as expected loss.
2. E = 500k > C = 200k. Protect.
3. Flips at p = 200k / 50M = 0.004.
4. protect_or_not(0, 50e6, 200_000) = (0.0, 200000,
   'accept risk'). The p = 0 check guards the rule.
5. The clean room wins for crown-jewel data. On-premise
   wins where p must go near zero regardless of cost.

Transfer: E = 0.005 x 200M = 1M > 300k. Protect. The
unpriced tail is criminal liability, which only
strengthens the case.

## C08 , validation costs

Breadth:

1. Every AI proposal needs a real-world check, and checks
   cost. Proposals beyond the assay budget build a queue.
2. Feasible n <= B / c.

Ladder:

1. Validation cost is the wet-lab price of checking AI
   proposals.
2. 200 x 5,000 = 1,000,000 dollars per month.
3. 400,000 / 5,000 = 80 proposals per month.
4. feasible_proposals(400_000, 1_000) = 400. The scaling
   check guards the division.
5. Assay scale-up wins where proposals are good. Triage
   wins where proposals are noisy.

Transfer: 80 assays carry 20 of information: effective
cost per independent result = 400k / 20 = 20k, 4x the
naive 5k. Diversify proposals first.

## C09 , domain expertise

Breadth:

1. Experts cannot be cloned: their hours gate releases,
   labels, and validation, and they are scarce.
2. Releases per month <= expert hours per month / hours
   per release.

Ladder:

1. The expert bottleneck is the scarce human judgment that
   paces the whole program.
2. 500 x 300 = 150,000 dollars per release.
3. 320 / 500 = 0.64 releases per month, about 7-8 per
   year.
4. max_releases(250) = 1.28, double of 0.64. The halving
   check guards the formula.
5. Hiring wins where the domain is the product and judgment
   cannot be triaged. Triage wins where AI can draft and
   experts check.

Transfer: the mistake costs a failed trial at 100M
against 150k saved. Rule: never substitute junior sign-off
for safety gates.

## C10 , adoption

Breadth:

1. Value equals potential times adoption. Pricing the
   endpoint assumes adoption the ramp never delivers.
2. Realized_t = a_t x V, summed and discounted.

Ladder:

1. Adoption-gated value is potential value times the
   realized adoption curve.
2. 100k + 350k + 700k = 1.15M over 3 years.
3. PV = 906,085.65 dollars.
4. adoption_value(1M, [1.0, 1.0, 1.0]) equals the 3-year
   annuity PV. The full-adoption check guards the
   discounting.
5. Training wins where the ramp is the constraint. Model
   investment wins where capability is the constraint.

Transfer: 10 percent all three years: PV = 100k x (1/1.1
+ 1/1.21 + 1/1.331) = 248,685. Verdict: the case fails.
fix the workflow fit first.

## C11 , human escalation

Breadth:

1. Each escalation buys trust at expert cost. The rate
   sets the per-task price of safety.
2. Per-task = e x c_e.

Ladder:

1. Human escalation is the expert review of AI outputs in
   high-stakes domains, priced per task.
2. 2.00 + 0.05 x 150 = 9.50 dollars per task.
3. 2.00 + 0.02 x 150 = 5.00 dollars.
4. escalation_cost(50_000, 0, 150) = (2.0, 100000.0). The
   e = 0 check guards the formula.
5. Escalation wins where tail risk is large. Autonomy wins
   where errors are cheap.

Transfer: 375k per year buys zero safety. Fix: measure
overturn rate and tie clinician incentives to real
review, or cut e with a better model.

## C12 , limitations

Breadth:

1. New scaffolds, targets, and assays are outside the
   training distribution by definition.
2. True = (1 - o) x a_in + o x a_ood.

Ladder:

1. The OOD limitation: models interpolate well and
   extrapolate poorly, and science needs extrapolation.
2. 0.7 x 0.95 + 0.3 x 0.55 = 0.83.
3. 0.83 x 50,000 - 5,000 = 36,500 dollars per proposal.
4. ood_value(0.0) = (0.95, 42500.0). The o = 0 check
   guards the mix.
5. OOD proposals win where novelty is the goal.
   Restriction wins where accuracy is the goal.

Transfer: true = 0.3 x 0.95 + 0.7 x 0.20 = 0.425. Net =
0.425 x 50k - 5k = 16,250. Policy: restrict to
in-distribution until OOD accuracy is measured.
