# prerequisites.md , cs329a

Shared bridges live at `../shared/prerequisites/`. Link, do not rebuild.
Each unit below names its bridge files plus the local remediation taught
inside this course.

## U01 Test-time compute and verification

- `../shared/prerequisites/p07_estimation.md`: sampling, estimators, standard
  errors, confidence intervals, calibration. Local remediation: lesson C01
  re-derives pass@N from Bernoulli sampling before any curve is drawn.
- `../shared/prerequisites/p14_transformer.md`: next-token sampling,
  temperature, top-p. Local remediation: lesson C01 defines a sample as one
  full decoded completion with a fixed decoding policy.
- `../shared/prerequisites/p22_experiments.md`: baselines, seeds, uncertainty.
  Local remediation: lesson C12 states seed and budget before each curve.

## U02 Feedback, tools, and constitutional learning

- `../shared/prerequisites/p17_rl.md`: rewards, policies, policy gradients.
  Local remediation: lesson C07 defines a reward signal as a scalar attached
  to a step or an episode before RLEF is discussed.
- `../shared/prerequisites/p20_tools.md`: tool-call/result loop, state,
  budgets. Local remediation: lesson C01 restates the ReAct loop as
  thought, action, observation triples with a typed trace.
- `../shared/prerequisites/p21_security.md`: trust boundaries, least
  privilege, prompt injection. Local remediation: lesson C12 treats the
  independent validator as a trust boundary and lists what it must not see.

## U03 Planning, search, and train-time RL

- `../shared/prerequisites/p09_optimization.md`: objectives, constraints,
  gradients. Local remediation: lesson C11 frames the compute budget as a
  hard constraint in the planning objective.
- `../shared/prerequisites/p17_rl.md`: value functions, credit assignment,
  on-policy versus off-policy. Local remediation: lesson C05 re-derives
  multi-step credit from a three-step toy before STaR and GRPO appear.
- `../shared/prerequisites/p20_tools.md`: tool environments and state.
  Local remediation: lesson C04 defines a plan node as a state plus a
  pending subplan before parallel execution is discussed.

## U04 Open-ended evolution and deep research

- `../shared/prerequisites/p20_tools.md`: code execution sandboxes.
  Local remediation: lesson C12 lists the sandbox rules before any
  self-modifying loop is designed.
- `../shared/prerequisites/p22_experiments.md`: holdouts, novelty claims,
  negative results. Local remediation: lessons C08, C09, C11 teach evidence
  provenance and holdout separation as first-class mechanisms, not asides.

## Diagnostic

`diagnostics/diagnostic.md` probes all four bridge groups with 12 questions.
`diagnostics/diagnostic_key.md` carries the key. The mastery ledger records
that no learner answers are invented, the diagnostic is a self-check tool.

## Not-yet-understood dependency rule

Every lesson file ends with a numbered dependency list for concepts the
learner may still lack. The list points at the bridge file and the local
remediation section, never at another course alone.
