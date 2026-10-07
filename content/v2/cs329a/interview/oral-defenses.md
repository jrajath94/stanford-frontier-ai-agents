# Oral defenses , 10 deep ladders x 8 follow-ups

Each ladder is an 8-rung oral exam on one mechanism. The
examiner goes deeper each rung. The candidate may not look at
notes. Keys in `keys-oral.md`. Provenance: original practice.
Not actual employer questions.

## O1 , U01 selection: best-of-N vs self-consistency

1. Define best-of-N and self-consistency in one breath each.
2. Toy: 5 samples, per-sample accuracy 0.7. Compute both
methods' success rates by hand.
3. Why does best-of-N need a verifier while self-consistency
does not?
4. State the matched-budget condition, and why N differs
between the methods.
5. Your verifier's pairwise accuracy measures 0.52. What do
you conclude, and what do you do?
6. The hybrid (verifier-weighted voting) beats both in the
capstone toy. Explain why, mechanistically.
7. An interviewer says "just use N=1000, more is better."
Dismantle this in three sentences.
8. Design the single experiment that would change your mind
about H2.

## O2 , U02 feedback: the ReAct loop to independent validation

1. Write the ReAct loop in five lines.
2. Toy: the tool returns an error on step 2 of 4. Trace what
the agent does next, and what it should do.
3. Why is execution feedback worth more than self-critique?
4. State the shortcut-exploitation failure (U02 C11) in one
sentence.
5. Your agent's tool success rate is 0.95 but task success is
0.40. Diagnose in two sentences.
6. When does the loop diverge (never terminates)? Name the
guard.
7. An interviewer says "tools make the model dumber."
Steel-man, then rebut.
8. Design the experiment that tests whether independent
validation (U02 C12) catches what execution feedback misses.

## O3 , U03 search: tree search to reward validity

1. Define state, action, and reward for tree search on
reasoning tasks.
2. Toy: branching factor 3, depth 2, one correct leaf.
Compute the random-search hit rate.
3. Why does a perfect verifier make search tractable?
4. State the reward-validity failure (U03 C12) in one
sentence.
5. Your search finds high-reward paths that are wrong.
Diagnose in two sentences.
6. Compare MCTS with beam search: when does each win?
7. An interviewer says "search is just slow sampling."
Dismantle this in three sentences.
8. Design the experiment that tests whether the reward model
or the search budget is the binding constraint.

## O4 , U04 evolution: selection to holdout separation

1. Define the evolutionary loop: variation, selection,
inheritance.
2. Toy: population 10, top 3 reproduce. Compute the selection
pressure in one line.
3. Why does novelty search help in deceptive landscapes?
4. State the holdout-separation rule (U04 C09) in one
sentence.
5. Your champion scores 0.95 on the selection metric and 0.60
on the holdout. Diagnose in two sentences.
6. When does evolution beat gradient methods? Name the
condition.
7. An interviewer says "evolution is just random search."
Steel-man, then rebut.
8. Design the experiment that tests whether the holdout gap
is overfit or distribution shift.

## O5 , U05 SWE agents: serial depth to parallel width

1. Define serial iterations S and parallel width K in the
CodeMonkeys setup.
2. Toy: coverage 0.832 at S=1, 0.997 at S=5. Compute the gain
per added iteration.
3. Why does depth raise coverage while width amortizes
context?
4. State the selection stage: what does voting with
model-generated tests select for?
5. Your pipeline's coverage stalls at S=3. Name two causes
and the measurement that separates them.
6. Context is halved. Do you cut S or K? Justify with the
coverage math.
7. An interviewer says "just run K=1000, coverage is all that
matters." Dismantle this in three sentences.
8. Design the experiment that tests whether the final
selection trajectory or the voting stage matters more.

## O6 , U06 memory: CacheBlend to Cartridges

1. Define the KV cache and why it is the memory of
inference.
2. Toy: 2,048 tokens, 15 percent recompute. Compute the
prefill saving.
3. Why does CacheBlend recompute only high-deviation tokens?
4. Define a Cartridge: what is trained, and what is the
40x claim?
5. Your blended cache produces wrong answers on chunk
boundaries. Diagnose in two sentences.
6. Compare CacheBlend with Cartridges: when does each win?
7. An interviewer says "just use a bigger context window."
Dismantle this in three sentences.
8. Design the experiment that tests whether the recompute
fraction or the deviation metric matters more.

## O7 , U07 formal systems: proof search to the autonomy envelope

1. Define goal, tactic, and kernel.
2. Toy: 12 tactics, 4-tactic proof. Compute the guided vs
random success rates.
3. Why is the kernel the free verifier?
4. State the autonomy envelope rule in one sentence.
5. Your prover closes nothing after the full budget. Name two
causes and the measurement that separates them.
6. The kernel has a soundness bug (accepts 2 percent of false
proofs). What breaks, and what must be re-proved?
7. An interviewer says "proofs will replace testing."
Steel-man, then rebut.
8. Design the experiment that tests whether the tactic
action space or the search policy is the binding constraint.

## O8 , U07/U08 validity: traces to judges

1. Define a faithful trace (U07 C11).
2. Toy: 100 traces, 30 are stories. Compute the story rate
and its meaning.
3. State the intervention test in one sentence.
4. Define the contamination gap (U08 C07).
5. Your same-model judge agrees with the generator at 0.85,
an independent judge at 0.60. Diagnose in two sentences.
6. When is a same-model judge acceptable? Name the
condition.
7. An interviewer says "LLM judges are fine, everyone uses
them." Dismantle this in three sentences.
8. Design the experiment that separates shared-bias
contamination from judge incompetence.

## O9 , U08 evaluation: GDPVal to project gates

1. Define the GDPVal pipeline: tasks, judges, metric.
2. Toy: 660 wins of 1,320. Compute the win rate and the SE
on the 220 gold set.
3. Why blinded pairwise comparison, not absolute scoring?
4. State the mean-min flip (U08 C05) in one sentence.
5. Your agent means 0.77 but mins 0.55. Ship or not? Justify
in two sentences.
6. Name the three eval fuels and the binding one in the toy.
7. An interviewer says "one number is enough to compare
agents." Dismantle this in three sentences.
8. Design the experiment that tests whether the duration
curve or the value weighting changes the ranking more.

## O10 , capstone: the full research pipeline

1. State a falsifiable hypothesis in the H1/H2/H_ext form.
2. Toy: your verifier measures 0.53 pairwise accuracy. What
is the verdict on H2?
3. Why matched budgets, and what is the exact accounting?
4. Name the three ablations and what each isolates.
5. Your ranking flips between seeds. What do you conclude?
6. Your extension fails (no judge inflation). How do you
report it?
7. An interviewer says "synthetic tasks prove nothing."
Steel-man, then rebut.
8. Design the single follow-up experiment you would run with
10x the budget.
