# CS329A , Self-Improving AI Agents , Stanford Frontier AI Learning System v2

Course: Stanford CS329A, Self-Improving AI Agents, Autumn 2025.
Builders: first half (U01-U04 plus root identity set), second half
(U05-U08 plus consolidation).
Baseline: 2026-10-07.

## What this pack is

Original learning materials built from the verified official course schedule at
https://cs329a.stanford.edu/ and the pack inventory for course 11 (cs329a).
It teaches test-time compute and verification, feedback with tools and
constitutional learning, planning with search and train-time RL,
open-ended evolution with deep research, software-engineering and kernel
agents, memory and caches, reasoning with formal systems and autonomy, and
long-horizon evaluation with research projects. A different agent audits the
full course later.

## Honesty note

Autumn 2025 twenty-session schedule verified, including presentations and
guests, from the official course page on 2026-10-07. Required paper contents
must still be inspected individually before claiming full seminar coverage.
Papers not yet inspected are labeled PLANNED or SOURCE ATTRIBUTION PENDING in
`source_manifest.md` and at point of use in lessons. Claim classification
carries dates. Presentations and guests are taught only at the level honestly
inspected, which for guest talks is the scheduled topic line from the official
schedule, not the talk content.

## Units built here

- U01 Test-time compute and verification (12 concepts, cs329a-U01-C01..C12)
- U02 Feedback, tools, and constitutional learning (12 concepts, cs329a-U02-C01..C12)
- U03 Planning, search, and train-time RL (12 concepts, cs329a-U03-C01..C12)
- U04 Open-ended evolution and deep research (12 concepts, cs329a-U04-C01..C12)
- U05 Software-engineering and kernel agents (12 concepts, cs329a-U05-C01..C12)
- U06 Memory, caches, and long-context representations (12 concepts, cs329a-U06-C01..C12)
- U07 Reasoning, formal systems, and autonomy (12 concepts, cs329a-U07-C01..C12)
- U08 Long-horizon evaluation and research projects (12 concepts, cs329a-U08-C01..C12)

96 concept rows in this build. Every row ends TAUGHT+ASSESSED or
SOURCE-UNREACHABLE with evidence in `coverage_matrix.md`.

## Directory map

- `lessons/` : u01-u08 lesson files, full 15-item contract per concept.
- `keys/` : exercise answer keys, separate from lessons.
- `labs/` : one lab per unit with an executed reference script in `labs/runs/`,
  lab answer keys in `labs/keys/`.
- `visuals/` : matplotlib render scripts `render_u01.py`..`render_u08.py` and
  computed PNG figures. Every render script strips PNG metadata in main().
- `interview/` : per-unit question banks and separate keys at the prompt
  quotas: six breadth questions, two deep ladders of eight follow-ups, two
  analytical exercises, one implementation or debug task, two
  changed-constraint scenarios, one research-critique question. Plus
  `transfer-sets.md` + `keys-transfer.md` (10 changed-scenario sets) and
  `oral-defenses.md` + `keys-oral.md` (10 deep ladders x 8 follow-ups).
- `capstones/` : one research capstone and one applied capstone, each with a
  full executed run script (`run_research_capstone.py`,
  `run_applied_capstone.py`), computed figures in `capstones/figs/`, and
  full docs. The first build's pilot scripts are superseded under
  `capstones/superseded/`.
- `crash-course.md`, `cheatsheet.md` : synthesized from all 8 units.
- `diagnostics/` : entry diagnostic plus key.
- Root files: `state.md`, `source_manifest.md`, `source_gaps.md`,
  `course_map.md`, `index.md`, `prerequisites.md`, `notation_and_shapes.md`,
  `glossary.md`, `currentness.md`, `coverage_matrix.md`, `visual_audit.md`,
  `mastery_ledger.md`, `errors.md`, `role_gap_map.md`.

## Claim classes used in this build

- VERIFIED: inspected directly by the builder on the dated official source.
- PLANNED: requested by the inventory, not yet taught or inspected.
- SOURCE ATTRIBUTION PENDING: taught from requested inventory content, exact
  source artifact not yet individually inspected.
- TAUGHT+ASSESSED: lesson contract complete plus assessment with a key.
- SOURCE-UNREACHABLE: source could not be reached, with evidence recorded.

## Rules that bind this build

1. ASD-STE100 on every deliverable, including .py scripts. Zero hard fails.
2. Watermark remover Layer A on every deliverable before delivery.
3. Visual system from the prompt pack binds every figure. Matplotlib-computed
   figures preferred. Every PNG passes a chunk audit (IHDR/IDAT/IEND only).
4. No invented numbers, timestamps, benchmarks, or test results. Toy numbers
   are computed and traceable. Lab scripts run and record observed output.
5. Academic integrity: homework learning objectives feed original equivalent
   practice. No solutions to assessed work. No exam dumps.

## Shared prerequisites

Prerequisite bridges P01-P24 live at
`../shared/prerequisites/`. This course links them and adds local remediation
in `prerequisites.md`. It does not rebuild them.
