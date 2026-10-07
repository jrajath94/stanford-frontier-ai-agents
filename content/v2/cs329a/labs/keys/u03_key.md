# Lab key U03

Keep separate from the lab. Test-mode answers live here only.

## L1.1
Level i holds b^i nodes. The total is the sum over levels 0..d, which
is the geometric sum (b^(d+1) - 1) / (b - 1).

## L1.2
With a cycle and no visited tracking, expansion never terminates: the
leaf count is infinite. The formula b^d assumes a tree, not a graph.

## L2.1
Advantages are deviations from the group mean. Deviations from a mean
always sum to 0, the division by std only rescales them.

## L2.2
An all-equal group teaches nothing: every advantage is 0. Small
groups hit this often on easy or impossible prompts, which is why
prompt selection drops solved and unsolved prompts.

## L3.1
The score of the unexpanded tail. Best-of-100-seen hides how many
good leaves were never visited, the budget line in U03 C11 makes that
opportunity cost explicit.

## L4.1
The keeper rate and the quality of the kept rationales. Both depend
on the base model's strength and the filter's strictness, the
schedule is an outcome, not an input.
