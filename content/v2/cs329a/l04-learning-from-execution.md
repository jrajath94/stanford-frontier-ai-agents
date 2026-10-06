---
page_id: cs329a-l04
course_slug: cs329a
course_name: "CS329A: Self-Improving AI Agents"
course_order: 8
order: 4
nav: "L04 · Learning from Execution"
title: "Lecture 4: Learning from Execution: The RLEF Loop"
summary: "A coding agent that can run tests can teach itself. RLEF turns pass/fail execution feedback into a reinforcement learning signal, with public tests for practice and hidden tests for the grade."
date: "2025-10-08"
instructor: "Azalia Mirhoseini, Aakanksha Chowdhery"
offering: "Autumn 2025"
concepts: [rlef, execution-feedback, reinforcement-learning, binary-reward, public-tests, private-tests, ppo, turn-level-value, policy-gradient]
sources:
  - tag: lecture
    label: "CS329A Lecture 3, second paper: RLEF (Autumn 2025)"
    url: https://www.youtube.com/watch?v=Lxh9RF5S-K0
  - tag: paper
    label: "RLEF: Reinforcement Learning from Execution Feedback"
  - tag: site
    label: "CS329A course site"
    url: https://cs329a.stanford.edu
---

## The problem: coding agents need a teacher

Lecture 3 gave the agent hands: it can write code and run it.
Now a harder question: how does the agent get better at writing
code? Human feedback is slow. But code has a built-in teacher:
run it and see. A program either passes its tests or it does not.
That pass/fail signal is free, fast, and honest. This chapter is
about turning it into learning.

**Reinforcement learning** (RL) is learning from rewards. The
model, called the **policy**, takes actions. The world returns a
**reward**, a number saying how good the outcome was. The policy
updates toward actions that earned high reward. Here the actions
are generated programs, and the reward comes from executing them.

## The toy: a palindrome fix, step by step

The lecture's example: write code that finds palindrome
substrings, strings that read the same forwards and backwards.
The loop runs in turns. Watch two of them.

```ascii
turn 1:
  model writes:  a straightforward palindrome checker
  run public tests:  FAIL, execution timeout on long inputs
  feedback to model: "timeout on input of length 500"

turn 2:
  model writes:  an optimized version, skips redundant checks
  run public tests:  PASS
  feedback to model: "all public tests pass"
```

The first attempt is too slow. The test output says exactly how:
timeout. The model reads that feedback and writes a faster
version. This is the **inference-time feedback loop**: try, run,
read the failure, try again. No weights change yet. The model is
just iterating with the compiler as its critic.

Then comes the training step. Collect the trajectories that ended
in passing solutions. Give them reward 1, failures reward 0, a
**binary reward**. Update the policy with RL so that
pass-producing behavior becomes more likely. This is the
**train-time loop**: the policy itself improves. The lecture
names the algorithm family as PPO, a standard policy-gradient
method, and stresses the two phases: exploit the current policy
with inference-time retries, then update the policy on the
execution results.

## The trick that makes it honest: two tiers of tests

Here is the failure the paper's design prevents. If the model
practices on the same tests it is graded on, it can memorize the
expected outputs instead of learning to code. The fix is a
**two-tier test strategy**:

- **Public tests**: a small set, visible during generation. Fast
  iteration. The model sees failures here and retries.
- **Private tests**: hidden during generation. They decide the
  reward. The model never sees them, so it cannot memorize them.

The separation is doing real work. Public tests guide the search.
Private tests grade it. Because the reward comes only from hidden
tests, the only way to earn reward 1 reliably is to write
actually correct code. The lecture calls this out as a key
innovation of the self-improvement loop: the model gets execution
feedback without getting the answers.

## A subtlety: who gets the credit

The policy writes code one token at a time, so the finest control
is per token. But the reward arrives per turn: the whole program
either passes or fails. The paper computes the **value function**,
the model's estimate of future reward, at the turn level, using
the last token of the response, and assigns a single advantage
number to all tokens in the turn. Every token in a passing
program shares the credit equally.

The lecture notes this is close in spirit to GSPO-style updates:
reward the whole sequence, not individual tokens. It is honest
about the tradeoff. Per-token credit would be more precise but
the signal does not exist: no test says "this semicolon was the
problem". Turn-level credit is coarse but matches what the world
actually reports.

## Where it breaks, part 1: the signal is sparse

Binary reward is a blunt instrument. A program that fails 9 of
10 tests gets the same reward, 0, as one that fails all 10, and
the same 0 as one with a syntax error on line 1. The model learns
nothing from near misses. Work the consequence: early in
training, when almost everything fails, almost every trajectory
carries reward 0, and the policy has no gradient to climb. The
loop needs the model to be good enough already that some
trajectories pass. Bootstrapping from zero is the hard part.

## Where it breaks, part 2: negatives teach little

The lecture is candid: learning from negative examples is not
nailed. The loop keeps the winners and drops the losers, so the
model learns what success looks like but gets no structured
lesson from failure. A failed trajectory contains information,
which step went wrong, but the binary reward discards it. Later
lectures return to this gap: process-level feedback, judging
intermediate steps, is an active research area precisely because
outcome-only reward wastes so much signal.

## The key question, answered

Can a coding agent improve with no human labels? Yes, where
execution is the teacher: public tests for iteration, hidden
tests for reward, RL to absorb the wins. The lecture reports this
as one of the first demonstrations that execution feedback alone
can drive large gains in coding models.

## Mapping back

| Missing piece | RLEF answer | How |
|---|---|---|
| No training signal for agents | Execution feedback | Run the code. Tests pass or fail. Free, fast, honest. |
| Memorizing the tests | Two tiers | Public tests guide retries. Hidden private tests decide the reward. |
| One-shot generation | Inference-time loop | Try, read the failure, retry until pass or turn limit. |
| Winners discarded | Train-time RL | PPO on binary rewards. Turn-level value shares credit across the program's tokens. |

## The honest price

The loop demands executable tests for every training problem.
Where tests do not exist, there is no signal. The binary reward
is sparse: near misses teach nothing, and failures are discarded
rather than diagnosed. And the whole thing assumes a base model
strong enough to pass sometimes. A model that never passes never
learns. RLEF closes the loop for code. The next chapters ask how
far the same idea reaches: planning over many attempts, sampling
at massive scale, and training on reasoning itself.

> [!QA]
> Q: What is RLEF in one paragraph?
> A: Reinforcement Learning from Execution Feedback. A coding agent generates a program, runs it against public tests, reads the failure output, and retries. Programs that pass earn reward 1 on a hidden set of private tests. Failures earn 0. An RL update, PPO in the paper, then shifts the policy toward pass-producing behavior. Two loops: inference-time retries exploit the current policy, train-time updates improve it.
> Follow-up: Why two sets of tests instead of one?
> A: To block memorization. If the model saw the grading tests during generation, it could learn their expected outputs by heart instead of learning to code. Public tests are for fast iteration. Private tests, hidden until grading, decide the reward. The only reliable way to earn reward 1 is genuinely correct code.

> [!QA]
> Q: Why is the value function computed at the turn level rather than per token?
> A: Because the reward exists only at the turn level: the whole program passes or fails. No test reports which token caused the failure, so per-token credit would be invented precision. The paper assigns one advantage value, computed from the last token of the response, to every token in the turn. Coarse, but honest about what the world reports.
> Follow-up: What is lost by doing that?
> A: All localization. A program that is perfect except one wrong line gets the same per-token update as a program that is wrong everywhere, since both earn reward 0. The model cannot learn "everything except line 7 was fine". This is the price of outcome-only feedback, and it motivates process-level rewards in later work.

> [!QA]
> Q: What does "learning from negatives is not nailed" mean?
> A: The loop trains on winners and discards losers. A failed trajectory, which test failed and why, carries information the binary reward throws away. Some papers try to learn from failures, but the lecture reports no settled method. In practice this means the loop is sample-hungry: it needs enough passes to learn from, and it learns nothing from the far more numerous failures.
> Follow-up: Could you just reward partial progress, like 7 of 10 tests?
> A: You could, and that densifies the signal, but it changes what is being optimized: the model may learn to pass easy tests while ignoring hard ones. Shaped rewards invite gaming. The paper's binary choice keeps the objective clean at the cost of sparsity. There is no free option here.

## Recap: the whole lesson on one screen

1. **Code has a free teacher.** Run the program. Tests pass or
   fail. No human needed.
2. **The toy.** Palindrome finder fails public tests with a
   timeout, reads the feedback, writes a faster version, passes.
3. **Two loops.** Inference-time: try, run, retry. Train-time:
   RL on the outcomes, PPO, policy improves.
4. **Two tiers.** Public tests for iteration, private hidden
   tests for the reward. Memorization blocked.
5. **Binary reward.** Pass is 1, fail is 0. Simple, honest,
   sparse.
6. **Turn-level credit.** One advantage value for all tokens in
   the program. Matches what the world reports. Loses
   localization.
7. **Sparse signal.** Near misses earn 0 like total failures.
   The model must already pass sometimes to learn at all.
8. **Negatives wasted.** Failures are discarded, not diagnosed.
   Learning from them is an open problem.

## Official sources and further reading

**Official:**
- CS329A Lecture 3, second half (Autumn 2025): the lecture this
  chapter follows. https://www.youtube.com/watch?v=Lxh9RF5S-K0

**Further reading:**
- RLEF paper: the two-tier test strategy and hybrid
  token/turn-level policy details.
- Schulman et al., PPO (2017): the policy-gradient algorithm
  family the paper builds on.

**Caveats from these sources.** Algorithmic details (the exact
PPO variant, the hybrid policy formulation) are summarized from
the lecture, not re-derived. Read the paper for the equations.
The "first demonstration" framing is the lecture's, for coding
LLMs with execution feedback in this form.

## Connections to the other courses

- **CS329A L03:** the inference-time half of this chapter: the
  try-run-retry trajectory is a ReAct loop whose tool is code
  execution.
- **CS329A L06:** the train-time half generalized: STaR applies
  the same keep-the-winners idea to reasoning traces.
- **CS329A L07:** the missing piece: judging intermediate steps,
  not just outcomes.
- **CS329Z:** building the harnesses: sandboxed code execution
  and test infrastructure for agents.
