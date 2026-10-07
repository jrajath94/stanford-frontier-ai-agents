# Answer key , U01 , AI economics and the full value chain

Keep separate from the lesson. Each deep-ladder answer gives the
minimum sufficient explanation.

## C01 , supply/demand

Breadth:

1. Equilibrium is the price at which the quantity buyers want
   equals the quantity sellers offer.
2. Price falls, quantity rises.

Deep ladder:

1. Equilibrium: the price where quantity demanded equals quantity
   supplied, so no buyer or seller wants to change their plan at
   that price.
2. 60 - P = 3P - 20 gives 80 = 4P, P = 20, Q = 40.
3. From a - bP = c + dP: P* = (a - c)/(b + d). a - c is demand at
   price zero minus supply at price zero (excess demand to absorb),
   b + d is the combined slope that absorbs it.
4. Checks: (a) plug P* into both curves, quantities match, (b)
   shift demand up, P* rises.
5. The curve model misleads when adjustment is slow or prices are
   administered, an auction uses real bids and needs no estimated
   curves.

Transfer: buyers are rationed at 10 dollars. A non-price
mechanism (queue, lottery, priority tiers, or willingness to
wait) decides who gets tokens. Expect: names the rationing and
one mechanism.

## C02 , complements/substitutes

Breadth:

1. Negative cross elasticity marks complements, positive marks
   substitutes.
2. Complements: GPUs and power, models and inference demand.
   Substitutes: API tokens and self-hosting, two model vendors.

Deep ladder:

1. Cross-price elasticity is the percent change in demand for one
   good divided by the percent change in the price of another.
2. E = 0.04 / (-0.10) = -0.40, complements.
3. From Qx(Px, Py) with Px held: the ratio of the two percent
   changes estimates E_xy. Held assumption: only Py moves.
4. Guard: raise on pct_py == 0, since no price move means no
   identification.
5. The ratio is enough for a first-pass classification, regression
   is needed when many prices move at once.

Transfer: not necessarily complementarity. One story (a hot new
model release) can raise both training and inference demand at
once. Name the confounder: the release, or a marketing push.

## C03 , fixed/variable costs

Breadth:

1. TC = FC + vQ. ATC = FC/Q + v. Q_be = FC/(P - v).
2. ATC = FC/Q + v falls because FC/Q shrinks as Q grows, v is
   untouched.

Deep ladder:

1. Fixed cost: cost that does not change with quantity this
   period. A flat monthly platform fee is fixed, per-token compute
   is variable.
2. Contribution = 6, Q_be = 60,000/6 = 10,000.
3. From (P - v)Q - FC = 0: Q_be = FC/(P - v). Needs P > v or the
   quantity is negative, meaning no volume works.
4. Guard: return None when p <= v.
5. The simple split misleads when FC is shared across products,
   activity-based costing allocates it by activity.

Transfer: old wins when FC_old + v_old x Q < v_new x Q (rental
has ~zero FC). Solve Q < FC_old / (v_new - v_old). Name the
crossover volume.

## C04 , capex/opex

Breadth:

1. Capex: one-time spend on a long-lived asset. Opex: recurring
   spend to operate.
2. Higher r discounts future rent more, so the rent PV falls and
   renting looks cheaper.

Deep ladder:

1. Present value: what a future payment is worth today given the
   discount rate.
2. 100/1.10 = 90.91 dollars.
3. Sum of the geometric series of 1/(1+r)^t for t = 1..T gives
   (1 - (1+r)^(-T))/r.
4. Check: at r = 0 the factor equals T.
5. Payback ignores discounting and everything after payback, NPV
   counts all years in today's dollars.

Transfer: compare PV of prepaid (upfront + zero marginal) vs PV
of on-demand over 3 years at the firm's r. Risks: usage falls
short of the commit (stranded prepay), prices fall (commit
overpays).

## C05 , value capture

Breadth:

1. Creation is total surplus (willingness to pay minus true
   costs). Capture is the share one firm keeps.
2. Bottlenecks capture more because buyers cannot route around
   them, so the layer can price above cost.

Deep ladder:

1. Capture share: a layer's kept profit as a share of total
   created value.
2. Shares: 11 - 5 = 6 for chips, 21.4 - 11 - 4 = 6.4 for cloud.
3. Sum of shares plus all own costs equals the final price, it is
   an identity that checks arithmetic.
4. Check: shares + costs = final price, flag negative shares.
5. The accounting split misleads inside one integrated firm where
   transfer prices are set by policy, not markets.

Transfer: model price = cost makes the model share zero. The
freed value flows to adjacent layers (cloud hosting, apps) that
can now price above cost against free intelligence.

## C06 , layers from chips to applications

Breadth:

1. Chips sell compute, clouds/DCs sell reliable compute at scale,
   model labs sell intelligence (weights or API), apps sell
   outcomes.
2. Each layer has a different efficient scale and skill set, one
   firm rarely runs all four at each layer's best scale.

Deep ladder:

1. The stack: four separable layers where each buys the layer
   below and sells a more finished product upward.
2. Example: chip 0.002, facility 0.010, model 0.008, total 0.020.
3. The cut is a fixed dollar amount at the bottom, upper layers
   add their own costs on top, so the percent saving shrinks.
4. Check: parts sum to the total.
5. The chip layer earns its box when chip supply or chip choice
   drives the decision (weeks 2-3), fold it otherwise.

Transfer: stack is open weights (price zero) on rented cloud,
the model layer has zero price and the economic stack is three
layers.

## C07 , consumer versus enterprise

Breadth:

1. Consumer: users x conversion x ARPU (per month). Enterprise:
   accounts x ACV (per year).
2. One enterprise account is worth hundreds of consumer-years,
   which funds sales humans.

Deep ladder:

1. ARPU: average revenue per user per month. ACV: annual contract
   value per account.
2. 4.0M per month consumer, 833k per month enterprise.
3. 200,000 / 240 = 833: one account equals 833 consumer-years of
   revenue.
4. Check: both results in dollars per month.
5. The binary split breaks in the prosumer middle (roughly 50 to
   10k dollars), which needs its own model.

Transfer: per-token enterprise pricing follows consumer math
(usage x price). What breaks: fixed sales/support cost per
account must now be covered by uncertain usage, the contract
needs a commit or floor.

## C08 , productivity versus adoption

Breadth:

1. Capability is what the tech can do, adoption is who uses it,
   productivity is realized output per input.
2. Productivity lags because adoption is slow, workflows must
   change, and measured output moves only when use is broad.

Deep ladder:

1. The adoption gap: the difference between what the technology
   can do and what the economy actually produces with it.
2. G = 0.40 x 0.50 / 0.75 = 0.2667, or 26.7 percent.
3. The curve saturates because late adopters gain less, k sets
   how fast gains approach the max.
4. Checks: G(0) = 0, G never exceeds g_max.
5. Bass adds separate innovator and imitator dynamics over time,
   the toy is a static snapshot.

Transfer: frictions the toy omits: workflow redesign time,
training, and measurement lag. Test: compare mandated vs
voluntary teams, or track output per hour weekly to separate
tool effects from workflow changes.

## C09 , forecasts versus observations

Breadth:

1. MSE = bias^2 + variance of errors.
2. Same MSE can hide bias in one and noise in the other, bias is
   fixable by shifting, noise is not.

Deep ladder:

1. Bias: average signed error. Noise: error without direction.
2. Errors +1, +3, bias +2, MSE (1+9)/2 = 5.
3. e_i = b + v_i, mean(e_i^2) = b^2 + mean(v_i^2), the cross term
   sums to zero because v_i averages to zero.
4. Check: bias^2 + variance equals MSE.
5. They disagree when an outlier dominates MSE, MAE resists it.

Transfer: missing is the range (uncertainty). Force it by
requiring a band with the forecast, or a contract clause tied
to actuals with a true-up.

## C10 , two-year comparison

Breadth:

1. Matched change, mix change, quality change.
2. The basket of goods changed, so the index mixes price change
   with composition change.

Deep ladder:

1. A matched comparison prices the same basket at both dates.
2. Matched -40 percent, observed -60 percent, mix -20 points.
3. Observed = matched + mix, assuming the basket is fixed within
   each line. The mix line absorbs basket change.
4. Check: matched + mix = observed.
5. Hedonic adjustment prices quality traits directly, use it when
   quality change dominates, the basket split when mix change is
   the story.

Transfer: ask (1) "is the basket identical?" and (2) "what is the
matched-model change versus the mix effect?" before repeating.

## C11 , uncertainty

Breadth:

1. Decisions break at the edges (shortfall, idle capacity), and
   only a range shows the edges.
2. Expected value hides the spread and the asymmetry of the bet.

Deep ladder:

1. Expected value: the probability-weighted average outcome.
2. E = 0.5 x 1 + 0.5 x 3 = 2.
3. The upside case (2B) outweighed the downside (0.5B), pulling E
   above the modal 1B.
4. Check: probabilities sum to 1, E lies within [min, max].
5. Expected value for survivable repeated losses, minimax when the
   worst case is ruin.

Transfer: put (1) the range of outcomes and (2) the cost of the
worst case on the slide, the base case alone cannot carry a
capacity decision.

## C12 , source claims

Breadth:

1. OFFICIAL-SCHEDULE, OFFICIAL-SOURCE, REQUESTED-BRANCH, SPEAKER
   CLAIM, TOY, NOT IN SOURCE.
2. Inspecting the artifact the claim came from and recording the
   inspection boundary.

Deep ladder:

1. Provenance: the recorded origin and evidence state of a claim.
2. "Demand curves slope down" as used in C01: REQUESTED-BRANCH
   (textbook micro, assumed), evidence: standard theory, not an
   inspected artifact.
3. Labels must travel because each retelling can silently upgrade
   authority, the label freezes the authority at its source.
4. Check: kind is in the allowed set.
5. Blind trust is fast but lets forecasts harden into facts,
   verify-everything is safe but paralyzes note-taking.

Transfer: process fix: forecasts leave your notes only with
their label attached, the memo template has a mandatory
evidence column.
