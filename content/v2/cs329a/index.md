# index.md , cs329a

Course: Stanford CS329A, Self-Improving AI Agents, Autumn 2025.
Baseline: 2026-10-07. Builders: first half (U01-U04), second half
(U05-U08 + consolidation).

## Start here

1. Read `README.md` for the honesty note and claim classes.
2. Take `diagnostics/diagnostic.md`. Check it against
   `diagnostics/diagnostic_key.md`.
3. Read `prerequisites.md` for links to the shared bridges and local
   remediation.
4. Work units in order: U01 through U08.
5. Each unit: lesson file, exercises (keys in `keys/`), lab (`labs/` plus
   executed run script), visuals (`visuals/`), interview bank
   (`interview/`), then the capstones and consolidation practice.

## Unit entries

### U01 Test-time compute and verification
Lesson: `lessons/u01_test_time_compute.md`. 12 concepts: repeated sampling,
best-of-N, self-consistency, inference architecture search, compute
allocation, generator/verifier gap, weak verifiers, outcome/process reward,
verifier training, calibration, selection bias, cost-success curves.
Sessions 2-3 of the official schedule.

### U02 Feedback, tools, and constitutional learning
Lesson: `lessons/u02_feedback_tools.md`. 12 concepts: ReAct, execution
feedback, code/tests, RLEF reading, critique versus learning update,
constitutional feedback, reward signals, constraints, tool errors, policy
updates, shortcut exploitation, independent validation. Session 4 of the
official schedule.

### U03 Planning, search, and train-time RL
Lesson: `lessons/u03_planning_search.md`. 12 concepts: tree search, adaptive
branching, decomposition, parallel planning/execution, multi-step credit,
synthetic traces, STaR, reasoning RL, DAPO/GRPO reading, on-policyness,
budget, reward validity. Sessions 5-6 of the official schedule.

### U04 Open-ended evolution and deep research
Lesson: `lessons/u04_open_evolution.md`. 12 concepts: agent architecture
search, candidate mutation, selection, AI Scientist/AlphaEvolve readings,
code-generation search, AlphaCode/AlphaCode2, search-enhanced reasoning,
evidence provenance, holdout separation, resource budgets, novelty claims,
safe iteration. Sessions 7-9 of the official schedule.

### U05 Software-engineering and kernel agents
Lesson: `lessons/u05_swe_kernel_agents.md`. 12 concepts: CodeMonkeys,
test-time code search, execution-grounded feedback, KernelBench,
performance versus correctness, agent-system interface, profiling,
flaky tests, hidden test leakage, sandboxing, reproducibility, rollback.
Session 13 of the official schedule.

### U06 Memory, caches, and long-context representations
Lesson: `lessons/u06_memory_caches.md`. 12 concepts: MemGPT, memory
actions, context versus persistence, Cartridges/self-study, cache reuse,
CacheBlend, retrieval, compression loss, invalidation, tenant privacy,
cross-task transfer, controlled comparison. Session 14 of the official
schedule (guest Junchen Jiang, schedule line only).

### U07 Reasoning, formal systems, and autonomy
Lesson: `lessons/u07_reasoning_formal.md`. 12 concepts: guest reasoning
evidence, AlphaProof/formal verification, AlphaGeometry,
conjecture/search/proof distinctions, symbolic environment, autonomy
limits, robot perception/action, multimodal feedback, sim-to-real scope,
safety, trace validity, guest gaps. Sessions 15, 16, 18, 19 of the
official schedule (guests at schedule-line level only).

### U08 Long-horizon evaluation and research projects
Lesson: `lessons/u08_long_horizon_eval.md`. 12 concepts: task duration,
economically valuable tasks, GDPVal, DeepScholar-Bench, success versus
reliability, stopping, judge contamination, budgets, ablations, project
milestones and poster, negative results, open questions. Session 17 of
the official schedule.

## Reference

- `glossary.md`: one-line definitions for every course term.
- `notation_and_shapes.md`: symbols, units, shapes.
- `coverage_matrix.md`: 96 rows with status and evidence.
- `crash-course.md`: the whole course in one pass.
- `cheatsheet.md`: dense reference, formulas and decision rules.
- `mastery_ledger.md`, `errors.md`: learning evidence and mistake log.
- `role_gap_map.md`: research, research engineering, FDE, ML, LLM, MLOps,
  and agent role bridges with residual gaps.
- `currentness.md`: what is dated and what stays current.
