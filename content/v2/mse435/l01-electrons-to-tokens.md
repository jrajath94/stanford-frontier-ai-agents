---
page_id: mse435-l01
course_slug: mse435
course_name: "MS&E 435: Economics of the AI Supercycle"
course_order: 9
order: 1
nav: "L01 · From Electrons to Tokens"
title: "Lecture 1: From Electrons to Tokens"
summary: "Why the five hyperscalers are spending $650B: the AI production function, the Cobb-Douglas growth equation, and digital labor as the first digitally scalable labor force in history."
date: "2026-04"
instructor: "Apoorv Agrawal"
offering: "Spring 2026"
video_id: GcCGzfKdCd0
video_title: "Building AI Factories"
video_caption: "Guest: Chase Lochmiller, Co-Founder and CEO of Crusoe. Session covers infrastructure and building AI factories at gigawatt scale."
concepts: [supercycle, capex, production-function, cobb-douglas, digital-labor, gdp-growth, energy-first]
sources:
  - tag: video
    label: "Stanford MS&E435 Economics of the AI Supercycle, Building AI Factories (Chase Lochmiller, Crusoe)"
    url: https://www.youtube.com/watch?v=GcCGzfKdCd0
  - tag: supplement
    label: "MS&E 435 course site: mse435.stanford.edu"
    url: https://mse435.stanford.edu/
---

## The chart that opens the course

The first session opens on one chart. It plots the capital
expenditure of the five hyperscalers on AI, and the line goes up
and to the right, fast. To put the scale in context, the host
frames it as one of the largest investments ever made: bigger
than the space program, bigger than the interstate highway
system, bigger than the Manhattan Project. Second only to the
United States defense budget.

The natural question is the one the host puts to the guest:
when the hyperscalers spend on the order of $650 billion
building data centers, where does that money actually go?

This chapter builds the answer from zero. It starts with what
it takes to produce AI at all, then shows why the spending is
rational under one economic model, and then follows the money
down into the physical stack. The next chapter opens the
dollar itself.

## The AI production function

Before the money, the recipe. The guest, Chase Lochmiller of
Crusoe, starts with a plain question: what does it take to
produce AI? His answer is an equation with five ingredients.

```ascii
AI = data + algorithms + compute + energy + data centers

data        the text, images, and labels models learn from
algorithms  backpropagation, neural networks, transformers
compute     GPUs doing parallel tensor math at high speed
energy      the electricity that runs the GPUs
data centers  the buildings that house and cool the machines
```

Read each ingredient the way an economist reads an input to a
factory. **Data** is raw material. Companies like Scale AI buy
and label it; the transcript also names Mercor
[uncertain: the transcript reads "Merkur"] and Handshake as
players in this market. **Algorithms** are the process
technology, invented mostly inside the research labs: new
architectures, recursive learning techniques, better ways to
use the data. **Compute** is the machinery: large numbers of
GPUs running the same math in parallel. **Energy** is the
fuel. **Data centers** are the factory buildings.

The striking claim is which ingredients draw the money.
Data and algorithms matter, but the guest says the spending
concentrates on the last three: compute, energy, and data
centers. That is where Crusoe sits, and that is where the
CapEx chart is pointing. The rest of this chapter explains
why investors believe the return justifies it.

## The growth equation

The guest reaches for a classic economics model to explain
the bet. It is called the **Cobb-Douglas** model of
production, and it decomposes the growth of an economy into
three additive parts.

```ascii
GDP growth = change in labor + change in capital + change in technology

labor       more workers, or more productive hours
capital     buildings, plants, equipment, invested money
technology  ideas that make labor more productive
```

A **supercycle** is a long wave of investment driven by a
general-purpose technology: the PC, the internet, mobile,
and now AI. The course site names AI "the biggest technology
supercycle since the PC, Internet, and Mobile." The
Cobb-Douglas frame says a supercycle earns its name when it
moves one of the three terms hard.

Technology gets most of the press. The guest's argument is
about labor. Historically, the labor term could only change
through the birth rate: a 20-year lead time, because a new
worker must be born, raised, schooled, fed, and housed
before producing anything. Labor was the slow term. Capital
could move fast. Labor could not.

Now run the toy version. Suppose an economy grows 3 percent
a year, split evenly: 1 point from labor, 1 from capital, 1
from technology. The labor point is capped by demography.
No investment decision made this quarter changes how many
20-year-olds exist. The term is, for all practical purposes,
fixed on any horizon a company plans against.

AI breaks the cap. When you hand a task to a coding agent
("build a CRM for my new product") and it does the work,
that is labor being produced. Not a tool assisting a worker.
Labor itself, created by buying data centers and GPUs. The
guest's phrase is **digital labor**: the first labor force
in history whose size changes through an investment
decision instead of a birth rate.

```ascii
traditional labor:  birth rate --> 20-year wait --> new worker
digital labor:      CapEx     --> build data center --> new workers
```

That is the thesis behind the chart. The $650 billion is
not a bet that chatbots are fun. It is a bet that the labor
term of the growth equation can now be scaled the way
capital always could, and that whoever builds the factories
for digital labor captures the return.

## Why energy comes first

Here the chapter turns from the thesis to the strategy it
implies. If digital labor is the prize, the bottleneck is
whatever gates the factories. The guest's founding insight,
from just under a decade of building, was that the scarce
resource was **energy**, not chips.

The reasoning is market logic. Data center capacity had
grown steadily through the web 2.0 era, clustering in
established hubs. Northern Virginia, which the guest names,
runs a large share of the internet. Building "the next data
center in Northern Virginia" was a crowded trade. Meanwhile
the new workloads, AI training with backpropagation and
proof-of-work crypto, shared one trait: at scale, they are
limited by energy.

So Crusoe inverted the usual plan. Instead of moving energy
to the computers, move the computers to the energy. Find
places with abundant cheap power that are not historical
data center markets, and build there.

The worked example is Abilene, Texas, and it deserves the
arithmetic. West Texas had attracted heavy renewable
investment because production tax credits paid developers
to produce clean electrons. The result was overbuild:
more generation than the grid could carry out, and no
marginal buyer. Power prices went negative. Crusoe signed
its first two buildings there in June 2024, and the site
is now described as one of the largest AI computing
campuses in the world, possibly the largest.

Figure L01-F1. The energy-first inversion. Source: original
diagram for Stanford Frontier AI, drawn from the session.

```ascii
usual plan:        build data center in hub --> buy expensive power
Crusoe plan:       find cheap stranded power --> build data center there
Abilene trigger:   tax credits --> renewable overbuild --> negative prices
```

The campus numbers set the scale for the whole course.
A 200 MW substation and a 1 GW substation, the latter
described as the largest privately owned substation in the
United States. One gigawatt is roughly the power draw of
the city of Denver, the guest's home town. The full campus
is 2.1 gigawatts in aggregate: two Denvers of power, all
feeding computers. Eight buildings serve Oracle and
OpenAI, the project known as Project Stargate, plus a
350 MW natural gas plant built to energize the cluster
and an expansion planned for Microsoft.

## The moving bottleneck

A common misunderstanding is that the binding constraint
in AI is fixed. The guest insists it moves, and the
history of the last four years proves it.

```ascii
4 years ago:    compute (get the chips)
then:          memory (memory stocks ripping)
today:         energized data centers (power shells you can plug into)
always:        labor (electricians, welders, plumbers, construction)
```

**Chips have softened as the bottleneck.** Access to GPUs
is better than it was. The binding constraint today is
finding places where you can put the chips and turn them
on: powered shells with the electrical and cooling plant
ready. And underneath every phase, labor: the guest calls
the shortage of tradespeople a bottleneck in its own
right, with 9,000 people on site at Abilene every day
against a town of 120,000.

This is why Crusoe is **vertically integrated**, meaning
it owns multiple layers of the stack instead of one. The
company works from energy development at the bottom,
through the data center buildings, up to GPU cluster
deployment and managed services at the top. When the
bottleneck moves, a single-layer company is stuck; a
vertically integrated one retools. The guest is explicit
about the boundary: not in the chip business, not in the
model business. Everything between energy and tokens.

Figure L01-F2. The bottleneck timeline. Source: original
diagram for Stanford Frontier AI, drawn from the session.

```mermaid
flowchart LR
  A["4 years ago: chips"] --> B["then: memory"]
  B --> C["today: energized shells"]
  C --> D["underneath: skilled labor"]
```

## Mapping back: why the money is rational

Each piece of this chapter answers the opening question.

| Opening puzzle | This chapter's answer |
|---|---|
| Why $650B of CapEx? | Digital labor: the labor term of GDP growth is now investable. The spending buys workers, not just tools. |
| What does AI need? | Five inputs: data, algorithms, compute, energy, data centers. The money concentrates on the last three. |
| Why start from energy? | At scale, energy is the scarce input. Stranded cheap power (Abilene) beats a crowded hub (Northern Virginia). |
| What gates growth? | A moving bottleneck: chips, then memory, now energized shells, always skilled labor. Vertical integration is the hedge. |

## The honest price: the thesis can be wrong

Every investment thesis has a falsifier, and this one is
sharp. The entire $650 billion rests on tokens staying
valuable: on digital labor actually substituting for human
labor at a price that covers the factories. If the demand
for tokens stalls, the chart is a monument to overbuild,
and the depreciation question in the next chapter becomes
an obituary.

The guest names his own long-run risks later in the
session: open source models taking share from closed
ones, and the legacy electrical stack being disrupted by
power electronics. The price of the thesis is that it must
be right about demand for a decade. The next chapter
checks whether the unit economics give it that decade.

> [!QA]
> Q: What is the AI production function, in plain words?
> A: Five inputs make AI: data, algorithms, compute, energy, and data centers. Data is the raw material, algorithms are the process technology, GPUs are the machinery, electricity is the fuel, and data centers are the factory buildings. The guest's key claim is that the money concentrates on the last three. Data labeling created a real market (Scale AI and others), and algorithms live in the labs, but the CapEx chart is compute, energy, and buildings.
> Follow-up: Why would an investor care about this decomposition?
> A: Because it tells you where the spending must flow. If AI output scales with compute and energy, then every unit of AI demand converts mechanically into demand for GPUs, power plants, and data centers. The investor question becomes unit economics per megawatt, which is the next chapter.

> [!QA]
> Q: Explain the Cobb-Douglas argument for the AI supercycle.
> A: Cobb-Douglas decomposes GDP growth into three parts: change in labor, change in capital, and change in technology. Historically the labor term moved only through the birth rate, with a 20-year lead time, so it was the slow term. Digital labor breaks that: an agent doing real work is labor produced by an investment decision. For the first time, the labor term can scale the way capital always could, which is the economic case for building AI factories at gigawatt scale.
> Follow-up: What would falsify this thesis?
> A: Token demand stalling. If digital labor does not substitute for human labor at prices that cover the factories, the CapEx is overbuild. The guest's own bear cases point the same way: open source eroding closed-model pricing power would compress the revenue side of the trade.

> [!QA]
> Q: Why did Crusoe start from energy instead of compute?
> A: At scale, energy was the scarce input, and markets are reasonably efficient everywhere else. The web 2.0 era had already filled the established hubs like Northern Virginia. The new workloads (AI training, proof-of-work) are energy-hungry at scale, so the winning move was to find cheap stranded power and bring the computers to it. Abilene is the worked example: renewable overbuild from production tax credits pushed power prices negative, and Crusoe built one of the world's largest AI campuses there, now 2.1 gigawatts in aggregate.
> Follow-up: What is the risk of the energy-first strategy?
> A: Stranded power is stranded for a reason: no transmission, no local demand. If the grid buildout catches up or the tax regime changes, the cost advantage narrows. The Abilene answer was to build its own 1 GW substation and a 350 MW gas plant, which converts the risk into more CapEx.

> [!QA]
> Q: What is a power shell, and why is it the bottleneck today?
> A: A power shell is an energized data center: the building, the substation, the cooling, everything needed so that you can plug in chips and start computing. Chips themselves have become easier to get. The scarce thing is a place to turn them on. Underneath that, skilled labor binds too: electricians, welders, plumbers, and construction workers, with projects like Abilene putting 9,000 people on site daily in a town of 120,000.
> Follow-up: Why does vertical integration help with a moving bottleneck?
> A: Because the bottleneck moves: chips four years ago, memory after that, energized shells today. A company that owns one layer is hostage to whichever layer binds. Crusoe spans energy development, buildings, GPU clusters, and managed services, so it can attack whichever layer is gating growth, while staying out of chips and models.

## Recap: the whole lesson on one screen

1. **The chart.** Hyperscaler AI CapEx goes up and to the
   right, fast. Roughly $650 billion. Bigger than the space
   program, the highways, the Manhattan Project.
2. **The recipe.** AI needs data, algorithms, compute,
   energy, and data centers. The money concentrates on the
   last three.
3. **The growth equation.** Cobb-Douglas: GDP growth is
   change in labor plus change in capital plus change in
   technology.
4. **The slow term.** Labor historically moved only via
   the birth rate: a 20-year lead time. Fixed on any
   planning horizon.
5. **Digital labor.** Agents doing real work are labor
   produced by investment. The labor term is now scalable
   like capital. That is the $650B thesis.
6. **Energy first.** At scale, energy is the scarce input.
   Move the computers to the cheap power, not the reverse.
7. **Abilene.** Tax credits caused renewable overbuild,
   prices went negative. Now a 2.1 GW campus: two Denvers
   of power, 9,000 workers on site, a 1 GW substation.
8. **The moving bottleneck.** Chips, then memory, now
   energized shells, always skilled labor. Vertical
   integration is the hedge. Next: the dollar anatomy.

## Official sources and further reading

**Official:**
- Building AI Factories (MS&E 435, Spring 2026), guest
  Chase Lochmiller, Crusoe:
  https://www.youtube.com/watch?v=GcCGzfKdCd0
- MS&E 435 course site: https://mse435.stanford.edu/

**Further reading:**
- The course site's framing line: AI is "the biggest
  technology supercycle since the PC, Internet, and
  Mobile."

**Caveats from these sources.** The $650B figure is the
host's framing of hyperscaler spend, not an audited total.
The transcript spells the guest's name "Lockmiller" in
places; the course site spells it "Lochmiller," used
here. One data-labeling company is transcribed as
"Merkur" [uncertain: likely Mercor]. The Cobb-Douglas
treatment is the guest's intuitive version (growth as a
sum of three changes), not the formal multiplicative
production function. Abilene "largest campus" is the
guest's claim, stated with hedging.

## Connections to the other courses

- **CS229S:** the systems course prices the same stack
  from the inside: what the GPUs cost to run, why
  inference is memory-bound, and what FlashAttention saves.
  Read it for the engineering behind the dollars here.
- **CS336:** builds the transformer and the training
  stack that all this infrastructure exists to serve.
- **CS329A / CS329Z:** the agents course covers the
  digital labor itself: what agents can do and where
  they break.
- **MS&E435 L02:** opens the $60M megawatt and checks
  whether the unit economics pay back.
