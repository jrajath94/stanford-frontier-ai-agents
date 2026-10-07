# Answer key , U02 , Silicon, power, and data centers

Keep separate from the lesson.

## C01 , GPU economy

Breadth:

1. Chip amortization, power, staff/overhead.
2. The chip cost is fixed per period, so more working hours
   spread it thinner, power and staff per hour do not move.

Deep ladder:

1. GPU-hour cost: the full cost of owning and running one GPU
   for one hour.
2. 25,000 / (4 x 8760 x 0.5) = 25,000 / 17,520 = 1.43 dollars.
3. c_h = capex/(life x 8760 x U) + power + staff. The first
   term is the fixed-cost spread from U01-C03.
4. Check: cost falls as U rises, floor at U = 1.
5. Build-up for make-vs-buy, market price for buy-vs-buy.

Transfer: true price = 1.08 dollars + 3 days of researcher
time. Convert: value of 3 days of loaded salary divided by
the hours the job needs, compare with paying spot to skip
the queue.

## C02 , custom accelerators

Breadth:

1. NRE: non-recurring engineering, the one-time design cost.
   Fixed because it does not scale with chips built.
2. N* = NRE / (H x s).

Deep ladder:

1. The bet: pay design once, save per hour forever, it pays
   only above a volume.
2. H = 7,446, per chip-year = 3,723, N* = 10M/3,723 = 2,686.
3. N x H x s = NRE solved for N, H x s is one chip's yearly
   return.
4. Check: N* x H x s equals NRE.
5. FPGA: medium volume, changing workloads, ASIC: high stable
   homogeneous volume.

Transfer: the shifting 40 percent. Quantify: expected life of
the workload mix times the saving, if the mix turns over
before payback, the N* math used the wrong horizon.

## C03 , memory/interconnect bottlenecks

Breadth:

1. Attainable = min(peak, intensity x bandwidth).
2. The ridge point I* = peak/B, where the bound switches.

Deep ladder:

1. Arithmetic intensity: FLOPs done per byte moved.
2. min(100, 50) = 50, memory-bound.
3. I x B converts a data rate to a compute rate, below I* the
   door binds, above it the cooks bind.
4. Check: attainable never exceeds peak.
5. Quantization helps the memory-bound side (fewer bytes per
   FLOP).

Transfer: the network is the missing door. Measure: bytes
moved per step over interconnect bandwidth, the roofline with
network B replaces HBM B.

## C04 , infrastructure lifecycle

Breadth:

1. Plan, build, operate, refresh.
2. Discounting multiplies late costs by small factors (e.g.
   1/1.1^7), so the refresh line shrinks most.

Deep ladder:

1. Lifecycle cost: all cash across plan, build, operate, and
   refresh, in present dollars.
2. PV = 100/1.1 + 10/1.1^2 + 10/1.1^3 = 90.91 + 8.26 + 7.51 =
   106.68M.
3. A dollar in year t is worth 1/(1+r)^t today, late dollars
   are cheap dollars.
4. Check: at r = 0 the result is the undiscounted sum.
5. Lease wins on uncertain demand, build wins on certain long
   demand.

Transfer: options: wait (pay delay, get new tech) vs proceed
(locked tech, on time). The deciding number: the PV cost of
delay versus the PV gain of the new generation.

## C05 , power constraints

Breadth:

1. 100 x 1000 / 1.4 = 71,428 GPUs.
2. It waits: queues, other regions, or next year's build.

Deep ladder:

1. The power constraint: the site cannot draw more than the
   grid allows, so GPU count is capped by watts.
2. 50 x 1000 / 2 = 25,000 GPUs.
3. N x p_gpu <= P_site x 1000 gives N_max, served =
   min(demand, limit) is physical rationing.
4. Check: served + waiting = demand.
5. Behind-the-meter when the grid queue is the delay, grid
   when interconnection is the path.

Transfer: water binds. Moves: (1) switch cooling (cost: capex,
payback math), (2) cut IT load to fit water (cost: fewer
GPUs, lost revenue).

## C06 , cooling

Breadth:

1. PUE: total facility power over IT power, >= 1.
2. Payback = extra capex / annual energy saving.

Deep ladder:

1. The trade: pay capex once for liquid, save power every
   hour, air is the reverse.
2. Saving = 50 x (1.6-1.2) = 20 kW, annual = 20 x 8760 x
   0.12 = 21,024, payback = 40,000/21,024 = 1.90 years.
3. Premium over dividend: one-time extra cost divided by
   yearly savings.
4. Check: lower PUE gives positive saving.
5. Immersion at extreme density, liquid cold plates at high
   but serviceable density.

Transfer: moves: (1) air cooling (higher power bill, needs
grid headroom), (2) dry coolers with less water (higher
capex, some efficiency loss). Cost each in dollars and MW.

## C07 , gigawatt scale

Breadth:

1. 1,000,000 / 1.4 = 714,285 GPUs.
2. Build (concrete) and energy (electrons).

Deep ladder:

1. Gigawatt scale: a single site at or above 1 GW, a grid
   planning event.
2. 500,000 / 2 = 250,000 GPUs.
3. Build = $/W x 10^9, the $/W bundles land, power, building,
   cooling per watt.
4. Check: GPUs x kW/GPU = 10^6.
5. One site when all constraints clear at one place and scale
   wins, five sites when any constraint binds or risk must
   spread.

Transfer: price it: discount x annual energy bill must exceed
the cost of 5 percent lost hours. Training tolerates
interruption (checkpoint/restart), inference does not (SLA
breach), so the required discount is far higher for
inference.

## C08 , build/lease tradeoffs

Breadth:

1. Build PV = capex + maint x annuity. Lease PV = N x 8760 x
   U x rate x annuity.
2. Below U* the bulk discount is wasted on idle hours, above
   it the discount is harvested.

Deep ladder:

1. The trade: buy cheap hours in bulk vs pay per used hour at
   a premium.
2. U* = 10M / (500 x 8760 x 3.00 x 3.1699) = 10 / 41.65 =
   0.24.
3. Set the PVs equal and solve, the annuity cancels only when
   maintenance is zero.
4. Checks: build PV flat in U, lease PV linear in U.
5. Colocation splits building from chips: rent space/power,
   own GPUs.

Transfer: split: own the base 50 percent (build), rent the
burst (lease). The single-U* math overbuilds for the average
and strands half the fleet.

## C09 , utilization

Breadth:

1. e = c / U.
2. Queues, deferred maintenance, and lost option value cost
   more than the saved GPUs.

Deep ladder:

1. Utilization: used hours over total hours.
2. 3.00 / 0.60 = 5.00 dollars per used hour.
3. Total cost over used hours, the total cancels, leaving the
   ratio.
4. Check: effective >= sticker.
5. Raise U for internal fleets, sell spot when idle hours
   have a buyer.

Transfer: (1) run low-priority jobs to look busy (stopped by
measuring useful utilization), (2) defer maintenance
(stopped by tracking incidents per GPU-month).

## C10 , depreciation

Breadth:

1. Year t book = C x (1 - t/T), annual charge C/T.
2. The charge reflects timing on the books, and the cash left at purchase.

Deep ladder:

1. Depreciation: spreading an asset's cost over its useful
   life on the books.
2. 90k/3 = 30k per year, books: 90, 60, 30, 0.
3. Yearly slice over yearly working hours, each division
   converts cost to the billing unit.
4. Check: schedule ends at zero.
5. Accelerated front-loads the charge (tax timing), cash is
   unchanged.

Transfer: right cost = opportunity cost: max(spot earnings,
resale value decay). Finance's zero ignores the forgone
2 dollars per hour.

## C11 , supply concentration

Breadth:

1. HHI = sum of squared shares, <1500 unconcentrated,
   1500-2500 moderate, >2500 high.
2. Squaring punishes bigness: one large firm scores far above
   several small ones.

Deep ladder:

1. Concentration: how few hands hold the supply.
2. 2500 + 900 + 400 = 3800, high.
3. 70^2 = 4900 vs two 35s = 2450, the split nearly halves
   the index.
4. Check: shares sum to 100, monopoly gives 10,000.
5. HHI is a quick screen, the chain map finds chokepoints
   (one fab, many chip firms).

Transfer: (1) qualify a second source (even at a premium, it
caps the allocation risk), (2) redesign for portability so
the next buy can switch.

## C12 , scenario analysis

Breadth:

1. A scenario is a named future with numbers, it is not a
   forecast with probabilities.
2. Minimize the worst regret: pick the option that never
   fails badly.

Deep ladder:

1. Scenario analysis: deciding across a few named futures
   instead of one forecast.
2. Lease regret: 0 vs build in scenario 1... compute: lease
   8M wins vs build 10M, scenario 2 lease 14M loses. Build
   never loses more than 2M, lease loses 4M. Resilient: build.
3. Regret = option cost minus best cost in that scenario,
   minimizing the max keeps the worst case bounded.
4. Check: the build column is constant across scenarios.
5. Scenarios for speed and communication, Monte Carlo for big
   irreversible bets.

Transfer: fourth scenario: supply freeze (no GPUs to rent at
any price). The lease column becomes infinite, build wins
absolutely and the table needs an availability row.
