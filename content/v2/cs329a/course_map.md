# course_map.md , cs329a

## Unit graph (full course: U01-U08)

```
U01 Test-time compute and verification
  needs P07 (estimation), P14 (transformer), P22 (experiments)
  feeds U03 (search uses sampling), U05 (selection for code),
  U08 (evaluation of compute tradeoffs)

U02 Feedback, tools, and constitutional learning
  needs P17 (RL), P20 (tools), P21 (security)
  feeds U03 (tool traces feed train-time RL), U05 (code agents)

U03 Planning, search, and train-time RL
  needs P09 (optimization), P17 (RL), P20 (tools)
  feeds U04 (search drives evolution), U07 (proof search),
  U08 (long-horizon eval)

U04 Open-ended evolution and deep research
  needs P20 (tools), P22 (experiments)
  feeds U08 (project frame), capstones

U05 Software-engineering and kernel agents
  needs P12, P15, P20, P22
  feeds U08 (agent eval), capstones
  session 13 (Nov 3), Agentic Frameworks for Software Engineering

U06 Memory, caches, and long-context representations
  needs P14, P19, P20
  feeds U07 (memory for long proofs), U08 (long-horizon tasks)
  session 14 (Nov 7), guest Junchen Jiang (LMCache, schedule line only)

U07 Reasoning, formal systems, and autonomy
  needs P17, P20, P22
  feeds U08 (verifiers and judges), capstones
  sessions 15 (Denny Zhou), 16 (Thang Luong), 18 (Misha Laskin),
  19 (Danny Driess). Guests at schedule-line level only

U08 Long-horizon evaluation and research projects
  needs P07, P22, P24
  feeds capstones, open questions
  session 17 (Nov 17), Agentic Evaluations and Long-Horizon Tasks
```

## Session mapping to the official Autumn 2025 schedule

| Unit | Sessions | Papers anchor |
|---|---|---|
| U01 | 2 (Sep 26), 3 (Sep 29) | repeated sampling, best-of-N, self-consistency, inference architecture search, verification |
| U02 | 4 (Oct 3) | ReAct, execution feedback, constitutional AI |
| U03 | 5 (Oct 6), 6 (Oct 10) | tree search, decomposition, parallel planning, STaR, reasoning RL, DAPO/GRPO |
| U04 | 7 (Oct 13), 8 (Oct 17), 9 guest (Oct 20) | agent architecture search, AI Scientist, AlphaEvolve, AlphaCode, deep research |
| U05 | 13 (Nov 3) | CodeMonkeys serial/parallel scaling, KernelBench, fast_p |
| U06 | 14 (Nov 7), guest Junchen Jiang | MemGPT, CacheBlend, Cartridges, LMCache (guest line only) |
| U07 | 15 (Nov 10), 16 (Nov 14), 18 (Nov 21), 19 (Dec 1), guests Denny Zhou, Thang Luong, Misha Laskin, Danny Driess | LLM reasoning, AlphaProof/AlphaGeometry, autonomy, robotics (guest lines only) |
| U08 | 17 (Nov 17) | GDPVal, DeepScholar-Bench, duration curves, judge contamination, project gates |

## File map per unit

| Unit | Lesson | Keys | Lab | Lab key | Visuals | Interview |
|---|---|---|---|---|---|---|
| U01 | lessons/u01_test_time_compute.md | keys/u01_answers.md | labs/u01_lab.md | labs/keys/u01_key.md | visuals/render_u01.py, u01_fig01..03.png | interview/u01_questions.md, u01_key.md |
| U02 | lessons/u02_feedback_tools.md | keys/u02_answers.md | labs/u02_lab.md | labs/keys/u02_key.md | visuals/render_u02.py, u02_fig01..03.png | interview/u02_questions.md, u02_key.md |
| U03 | lessons/u03_planning_search.md | keys/u03_answers.md | labs/u03_lab.md | labs/keys/u03_key.md | visuals/render_u03.py, u03_fig01..03.png | interview/u03_questions.md, u03_key.md |
| U04 | lessons/u04_open_evolution.md | keys/u04_answers.md | labs/u04_lab.md | labs/keys/u04_key.md | visuals/render_u04.py, u04_fig01..03.png | interview/u04_questions.md, u04_key.md |
| U05 | lessons/u05_swe_kernel_agents.md | keys/u05_answers.md | labs/u05_lab.md | labs/keys/u05_key.md | visuals/render_u05.py, u05_fig01..03.png | interview/u05_questions.md, u05_key.md |
| U06 | lessons/u06_memory_caches.md | keys/u06_answers.md | labs/u06_lab.md | labs/keys/u06_key.md | visuals/render_u06.py, u06_fig01..03.png | interview/u06_questions.md, u06_key.md |
| U07 | lessons/u07_reasoning_formal.md | keys/u07_answers.md | labs/u07_lab.md | labs/keys/u07_key.md | visuals/render_u07.py, u07_fig01..03.png | interview/u07_questions.md, u07_key.md |
| U08 | lessons/u08_long_horizon_eval.md | keys/u08_answers.md | labs/u08_lab.md | labs/keys/u08_key.md | visuals/render_u08.py, u08_fig01..03.png | interview/u08_questions.md, u08_key.md |

Capstones: capstones/research_capstone.md, capstones/applied_capstone.md,
with pilot scripts superseded to capstones/superseded/pilot_research.py
and capstones/superseded/pilot_applied.py.
