# Lab key U08

Keep separate from the lab. Test-mode answers live here only.

## L1.1
Each 8 h task costs 8 hours of agent compute, so the budget
buys few of them. But the 8 h point is the noisiest (fewest
samples) and the most important (the economic prize). The
honest move: report the CI, which will be widest at 8 h, and
buy more 8 h tasks before claiming anything about them.

## L2.1
The min (0.55) describes it. The deployed agent sees the full
mix, and the production workload is the 0.55 task: users meet
0.55, not 0.767. The mean described the research agent. The
min describes the shipped one.

## L3.1
The residual gap measures shared LLM bias: the things all
large models get wrong the same way (fluency over substance,
certain error patterns). The far judge removes the
lab-specific similarity but not the species-level bias. Only
a human judge removes that.

## L4.1
The ablation misses what was never measured: safety is not in
the score, so the delta is zero by construction. Catch it
with a separate safety ablation: re-run the component
removal against the incident metric (violations, harm), not
the task score. Two metrics, two deltas.

## L5.1
(1) Halve the audit sample from 20 to 10: saves $300. Risk:
the audit CI widens, and a rare failure mode slips through.
(2) Replace the $0.50 judge with a verifier-graded subset or
a cheaper model: saves up to $100. Risk: judge contamination
rises (C07), and the savings are small because the judge was
never the binding fuel.
