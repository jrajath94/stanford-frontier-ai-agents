---
page_id: cs329a-l09
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 9
nav: "L09 · The Verifier Bottleneck"
title: "Lecture 9: The Verifier Bottleneck: Who Judges the Judge"
summary: "Every loop in this course leans on a verifier. Outcome checks miss broken reasoning, and LLM judges certify bad proofs. DeepSeek-Math V2 answers with a meta-verifier, and multi-agent debate supplies the diversity single agents lose."
date: "2025-11-05"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
video_id: AyO6wyu4DEg
concepts: [verification, outcome-reward, process-reward, llm-as-judge, meta-verifier, deepseekmath-v2, multi-agent-debate, diversity-collapse, reward-hacking]
sources:
  - tag: lecture
    label: "CS329A Lecture 7: quarter recap, verification, multi-agent fine-tuning (Autumn 2025)"
    url: https://www.youtube.com/watch?v=AyO6wyu4DEg
  - tag: paper
    label: "DeepSeek-Math V2: self-verification loops for theorem proving"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: the judge is the load-bearing wall

Every chapter so far leans on the same part. Lecture 2 needs a
verifier to pick winning samples. Lecture 4 needs hidden tests
to grade code. Lecture 6 needs example tests to filter programs.
Lecture 8 needs answer keys to keep rationales. Remove the
verifier and every loop collapses.

So ask the uncomfortable question: how good are our verifiers?
Two kinds exist. An **outcome reward** checks the final answer:
does it match, do the tests pass. A **process reward** checks
the steps: is each reasoning step valid. Outcome rewards are
cheap and available. Process rewards are expensive and mostly
do not exist. The course has been running on outcome rewards
throughout. This chapter shows what that costs.

## First failure, demonstrated: right answer, wrong reasoning

A model proves a theorem. The final line matches the expected
result. The outcome verifier approves. But step 4 of the proof
does not follow from step 3: there is a gap, a leap the proof
does not earn. The verifier cannot see it. It only checked the
ending.

Train on this proof, as Lecture 8's loop would, and the model
learns that gaps are acceptable. The loop hill-climbs on the
metric, correct final answers, while the unmeasured thing,
valid reasoning, decays. The lecture's warning is general:
saturating benchmarks with outcome rewards does not mean the
reasoning got better. It means the answers match.

## Second failure, demonstrated: the judge certifies nonsense

If outcome checks are blind, use the model itself as judge:
**LLM-as-judge**, ask the model whether a proof is valid. The
lecture reports the embarrassing result in theorem proving:
models trained on quantitative reasoning routinely claim that
mathematically invalid proofs are valid. The judge is
confident and wrong. Expert humans spot the gaps instantly.
The model judge does not. A verifier that approves bad proofs
is worse than no verifier: it actively teaches bad reasoning.

## The key question

If verifiers bottleneck everything, and outcome checks are
blind while model judges are gullible, how do we build a
verifier we can trust?

## The new idea: the meta-verifier

**DeepSeek-Math V2** adds one level. Keep the generator that
writes proofs and the verifier that judges them, but add a
**meta-verifier** that judges the judge.

The construction, step by step:

1. Humans examine proofs and mark the real issues, with no
   reference solutions: "step 4 does not follow from step 3."
2. Train an LLM on those annotations to do the same: find
   issues in proofs, then score the proof from 0 to 1 based
   on the issues found.
3. The meta-verifier reviews the verifier's analysis: do the
   claimed issues actually exist? Does the score follow from
   the issues? Experts annotate the quality of this review,
   and the meta-verifier learns from that.
4. Close the loop: the verifier's scores train the generator.
   the generator produces harder proofs. Harder proofs train
   a sharper verifier. Each side lifts the other.

```ascii
generator --proofs--> verifier --issues + score--> meta-verifier
    ^                      |                          |
    |                      v                          v
    +---- harder proofs <--+--- sharper judging <----+
```

The numbers the lecture reports: over 8 iterations of this
loop, proof scores keep climbing. With best-of-32 selection,
picking the top proof out of 32 generated, the system reaches
42 percent proof score on the IMO 2024 shortlist. The point is
not the number. The point is the hill keeps climbing without
new human labels after seeding: the loop manufactures its own
ever-harder training signal.

Why does the meta level help? Because the failure it targets
is specific: verifiers that invent issues, or miss real ones,
or assign scores their own analysis does not support. The
meta-verifier checks the work of the judge the way a senior
reviewer checks a junior's grading. One level of "show your
work" applied to evaluation itself.

## The diversity problem, and the multi-agent answer

The recap lecture raises a second bottleneck: **diversity**.
Self-improvement needs varied reasoning chains to learn from.
But fine-tuning a single agent collapses diversity: the model
converges on its favorite patterns, and later rounds have
nothing new to select from. The lecture shows the symptom as
accuracy that collapses, or stalls, under continued
single-agent fine-tuning.

The fix it presents is **multi-agent debate fine-tuning**.
Several generator agents, fine-tuned from the same base but
diverging, each produce an answer. Their answers are
summarized together. A critic model critiques the combined
set. Then a second round: every generator writes an updated
answer informed by the critique, and majority vote plus
summarization produces the final. The trajectories, initial
answers, critiques, revisions, become fine-tuning data.

Two results the lecture highlights. First, with multi-agent
fine-tuning, performance keeps rising across iterations where
single-agent fine-tuning collapses. Second, the responses stay
diverse: measured by embedding dissimilarity, the agents keep
disagreeing productively instead of converging. Diversity is
not a starting condition that decays. The debate structure
maintains it. And the gains transfer: fine-tuned on math, the
agents improve on adjacent domains like GSM8K too.

The lecture's summary line: if you want self-improvement, the
reasoning chains feeding it must stay diverse, and multiple
agents are a practical way to keep them that way.

## Where it breaks: verification has a speed limit

Step back and the deepest bottleneck appears. The whole
edifice, sampling, RL, meta-verification, multi-agent debate,
assumes verifiers that are fast. RL loops need thousands of
iterations. Test-time scaling needs judgments per question.
The lecture names the domains where this fails: chip design,
where one simulation takes days. Wet-lab chemistry, where one
experiment takes weeks. Creative work, where no objective
verifier exists at all.

The workaround is a learned stand-in: train a reward model to
predict the slow simulator's verdict, and put the fast model
in the loop. But now the loop optimizes the stand-in, not the
world, and any inaccuracy is an invitation to **reward
hacking**: the model learns to please the predictor rather
than solve the problem. The lecture is blunt that this is an
open problem. Verification is the bottleneck of the entire
research program, and for slow or subjective domains there is
no good answer yet.

## Mapping back: what each idea fixes

| Verification failure | Answer | How |
|---|---|---|
| Outcome checks miss broken reasoning | Process-level judging | Score the steps, not just the ending. DeepSeek-Math V2's verifier finds issues per step. |
| LLM judges certify invalid proofs | Meta-verifier | Judge the judge: check that claimed issues exist and scores follow from them. |
| Single-agent fine-tuning collapses | Multi-agent debate | Generators plus critic keep chains diverse. Performance climbs where single-agent stalls. |
| Gains do not transfer | Diverse debate data | Fine-tuned on math, agents improve on adjacent GSM8K too. |
| Slow real-world verifiers | Learned reward stand-ins | Fast predictor replaces slow simulation. Price is reward hacking risk. |

## The honest price

Meta-verification needs humans to seed the issue-finding data:
expert annotators marking proof flaws with no reference
solutions. That seed is expensive and domain-specific. The
generator-verifier loop can then run on its own, but it
hill-climbs inside the seeded notion of correctness. Multi-agent
debate multiplies inference cost by the number of agents and
rounds. And none of it touches the slow-verifier domains, where
the loop cannot turn at all. The verifier bottleneck is not
solved. It is pushed one level up, and the top level still
needs humans.

> [!QA]
> Q: Why are outcome rewards not enough?
> A: They check the ending, not the reasoning. A proof with a gap at step 4 and the right final line passes. Training on such proofs teaches the model that gaps are fine, so benchmark scores saturate while reasoning quality decays. The lecture's verdict: outcome rewards enabled the field's progress and now limit it. Process-level judgment, scoring the steps, is the direction.
> Follow-up: Why is process reward so hard to build?
> A: It needs step-level labels: which step is wrong and why. Humans can do it but slowly and expensively. Models asked to do it, LLM-as-judge, certify invalid proofs as valid. DeepSeek-Math V2's answer is to train the step-judge on human-marked proof issues, then add a meta level that audits the judge. Each level costs human seeding.

> [!QA]
> Q: What does the meta-verifier actually check?
> A: The verifier's work, not the proof directly. Given a proof and the verifier's analysis, the meta-verifier asks: do the claimed issues really exist in the proof, and does the 0-to-1 score follow from those issues? It catches fabricated errors and unsupported scores. Experts annotate review quality to train it. Then the improved verifier trains a better generator, which writes harder proofs, which sharpen the verifier further.
> Follow-up: Does the loop run without humans after seeding?
> A: In the reported result, yes for the 8 climbing iterations: the seed data trains the issue-finder, and automation takes over labeling from there. But the seed defines correctness, and the loop cannot outgrow it. Humans set the standard. The loop scales it.

> [!QA]
> Q: Why does multi-agent fine-tuning beat single-agent fine-tuning?
> A: Diversity. A single agent fine-tuned repeatedly converges on its favorite reasoning patterns. Later rounds select from a shrinking pool and accuracy collapses. Multiple generators plus a critic keep producing genuinely different chains: embedding dissimilarity stays high across iterations, and performance keeps climbing. The debate structure manufactures the disagreement that selection needs.
> Follow-up: Is this just ensembling?
> A: No. Ensembling votes once. Here the agents interact: summarize, critique, revise, vote, and the whole trajectory becomes training data for the next round. The product is not a better vote but better agents, and the gains transfer to adjacent domains the debate never trained on.

## Recap: the whole lesson on one screen

1. **The load-bearing wall.** Every loop in the course needs a
   verifier. Ask how good the verifiers are.
2. **Right answer, wrong reasoning.** Outcome checks approve
   proofs with gaps at step 4. Training on them teaches gaps.
3. **The gullible judge.** LLM-as-judge certifies invalid
   proofs as valid. Worse than no verifier.
4. **The key question.** How do we build a verifier we can
   trust?
5. **Meta-verifier.** Judge the judge: do the claimed issues
   exist, does the score follow. Generator and verifier then
   lift each other.
6. **The numbers.** 8 iterations climbing. Best-of-32 reaches
   42% proof score on the IMO 2024 shortlist.
7. **Diversity collapse.** Single-agent fine-tuning converges
   and stalls. Multi-agent debate, generators plus critic,
   keeps chains diverse and climbing, and transfers to new
   domains.
8. **The honest price.** Human-seeded standards, multiplied
   inference cost, and no answer for slow-verifier domains.
   The bottleneck moves up one level. The top still needs
   humans.

## Official sources and further reading

**Official:**
- CS329A Lecture 7 (Autumn 2025): the lecture this chapter
  follows. https://www.youtube.com/watch?v=AyO6wyu4DEg
- DeepSeek-Math V2: the meta-verifier architecture and the
  IMO shortlist result.

**Further reading:**
- Multi-agent debate fine-tuning literature: the generator,
  summarizer, critic loop the lecture summarizes.
- Christiano et al., RLHF (2017): learned reward models, the
  ancestors of the stand-ins discussed here.

**Caveats from these sources.** DeepSeek-Math V2 details are
the lecture's summary. The 42% figure is best-of-32 on the
IMO 2024 shortlist, not pass@1. The multi-agent debate paper
is unnamed in the lecture. Treat the description as the
lecturers' summary. Slow-domain examples (chip sims, wet labs)
are the lecturers' illustrations of the general point.

## Connections to the other courses

- **CS329A L02:** the verifier this chapter interrogates is
  the one Lecture 2 assumed as an oracle.
- **CS329A L08:** STaR's leak, unfiltered rationales, is what
  process-level judging is built to fix.
- **CS329A L04:** learned stand-in rewards are the
  generalization of RLEF's hidden tests to domains without
  tests.
- **CS329Z:** evaluation chapters: building outcome
  benchmarks, and why they saturate.
