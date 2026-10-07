# U05 lab: optimization and agent data

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: toy prompt optimizer

Implement the C01 optimizer: 4 candidate prompts with fixed dev scores [0.55, 0.62, 0.70, 0.78] on 20 examples. Report the argmax, the search cost in scored calls, and the per-candidate SE. Then simulate a 5-example dev set on 5 seeds (Gaussian noise with the binomial SE) and report how often the winner flips.

## Task 2: knob decision table

Implement the C02 table: knobs ("prompt rewrite", 0.79, 2 h, 1.0x), ("fine-tune", 0.83, 50 GPU-h, 1.0x), ("big model", 0.86, 0, 3.0x). Report the cheapest pick at bars 0.78 and 0.80. Report the SE on 200 examples at 0.79.

## Task 3: LoRA adapter and merge

Implement the C03 forward pass y = W x + (alpha/r) B (A x) with d = k = 1024, r = 8, alpha = 8. Report the full vs adapter parameter counts and ratio. Verify the merged W gives the same output (max abs diff). Report the rank of B A. Report 7B-parameter memory at fp16 vs 4-bit.

## Task 4: distillation and synthetic loop

(a) Distillation toy: teacher accuracy 0.90. Student on 1000 teacher labels 0.85, on 200 gold labels 0.75. Report the gain and the labeling cost. (b) Synthetic loop: 1000 generated, verifier accuracy 0.85, acceptance 0.85. Report expected good labels. Simulate 3 generations of Gaussian resampling with 5 percent tail truncation at seed 0 and report the feature variances.

## Task 5: DPO loss

Implement the C05 loss for beta = 0.1 on the two pairs: theta (w -2.0, l -2.5) vs ref (w -2.2, l -2.3), and theta (w -2.5, l -2.0) vs the same ref. Report m, beta m, and the loss per pair. Verify the theta-equals-ref loss equals log 2.

## Task 6: flywheel and selection

(a) Flywheel: 1000 users/day, 10 percent flagged, $2 per annotation. Report daily yield, daily cost, weekly yield. (b) Selection: budget 100 of 10,000 traces. Report the uncertainty vs random gain gap (0.08 vs 0.02) and the duplicate-filter saving when 2000 of 10,000 are near-duplicates.

## Task 7: eval hygiene

(a) Contamination: 5000 train docs, 200 eval docs, 12 sharing a 13-gram. Report the leakage rate, the reported mean (leaked slice 0.88, clean slice 0.74), and the inflation. (b) Validator: scores [0.9, 0.8, 0.8, 0.7, 0.7, 0.6, 0.6, 0.5, 0.5, 0.4] vs human [1, 1, 0, 1, 0, 1, 0, 0, 1, 0]. Report the calibration gap and the accuracy at threshold 0.5. (c) Holdout: true ability 0.74, two peeks add 0.04 of bias. Report the inflated number.
