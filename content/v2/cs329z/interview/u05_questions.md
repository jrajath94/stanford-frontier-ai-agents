# U05 interview bank: questions

Original practice questions. Not actual employer questions. No invented attribution.

## Breadth (6)

B1. Name the four prompt-optimizer families in the S09 title and the one loop they share.
B2. State the three optimization knobs and the order in which you spend on them.
B3. Write the LoRA update formula and count the trainable parameters for d = k = 1024, r = 8.
B4. What does DPO train on, and what two stages does it replace?
B5. Name the three agent-data kinds and the cost of 1000 items of each.
B6. Name the three eval tiers and the access rule for each.

## Deep ladders (2 x 5)

### Ladder 1: natural-language optimizer

L1.1 Define: candidate prompt, dev set, metric, feedback, update.
L1.2 Toy: 4 prompts score 0.55, 0.62, 0.70, 0.78 on 20 examples. Name the argmax, the search cost, and the SE.
L1.3 Derive: why does a diagnosed edit beat a random edit at equal call budgets?
L1.4 Implement and complexity: write the propose-score-reflect-update loop. State cost per round.
L1.5 Compare: reflection-guided search vs LoRA on what each changes and when each wins.

### Ladder 2: DPO

L2.1 Define: preference pair, policy, reference, margin m, beta.
L2.2 Toy: beta = 0.1, pair 1 m = 0.4, pair 2 m = -0.6. Compute both losses.
L2.3 Derive: what does beta control, and what happens at beta = 0?
L2.4 Implement and complexity: write the loss. State cost per pair.
L2.5 Compare: DPO vs RLHF vs SFT-on-winners on data needs and failure modes.

## Analytical/quantitative (2)

A1. A validator scores 10 items with mean 0.65. Human labels give mean 0.50. The optimizer raises the validator mean from 0.65 to 0.90. Give the calibration gap and explain why the human-judged gain is suspect.
A2. A 7B model trains with LoRA r = 16 on all attention matrices of 32 layers, each matrix 4096x4096. Count the adapter parameters. Compare with full fine-tuning of those matrices.

## Implementation/debug (1)

I1. Your prompt optimizer improves the dev score from 0.62 to 0.95 in 3 rounds, but the sealed set shows no gain. Name two bugs and how you check each.

## Changed-constraint scenarios (2)

S1. Human annotation costs $20 per item and the budget is $100. The task is checkable by code. Redesign the C06-C08 data plan.
S2. The reference model for DPO is unavailable (only the pairs exist). What breaks in the loss, and what is the repair?

## Research critique (1)

R1. "Prompt optimization makes fine-tuning obsolete." State the strongest version, then give two reasons it fails and one experiment that would change your mind.

## Concept-targeted supplements

CS1. (U05-C01) Name the four prompt-optimization methods in the GEPA / MIPROv2 / OPRO / TextGrad family and state in one line what each one's search signal is. What breaks when the dev set has only 5 examples?
