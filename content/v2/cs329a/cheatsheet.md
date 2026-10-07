# Cheatsheet , cs329a

One page per unit is the goal. This is the dense reference.
Formulas, decision rules, toy numbers, failure modes. Detail in
`lessons/`. The fast pass in `crash-course.md`.

## U01 test-time compute

- pass@N = 1-(1-p)^N. p=0.25, N=5: 0.76.
- Best-of-N: sample N, keep verifier's top. Needs verifier
pairwise accuracy > 0.60. Below 0.55 it is untestable.
- Self-consistency: sample N, majority vote. Needs per-sample
accuracy above chance.
- Matched budget: N_sc * gen = N_bon * (gen + score).
- Selection bias: check score-vs-length correlation.
- Cost-success curve is concave: read it before allocating.

## U02 feedback and tools

- ReAct: thought -> action -> observation -> answer.
- Execution feedback = ground truth. Self-critique = opinion.
- Tool error: read it, fix, retry once. Then replan.
- Shortcut: the agent edits the test. Catch with independent
validation (separate judge, locked tests).
- Critique changes the try. A gradient changes the weights.

## U03 planning and search

- Tree search: state, action, reward. Random hit rate:
correct-leaves / branching^depth.
- Perfect verifier: free node labels. Learn only the policy.
- Reward validity: correlate reward with truth on held-out
traces before trusting search.
- Budget binds: fix budget, then tune. Never the reverse.

## U04 open evolution

- Loop: vary, select, inherit. Selection pressure = fraction
that reproduces.
- Deceptive proxy: selection grows what it measures.
- Holdout rule: champion scored on unseen data with the true
metric. Gap = deception meter.
- Kill rule: a gate without teeth is theater.

## U05 SWE and kernel agents

- Coverage: 0.832 (S=1) to 0.997 (S=5) at K=8. Depth buys
coverage. Width amortizes context (25.0% -> 7.7%).
- Selection: generate, vote with generated tests, final
trajectory.
- fast_p: correct AND >= p x faster. Toy: correctness 0.60,
fast_1 0.40.
- Amdahl: speedup = 1/((1-f) + f/s). 2x on 60%: 1.43x.
Ceiling 1/(1-f) = 2.5x.

## U06 memory and caches

- CacheBlend: recompute high-deviation tokens only. Toy:
2048 -> 307 + 64 check = 5.52x.
- MemGPT: 8 hot slots, 12 paged to archival, 5-search recall
index. Evict the coldest. Search returns them.
- Cartridge: trained KV per corpus. 20,480 -> 512 slots
(40x). Training amortizes over queries.

## U07 reasoning, formal, autonomy

- Proof search: goal, tactic, kernel. Random (1/12)^4.
guided (1/3)^4.
- AlphaGeometry: net proposes, engine deduces.
- Report search nodes and proof steps separately.
- Reality gap: sim - real. Randomize to narrow it.
- Envelope: authority <= verified capability + margin.
- Faithful trace: flip the cited fact. Behavior must change.

## U08 long-horizon eval

- Duration curve: success vs hours. Toy: 0.90 -> 0.35.
- Value = hours x rate. Score where the money is.
- GDPVal: blinded pairwise win rate. SE = sqrt(p(1-p)/n).
- DeepScholar: synthesis / retrieval / verifiability.
- Ship on the min, not the mean.
- Stop: continue while marginal value > marginal cost.
- Contamination gap = same-model agreement - independent
agreement.
- Budget fuels: agent + judge + audit. The audit binds.
- Ablation delta = full - removed. Causal, not correlational.

## Cross-unit rules

- Generate candidates, verify cheaply, select honestly.
- The verifier/judge is part of the apparatus: calibrate it,
measure its bias, keep it at a distance.
- Report the tail (min), the cost (budget), and the negative
(null with power).
- A gate without a kill rule is theater. A metric without a
falsification is a wish.
