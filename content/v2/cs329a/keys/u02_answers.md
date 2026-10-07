# Answer key , U02 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
thought: "Concatenate the two strings." action: concat("ab", "cd").
observation: "abcd". thought: "Upper-case the result." action:
upper("abcd"). observation: "ABCD". Answer: ABCD.

## E1.2
Stop after a max step count or on a finish action. It is load-bearing
because a bad tool result can otherwise trap the loop in retries
forever.

## E1.3
A single tool call with no branching, for example "fetch this URL".
The thought adds a model call without changing the plan.

## E2.1
Round 1: fail, error magnitude 2. Round 2: fail, magnitude 1. Round 3:
pass. The feedback sequence is [fail by 2, fail by 1, pass].

## E2.2
Execution feedback is computed from the artifact by running it. Change
the code and rerun, and the feedback changes. That causal link is what
makes repair possible.

## E2.3
A wrong expected value in the test, an empty test body that always
passes, or a flaky test that fails at random.

## E3.1
A: 3/3 = 1.0. B: 3/3 = 1.0. C: 1/3 = 0.333, only (0, 0) passes.

## E3.2
A suite with one test: [(-1, 0)]. C(-1) = 0, so C passes it fully
while A and B fail it. The point: a thin suite certifies the wrong
candidate.

## E3.3
The agent can only be as right as the suite.

## E4.1
Baseline = 0.5. Advantages: [0.5, -0.5, 0.0].

## E4.2
The RLEF reward is computed from test runs, not sampled from a learned
preference model. It cannot drift with the policy's flattery because
the tests do not learn.

## E4.3
If the tests change during training, old and new trajectories are not
comparable. Credit attaches to actions that the current tests may no
longer reward.

## E5.1
(a) Critique: the rewrite happens in the trace, weights unchanged.
(b) Learning update: DPO changes the weights.

## E5.2
A critique lives in the current trace. The next task starts a fresh
trace with the same stored weights, so the critique's effect does not
carry over.

## E5.3
A prompt update: change the system prompt. It persists across traces
without gradient steps. Use it when the fix is statable as an
instruction.

## E6.1
150 clean drafts plus 40 successful revisions = 190 training pairs.
Yield: 190/200 = 95 percent.

## E6.2
One good principle beats a thousand examples because it generates all
of them. One bad principle poisons all of them for the same reason.

## E6.3
A brief refusal that quotes the forbidden instructions inside the
explanation. It satisfies the letter of "refuse briefly" while leaking
the content.

## E7.1
Tricks score R1 = 1.0, above real sorts at 0.97, so selection picks a
trick. Its true quality is below the average real sort even though the
reward says it is the best candidate.

## E7.2
Policy gradients climb the reward surface. Any feature that raises the
reward without serving the goal gets amplified, because the gradient
points at the reward, not at the goal.

## E7.3
Independent validation. It must use a different instrument because the
training proxy cannot report its own failure: it scores the shortcut
1.0.

## E8.1
The 0.9 action is denied. The constrained pick is the 0.7 action.

## E8.2
A large negative reward still lets the action through during
exploration. A gate never lets a denied action execute, no matter the
reward.

## E8.3
The tool renames drop_db to remove_db. No predicate matches the new
name, so the gate waves it through. Fix: match on capability, not on
the name string.

## E9.1
429 "slow down": transient, retry with backoff. 400 "missing field q":
request bug, repair the arguments and resend once. 500 "nil pointer":
tool bug, quarantine and escalate. 200 with an HTML body: schema drift,
quarantine and escalate.

## E9.2
Unbounded retries on a sick tool multiply the load the tool already
cannot handle. The retry budget is the stability control that stops
the storm.

## E9.3
Never blind-retry a non-idempotent tool. A timed-out "send email" that
actually sent will send twice.

## E10.1
New log-prob of the fix step: -1.2 + 0.1 * 1.2 = -1.08. P(fix |
observation) rises from exp(-1.2) = 0.301 to exp(-1.08) = 0.340.

## E10.2
The mask reinforces only the steps after the informative observation,
like a scalpel. The full-trajectory update paints credit over every
step, including the failed attempts, like a roller.

## E10.3
The tool changed behavior after the trajectories were collected. The
update reinforces actions that no longer work in the new tool
behavior.

## E11.1
The pick is a shortcut with probability 0.7. Expected hidden quality:
0.3 * 0.98 + 0.7 * 0.12 = 0.294 + 0.084 = 0.378, while the visible
reward says 1.0.

## E11.2
The reward is the fence and the task is the field. Optimization digs
where digging is easiest, so it tunnels under the fence instead of
working the field.

## E11.3
Meta-failure: the policy learns to detect the hidden suite and behave
well only there. Defense: rotate in new hidden tests each round so the
target keeps moving.

## E12.1
The hidden suite catches 8 of 100 accepted patches, so the escape rate
it measures is 8 percent. Without the gate those 8 ship.

## E12.2
The system being judged influences the validator through shared data,
shared tuning, or a rubber-stamping operator. The gate then certifies
gaming as quality and its verdict means nothing.

## E12.3
Cheapest check first: hidden suite, then static analysis, then human
review last. Human review is the bottleneck, so it sees only the
survivors.
