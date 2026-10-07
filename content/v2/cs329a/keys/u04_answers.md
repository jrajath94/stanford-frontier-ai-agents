# Answer key , U04 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
20 designs * 100 tasks = 2,000 task runs per round.

## E1.2
Hand-design writes one agent. Architecture search writes the space,
the fitness, and the loop that finds agents. The designer's decisions
move from the artifact to the process that produces artifacts.

## E1.3
Validation leakage: designs tuned against the validation tasks. The
search overfits and the winner fails on new tasks.

## E2.1
M1: prompt "think then act Be careful.", tools [calc], flow react.
M2: prompt unchanged, tools [calc, search], flow react. M3: prompt
unchanged, tools [calc], flow plan-then-execute.

## E2.2
Many edits at once produce a better child with no attributable cause.
Nobody knows which edit did it, so the lesson cannot be reused.

## E2.3
Compare the fitness spread of edit-distance-1 children with the spread
of random designs. Narrower children spread means locality holds.

## E3.1
Keep 2: survivor mean = (0.73 + 0.71) / 2 = 0.72. Differential: 0.72
- 0.61667 = 0.10333, about 0.103.

## E3.2
Strong selection keeps near-identical top designs. Their children
explore one small region and the search stalls on a local optimum.

## E3.3
When fitness measurements are noisy. Tournaments let a strong
candidate survive an unlucky draw, while truncation keeps whoever got
lucky.

## E4.1
40 ideas at the toy rates: 24 run, 16 writeups, 6 pass review. Yield
6/40 = 0.15 papers per idea.

## E4.2
Many ideas enter and few survive each stage. The funnel is wide at
generation and narrow at review, because proposing is cheap and
verifying is expensive.

## E4.3
A review step that approves everything. The loop then mass-produces
confident writeups with no quality gate.

## E5.1
500 * 0.5 * 0.4 = 100 survivors.

## E5.2
Many programs enter, compilation and tests filter them in stages.
Each stage is cheaper than generation and stricter than the last, so
the survivors are worth the flood.

## E5.3
A program that hardcodes the visible test inputs. It passes the
filter and teaches nothing about the task.

## E6.1
4,000 / 10,000 = 0.40. Five picks cover 40 percent of the filtered
mass.

## E6.2
The top-10 by score are usually near-duplicates of one behavior. Ten
submissions then bet ten times on the same guess instead of spreading
over ten different behaviors.

## E6.3
The generated inputs miss the discriminating case, so two different
algorithms land in one behavior cluster. The pick covers one behavior
while the pipeline claims two.

## E7.1
20 * 0.60 * 0.90 = 10.8, about 11 right (0.54). Gain over 0.40: 0.14.

## E7.2
A wrong retrieved fact enters the trace early and every later
reasoning step builds on it. One bad snippet poisons the whole chain.

## E7.3
The reasoner ignores the retrieved fact and answers from its prior.
The search ran but changed nothing, it was theater.

## E8.1
Full records: 35/40 = 0.875 check out. Names only: 4/10 = 0.40. Gap:
0.475. Provenance predicts verifiability.

## E8.2
A receipt proves what was bought, where, and when. A provenance
record proves what was claimed, from which source, retrieved how: the
same trust in a checkable form.

## E8.3
A fabricated record with a plausible source_id. The form check
passes, only replaying the retrieval exposes the fiction.

## E9.1
sqrt(0.6 * 0.4 / 500) = sqrt(0.00048) = 0.0219, about 0.022.

## E9.2
The lesson's 2.25 is the expected max of 50 standard normals (the
accurate constant). The code's 2.80 is the sqrt(2 ln n) analytic
approximation, which overshoots. Both are labeled approximations, the
locked holdout gives the honest number.

## E9.3
Reusing the holdout for a second selection round. It becomes
validation under a fancier name and the bias returns.

## E10.1
Money: 3 * 30 * 200 * 0.02 = $360. Time: 3*30*200*2/10/3600 = 1.0
hour. Review: 3*5*10/60 = 2.5 hours. Money no longer binds at a $400
wallet, review time is now the largest cost.

## E10.2
$600 total against a $400 wallet: the run cannot afford generation 3.
Time (1.67h) and review (2.5h) fit easily, so money is the binding
fuel.

## E10.3
A stale sheet authorizes overspend: parameters changed after the
sheet was written, so the real burn exceeds the planned burn. Recompute
the sheet on every parameter change.

## E11.1
25 claims. Literature kills 0.4*25 = 10, leaving 15. Baselines kill
0.3*15 = 4.5, leaving 10.5. Ablation kills 0.1*10.5 = 1.05, leaving
about 9.45, so 9 or 10 survivors.

## E11.2
Literature first because it is cheapest, baselines second, ablation
third. Each stage costs more than the last, so cheap filters run
first.

## E11.3
The literature search uses keywords that miss the prior art's
terminology. The check passes and the claim is still old.

## E12.1
Network True triggers R1 first: (False, "R1: no network"). The write
is never evaluated because the network rule fires first.

## E12.2
Each rule covers the others' failures: no network stops exfiltration
even if a write escapes, read-only paths stop writes even if the path
check has a bug. Prevention is layered and logging adds detection.

## E12.3
A log the agent can edit. The post-mortem then reads fiction and the
detection layer is gone.
