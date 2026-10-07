# Interview bank U03 , Planning, search, and train-time RL

Provenance: original practice questions. Not actual employer questions.
Keys in `u03_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. State the leaf count of full tree expansion and the BFS vs DFS
memory difference.
B2. What is adaptive branching, in one rule?
B3. What does "as-needed" mean in decomposition, and what does it
save?
B4. Define the critical path and compute it for durations {A: 4, B: 6,
C: 5} with C depending on A.
B5. Write the GRPO advantage formula and say what the group replaces.
B6. Define on-policy and name one failure from training off-policy
without correction.

## Deep ladders (2 x 5)

Ladder 1 , tree search to budget.
D1.1 Define the search node, branching factor, and depth.
D1.2 Toy: b = 3, d = 2. Count leaves and total nodes, state BFS visit
order for the first 4 nodes.
D1.3 Derive the b^d leaf count and the O(b^d) time claim.
D1.4 Implement BFS, state its memory cost and DFS's.
D1.5 Compare full tree search with N independent sampling chains. When
does the tree win?
D1.6 Debug: the search never terminates on your task. Name two causes
and the fix for each.
D1.7 Critique the discrete-action assumption. What breaks for free-
text actions?
D1.8 Design a matched-budget experiment comparing tree search with
sampling chains, and state what would falsify the tree's value.

Ladder 2 , GRPO to reward validity.
D2.1 Define the GRPO group, the reward, and the advantage formula.
D2.2 Toy: rewards [2, 0, 1, 1]. Compute mean, std, and advantages.
D2.3 Derive why the group baseline removes prompt difficulty and why
dividing by std matters.
D2.4 Implement grpo_advantages with the std guard, state the small-G
risk.
D2.5 Compare GRPO with PPO. When does the value network earn its keep?
D2.6 Debug: all advantages are 0 across many prompts. Name two causes
and the fix for each.
D2.7 Critique within-group comparability. When does ranking punish a
valid answer?
D2.8 Design the reward-validity audit schedule for a training run and
state the verdict rule.

## Analytical exercises (2)

A1. A search has b = 4, d = 3, budget B = 100 node expansions. How
many depth-3 nodes go unexpanded? If each expansion costs 2 seconds
but 10 percent of nodes need a tool call costing 60 seconds, compute
the true expected wall-clock for 100 expansions and state what the
node-count budget hides.
A2. A validity audit reports train reward 0.90, held-out 0.72, human
pass rate 0.70, tolerance 0.1. Compute the verdict. Then compute the
gaming margin (reward rise minus human fall) if the run started at
train 0.60 and human 0.90, and state what the margin means.

## Implementation / debug (1)

I1. Your reasoning-RL run shows the reward climbing but human judges
say quality is flat. Sketch the training loop code with the audit
hook you would add, then name the two most likely causes and the
single measurement that separates them. State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: the action space is free text, so the
branching factor is effectively infinite. Which search methods
survive, and what replaces node expansion?
S2. Constraint change: rewards arrive only at the end of 50-step
trajectories and are binary. Which credit methods survive, and what
new assumption does each need?

## Research critique (1)

R1. "Reasoning RL with verifiable rewards discovers what STaR cannot,
so imitation is obsolete." Identify the claim's strongest true part,
its weakest assumption, and the single experiment that would most
change your mind.
