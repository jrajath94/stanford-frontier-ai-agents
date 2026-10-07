# U04 capstone: ReAct vs plan-and-execute on surprise tasks (proposed, not executed)

Status: design only. No experiment has run. All numbers below are planned, not measured.

## Replication

Reproduce the C04 toy comparison: 60 synthetic tasks, 30 with predictable steps and 30 with one surprise observation mid-task. Run ReAct, plan-and-execute, and reflection (stub model, seeded). Success criterion: the accuracy ranking reflection >= ReAct > planning on surprise tasks, and planning cheapest per success on predictable tasks.

## Extension

Question: does a surprise detector (replan when the observation contradicts the plan) close the gap between planning and ReAct?

Falsifiable hypothesis: plan-and-execute with a replan trigger matches ReAct accuracy on surprise tasks at lower step cost.

Literature: agent patterns (planned S06), ReAct/plan/reflection from U04-C04.

Data: 60 synthetic tasks with scripted observations. No human data.

Baselines: ReAct. Plan-and-execute. Plan-and-execute with replan. Reflection.

Matched budgets: step budgets equated per arm where the comparison needs it. Otherwise report cost per success.

Metrics: task success rate, steps per task, cost per success.

Controls: same tasks, same stub, same seeds.

Ablations: surprise rate {0, 1, 3} per task.

Seed variation: 5 seeds. Report means and standard errors.

Uncertainty: binomial intervals on success rates. Paired tests across arms.

Failure criteria: if the replication shows planning beating ReAct on surprise tasks, the surprises are not surprising. Redesign the task set.

Reproducibility: task scripts, stub code, and seeds committed.

Negative results: if the replan trigger never fires, report it. The detector is miscalibrated.

Limitations: scripted surprises, not real environments. No claim about real agents.

Ethical considerations: none. Synthetic data, no human subjects.
