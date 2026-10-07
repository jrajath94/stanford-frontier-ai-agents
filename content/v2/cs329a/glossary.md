# glossary.md , cs329a U01-U08

- Advantage: how much better an action is than the average action in a state.
- AlphaCode: system for competition-level code generation with large-scale
  sampling, filtering, and clustering. Source attribution pending.
- AlphaEvolve: evolutionary coding agent for algorithm design.
  Source attribution pending.
- Architecture search (inference): search over inference-time techniques
  and their settings for a task. Source attribution pending.
- Best-of-N: draw N samples, return the one with the highest verifier score.
- Calibration: match between stated confidence and observed accuracy.
- Constitutional AI: training with AI-generated feedback guided by a written
  constitution of principles. Source attribution pending.
- Cost-success curve: task success as a function of inference compute budget.
- Critique: judgment of output that does not change model weights.
- DAPO: open-source LLM reinforcement learning system at scale.
  Source attribution pending.
- Decomposition: split a task into subtasks solved separately.
- Execution feedback: signal from running code or a tool, such as a test
  result or an error trace.
- Generator/verifier gap: difference between the ability to produce a
  correct answer and the ability to recognize one.
- GRPO: group-relative policy optimization, advantages computed against a
  group baseline instead of a learned value model. Source attribution
  pending.
- Holdout separation: a locked test set kept apart from all selection and
  tuning decisions.
- Independent validation: a separate check with its own data and rules,
  not tuned on the system it judges.
- LATS: language agent tree search, unifying reasoning, acting, and
  planning. Source attribution pending.
- On-policy: training data drawn from the current policy.
- Outcome reward: scalar feedback on the final result only.
- Pass@N: probability that at least one of N independent samples is correct.
- Process reward: scalar feedback on intermediate steps.
- ReAct: loop of thought, action, and observation for tool use.
  Source attribution pending.
- Reward hacking: the policy exploits a flaw in the reward instead of the
  intended task. Also called shortcut exploitation.
- RLEF: reinforcement learning from execution feedback.
  Source attribution pending.
- Selection bias: systematic error from choosing samples by a biased score.
- Self-consistency: sample several reasoning paths, take the majority
  answer.
- STaR: bootstrap reasoning by training on self-generated rationales that
  lead to correct answers. Source attribution pending.
- Test-time compute: inference budget spent per query, such as samples,
  search steps, or verifier calls.
- Tree search: explore action sequences as a tree of states.
- Verifier: model or rule that scores candidate outputs.
- Weak verifier: a verifier weaker than the generator that still helps
  selection. Source attribution pending.

- Ablation delta: full-system score minus score with one component removed. Causal, not correlational.
- AlphaGeometry: neuro-symbolic geometry prover: the net proposes constructions, the symbolic engine closes by deduction. Source attribution pending.
- AlphaProof: formal mathematics proving with learning-guided search. Source attribution pending.
- Amdahl's law: speedup = 1/((1-f) + f/s). The unoptimized share caps everything.
- Archival store: MemGPT's cold tier: evicted facts paged out of main context, returned via search.
- Autonomy envelope: authority must not exceed verified capability, with margin.
- Blind-spot question: a question where the generator and a contaminated verifier share the failure mode.
- CacheBlend: reuse non-prefix chunk KV caches. Recompute only high-deviation tokens. Source attribution pending.
- Cartridge: a small trained KV cache per corpus, built by self-study. Source attribution pending.
- CodeMonkeys: SWE-agent scaling: serial iterations raise coverage, parallel width amortizes context. Source attribution pending.
- Contamination gap: same-model judge agreement minus independent-judge agreement.
- DeepScholar-Bench: live benchmark for research synthesis: synthesis, retrieval quality, verifiability. Source attribution pending.
- Deviation check: CacheBlend's scan for high-KV-deviation tokens before selective recompute.
- Duration curve: task success rate versus task duration in hours.
- fast_p: share of kernels both correct and at least p times faster than reference.
- Flaky test: a test that passes or fails nondeterministically.
- Gate: a project milestone with exit criteria and a kill rule.
- GDPVal: benchmark of economically valuable tasks with blinded expert comparison. Source attribution pending.
- Hidden test leakage: the agent sees or infers the hidden tests it is graded on.
- Judge contamination: the judge shares the generator's training and blind spots.
- Kernel (proof): the trusted checker that accepts or rejects a formal proof step.
- KernelBench: benchmark: rewrite a PyTorch reference as a fast GPU kernel. Source attribution pending.
- KV cache: stored keys and values of past tokens. The working memory of inference.
- LMCache: guest-topic KV cache sharing system (schedule line only). Source attribution pending.
- Mean-min flip: the mean picks one agent, the minimum picks the other.
- MemGPT: agent that pages its own memory between main context and archival storage. Source attribution pending.
- Negative result: a preregistered hypothesis rejected with power. Reported, not filed away.
- Optimal stopping: continue while the next step's expected value beats its cost.
- Preregistration: the falsification is written before the run, so the measurement decides.
- Profiling: measuring where time goes before optimizing.
- Reality gap: simulator success minus real-world success.
- Sandboxing: running untrusted agent code in an isolated environment.
- Selection trajectory: the final pick among candidate trajectories in a SWE-agent pipeline.
- Self-study: training a Cartridge on synthetic conversations distilled from a corpus.
- Serial depth: refinement iterations per trajectory in test-time code search.
- Sim-to-real: transferring a policy trained in simulation to the real world.
- Stopping rule: stop when marginal gain falls below marginal cost.
- Tactic: one proof step in a formal proof assistant.
- Task value: hours saved times the hourly rate of that time.
- Trace faithfulness: a trace is faithful iff flipping its cited fact changes the behavior.
- Value capture: the share of total task value the agent's successes represent.
- Verifier-weighted voting: the hybrid: weight each sample's vote by its verifier score.
- Wilson interval: a confidence interval for a binomial rate, used on all toy success rates.
