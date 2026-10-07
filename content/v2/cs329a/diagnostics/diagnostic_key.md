# Diagnostic key , cs329a U01-U08

D1. Failure probability per sample is 0.7. All five fail with probability
0.7^5 = 0.16807. At least one succeeds with probability 1 - 0.16807 =
0.83193, about 0.83.

D2. Two ways: (a) the verifier scores a wrong but fluent sample highest,
so selection beats the majority, (b) the verifier score correlates with
length or style, and the correct sample loses on that bias.

D3. A verifier is calibrated when its stated confidence matches its
observed accuracy. Toy: scores 0.9, 0.9, 0.9, 0.9 on four samples where
only one is correct. Stated confidence 0.9, observed accuracy 0.25.
Miscalibrated high.

D4. Thought, Action, Observation, in that order. The action calls a tool.
The observation is the tool result. The next thought reads it.

D5. Failure classes: (a) transient tool fault, such as a timeout, recovery
is retry with backoff. (b) malformed agent request, such as a bad
argument, recovery is repair the call from the error message and resend.

D6. A critique judges output without changing weights, for example "this
function ignores empty input". A learning update changes the policy, for
example a gradient step on the corrected trajectory.

D7. The step that caused success deserves the credit, but the trajectory
alone does not say which step that was. Missing: a per-step value signal
or a controlled ablation that changes one step at a time.

D8. On-policy means the data used for an update came from the current
policy. Off-policy without correction biases the gradient toward stale
behavior and the policy can collapse to actions the old data favored.

D9. Full expansion: 3^4 = 81 leaves. Prune half the branches at each
depth: 1.5 is not an integer branch count, with floor, 1 branch per depth
gives 1 leaf, with the intended reading of keeping half the children at
each node, leaves are (3/2)^4 = 5.06, so the honest answer is that the
question needs an integer rule. Accept: 81 full, about 5 with exact halves,
or 16 if you keep 2 of 3 children each level (2^4).

D10. Leaks: (a) tuning the mutation operator on the validation set, then
reporting on it, (b) reusing validation prompts in training traces. Rule:
lock a held-out test set before evolution starts, and report selection
decisions only from the validation split.

D11. Hypothesis: raising the search budget from N to 4N raises the
task success rate. Refutation: measured success rate at 4N is equal to or
below the rate at N across three seeds with matched total compute.

D12. Three rules: no network access outside an allowlist, no writes
outside the task directory, every run logged with the exact command and
seed, and a kill switch on wall-clock time.

D13. Intensity = 0.4e9 FLOP / 2e6 bytes = 200 FLOP per byte. Ridge
point = 50e12 / 1e12 = 50 FLOP per byte. 200 > 50, so the kernel is
compute-bound: it asks for more FLOPs per byte than the machine's
balance point.

D14. Four declarations: the tool name, the argument schema with types,
the return schema, and the side effects plus limits (writes, network,
timeout, cost).

D15. Four items: the exact code version (commit hash), the full
configuration (model, prompts, tool versions), the random seeds, and
the complete input plus environment state.

D16. KV bytes = 2 * 12 * 8 * 1000 * 64 * 2 = 24,576,000 bytes, about
24.6 MB. The leading 2 counts keys plus values.

D17. Precision-first is right when retrieved noise poisons the agent's
reasoning, so each returned fact must be trustworthy. Recall-first is
right when a missing fact fails the task, so coverage matters more than
purity.

D18. Context is the working memory the model sees right now, limited
and transient. Persistence is the durable store that survives across
sessions. Example: the current user request belongs in context, the
user's standing preferences belong in persistence.

D19. The kernel checks every proof step against fixed logical rules, so
its yes cannot be swayed by fluent but wrong text, while the proposer's
confidence is just a learned guess.

D20. Credit assignment is the problem of deciding which of the many
proposed tactics deserves the reward when only the final proof verdict
is observed.

D21. Flip the fact the trace cites and rerun the agent, holding
everything else fixed. Verdict: the trace is faithful iff the behavior
changes, otherwise it is a story.

D22. Rate p = 0.30. SE = sqrt(p * (1 - p) / n) = sqrt(0.30 * 0.70 /
100) = sqrt(0.0021) = 0.0458, about 0.046.

D23. The minimum is the right metric when one bad task means a
production failure, so the shipping number is the worst case, not the
average. Here the minimum picks B (0.70 beats 0.55).

D24. Judge contamination is shared bias between the generator and the
judge that inflates agreement scores without reflecting quality. One
detection: compare the same-model judge's agreement with an
independent-model judge's agreement on the same outputs.
