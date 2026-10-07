# U04 answer keys

Kept separate from `lessons/u04_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: 4 candidates x 20 examples = 80 scored calls, paid once at compile time.
- E2: the metric counts keywords, so the search finds the prompt that stuffs the most keywords. The metric and the goal disagree. The optimizer obeys the metric.
- E3: the metric must measure the real goal. A bad metric optimizes the wrong thing.

## C02

- E1: (plan, act), (act, observe), (observe, plan), (observe, done).
- E2: the framework drops history silently at 8k tokens. Long tasks lose their early steps and fail with no error message.
- E3: use a framework when the control flow is a real graph or the data plumbing is heavy. Hand-roll when the loop is simple and debuggability dominates.

## C03

- E1: sqrt(0.12 x 0.88 x 0.02) = sqrt(0.002112) = 0.046.
- E2: the critic rewards flattery. The generator learns to please the critic instead of improving the draft. The loop converges to praise.
- E3: workflows when the path is known (predictability, debuggability). Agents when the steps are unpredictable.

## C04

- E1: ReAct 7/0.9 = 7.78. Planning 5/0.75 = 6.67. Reflection 12/0.95 = 12.63 steps per success.
- E2: sqrt(0.95 x 0.05/20 + 0.9 x 0.1/20) = sqrt(0.006875) = 0.083. The 1-point gap sits inside the noise.
- E3: ReAct for unpredictable but checkable steps. Planning for stable environments. Reflection for costly, detectable errors.

## C05

- E1: 4/9 = 0.444, about 0.44.
- E2: the chart has no observe-to-reflect edge, so the agent can never transition to self-check. Reflection is unreachable by construction.
- E3: the chart must list every legal transition. An uncharted transition is a bug, not a feature.

## C06

- E1: 8000/500 = 16x compression.
- E2: sqrt(0.7 x 0.3/10) = sqrt(0.021) = 0.145.
- E3: the summary dropped the constraint. The agent never saw "no emails after 5pm" and violated it at step 40.

## C07

- E1: 50 steps x 20 tokens = 1000 tokens of notes.
- E2: the agent wrote a guess into the file. Later reads treat it as fact. The file launders the hallucination into memory.
- E3: files for exact facts (constraints, ids, counts). Vectors for fuzzy recall.

## C08

- E1: 8000/200 = 40x smaller.
- E2: the envelope omitted the aisle-seat constraint. B booked a middle seat. The task succeeded on paper and failed the user.
- E3: task, state, constraints, done.

## C09

- E1: blackboard 30 writes + 30 reads. Messages 30 sends + 30 receives, each agent reading its 10.
- E2: both agents wrote the plan section. The second write clobbered the first. The plan is now a merge conflict.
- E3: blackboard for tight collaboration on one artifact. Messages for privacy or loose coupling. Handoffs for strict sequences.

## C10

- E1: 0.9^3 = 0.729. 0.98^3 = 0.941.
- E2: failures avoided per run 0.212 x 10,000 = 2120 tokens saved. 2120/600 = 3.53, about 3.5x.
- E3: the agents share one wrong tool and fail together. Independence fails, so the product overestimates reliability.

## C11

- E1: (0.81 - 0.74)/(5 - 1) = 0.07/4 = 0.0175 per unit extra cost.
- E2: sqrt(0.07 x 0.93 x 0.02) = sqrt(0.001302) = 0.036.
- E3: the multi-agent ran on easier items. The score measures the eval split, not the architecture.

## C12

- E1: 5000 - 1500 = 3500 tokens saved per stuck run.
- E2: the observations differ trivially ("error 1", "error 2"), so exact-match stall detection never fires. The loop spins on noise.
- E3: each rule covers a failure mode the others miss. One brake is none when that brake fails.
