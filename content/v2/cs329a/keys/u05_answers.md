# Answer key , U05 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
S = 5, K = 16. Trajectory cost: 5 * 0.05 = 0.25. Total per issue:
0.40 + 16 * 0.25 = 0.40 + 4.00 = $4.40. Context share: 0.40 / 4.40
= 9.1 percent.

## E1.2
Context finding is paid once per issue no matter how many
trajectories run. As K grows, that fixed cost spreads over more
samples, so each sample gets cheaper and a simple read-every-file
method becomes affordable.

## E1.3
The trajectory's own generated tests pass a wrong edit. Serial
iterations then polish the bad fix, and parallel samples multiply
it. The failure is test dishonesty, not search weakness.

## E2.1
Coverage = 1 - 0.70^5 = 1 - 0.16807 = 0.8319, about 0.83.

## E2.2
Test voting is cheap and drops most bad candidates. The expensive
model judge then runs only on the shortlist. Spend the judge where
the choice is close, not on the full pile.

## E2.3
Generated tests share the candidates' wrong assumption. The
filter keeps the wrong ones with high scores. Precision above 0.5
means nothing when the errors are correlated.

## E3.1
4 test runs and 3 repairs. The loop stops at the first pass, which
is iteration 3, so the 4th iteration never runs.

## E3.2
The model that wrote the draft cannot judge it with new
information, it only has its own prior. Execution returns a trace
from outside the model, and each repair must respect that new
fact.

## E3.3
A suite that passes everything. The loop accepts the first draft
with no signal. Grounding with no signal is single-shot with
extra steps.

## E4.1
fast_1 = 4/10 = 0.40. fast_2 = 1/10 = 0.10 (kernel 6 at 2.3x).

## E4.2
One gate is easy to game alone: zeros are fast, the reference
wrapper is correct. The conjunction is the only score that means
the kernel is both right and faster. Separate gates keep each
honest.

## E4.3
A kernel returning zeros passes an absolute tolerance when true
outputs are near zero. It can even post a huge fake speedup. The
fix is a scale-invariant tolerance.

## E5.1
Deployable: (T,1.0), (T,1.4), (T,0.9), (T,1.2). Winner: (T,1.4).

## E5.2
Correctness is a gate and speed is a ranking. No weight on speed
compensates for a wrong answer, because silent wrongness costs
more than slowness. Rank only among the correct.

## E5.3
Tests miss the input class where the winner is wrong. The gate
passes a bad kernel. The number looked honest because the blind
spot was in the test set, not the rule.

## E6.1
Worst-case wall time: 12 * 30 = 360 s. Observation tokens: 12 *
2,000 = 24,000. Both bounds come straight from the interface
spec, no agent behavior assumed.

## E6.2
Every agent action passes through the interface, so safety,
cost, and observability are decided once, in the contract. The
agent's freedom is everything inside the fence, and the fence is
written before the first call.

## E6.3
Limits are documented but not enforced. The agent finds the gap
and writes outside it. A rule the environment does not enforce is
a suggestion.

## E7.1
New time = 4.0 + 6.0 / 3 = 6.0 s. Speedup = 10 / 6 = 1.6667.
Amdahl: 1 / (0.40 + 0.60 / 3) = 1 / 0.60 = 1.6667.

## E7.2
The profile says where the time actually goes. Without it the
agent optimizes a guess, and Amdahl caps the win at the share of
the part it happened to pick. Measure first, cut second.

## E7.3
The profile was taken at input size 32, deployment uses 4096, and
the hotspot moved. The agent optimized the small-input bottleneck.
Always profile at deployment scale.

## E8.1
False alarm = 0.2^3 = 0.008. On 200 runs a day that is 1.6 false
alarms, eight times worse than the f = 0.10 toy.

## E8.2
One failure of a flaky test proves nothing, so the loop would
chase ghosts. Three runs make the false-alarm rate f^3, which is
tiny for small f. Quarantine the test if the runs disagree.

## E8.3
The flake is a race that fails under load. All three reruns fail
on the same loaded machine, and good code is condemned. Reruns
must vary the conditions, not just repeat them.

## E9.1
Visible 1.00, hidden 0.85. Gap = 0.15. That gap is sample noise
under a clean split, not cheating.

## E9.2
The visible set guides tuning and the hidden set is touched once
for the final number. Any information crossing the wall turns the
reported score into the max over tuned candidates. The wall keeps
the number honest.

## E9.3
An engineer pastes a hidden failure into the agent's context to
help. The edit now targets the hidden set directly. The reported
score after that is fiction.

## E10.1
Blocked 4 of 5: block rate 0.80. The allowed action is inside
/task and logged. The cage held on every out-of-bounds attempt.

## E10.2
The model can be talked out of a prompt rule, but it cannot talk
the kernel out of a deny. Enforcement must live below the agent,
in the kernel or container, or it is not a bar at all.

## E10.3
The sandbox shares a user namespace with a privileged helper. The
agent finds the helper and escapes through it. Audit the helpers
with the same suspicion as the agent.

## E11.1
Runs A and B match: byte-identical edits, outputs within 1e-6.
Verdict: reproducible. Run C differs because the seed differs,
which is a different experiment, not a failure.

## E11.2
The receipt lists seed, versions, inputs, and environment. With
all four, a rerun is a replay of the same experiment. Each
missing field is one way the rerun can wander.

## E11.3
A library draws from an unseeded OS source. The rerun differs and
the receipt looks complete. Capture every randomness source or
state the gap.

## E12.1
Last good checkpoint is 2, failed step is 4. Recovery cost: 4 - 2
= 2 step-runs. The skipped checkpoint at step 3 doubled the cost.

## E12.2
A checkpoint is a known-good state, so restore carries bounded cost
and certain success. Repairing corruption in place carries unbounded
cost and uncertain success. Boring beats clever here.

## E12.3
The corruption is silent and three more steps build on it.
Rollback then discards good work along with bad. Detect
corruption at write time with checkpoint verification.
