# CS329Z: Engineering AI Agents (v2 crash course)

Builder scope: U01-U08 plus the root identity set (first builder: U01-U04 + root. Second builder: U05-U08 + consolidation, 2026-10-07). A separate agent audits the full course later (RUN 6).

## What this is

An independent crash course that teaches compound AI systems from first principles: what separates a model from a system, decomposition, LLM internals for builders, retrieval and evidence engineering, tool use and protocols, runtime safety, frameworks and workflows, memory, and multi-agent coordination. Each concept carries the full 15-item lesson contract, computed toys, original code, labs, figures, and interview banks with separated answer keys.

## Honesty note

Fall 2026 schedule verified. Initial four sessions precede baseline. Every later scheduled family must map to an explicit subunit and keep planned/released/inspected distinctions. Sessions S01-S04 (Sep 23, Sep 28, Sep 30, Oct 5) precede the Oct 6 baseline and carry released slide links. This build inspects the official schedule text only and treats slide decks as linked but not opened. Session S05 (Oct 7) and all later sessions are PLANNED / SOURCE ATTRIBUTION PENDING until artifact-verified. Concepts that map to released session titles are labeled source-supported at title level. Everything else is independent theory with the same pending label. Nothing in this course claims instructor authorship, and no unpublished course material is reproduced.

## Map

- `course_map.md`, session-to-unit map with claim classification and dates.
- `index.md`, every file in this course with one-line purpose.
- `lessons/`, U01-U08 lesson files, one per unit, 12 concepts each, full 15-item contract per concept.
- `answer_keys/`, lesson exercise keys, kept separate from lessons.
- `labs/`, one lab per unit plus `*_lab_keys.md` with execution-verified outputs.
- `interview/`, per-unit question banks and separate keys at the prompt quotas, plus 10 transfer sets and 10 oral-defense ladders with separate keys.
- `visuals/`, committed matplotlib render scripts (`render_uXX_fNN.py`) and their PNG outputs.
- `capstones/`, per-unit proposed designs plus two executed capstones (research replication, applied/FDE).
- `prerequisites.md`, prerequisite graph, links to shared P01-P24 bridges, local remediation, diagnostic.
- `diagnostics/`, diagnostic answer key.

## Status

See `state.md` for the build checkpoint. See `coverage_matrix.md` for the 96 owned rows and their statuses (96/96 TAUGHT+ASSESSED). See `crash-course.md` and `cheatsheet.md` for the all-units synthesis. See `source_gaps.md` for unresolved gaps with evidence. See `errors.md` for known risks.

## Rules that bind this course

1. ASD-STE100: `~/workspace/skills/ste-lint/bin/ste_check.py`, zero hard fails on every deliverable including `.py` scripts.
2. `~/workspace/skills/watermarks-remover/bin/wm_clean.py` Layer A on every deliverable.
3. Visual system in `~/workspace/prompt-pack-v2/frontier_ai_prompt_pack_v2/visual_system_generic.md` binds every figure. Matplotlib-computed preferred. Every PNG is PIL-verified (IHDR/IDAT/IEND only) and metadata-stripped in the render script.
4. No invented numbers, timestamps, benchmarks, or test results. No exam dumps. No auth bypass.
5. Write only under `~/workspace/stanford-frontier-ai/v2-pack/cs329z/`.
