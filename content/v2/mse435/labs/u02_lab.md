# Lab U02 , Silicon, power, and data centers

Run `python3 u02_lab_run.py` to verify every computed answer.
The key in `u02_lab_key.md` records the verified outputs. Work
each task by hand first, then check against the runner.

## Task 1 , cost build-up sweep (C01)

Capex 25,000 per GPU, 4-year life, 1.4 kW, 0.10 $/kWh, staff
0.10 $/h. Sweep U over [0.2, 0.4, 0.6, 0.85, 1.0]. Report the
three parts and the total.

## Task 2 , custom chip volume (C02)

NRE in [20M, 50M] dollars, saving per chip-hour in [0.40,
0.82, 1.20] dollars, U = 0.85. Report the break-even chip
count for each pair.

## Task 3 , roofline sweep (C03)

Peak 300 TFLOP/s, bandwidth 2 TB/s. Sweep intensity over [40,
100, 150, 500] FLOP/byte. Report attainable TFLOP/s and the
binding side.

## Task 4 , lifecycle under two paths (C04)

Plan 5M, build 400M at year 1.5, refresh 120M at year 7, r =
10 percent. Path A opex 40M/yr years 2-7. Path B opex 25M/yr
years 2-7 (low demand). Report both PVs and the difference.

## Task 5 , capacity from power (C05)

Compute max GPUs at 1.4 kW each for sites of 50, 100, and 1000
MW. For the 100 MW site, report served and waiting at demand
70 and 140 MW.

## Task 6 , cooling payback grid (C06)

100 kW IT rack, air PUE 1.5 capex 150k, liquid PUE 1.15 capex
220k. Sweep power price over [0.06, 0.10, 0.16] $/kWh and
utilization over [0.4, 0.85] (saving scales with U). Report
payback years.

## Task 7 , gigawatt scale (C07)

Report GPUs, homes, build dollars, and annual energy dollars
for 1 GW at 10 $/W, 1.4 kW/GPU, 1.25 kW/home, 0.08 $/kWh.
Then: the utility offers interruptible power (5 percent of
hours cut) for training. At 2.00 $/GPU-h value, what annual
discount per kWh makes the interruption break even?

## Task 8 , crossover sweep (C08)

Build 30M capex + 1M/yr, 1000 GPUs, 4 years, r = 10 percent.
Sweep lease rate over [1.50, 2.50, 3.50] $/GPU-h. Report U*
for each.

## Task 9 , effective cost (C09)

Sticker 2.02 $/GPU-h. Report effective cost at U in [0.4,
0.6, 0.85, 0.95]. Then: at U = 0.95 the queue delay averages
2 days per job. If a researcher-day is worth 800 dollars and
a job needs 100 GPU-hours, what is the delay cost per job?

## Task 10 , book vs market (C10)

Server cost 200,000, 4-year straight line. Market value falls
40 percent per year from 200,000. Report book and market at
years 0-4 and the year the gap is largest.

## Task 11 , HHI under entry (C11)

Base shares [70, 15, 10, 5]. A new entrant takes 10 points
from the leader: [60, 15, 10, 5, 10]. Report both HHIs and
bands.

## Task 12 , scenario table (C12)

Build PV 33.17M. 1000 GPUs, U = 0.60, 4 years, r = 10
percent. Lease rates: fast fall 1.50, flat 2.50, shortage
3.50. Report the table and the resilient pick. Add a fourth
scenario, supply freeze (lease unavailable), and state how
the table changes.
