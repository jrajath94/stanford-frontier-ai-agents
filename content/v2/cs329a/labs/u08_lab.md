# Lab U08 , Long-horizon evaluation and research projects

Run script: `runs/run_u08.py`. Deterministic. Status: executed
2026-10-07. Observed outputs are recorded below.

## Exercise 1 , duration curve

Task: build the duration-success curve from lesson U08 C01 (100
tasks per horizon).

Expected: decreasing curve, 0.90 at 0.25 h, 0.35 at 8 h, drop
0.55.

Observed: curve={0.25: 0.9, 1: 0.7, 4: 0.5, 8: 0.35}, drop=0.55.

Verdict: PASS. Matches lesson U08 C01 item 6.

Analysis questions (answers in `keys/u08_key.md`):
L1.1: why does the 8 h point need the most tasks and get the
fewest?

## Exercise 2 , mean vs min

Task: rank agents A [0.90, 0.55, 0.85] and B [0.72, 0.74, 0.70]
by mean and by min.

Expected: mean picks A (0.7667 vs 0.72), min picks B (0.70 vs
0.55).

Observed: A mean=0.7667 min=0.55. B mean=0.72 min=0.70.

Verdict: PASS. Matches lesson U08 C05 item 6.

Analysis questions:
L2.1: the 0.55 task is the production workload. Which number
describes the deployed agent, and why?

## Exercise 3 , judge contamination

Task: compute the contamination gap between a same-model judge
(0.85) and an independent judge (0.60).

Expected: gap 0.25, honest score near 0.60.

Observed: gap=0.25 honest=0.60.

Verdict: PASS. Matches lesson U08 C07 item 6.

Analysis questions:
L3.1: the far judge is also an LLM from a different lab. What
does the residual gap measure?

## Exercise 4 , ablations and stopping

Task: compute ablation deltas (full 0.72, no-memory 0.58,
no-search 0.65, neither 0.50) and the optimal stop for gains
[0.10, 0.06, 0.03, 0.01] at $2000/point and $50/h.

Expected: memory 0.14, search 0.07, interaction +0.01, stop
after h3 with net $230.

Observed: deltas={'memory': 0.14, 'search': 0.07},
joint=0.22 interaction=0.01, stop=3 net=230.

Verdict: PASS. Matches lesson U08 C09 and C06 item 6.

Analysis questions:
L4.1: a component shows zero delta but is load-bearing for
safety. What does the ablation miss, and how would you catch
it?

## Exercise 5 , eval budget, profiles, gates

Task: budget the eval (200 tasks, $2 agent, $0.50 judge, 20
audits at $30), compute the DeepScholar toy profile, the
GDPVal toy win rate and SE, the negative-result verdict, and
the value capture.

Expected: total $1,100 binding audit. Profile synthesis 0.575,
retrieval 0.3167, verifiability 0.625. Win 0.50 SE 0.0337.
verdict rejected. Value capture 0.4386.

Observed: parts={'agent': 400.0, 'judge': 100.0, 'audit': 600.0}.
Total=1100 binding=audit. Profile={'synthesis': 0.575,
'retrieval': 0.3167, 'verifiability': 0.625}. Win=0.50
se=0.0337. Verdict=rejected. Value_capture=0.4386.

Verdict: PASS. Matches lesson U08 C08, C04, C03, C11, C02
item 6.

Analysis questions:
L5.1: the audit binds. Name two ways to halve the budget
without touching the task count, and the risk of each.
