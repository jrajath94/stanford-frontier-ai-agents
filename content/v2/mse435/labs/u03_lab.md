# Lab U03 , Enterprise infrastructure and token markets

Run `python3 u03_lab_run.py` to verify every computed answer.
The key in `u03_lab_key.md` records the verified outputs. Work
each task by hand first, then check against the runner.

## Task 1 , repricing with error costs (C01)

10,000 tasks per month, human 50 dollars, AI 0.50 dollars,
fixed 20,000. Sweep ai_share over [1.0, 0.9, 0.7, 0.5].
Then: wrong AI answers cost 200 dollars each, at ai_share
0.9 the error rate is 5 percent of AI tasks. Add the error
cost and report the true total.

## Task 2 , integration overrun (C02)

Base: api 5k/mo, plumbing 150k, security 100k, workflow
200k, training 45k, 2 years. Recompute with plumbing at 2x
and workflow at 1.5x. Report both totals and the overrun.

## Task 3 , stack crossover (C03)

Open: hosting 30k/mo + 200k integration. Closed: api_mo +
50k integration, 24 months. Sweep api_mo over [20k, 30k,
40k, 60k]. Report the winner at each.

## Task 4 , supply under mix shifts (C04)

1,000 GPUs, U = 0.85. Sweep tok/s over [15, 30, 50, 80].
Report B tokens per day and blocks per day.

## Task 5 , shock with sticky supply (C05)

Demand Qd = 100 - 2P jumps to 160 - 2P. Supply Qs = 20 + 3P
normally, but overnight it is fixed at 68. Report the
overnight P* and the later P* once supply adjusts.

## Task 6 , bottleneck sequence (C06)

Stages [100, 40, 80] rps. You have 200k per upgrade, each
upgrade doubles one stage. Spend two upgrades greedily on
the binding stage each round. Report the rate after each.

## Task 7 , unit cost curve (C07)

Training 5M, inference 4 $/1M. Sweep lifetime tokens over
[10B, 50B, 200B, 500B, 2T]. Report amortized and total per
1M.

## Task 8 , contract paths (C08)

Commit 120 blocks/yr, contract 3.00, r = 10 percent, 3
years. Market paths: [4,3,2], [4,2,1], [3,3,3], [5,5,5].
Report both PVs and the winner for each.

## Task 9 , ownership with lift (C09)

Build 2M + 300k/yr, rent 500k/yr, 3 years, r = 10 percent.
Sweep lift over [0, 0.5M, 1M, 2M] per year. Report own vs
rent PV and the winner.

## Task 10 , fence pricing (C10)

10,000 tickets, resolution with/without data [0.85, 0.55],
miss cost 50. Breach: probability per year in [0.005, 0.01,
0.05], loss 20M. Report monthly fence cost and monthly
benefit for each probability.

## Task 11 , price stack shocks (C11)

Base: cost 2.50, margin 1.00, buffer 0.50. Shock c to
[2.00, 2.50, 3.00, 3.50] (price fixed at 4.00). Report the
implied margin + buffer and flag the loss-making cases.

## Task 12 , tornado (C12)

Base 4.00. Drivers: utilization [2.80, 5.20], power price
[3.20, 4.80], batch size [3.40, 4.60], chip cost [3.50,
4.50]. Report the ranking by swing.
