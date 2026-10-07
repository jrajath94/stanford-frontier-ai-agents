# U05 answer keys

Kept separate from `lessons/u05_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: 4 candidates x 20 examples = 80 scored calls. SE = sqrt(0.7 x 0.3/20) = sqrt(0.0105) = 0.10.
- E2: the feedback names the wrong fault, so the edit optimizes the wrong thing. The scores fall because the diagnosis was fiction.
- E3: trust only gaps larger than about 2 standard errors. A 0.08 gap on n = 20 is not a finding.

## C02

- E1: at bar 0.78 the prompt rewrite (0.79) wins. At bar 0.80 fine-tuning (0.83) wins.
- E2: sqrt(0.79 x 0.21/200) = sqrt(0.00083) = 0.029.
- E3: spend in order: words first, weights second, compute last.

## C03

- E1: 8 x 1024 + 8 x 1024 = 16,384. Ratio 1,048,576/16,384 = 64.
- E2: 7B x 0.5 bytes = 3.5 GB.
- E3: the task's weight change must have rank at most r. Otherwise the adapter underfits.

## C04

- E1: 0.85 - 0.75 = 0.10.
- E2: the teacher is confidently wrong on a slice, and the student copies the confidence with the errors.
- E3: the teacher's quality bounds the student. A random teacher gives a random student.

## C05

- E1: m = (-2.0 + 2.5) - (-2.2 + 2.3) = 0.5 - 0.1 = 0.4.
- E2: the pairs reward length, so the loss pushes probability toward longer answers. The policy learns the annotators' bias.
- E3: small beta keeps the policy close to the reference. Large beta lets it chase the preferences hard.

## C06

- E1: 25 demos at $2 = $50. 5000 traces at $0.01 = $50. Total $100.
- E2: unfiltered traces include the agent's mistakes, and the learner copies them. The bad habits compound.
- E3: demos for the target moves, traces for coverage, feedback for ranking. Mix all three.

## C07

- E1: 1000 x 0.85 x 0.85 = 722.5.
- E2: the verifier shares the generator's blind spot, so both accept the same bad examples. The loop converges to the blind spot.
- E3: track the feature variance each generation. Falling variance is the collapse alarm.

## C08

- E1: 1000 x 0.10 x 7 = 700 traces per week.
- E2: the flag rule selects failures only, so the retrain set forgets successes. The model degrades on the easy cases.
- E3: audit the flag rule quarterly. A biased flag compounds.

## C09

- E1: 0.08 - 0.02 = 0.06.
- E2: the top-100 are near-duplicates of one template. The budget buys the same lesson 100 times.
- E3: validate the selection rule on a pilot before spending the full budget.

## C10

- E1: 12/200 = 0.06.
- E2: the paraphrase shares no 13-gram, so the detector misses it. The score stays inflated.
- E3: training teaches, eval judges. A judge with prior access to the answers is not a judge.

## C11

- E1: mean v = 0.65, mean h = 0.50. Gap = 0.15.
- E2: the optimizer climbs the validator's 0.15 optimism while human-judged quality stays flat. The metric became the goal.
- E3: calibrate before optimizing. The optimizer amplifies validator errors.

## C12

- E1: 0.74 + 0.04 = 0.78.
- E2: the debug informed the next tune, so the vault became dev. The number is no longer unbiased.
- E3: dev is the workbench, the test is the referee, the vault opens once.
