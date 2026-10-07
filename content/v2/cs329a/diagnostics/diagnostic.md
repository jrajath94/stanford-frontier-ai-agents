# Entry diagnostic , cs329a U01-U08

Answer closed-book. Then check `diagnostic_key.md`. Record confident
mistakes in `errors.md`. This diagnostic is a self-check tool. No learner
answers are invented or recorded.

## Estimation and sampling (U01 bridges)

D1. A generator answers a question correctly with probability 0.3 on each
independent sample. You draw 5 samples. What is the probability that at
least one sample is correct? Show the steps.

D2. In D1, a verifier picks the highest-scoring sample. Name two ways the
verifier can make the final answer worse than the majority vote.

D3. Define calibration for a verifier in one sentence, then give a toy with
four scored samples where the verifier is miscalibrated.

## Tools and agents (U02 bridges)

D4. Write the three fields of one ReAct step and the order they appear in.

D5. A tool returns an error string instead of a result. List two different
failure classes this can belong to, and one recovery action for each.

D6. What is the difference between a critique and a learning update? Give
one concrete example of each for a code agent.

## RL and planning (U03 bridges)

D7. A three-step trajectory earns reward 1 only at the final step. A
policy-gradient update changes all three step probabilities. Which step
deserves the credit, and what information would settle it?

D8. Define on-policy in one sentence. Then state one failure that follows
when a reasoning-RL run goes off-policy without correction.

D9. A search tree with branch factor 3 and depth 4. How many leaf nodes
does full expansion visit? If you prune half the branches at each depth,
how many leaves remain?

## Experiments and safety (U04 bridges)

D10. You evolve agent prompts and select on a validation set. Name two
leaks that can inflate the reported score, and the holdout rule that stops
each.

D11. Define a falsifiable hypothesis for the claim "more search always
helps". State the observable result that would refute it.

D12. List three sandbox rules for an agent that edits and runs its own
code.

## Code, hardware, interfaces (U05 bridges)

D13. A kernel moves 2 MB of data and performs 0.4 GFLOP. Compute its
arithmetic intensity in FLOP per byte. The machine does 50 TFLOP/s with
1 TB/s of memory bandwidth. Is the kernel memory-bound or compute-bound?
Show the steps.

D14. An agent tool spec must declare four things before the agent may
call it. Name all four.

D15. A teammate cannot reproduce your agent run. List the four items
that must be logged with every run so the result is reproducible.

## Memory and retrieval (U06 bridges)

D16. A model has 12 layers, 8 KV heads, head dim 64, and stores fp16
(2 bytes per value). For 1,000 tokens, how many bytes does the KV cache
hold? Use KV bytes = 2 * layers * kv_heads * tokens * d_head * bytes.
Show the steps.

D17. Retrieval feeds an agent loop. State in one sentence when
precision-first retrieval is the right choice, and in one sentence when
recall-first is.

D18. Define the difference between context and persistence in one
sentence each. Then give one example of a fact that belongs in each.

## Formal methods and autonomy (U07 bridges)

D19. A proof search proposes tactics and a kernel accepts or rejects
each one. State in one sentence why the kernel's yes is more trustworthy
than the proposer's confidence.

D20. Define the credit assignment problem in one sentence, using the
tactic-search setting.

D21. State the intervention test for trace faithfulness in two
sentences: the operation, then the verdict rule.

## Evaluation contracts (U08 bridges)

D22. An agent succeeds on 30 of 100 tasks. Compute the standard error
of the success rate. Show the steps.

D23. Agent A has task scores 0.90, 0.55, 0.85. Agent B has 0.72, 0.74,
0.70. The mean picks A. State in two sentences when the minimum is the
right shipping metric, and which agent it picks here.

D24. Define judge contamination in one sentence. Then name one
measurement that detects it.
