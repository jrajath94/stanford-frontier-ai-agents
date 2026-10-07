# Interview key , U02

## B1

Sufficient: c = 25,000/(4 x 8760 x U) + 1.4 x 0.10 + 0.10.
The capex term moves with U, power and staff do not.
Strong: gives the floor at U = 1 (0.95 $/h) and notes idle
power understates low-U cost.
Red flags: dividing power by U too.
Rubric: 2 for the formula, 1 for naming the moving term.
Remediation: C01.

## B2

Sufficient: attainable = min(peak, intensity x bandwidth).
The ridge point is the intensity where the two are equal.
Strong: computes I* = peak/B and classifies both sides.
Red flags: swapping the sides.
Rubric: 1 for the rule, 1 for the ridge, 1 for an example.
Remediation: C03.

## B3

Sufficient: PUE = total power / IT power = 1.5. The 0.5 is
overhead per watt of compute (cooling, conversion, fans).
Strong: converts to dollars: 50 kW x 8760 x price.
Red flags: calling PUE an efficiency percent.
Rubric: 1 for the number, 1 for the definition, 1 for the
0.5.
Remediation: C06.

## B4

Sufficient: HHI = sum of squared market shares. Bands: <1500
unconcentrated, 1500-2500 moderate, >2500 high.
Strong: notes it is a convention for screening, and that
market definition drives it.
Red flags: treating 2500 as a law of nature.
Rubric: 2 for formula and bands, 1 for the caveat.
Remediation: C11.

## B5

Sufficient: the crossover utilization U*. Below it lease
wins, above it build wins.
Strong: computes U* = 0.478 for the toy and quotes it with
the recommendation.
Red flags: comparing sticker prices without utilization.
Rubric: 2 for naming U*, 1 for the direction.
Remediation: C08.

## B6

Sufficient: plan, build, operate, refresh. Discounting
shrinks the refresh (latest cash) most.
Strong: gives the discount factor intuition (1/1.1^7).
Red flags: naming only three phases.
Rubric: 1 per phase set, 1 for the discount answer.
Remediation: C04.

## L1

L1.1 Utilization: used hours over total hours. Effective cost:
sticker divided by U.
L1.2 3.00 / 0.50 = 6.00 dollars per used hour.
L1.3 Both true: 95 percent of hours are busy, but the busy
hours serve low-priority work while priority jobs queue,
or fragmentation leaves no large block free.
L1.4 Game: run junk jobs (fix: useful utilization), defer
maintenance (fix: incidents per GPU-month).
L1.5 Right when idle hours have no option value and no
buyer. Wrong when queues delay research or headroom has
option value.
Red flags: "high U is always good".
Rubric: 2 for L1.2, 1 each for the rest.
Remediation: C09.

## L2

L2.1 The site cannot draw more than the grid allows, capping
the GPU count.
L2.2 200 x 1000 / 2 = 100,000 GPUs.
L2.3 Served 200 MW, waiting 100 MW. Allocate by price (spot
market) or by queue (priority), price rations by
willingness to pay, queue by patience or rank.
L2.4 Water binds now, the power offer is moot until cooling
water is permitted.
L2.5 Examples: a site blocked on water permits, a build
waiting on transformers (supply chain). Bound instead:
permits and equipment lead time.
Red flags: insisting power is always the wall.
Rubric: 2 for L2.2, 1 each for the rest.
Remediation: C05.

## A1

Sufficient: H = 8760 x 0.80 = 7,008 h/yr. Lifetime saving
per chip without slip = 4 x 7,008 x 1.00 = 28,032 dollars.
N* = 80M / 28,032 = 2,854 chips. With year 1 at zero saving,
lifetime saving per chip = 3 x 7,008 = 21,024 dollars.
N* = 80M / 21,024 = 3,805 chips. Lesson: schedule slips
raise the volume bar, the NRE is sunk while the saving
waits.
Strong: states both numbers and the lesson in one line.
Red flags: dividing annual instead of lifetime.
Rubric: 2 for the first N*, 2 for the slipped one, 1 for
the lesson.
Remediation: C02.

## A2

Sufficient: annual charge = 300,000/5 = 60,000. Per GPU-hour
= 60,000 / (8 x 8760 x 0.75) = 60,000 / 52,560 = 1.14
dollars. Book at year 3 = 300,000 x (1 - 3/5) = 120,000.
The 30,000 gap says the market depreciates faster than
straight-line: economic life is shorter than book life.
Strong: recommends deciding keep-vs-sell on the 90,000
market value, not the 120,000 book.
Red flags: refusing the sale because "book says 120k".
Rubric: 2 for the charges, 1 for the book, 2 for the gap
reading.
Remediation: C10.

## D1

Sufficient: bug: the branches are swapped AND the first
branch returns peak instead of intensity x bw. Below the
ridge the workload is memory-bound at intensity x bw, not
compute-bound at peak. Fix:

```python
def roofline(peak, bw, intensity):
    if intensity * bw < peak:
        return intensity * bw, "memory-bound"
    return peak, "compute-bound"
```

Invariant restored: attainable never exceeds peak, and the
label matches the binding side.
Red flags: fixing only the label.
Rubric: 1 for the swap, 1 for the value, 1 for the fix, 1
for the invariant.
Remediation: C03.

## S1

Sufficient: falling lease rates lower the lease PV, so U*
rises (build needs higher utilization to win). The decision
now needs the rate path, not one rate.
Strong: sketches the comparison with rate_t = 2.50 x 0.85^t
and notes the option value of waiting to build.
Red flags: keeping the flat-rate U*.
Rubric: 2 for the direction, 1 for the new input, 1 for the
option point.
Remediation: C08 section 11, C12.

## S2

Sufficient: saving scales with U: at 0.35 the annual saving
is 0.35/0.85 of before, so payback roughly doubles to ~4.6+
years, past the refresh. Logic: defer the retrofit.
Option value of waiting: keep the capex, retrofit when
utilization recovers or power prices rise.
Strong: computes the scaled payback and names the trigger
(U back above ~0.6 or power above 0.14).
Red flags: proceeding because "the math worked at full
utilization".
Rubric: 2 for the rescaling, 1 for the decision, 1 for the
option argument.
Remediation: C06 section 11.

## R1

Sufficient: threats: (1) batch-1 benchmark flatters the
custom chip (GPUs win at large batch), (2) one workload,
not the fleet mix, (3) TCO needs utilization, power, and
software cost, not one kernel. Tests: (1) rerun at the
buyer's batch, (2) run the buyer's top-3 workloads, (3)
ask for the full cost build-up. Belief needs: independent
replication on the buyer's workload at the buyer's
utilization.
Strong: names the identifying gap (no counterfactual) and
prices the missing software cost.
Red flags: accepting vendor benchmarks as TCO.
Rubric: 1 per threat with test, 1 for the belief bar.
Remediation: C02, C03, C12.
