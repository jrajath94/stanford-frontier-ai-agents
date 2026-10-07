# Answer key , U03 , Enterprise infrastructure and token markets

Keep separate from the lesson.

## C01 , service-as-software thesis

Breadth:

1. AI turns labor-like services into software-priced
   products: marginal task cost falls toward compute cost.
2. Human cost is linear in tasks, AI cost is sublinear (fixed
   model cost spread + tiny marginal), so the ratio grows
   with volume.

Deep ladder:

1. The thesis: services priced like software because AI
   delivers them at compute cost.
2. Human: 200,000. AI: 2,000 + 10,000 = 12,000.
3. 50/0.50 = 100, the human side cannot spread its fixed
   cost across tasks the way software does.
4. Check: at ai_share = 0 cost is all-human plus fixed.
5. Labor arbitrage where AI quality fails, the thesis where
   quality holds and volume is large.

Transfer: deploy if ai_share x saving > error_rate x tasks x
500. Solve for the max tolerable error rate.

## C02 , enterprise integration

Breadth:

1. Model API, data plumbing, security/compliance, workflow
   redesign, training.
2. The model is ~11 percent of year-1 cost, budgeting it
   alone misses 9x.

Deep ladder:

1. Integration cost: everything around the model needed to
   get an outcome.
2. Year 1: 555,000. Two-year: 695,000.
3. 555,000/60,000 = 9.25x, the car costs 9x the engine.
4. Check: years = 1 gives yr1 only.
5. Vertical app for standard workflows, build-up for custom
   workflows and proprietary data.

Transfer: security and plumbing lines move (rework cost),
workflow and training lines stretch (delay). Contingency: a
coupled-risk reserve, not per-line padding.

## C03 , open/closed stacks

Breadth:

1. Open: hold the weights, pay to host, own ops. Closed:
   rent intelligence per token, vendor sets price and rules.
2. Open is fixed-heavy, closed is variable, volume decides,
   like build vs lease.

Deep ladder:

1. Control premium: what the firm pays for data control and
   no vendor dependence.
2. Open 920k, closed 1,010k, at half volume open 680k,
   closed 530k.
3. Premium = closed - open at indifference, here open wins
   before any premium.
4. Check: the winner flips with volume.
5. Hybrid when data classes differ (sensitive vs bursty).

Transfer: closed year-2 at 1.4x price: 40,000 x 12 x 1.4 +
480,000... recompute: year 1: 480,000 + 50,000, year 2:
672,000. Total 1,202,000 vs open 920,000. Clause: price
cap or termination-for-convenience.

## C04 , compute supply

Breadth:

1. Supply/day = N x s x U x 86,400.
2. s varies 10x with model and batching, a point estimate
   lies.

Deep ladder:

1. Token supply: the tokens per day a fleet can serve.
2. 500 x 40 x 0.9 x 86,400 = 1.5552T per day.
3. N x s is the line rate, U the sold share, 86,400 the
   day conversion.
4. Check: linear in each input, zero at U = 0.
5. Build at high steady volume, buy tokens at low/spiky
   volume.

Transfer: levers: add GPUs (slow) or raise s via batching
(fast). The contract breaks first on the throughput promise,
renegotiate the SLA before the GPUs arrive.

## C05 , token demand

Breadth:

1. P in $/1M tokens, Q in B tokens/day, P* = (a-c)/(b+d).
2. A steep supply curve absorbs the shock in quantity, not
   price.

Deep ladder:

1. Token demand: the quantity buyers want at a token price.
2. P* = 16, Q* = 68.
3. (160-20)/5 = 28, up 75 percent, (140-20)/5... quantity
   104, up 53 percent.
4. Check: plug back into both curves.
5. Clearing where spot/auction pricing exists,
   administered where vendors post prices.

Transfer: allocation by queue, tier, or relationship. The
implicit price is the wait cost plus the value of the
forgone use.

## C06 , capacity bottlenecks

Breadth:

1. System rate = min(stage capacities).
2. The next-slowest stage becomes the min.

Deep ladder:

1. Bottleneck: the stage that sets the line's rate.
2. Rate 30, utils 0.5, 0.5, 1.0.
3. Serial rate is the min, other stages' extra capacity is
   unused.
4. Check: the binding stage shows utilization 1.0.
5. Upgrade a single box, parallelize a scalable stage.

Transfer: rework: the GPU stage is now the min, move the
batcher budget to GPUs or batching policy. Two sentences,
then remeasure.

## C07 , inference versus training economics

Breadth:

1. Training: one-time tuition spread over tokens.
   Inference: rent paid per token forever.
2. T/V shrinks with volume while i is constant, so tuition
   vanishes from the unit cost.

Deep ladder:

1. Amortization: spreading a one-time cost over its lifetime
   output.
2. 2M/100B x 1M = 20, unit = 23 dollars per 1M.
3. Set T/V x 1M = i, below it tuition dominates.
4. Check: total never below i.
5. One big T for shared tasks, per-customer fine-tunes for
   deeply different tasks.

Transfer: unit = (500k x 12)/V x 1M + i, with T recurring
yearly. It works when V is large enough that the yearly
tuition per token stays small.

## C08 , long contracts

Breadth:

1. Contract PV = sum p_c Q/(1+r)^t, market PV = sum p_t
   Q/(1+r)^t, sign the smaller.
2. The price path and exit terms decide, not the headline.

Deep ladder:

1. A long contract is price insurance: lock the price, lock
   the demand.
2. 4/1.1 = 3.636 (per block-year, x120 = 436.4).
3. Discounting weights near years most, where the lock
   helps most against high early market prices.
4. Check: flat path at p_c gives equality.
5. Long lock for certain usage and flat/rising paths, short
   commits for uncertain paths.

Transfer: sign the commit at the P10 usage case, demand a
downward flex or termination clause for the downside.

## C09 , ownership

Breadth:

1. Weights, data rights, evals, the team that can change
   them.
2. Cost-only math omits differentiation lift, which is the
   owner's main return.

Deep ladder:

1. Ownership: holding the asset and the right to change it.
2. Own 2.746M, rent 1.243M, with 1M lift, own 0.259M net.
3. The annuity converts yearly flows to present dollars for
   comparison.
4. Check: own falls as lift rises.
5. Full ownership when the base differentiates, own data +
   rent weights as the default.

Transfer: the own column loses the team: add rebuild cost
or a retention package. Cheapest hedge: document, cross-
train, and escrow the training pipeline before resignations.

## C10 , data governance

Breadth:

1. The price of the fence (lost quality) and the purpose
   (risk kept out).
2. Tail losses dominate means, scenarios show the tails.

Deep ladder:

1. Data governance: rules for what data the model may
   touch.
2. 10,000 x 0.20 x 50 = 100,000 per month.
3. 100,000/4,167 = 24x, overturned by a larger tail loss
   (reputation) or higher breach probability.
4. Check: cost rises with the resolution gap.
5. Ban when controls cannot be trusted, technical controls
   when quality loss is large and risk is real.

Transfer: people failed, not the rule. Controls: DLP on
endpoints and audit of model inputs, plus just-in-time
access instead of standing access.

## C11 , unit prices

Breadth:

1. True unit cost, margin, risk buffer.
2. c moves with utilization and batching, the stack rots.

Deep ladder:

1. Unit price: what one billing block sells for.
2. p = 4.00, margin rate = 0.75/4.00 = 18.75 percent.
3. Blocks = fixed/(p - c), contribution is p - c.
4. Check: parts sum to p.
5. Value pricing where ROI is demonstrable, cost-plus where
   buyers can compute your c.

Transfer: stories: (1) lower c (efficiency), (2) subsidy
(losses). Test: watch their price when funding news or
utilization proxies move.

## C12 , sensitivity

Breadth:

1. It ranks drivers by swing, it does not forecast what
   happens.
2. Honest ranges beat guessed ones, owners know their
   input's range.

Deep ladder:

1. Sensitivity: how much the outcome moves per input.
2. A swing 6, B swing 2, A first.
3. The sort puts scarce attention on the biggest mover.
4. Check: descending swings.
5. Tornado for the first meeting, Monte Carlo for the final
   call.

Transfer: rank by actionable swing (swing x ability to
move it). The decision becomes which lever to pull, not
which bar is longest.
