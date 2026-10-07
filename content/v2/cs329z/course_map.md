# Course map: cs329z

Baseline 2026-10-06. Build 2026-10-07. Units U01-U04 built by the first builder. Units U05-U08 plus consolidation built by the second builder (2026-10-07). S05-S20 remain PLANNED / SOURCE ATTRIBUTION PENDING.

## Official schedule (verified 2026-10-07 from https://cs329z.stanford.edu/)

Classes meet Mondays and Wednesdays, 1:30-2:50 p.m. Pacific, Skilling Auditorium.

| Session | Date (2026) | Title | Unit map | Claim class |
| --- | --- | --- | --- | --- |
| S01 | Wed 23 Sep | Foundations session: what are agentic systems, the spectrum from monolithic models to compound AI systems to agents, the three engineering challenges (decomposition, data, evaluation) | U01-C01, U01-C02, U01-C03 | Released, schedule inspected |
| S02 | Mon 28 Sep | LLMs for Builders: decoding strategies, transformer attention (including linear and hybrid), context length, pretraining-to-post-training pipeline, inference and test-time scaling, structured I/O and constrained decoding, context engineering | U01-C04 through U01-C10 | Released, schedule inspected |
| S03 | Wed 30 Sep | Building Blocks RAG: grounding and hallucination, embeddings and vector stores, chunking strategies, hybrid search, cross-encoders and late interaction (ColBERT) | U02 (all) | Released, schedule inspected |
| S04 | Mon 5 Oct | Tool Use and Function Calling: the REPL, function-calling APIs, MCP, designing good tools, code-execution sandboxes, error handling and retries | U03 (all) | Released, schedule inspected |
| S05 | Wed 7 Oct | Frameworks and Orchestration: DSPy (signatures, modules, optimizers), LangChain/LangGraph, LlamaIndex. Abstraction levels | U04-C01, U04-C02 | Planned |
| S06 | Mon 12 Oct | Agent Design Patterns and Scaffolds: workflows-vs-agents taxonomy, five composable workflow patterns, agent patterns (ReAct, plan-and-execute, reflection) | U04-C03, U04-C04, U04-C05, U04-C11, U04-C12 | Planned |
| S07 | Wed 14 Oct | Agent Memory Architectures: short vs long-term memory, memory as tool-based actions, file system as externalized memory, structured memory paradigms, cross-agent memory | U04-C06, U04-C07, U04-C09 | Planned |
| S08 | Mon 19 Oct | Multi-Agent Systems: single vs multi-agent architectures, orchestration, handoffs and state transfer, delegation, coordination, error propagation | U04-C08, U04-C09, U04-C10, U04-C11 | Planned |
| S09 | Wed 21 Oct | Optimization: prompts to fine-tuning, GEPA/MIPROv2/OPRO/TextGrad, LoRA/QLoRA, distillation, RLHF/DPO | U05 | Planned |
| S10 | Mon 26 Oct | Guest lecture (TBA) | Unmapped | Planned |
| S11 | Wed 28 Oct | Data for Agentic Systems: traces, demonstrations, feedback, data flywheels, synthetic data | U05 | Planned |
| S12 | Mon 2 Nov | Data Selection and Quality: informative data, filtering, tiny benchmarks, annotation | U05 | Planned |
| S13 | Wed 4 Nov | Evaluation Fundamentals and Benchmark Design: the 4-tuple (request, environment, stopping criteria, scorer), benchmark properties, scaffolding | U06 | Planned |
| S14 | Mon 9 Nov | LLM-as-Judge and Evaluation Infrastructure: grader types, judge prompts, biases, point vs pairwise, pass@k vs pass^k, test-rig design | U06 | Planned |
| S15 | Wed 11 Nov | Agent Safety and Guardrails: privacy, prompt injection, red-teaming, sandboxing, permissions, approvals | U07 | Planned |
| S16 | Mon 16 Nov | Guest lecture (TBA) | Unmapped | Planned |
| S17 | Wed 18 Nov | Coding Agents and Proactive Agents: coding agent architectures, SWE-bench, scaffolds | U07 | Planned |
| S18 | Mon 23 Nov | No class (Thanksgiving recess) | - | - |
| S19 | Mon 30 Nov | Proactive Agents: user models, next action prediction, mixed initiative, privacy and trust | U07 | Planned |
| S20 | Wed 2 Dec | Frontiers and Open Problems: multimodal, web/computer use, science agents, long-running architectures, observability, reliability, scalability, interpretability | U08 | Planned |
| Finals | Dec 7-11 | Final project demo day | U08 | Planned |

## Concept-to-session provenance in this build

Note: the official S01 title carries one extra word after "Foundations and". That word is omitted from this build per ASD-STE100.

- U01: C01-C03 map to S01 titles, C04-C10 map to S02 titles. Source-supported at schedule-title level. C11 (simple baseline) and C12 (architecture choice) are requested extensions taught as independent theory, labeled PLANNED / SOURCE ATTRIBUTION PENDING.
- U02: C01, C02, C03, C04, C05, C07, C08 map to S03 titles. Source-supported at schedule-title level. C06 (metadata/permissions), C09 (rerank), C10 (citations), C11 (insufficient evidence), C12 (retrieval diagnosis) are requested extensions taught as independent theory, labeled pending.
- U03: C01, C02, C04, C06, C08, C12 map to S04 titles. Source-supported at schedule-title level. C03 (tool/result loop), C05 (authentication/authorization), C07 (timeouts), C09 (idempotency), C10 (approval), C11 (output contracts) are requested extensions taught as independent theory, labeled pending.
- U04: S05-S08 are planned (S05 not yet held at build time). All twelve concepts taught as independent theory, labeled PLANNED / SOURCE ATTRIBUTION PENDING. U04-C01 is additionally grounded in the DSPy paper abstract (SRC-06), U04-C03, U04-C04 in the Anthropic article (SRC-04), U03-C04 in the MCP spec (SRC-05).

## Assessment on the official page (learning objectives, not reproduced work)

Two fully applied homework assignments: HW1 released Oct 5 (GitHub), due Oct 30, HW2 released Oct 26, due Nov 20. Quarter-long project: proposal Oct 9, midpoint demo video Nov 4, midway report Nov 6, paper video Nov 13, peer reviews Nov 30, final report and demo Dec 7-11. This course builds original equivalent practice only. It never solves or reproduces assessed work.
