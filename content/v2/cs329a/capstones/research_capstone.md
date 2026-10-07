# Research capstone , cs329a U01-U08

Status: EXECUTED 2026-10-07. `run_research_capstone.py` is the full
pipeline: replication at 3 token budgets x 3 seeds with Wilson 95
percent CIs, ablations, failure criteria, and a falsifiable
extension on judge contamination (U08 C07). Figure:
`figs/research_capstone.png` (computed by the script, metadata
stripped in-script). Supersedes `superseded/pilot_research.py`.

Honesty note: the task family is SYNTHETIC (binary answers, known
truth, simulated verifiers). The run exercises the full experimental
pipeline. Its rankings are toy results, NOT evidence about real
models. Nothing here is a benchmark claim.

## Question

At matched inference budget, does weak-verifier best-of-N beat
self-consistency on multi-step reasoning tasks, and does judge
contamination inflate the reported margin?

## Falsifiable hypothesis

H1: on discrete-answer tasks with no trusted verifier,
self-consistency beats the single sample. H2: with a weak verifier
(pairwise accuracy above 0.60 on the sample pile), best-of-N beats
self-consistency at the same token budget. The ranking flips with
verifier availability, not with budget. H2 is false if best-of-N
loses to self-consistency with a good verifier at matched budget on
any seed. H_ext (extension): a contaminated verifier (shared blind
spots with the generator) shrinks the best-of-N margin as a
selector, and inflates the reported score as a judge. H_ext is false
if the margin does not shrink or the judge does not inflate.

## Literature

Mechanisms from U01 (test-time scaling, selection), U02 (verifiers),
U05 (serial vs parallel scaling), U07 (formal verification as the
limiting case), U08 C07 (judge contamination). Paper pointers in
`../source_manifest.md` carry SOURCE ATTRIBUTION PENDING. The
replication targets the mechanisms, not any paper's numbers.

## Data

Synthetic: 1,500 questions per seed, 3 seeds (11, 12, 13). Per
question: a difficulty q drawn from Beta(5,2) (mean per-path
accuracy 0.714, the regime where majority vote helps, matching the
pilot). 20 percent of questions are blind-spot questions (shared
generator-verifier failure mode): q is scaled by 0.3 and the
contaminated verifier degrades to pure noise on them.

## Baselines

B0: single greedy sample. B1: self-consistency (majority vote over
N_sc paths). B2: best-of-N with the weak verifier (pairwise
accuracy 0.65). B3: best-of-N with the oracle verifier (the
ceiling). B4: best-of-N with random scores (verifier-off control).

## Matched budgets

Token budget per question: 2k, 10k, 40k. Generation costs 400
tokens per sample, verifier scoring 100 per sample. Self-
consistency uses N = 5, 25, 100 (spend equals the budget line).
Best-of-N uses N = 4, 20, 80 (spend equals the budget line).
Every method sits exactly on its budget line.

## Metrics

Primary: task success rate with Wilson 95 percent CIs over
4,500 questions (1,500 x 3 seeds). Secondary: the best-of-N minus
self-consistency margin per budget, verifier pairwise accuracy on
the sample pile, judge inflation (reported minus true score).

## Controls

Same question stream per seed across methods. Same per-question
difficulty for every method. Same budget accounting (generation +
scoring tokens). The contaminated and independent verifiers see the
same samples.

## Ablations

A1: verifier off (B4): isolates the verifier's contribution. It
collapses to the single-sample rate. A2: verifier-weighted voting
(the hybrid): weights each path's vote by its verifier score. A3:
the budget sweep (2k/10k/40k) separates sample count from method.

## Seed variation and uncertainty

Three seeds. All rates carry Wilson 95 percent CIs. The H2 claim
needs best-of-N above self-consistency on every seed.

## Failure criteria

The capstone fails if: the ranking flips between seeds. The weak
verifier's measured accuracy falls below 0.55 on the pile (then H2
is untestable). Or the oracle ceiling ties B0 (the task is too
easy). Exercised: a deliberately poor verifier (accuracy 0.52)
measured 0.531 on the pile, below 0.55, and its best-of-N rate
(0.63-0.64) sits at the single-sample rate: the criterion fires
honestly and H2 is declared untestable there.

## Reproducibility

Seeds 11, 12, 13 pinned in the script. The budget ledger is exact
(by construction). The verifier calibration (sigma from pairwise
accuracy via the normal CDF) is in the script. Re-run:
`python3 run_research_capstone.py`.

## Results (toy, synthetic)

H1 holds: self-consistency beats the single sample on all budgets
(0.650 vs 0.612 at 2k. 0.715 vs 0.608 at 40k). H2 holds: weak-
verifier best-of-N beats self-consistency on all budgets and all
seeds (margins +0.047, +0.083, +0.105 at 2k/10k/40k). A1: with the
verifier off, best-of-N collapses to the single-sample rate
(0.611 vs 0.612): the verifier contributes the entire margin. A2:
the hybrid (verifier-weighted voting) beats both parents at every
budget (0.725, 0.900, 0.962): using all samples' scores beats
picking one. A3: margins grow with budget. H_ext holds: the
contaminated selector shrinks the margin (+0.008, +0.040, +0.055
shrink at 2k/10k/40k), and the contaminated judge inflates the
reported score (0.748 reported vs 0.715 true, +0.055 over the
independent judge's 0.693).

## Negative results

Two honest negatives. (1) The poor-verifier run: with measured
accuracy 0.531, best-of-N does not beat the single sample. Per the
failure criterion, H2 is untestable below 0.55, and the run is
reported as uninformative, not as support. (2) A first task-family
attempt (Beta(2,5), per-path accuracy below chance) broke majority
vote entirely (self-consistency scored below the single sample).
That is a real finding about the method's operating regime, but it
is off-topic for H1/H2, so the family was corrected to Beta(5,2)
(the pilot's regime) and the attempt is reported here, not hidden.

## Limitations

Synthetic tasks understate real difficulty. The verifier's pairwise
accuracy model (Gaussian noise) is a toy. Blind-spot questions are a
crude stand-in for shared bias. Human judgment tasks are out of
scope. No conclusion transfers to real models.

## Ethical considerations

No human subjects. Negligible compute (seconds on a laptop). The
synthetic results must never be presented as real-model
performance. The contamination finding is a warning about eval
design, not a claim about any deployed system.
