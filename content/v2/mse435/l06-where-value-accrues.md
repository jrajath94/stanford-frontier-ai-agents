---
page_id: mse435-l06
course_slug: mse435
course_name: "MS&E 435: Economics of the AI Supercycle"
course_order: 9
order: 6
nav: "L06 · Where Value Accrues"
title: "Lecture 6: Where Value Accrues"
summary: "The course's core question: in 2026 value accrues below the model. The token economy's new primitives: the AI gateway as CDN for tokens, the sandbox as EC2 for agents, and how to bet."
date: "2026-04"
instructor: "Apoorv Agrawal"
offering: "Spring 2026"
video_id: HA7lZd7zk3M
video_title: "Applications, Coding AI"
video_caption: "Guest: Guillermo Rauch, Founder and CEO of Vercel. This lesson covers the second half: value accrual, the token economy, and long/short picks."
concepts: [value-accrual, token-economy, ai-gateway, semantic-cache, sandbox, block-economy, pricing-models, long-short]
sources:
  - tag: video
    label: "Stanford MS&E435 Economics of the AI Supercycle, Applications, Coding AI (Guillermo Rauch, Vercel)"
    url: https://www.youtube.com/watch?v=HA7lZd7zk3M
---

## The course's core question

Every session of MS&E435 circles one question, and the
host asks it directly in this one: from chips to data
centers to infrastructure below the model, the model,
and the agents above it, **where will value accrue?**

Rauch's answer is dated and specific: "at least in
2026, right this second," value concentrates **below
the model**. Chips, data centers, power, cooling,
energy. Above the model there is real value, in coding
models, customer support, legal, and other verticals,
but it is narrow and concentrated. The money is in the
picks and shovels.

This chapter is the map of that answer: why the value
sits where it does, the new primitives being built to
capture it, and how the guests say to bet.

## Why below the model wins (for now)

Three forces push value down the stack, and each one
has a number from the course.

**1. The CapEx is the moat.** L02 priced it: $60M per
MW, $60B per gigawatt. Capital at that scale is its
own barrier. Few players can finance AI factories, so
the returns concentrate among those who can.

**2. Demand outruns supply.** The Applied Compute
session named compute scarcity outright: demand far
outpacing supply. Scarcity prices flow to the scarce
input. Today that input is energized compute, not
model weights.

**3. Models commoditize faster than infrastructure.**
The Crusoe session's long/short said it plainly: old
compute commoditizes, but so do old models, and open
source takes share from closed-source model players.
A data center's revenue can be repriced per token for
a decade. A model's pricing power erodes with every
open release.

The honest qualifier is the date. "In 2026" is doing
real work in Rauch's sentence. Value accrual moves as
bottlenecks move, and L01 showed bottlenecks always
move.

## Tokens: the new commodity

The unit of the new economy is the **token**: a chunk
of text the model reads or writes, roughly a word or
part of one. Rauch's framing: Vercel used to stream
pixels to users. Now it streams intelligence in the
form of tokens. Tokens are, in his phrase, "the new
hot commodity."

This changes the pricing model of software. **SaaS**
sold **seats**: a fixed price per user per month.
The token economy sells **intelligence by the unit**:
pay for what you use, metered in tokens. The death of
the seat and the rise of the token is the same event
as L05's SaaS reckoning, priced.

Figure L06-F1. Seats versus tokens. Source: original
diagram for Stanford Frontier AI, drawn from the
session.

```ascii
SaaS:          $X per seat per month      (pay for access)
token economy: $Y per million tokens     (pay for intelligence used)

The meter moves from the user to the unit of cognition.
```

## The AI gateway: a CDN for tokens

Every new commodity needs infrastructure, and the
session builds it by analogy. In the first internet,
pages needed **CDNs** (content delivery networks):
companies like Akamai and Fastly that scaled,
accelerated, and secured the delivery of pixels.

Tokens need the same treatment. Rauch's **AI gateway**
is "a CDN for tokens": a layer in front of the model
providers that observes token traffic, fails over
between providers, secures it, accelerates it, caches
it, and load-balances it.

The worked example is the session's most memorable
piece of arithmetic. Saying "thanks" to a flagship
model activates something like **300 GPUs** to produce
"you are welcome." A smart gateway sees the request,
recognizes it needs no frontier intelligence, and
routes it to a small model behind the scenes. That is
**semantic caching**: caching by meaning, not by exact
text. The 300 GPUs stand down. The margin is the
difference between flagship cost and small-model cost,
captured on every trivial request at planetary scale.

```ascii
naive:    "thanks" --> flagship --> ~300 GPUs --> reply
gateway:  "thanks" --> small model --> reply (cached by meaning)
```

Rauch notes the product reuses about 95 percent of
Vercel's existing CDN machinery: the same rocket
engine, new fuel. That reuse is itself an economic
point about why incumbents of the pixel CDN era have
a head start in the token CDN era.

## The sandbox: EC2 for agents

The second primitive is compute. **EC2** taught the
world elastic compute: a computer per credit card,
scalable to a million machines. But EC2 was designed
for human-written code.

Agents need their own unit. Rauch's **sandbox** is, in
his words, the EC2 of agents: an ephemeral computer
handed to an agent to work in. The mechanism has a
striking precedent. In post-training, models are
handed Docker containers with broad permissions: they
cut their teeth inside mini-computers before facing
the world. Giving a model a computer extracts more
capability from it, the way giving a new hire a laptop
extracts more from the hire. IT pre-installs software
for the human. The sandbox pre-provisions tools for
the agent.

The economics follow. Vercel's sandbox reuses the same
virtualization primitive as every deployment on the
platform, which is why, Rauch says, almost nothing
broke during the deployment surge: the company 3x'd
in months and doubled daily deployments since
January on machinery it already operated. And the
security corollary: like the PC revolution brought
viruses and phishing, agents bring exfiltration and
leakage, so sandbox security is a product category
being born in real time.

Figure L06-F2. The primitive map. Source: original
diagram for Stanford Frontier AI, drawn from the
session.

```mermaid
flowchart LR
  A["pixels era: CDN"] --> B["tokens era: AI gateway"]
  C["humans era: EC2"] --> D["agents era: sandbox"]
  B --> E["observe, fail over, cache, balance"]
  D --> F["ephemeral computer per agent"]
```

## The block economy: why agents picked Vercel

The host presses on the session's most startling
statistic: in a test of 86 agent runs, Claude chose
Vercel's deployment option **86 out of 86 times**,
and the report the guest cites gives Vercel's UI
engine a 90.1 percent "near monopoly." Was it a deal?
Rauch will not confirm or deny commercial
arrangements, but his substantive answer is a theory
of agent choice.

Agents reuse what they know. Models trained on the
internet's code learned Next.js, React, and the
open-source stack deeply. When asked to build a SaaS
app, the agent reaches for the familiar. But there is
a deeper mechanism: **local reasoning**. Rauch's
example is Tailwind, the CSS framework he bet on early
despite its ugly-looking code. Tailwind lets a
developer reason about one component in isolation: it
works the same wherever it is placed. That property,
shared by React and Next.js, is what makes code
**composable** for agents operating in a finite
**context window** (about a million tokens: not nearly
enough to hold all of humanity's code). The agent
cannot swallow the world, so it assembles blocks.

Mitchell Hashimoto, the HashiCorp founder who joined
Vercel's board, calls this the **block economy**: the
market for building blocks agents can snap together.
Rauch's strategic moral: if you want Claude Code or
Codex to choose your technology, build blocks with
agentic ergonomics. Open infrastructure wins because
agents need a target to throw code at.

## How to bet: the long/short

Both guest sessions end with long/short picks, and
together they are the course's investment summary.

**Rauch's long:** anyone "moving at the speed of
tokens." Concretely: companies with consumption-based
pricing, instant signup, and agent-ready interfaces
(MCP, CLIs, APIs). His provocation to his own company:
"no more rate limits." Rate limiters encode guesses
about maximum demand ("no company will deploy more
than 100 times per minute"), and in the agent era
those guesses keep being wrong. A YC company that did
not exist three months earlier now produces deployment
volumes that surprise Vercel itself.

**Rauch's short:** static data and content businesses
(his early call: Stack Overflow, a database of
programming Q&A, against free model answers);
companies built on the premise that code is scarce or
hard to produce (drag-and-drop builders, "coding with
training wheels," which he calls patronizing); and
companies that do not open up, the e-brochure
enterprises where agents cannot reach the raw signal.

**Lochmiller's long/short** (from the Crusoe
session): long the buildout, with the bear case aimed
at the legacy electrical stack (Eaton, Schneider):
fine near-term, at risk long-term if power
electronics and solid-state transformers collapse
their costs. And open source taking share from
closed-source model players.

The through-line: bet on the layers where demand is
growing faster than supply can respond, and against
the layers where AI turns a scarce asset (code,
answers, interfaces) into a commodity.

## Mapping back: the accrual map

| Stack layer | Value in 2026 | Why |
|---|---|---|
| Energy, power equipment | High and rising | The scarce input; turbines tripled; grid buildout lags. |
| Data centers, GPUs | High | $60B/GW moat; demand outruns supply; 2-4yr payback. |
| Model labs | Concentrated | Coding models monetize; open source erodes closed pricing. |
| Token infrastructure | Being built | AI gateway, sandbox: the CDN and EC2 of the agent era. |
| SaaS applications | Bifurcating | Systems of record hold; plastic presentation layers commoditize. |
| Static content/data | Short | Models answer for free; generator-verifier gap automates tasks. |

## The honest price: today's map expires

The chapter's price is the one Rauch states himself:
the map is dated 2026. Value accrues below the model
**right this second** because that is where scarcity
sits. Scarcity moves. If compute supply catches
demand, if open models commoditize the gateway layer,
if agents learn to route around today's primitives,
the map redraws. The durable skill the course teaches
is not the 2026 answer but the method: find the
bottleneck, price the unit, follow the margin. That
method is the whole course in one line.

> [!QA]
> Q: Where does value accrue in the AI stack, and why below the model?
> A: In 2026, below the model: chips, data centers, power, cooling, energy. Three reasons. The CapEx is the moat: $60B per gigawatt admits few players. Demand outruns supply: compute scarcity is the stated fact of the era. And models commoditize faster than concrete: open source erodes closed-model pricing while a data center reprices per token for a decade. Above the model, value exists but is narrow: coding models, support, legal.
> Follow-up: What moves value up the stack?
> A: Scarcity moving. If energized compute stops being the bottleneck, pricing power flows to whoever owns the customer relationship or the proprietary data. The specialization layer of L04 is the candidate: enterprise evals and telemetry cannot be commoditized by open weights. Watch the bottleneck, not the layer.

> [!QA]
> Q: What is the AI gateway, and what is semantic caching?
> A: The AI gateway is a CDN for tokens: it observes, fails over, secures, accelerates, caches, and load-balances traffic to model providers, the way Akamai did for pixels. Semantic caching is its sharpest trick: cache by meaning, not exact text. Saying "thanks" to a flagship model can activate around 300 GPUs to write "you are welcome." The gateway routes that to a small model instead. The margin is the cost difference, captured on every trivial request at scale.
> Follow-up: Why does Vercel have a head start here?
> A: Reuse. Rauch says the gateway reuses about 95 percent of the CDN machinery Vercel already operates: the same rocket engine, new fuel. Pixel delivery and token delivery share the hard problems: global points of presence, failover, caching, abuse handling. The incumbent advantage transferred across the commodity boundary.

> [!QA]
> Q: What is the sandbox, and why do agents need computers?
> A: The sandbox is EC2 for agents: an ephemeral computer provisioned per agent task, then destroyed. Agents need computers because tool use extracts more capability from a model: in post-training, models are handed Docker containers and learn by doing, the way a new hire with a laptop outperforms one without. IT pre-installs software for humans; the sandbox pre-provisions tools for agents. Vercel's version reuses its deployment virtualization primitive, which is why the 3x deployment surge broke almost nothing.
> Follow-up: What is the security implication?
> A: A new product category. The PC era brought viruses and phishing with every new computer; the agent era brings exfiltration and data leakage with every new sandbox. Agents can be tricked into leaking data the way users were tricked by Nigerian-prince emails. Sandbox isolation, permissions, and monitoring are being built now, in real time, as the attack surface grows.

> [!QA]
> Q: What is the block economy?
> A: Mitchell Hashimoto's term for the market in composable building blocks that agents snap together. Agents cannot fit all of humanity's code in a million-token context window, so they assemble local-reasoning components: Tailwind, React, Next.js, shadcn. The 86-out-of-86 result, Claude choosing Vercel's deployment every time, is agents voting for the blocks they know. The strategic moral: to be chosen by agents, build open blocks with agentic ergonomics, because agents reuse what they can reason about locally.
> Follow-up: How does the block economy relate to the 100ms Amazon rule?
> A: Both are about the economics of the interface. Amazon found that 100ms of slowdown costs 1 percent of conversion: speed is money in the pixel era. In the block economy, composability is money: the block that snaps in fastest wins the agent's choice. Different eras, same lesson: reduce the friction between intent and outcome, and the market pays.

## Recap: the whole lesson on one screen

1. **The question.** From chips to agents: where does
   value accrue? In 2026: below the model.
2. **Why below.** The CapEx is the moat ($60B/GW),
   demand outruns supply, and models commoditize
   faster than concrete.
3. **Tokens.** The new commodity. Vercel went from
   streaming pixels to streaming intelligence.
   Pricing moves from seats to tokens.
4. **The AI gateway.** A CDN for tokens: observe,
   fail over, secure, accelerate, cache, balance.
   Semantic caching stands down 300 GPUs for
   "thanks."
5. **The sandbox.** EC2 for agents: an ephemeral
   computer per task. Models plus computers beat
   models alone, like hires plus laptops.
6. **The block economy.** Agents assemble
   local-reasoning blocks (86/86 for Vercel).
   Build open blocks with agentic ergonomics.
7. **The bets.** Long: anyone moving at the speed
   of tokens (usage pricing, MCP, instant signup).
   Short: static content, code-is-scarce builders,
   closed e-brochure enterprises.
8. **The expiry.** The map is dated 2026. The durable
   skill is the method: find the bottleneck, price
   the unit, follow the margin.

## Official sources and further reading

**Official:**
- Applications, Coding AI (MS&E 435, Spring 2026),
  guest Guillermo Rauch, Vercel:
  https://www.youtube.com/watch?v=HA7lZd7zk3M
- MS&E 435 course site: https://mse435.stanford.edu/

**Further reading:**
- The "Economics of Generative AI" session (course
  introduction): value accrual in the AI stack, market
  trends and revenue:
  https://www.youtube.com/watch?v=LNSvp-9b-J0

**Caveats from these sources.** "In 2026" is Rauch's
own dating of the below-the-model call. The 300-GPU
"thanks" is his illustrative meme, not a metered
measurement. The 86/86 and 90.1 percent figures come
from a report the guest cites, not from Vercel's own
audit. The Amazon 100ms-to-1-percent figure is
Amazon's published finding as quoted by the guest.

## Connections to the other courses

- **MS&E435 L01/L02:** the below-the-model value:
  the digital-labor thesis and the $60M megawatt it
  prices.
- **MS&E435 L05:** the seat-to-token transition from
  the application side: why SaaS pricing had to die.
- **CS229S:** the systems behind the gateway and
  sandbox: caching, batching, and serving at scale.
- **CME295:** product thinking for the token era:
  what to build when intelligence is metered.
