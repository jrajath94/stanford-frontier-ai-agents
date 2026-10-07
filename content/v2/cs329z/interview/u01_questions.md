# U01 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Define a model and a compound AI system in one sentence each.
B2. Name the three engineering challenges from the S01 framing.
B3. Write the attention equation and name the shape of each matrix.
B4. What does temperature do to a softmax distribution?
B5. What is the KV cache, and what does it cost in bytes?
B6. State the difference between structured I/O and constrained decoding.

## Deep ladders (2 x 5)

### Ladder 1: temperature sampling

L1.1 Define: write p_i for logits z at temperature T.
L1.2 Toy: compute p for z = [1, 2, 3] at T = 1.
L1.3 Derive: show the limit T -> 0 puts mass 1 on the argmax.
L1.4 Implement and complexity: write the sampler and state its per-step cost.
L1.5 Compare: how does top-k change the distribution differently from temperature?

### Ladder 2: test-time scaling

L2.1 Define: write pass@k under independence.
L2.2 Toy: p = 0.3, k = 8. Compute pass@8.
L2.3 Derive: when does majority vote help, in terms of p?
L2.4 Implement and complexity: write the simulator. State cost in k.
L2.5 Compare: 8 samples from a small model vs 1 sample from a 4x-cost model. Which wins on the toy numbers?

## Analytical/quantitative (2)

A1. A transformer has L = 32, d = 4096. Estimate attention FLOPs per forward pass at n = 8192. Show the arithmetic.
A2. An eval reports 0.80 on n = 25 items. Give the standard error and the n needed to resolve a 0.05 gap at z = 2.

## Implementation/debug (1)

I1. Your masked sampler emits disallowed tokens 5 percent of the time. The mask looks right. Name two bugs that cause this and how you check each.

## Changed-constraint scenarios (2)

S1. The latency budget allows exactly one model call. Which U01 mechanisms still apply, and which die?
S2. The corpus updates every hour. You chose a fine-tuned monolith. What breaks, and what is the cheapest fix?

## Research critique (1)

R1. "Bigger context windows make retrieval obsolete." State the strongest version of this claim, then give two reasons it fails and one experiment that would change your mind.

## Concept-targeted supplements

CS1. (U01-C03) Two systems score 8/10 and 7/10 on your eval. Which ships, and what is the statistical argument? Name two ways the eval itself can lie about a system.
