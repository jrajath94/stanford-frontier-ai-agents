---
page_id: mse435-cheatsheet
course_slug: mse435
course_name: "MS&E 435: Economics of the AI Supercycle"
course_order: 9
order: 900
nav: "MS&E 435 · Cheatsheet"
title: "MS&E 435 Cheatsheet"
summary: "Every key fact from MS&E 435 on one dense page: the thesis, the dollar, the models, the enterprise layer, SaaS, and where value accrues."
date: "2026-04"
instructor: "Apoorv Agrawal"
offering: "Spring 2026"
---

The whole course as a set of short stories. Each block
tells one idea the way the lesson tells it: the
problem, the number, the fix. Follow the links for the
full derivations.

<div class="cheat-cols" markdown="1">

<div class="cheat-block" markdown="1">

### Digital labor

GDP growth = change in labor + change in capital +
change in technology (Cobb-Douglas, intuitive form).
Labor historically moved only through the birth rate,
a 20-year lead time. Agents doing real work are labor
produced by investment: the first labor force in
history that scales like capital. That is the $650B
CapEx thesis. It is bigger than the space program,
the highways, and the Manhattan Project. Falsifier:
token demand stalling.
[L01](l01-electrons-to-tokens.html)

</div>

<div class="cheat-block" markdown="1">

### The AI production function

AI = data + algorithms + compute + energy + data
centers. The money concentrates on the last three.
Crusoe's founding inversion: at scale, energy is the
scarce input, so move the computers to the cheap
power. Abilene: renewable overbuild from tax credits
pushed power prices negative. Now a 2.1 GW campus
(two Denvers), a 1 GW substation, 9,000 workers on
site in a town of 120,000. Bottlenecks move: chips,
then memory, now energized shells, always skilled
labor. Vertical integration is the hedge.
[L01](l01-electrons-to-tokens.html)

</div>

<div class="cheat-block" markdown="1">

### The $60M megawatt

$20M/MW builds the factory: labor $4.7M (the
bottleneck bar), gas plant $2-3M (turbines tripled
from $1M/MW), electrical (34.5 kV to 480 V),
mechanical (1M-gallon closed water loop, home-scale
annual use), materials. $40M/MW fills it: GPUs $30M,
networking $4M (one coherent cluster), CPUs + storage
$3M (CPUs now scarce too). Total $60B per gigawatt.
Half of it is GPUs. [L02](l02-sixty-million-megawatt.html)

</div>

<div class="cheat-block" markdown="1">

### The payback

OpEx is only $1-2M/MW/yr. Renting bare chips brings
~$15M/MW/yr: a four-year payback on a revenue basis.
Add the managed token layer ("from electrons to
tokens") and revenue rises toward $30M/MW/yr: about
a two-year payback. The variable that matters is
depreciation: six years is the standard, and H100
rental prices rose above launch three years in.
Abstraction (customers never see the chip) stretches
useful life. [L02](l02-sixty-million-megawatt.html)

</div>

<div class="cheat-block" markdown="1">

### The model eras

2012 AlexNet: GPUs + ImageNet beat handcrafted
features. The bargain: uninterpretable scale.
2017 transformer: self-attention parallelizes on
GPUs, scales to long sequences. 2018-19
pre-training: next-token prediction on internet
text, backprop, trillions of tokens. The product: compression of
human knowledge into weights. Scaling laws: Kaplan
(bigger performs better, GPT-3), Chinchilla (scale
data with parameters). Intelligence becomes a
capital allocation problem. Then RLHF steers it
(GPT-4). Then o1 adds test-time compute. Chain of
thought emerges untrained. Plus tool use: agents.
[L03](l03-how-models-get-smarter.html)

</div>

<div class="cheat-block" markdown="1">

### The bottleneck tour

Compute, then architecture, then pre-training data,
then usability, now RL environments, next continual
learning (the hot-stove problem: one loud signal,
permanent learning). Code came first for three
reasons: RLVR gives free verifiable rewards
(compiles, unit tests), code tokens are abundant,
and code is AGI-complete, the general language for
acting on the world. Price of the chapter: the
pre-training data wall. Only frontier labs can still
play there. [L03](l03-how-models-get-smarter.html)

</div>

<div class="cheat-block" markdown="1">

### Evals and the 5 percent

Evals set the roadmap: define the hill, RL is the
eval-maxing machine (SWE-bench started the code
race). Never train on the eval itself. Evals stack
in tiers: lab evals steer base models, enterprise
evals steer specialization (JPMorgan's good is not
Goldman's). DeepSeek: ~150k GPU-hours of RL on
2.4-2.5M of pre-training, about 5%. Post-training is
cheap and its share is growing (data-center-wide
RL). General models set the floor. Specialization
sets the ceiling. [L04](l04-evals-rlvr-enterprise.html)

</div>

<div class="cheat-block" markdown="1">

### DoorDash and the Pareto frontier

DoorDash onboards 100k+ merchants a year. Menu
images plus a strict style guide defeated general
models. Fix: human-corrected outputs defined the
error rate, RL minimized it directly. No prompting.
Cognition/Windsurf: a small model trained hard on
bug-catching answers in under 2 seconds with
big-model accuracy. The production pattern is an
ensemble: general orchestrator, fast specialists,
proprietary data. Cursor's Composer shows continual
learning early: accept/revert telemetry as implicit
rewards, hours per step, massive batches.
[L04](l04-evals-rlvr-enterprise.html)

</div>

<div class="cheat-block" markdown="1">

### The SaaS reckoning

Coding agents are the biggest TAM expansion in
software history: the programmer-headcount cap on
cloud demand is gone. "Writing code does not make you
special. Deploying code does." Agentic
infrastructure has three sides: for agents (deploy
agent-written code), to build agents (ship your own:
Vercel's support agent answers 93%), automated by
agents (the self-driving cloud). SaaS was one shared
interface for everyone. Now the presentation layer
goes plastic (two people rebuilt Salesforce's
surface) while the system of record holds. Software
is basically free. Reflexivity says engagement
compounds anyway. Retention is the metric to watch.
[L05](l05-software-is-dead.html)

</div>

<div class="cheat-block" markdown="1">

### Where value accrues

In 2026: below the model. The CapEx is the moat
($60B/GW), demand outruns supply, and models
commoditize faster than concrete. Tokens are the new
commodity. Pricing moves from seats to tokens. The
AI gateway is a CDN for tokens (observe, fail over,
cache, balance). Semantic caching stands down ~300
GPUs when "thanks" needs no flagship. The sandbox is
EC2 for agents: an ephemeral computer per task.
The block economy: agents assemble local-reasoning
blocks (Claude picked Vercel 86/86). Long: anyone
moving at the speed of tokens. Short: static
content, code-is-scarce builders, closed
enterprises. The map is dated 2026. The method
(find the bottleneck, price the unit, follow the
margin) is durable. [L06](l06-where-value-accrues.html)

</div>

</div>
