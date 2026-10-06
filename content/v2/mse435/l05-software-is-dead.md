---
page_id: mse435-l05
course_slug: mse435
course_name: "MS&E 435: Economics of the AI Supercycle"
course_order: 9
order: 5
nav: "L05 · The SaaS Reckoning"
title: "Lecture 5: Software Is Dead, Long Live the Agent"
summary: "What coding agents do to the software business: the TAM explodes, writing code stops being special, SaaS becomes plastic, and the three-sided agentic infrastructure triangle."
date: "2026-04"
instructor: "Apoorv Agrawal"
offering: "Spring 2026"
video_id: HA7lZd7zk3M
video_title: "Applications, Coding AI"
video_caption: "Guest: Guillermo Rauch, Founder and CEO of Vercel. This lesson covers the first half: coding agents, the TAM explosion, and the death of SaaS."
concepts: [saas, coding-agents, tam-expansion, agentic-infrastructure, throwaway-software, system-of-record, reflexivity]
sources:
  - tag: video
    label: "Stanford MS&E435 Economics of the AI Supercycle, Applications, Coding AI (Guillermo Rauch, Vercel)"
    url: https://www.youtube.com/watch?v=HA7lZd7zk3M
---

## The question from L04

L04 showed enterprises building their own specialized
models. Follow that to its conclusion and an
uncomfortable question appears for the software
industry. If every company can generate its own tools,
what happens to the companies that sell software? This
chapter is the SaaS reckoning, told by Guillermo Rauch,
founder and CEO of Vercel, a $9.3 billion company that
sits exactly where the reckoning lands.

His background matters to the argument. Rauch grew up
in a suburb of Buenos Aires, taught himself to code,
learned English from software manuals, and bet his
company on open source because free tools were the only
tools he could access as a teenager. Vercel's founding
obsession was **developer experience**: deploying a
website on the clouds of the day took a seasoned
engineer weeks, and Rauch decided that was absurd.

## The TAM explodes

**TAM** is total addressable market: everyone who could
ever buy your product. Rauch's original TAM math was
simple. Roughly 20 million developers in the world
could create front-end projects, and Vercel would give
them the superpower to deploy: not just deploy, but
deploy globally fast and scalable, with no load
balancers to configure.

![The TAM expansion: who can create software](assets/plate-l05-tam.svg "Plate L05-F1. From the mainframe priesthood to anyone who can describe it. Shell 2. Source: original, drawn from the session. Project: Stanford Frontier AI.")

### Subchapter: the access ladder, with numbers

Rauch tells it as a history of expanding access. First
developers were a tiny priesthood around university
mainframes: thousands of people. Then the PC, the web,
and open source widened the circle to millions. Coding
bootcamps promised React in three months and added
hundreds of thousands. Vercel's bet was 20 million
developers. Each wave multiplied the creators by an
order of magnitude.

### Subchapter: the agents break the cap

Then coding agents arrived, and the math broke open. AI
is the biggest wave: anyone who can describe what they
want can now create software. The numbers moved fast.
Starting around October 2025, with the arrival of
strong coding models (the guest names Opus 4.5),
deployments on Vercel surged. His metaphor: coding
agents are the peanut butter being spread across the
whole world, and Vercel is the jelly: the deployment
layer underneath.

### Subchapter: elastic compute's broken cap

The cloud's economics used to be bounded by headcount.
**Elastic compute**, the EC2 idea of a computer per
credit card, was designed for human-written code: how
much compute you could sell was capped by how many
programmers existed. That cap is gone. Demand now
comes from agents writing, repairing, and securing
software around the clock. The marginal creator is no
longer a person with a salary. It is an agent with a
token budget.

## Writing code is not special. Deploying is.

Rauch's sharpest line is a redefinition of where value
lives. "Writing code does not make you special.
Deploying code and putting it in front of a customer
does make you special."

### Subchapter: the dead-software pile

The evidence is the world's pile of dead software.
GitHub, SourceForge, and their ancestors hold mountains
of code that never runs anywhere. Nobody can easily run
most repositories. The learning, Rauch argues, only
starts when a user confronts the running version. Code
is inventory. Running software is revenue.

### Subchapter: agents deploy compulsively

That is why agents changed his business: coding agents
do not share the human bias of keeping code safe on a
laptop. They love to deploy. The agent writes, tests,
ships, and iterates without the human's fear of the
red button. The behavior that made Vercel valuable,
frictionless deployment, is the behavior agents want
most.

### Subchapter: where value moved

This reframes the cloud itself. Rauch jokes that if
Amazon started AWS today it would not be Amazon Web
Services but **Amazon Agent Services**, because the
entity people now ship is the agent, not the page.
The infrastructure primitives are being rebuilt for
that entity, which is the next chapter's subject.
Value moved from the artifact (code) to the outcome
(running software in front of customers).

## The three-sided triangle

**Agentic infrastructure**, Rauch's term for the
rebuild, has three sides.

![The agentic infrastructure triangle](assets/plate-l05-triangle.webp "Plate L05-F2. Infrastructure for agents, to build agents, automated by agents. Shell 3. Source: original diagram for Stanford Frontier AI. Project: Stanford Frontier AI.")

### Subchapter: side 1, for coding agents

The peanut butter needs the jelly. When you use Claude
Code, Codex, or v0, the agent writes software that must
deploy somewhere. That somewhere, with domains, CDN,
and scaling handled, is side one. The economics:
every agent-written app is a deployment customer. The
more agents write, the more side one earns.

### Subchapter: side 2, to build your own agents

The guest's example: a founder pitching an AI-native
school. The product is not a set of web pages. It is
an agent, with humans (teachers, students) in the
loop. Vercel's own support agent belongs here: it now
answers **93 percent** of user inquiries, improved
satisfaction versus humans, and let the company give
free support to far more people. The 93 percent is the
proof that an agent can be the product, not the demo.

### Subchapter: side 3, automated by agents

The self-driving cloud. Rauch borrows an anecdote from
Stripe's founder: his pager-duty ringtone was ducks,
and years later hearing ducks still spikes his
cortisol. Running software at scale means 3 a.m.
pages. Vercel automated much of it, but the vision is
total: an agent that configures, monitors, and
optimizes everything, then reports back ("I made your
software twice as fast, here is the PR, conversion is
up").

## SaaS was the lowest common denominator

Now the reckoning proper. **SaaS**, software as a
service, was built on a compromise. Smart product
teams locked themselves in rooms and asked: what one
interface makes the most customers happy? Then they
shipped that interface to everyone. It worked because
building software was expensive, so one shared design
had to serve thousands of companies.

### Subchapter: the compromise mechanism, worked

Toy the economics. A SaaS company spends $2M building
one interface that serves 1,000 customers. Cost per
customer: $2,000. Building 1,000 tailored interfaces
would cost $2B. So the company builds one and calls it
a product. The compromise is not a choice. It is
arithmetic. When generation gets cheap, the arithmetic
flips: tailored interfaces cost prompts, not
engineers.

### Subchapter: the parking lot

Rauch's claim: that compromise is ending, because the
cost of a tailored interface collapsed. Two exhibits
from the session. **The parking lot.** A startup CEO
replaced the company's parking management software
with something he live-coded in v0, and saved real
money. How many brilliant Palo Alto companies were
ever going to build great parking software? None. An
entire category of mediocre software existed only
because building the good version was not worth
anyone's time. Now it is one or two prompts away.

### Subchapter: the Salesforce rebuild

**The Salesforce rebuild.** Inside Vercel, a team of
two rebuilt all of Salesforce for internal use:
account research, opportunity briefs, pitch
intelligence, generated on demand. Salesforce the
company is worth hundreds of billions. Two people
rebuilt its surface for their company's needs.

### Subchapter: the system of record stays

The crucial qualifier, which Rauch stresses: the
**system of record** stays. The database, the access
control lists, the workflows Salesforce built over
decades: those are not regenerated. What becomes
plastic is the **presentation layer**: the pixels on
top of the system of record, tuned to each business.
The split is not SaaS versus agents. SaaS keeps the system of record and grows an
agent-shaped surface.

![What goes plastic and what holds: the SaaS split](assets/plate-l05-split.svg "Plate L05-F3. The presentation layer goes plastic. The system of record holds. Shell 3. Source: original, drawn from the session. Project: Stanford Frontier AI.")

## Throwaway software and reflexivity

Push the logic one step further and software becomes
disposable. Rauch reports customers buying Vercel and
v0 so sales engineers can walk into a prospect meeting
with a custom version of the product already built.
Living software beats a slide deck. Three calls later
it is thrown away. Useful for one call, dead by
Wednesday.

### Subchapter: the retention question, worked

The host puts it sharply: **retention**. If software
is free and disposable, do people still need it on
Wednesday morning, or was it a Saturday-morning toy?
Toy the math: 100 generated apps, 90 die in a week,
10 become workflows. The 10 compound. The 90 were
cheap. The question is not whether most generated
software dies. It is whether the survivors are worth
more than the total cost of generation. At prompt
prices, they are.

### Subchapter: reflexivity

His summary line: "software is basically now free."
But free drives engagement, through what Shopify's
Tobi Lutke calls the **reflexivity of AI**. Once you
know you are one prompt away from communicating with
high-fidelity software, you never go back. Rauch wrote
years ago that it is hard to forego efficiency. the
coding-agent era is that essay coming true. Engineers
tell him they could never code the old way again.

## What stays hard

A common misunderstanding is that all software work
collapses to prompting. Rauch, who runs a company
that cannot stop hiring engineers, disagrees. The
audience for software changed, not the difficulty of
the deep work.

### Subchapter: the single-line quorum

His exhibit is Vercel's own infrastructure: sometimes
it takes a quorum of three agents plus smart humans
staring at a single line of code to decide what is
true. The plumbing of the agentic world, sandboxes,
gateways, isolation, remains genuinely hard
engineering.

### Subchapter: agent-to-agent support

What changed is who shows up at the door: customers
who have never heard of Vercel, whose agent brought
them there, asking for help through a transcript.
Support is becoming agent-to-agent, and Rauch's team
debugs by reading the customer's agent's transcript
like a flight recorder. The support ticket is now a
log of another machine's reasoning.

## What is used where: the coding-agent market, October 2026

- **Claude Code (Anthropic)** is the enterprise coding
  standard: roughly 54 percent of the enterprise
  coding market in early 2026, a multi-billion-dollar
  revenue line, and the default model inside Cursor.
  This is the agent Rauch's triangle is built for.
- **Codex (OpenAI)** is the challenger: OpenAI's
  agentic coding product, priced on the GPT-6 ladder.
  In enterprise coding share it sits near 21 percent,
  well behind Claude Code.
- **Cursor** is the distribution proof: the editor
  that made agents the default way to write code, with
  Claude as the default model and its own Composer
  model showing the continual-learning pattern from
  L04.
- **v0 (Vercel)** is the generation-to-deployment
  loop: the product in the parking-lot and Salesforce
  exhibits, generating interfaces from prompts and
  deploying them on the same platform.
- **Windsurf / Cognition** is the specialist bet: the
  small-model, sub-two-second feedback loop from L04's
  Pareto frontier, now an enterprise product category.

## Mapping back: the SaaS question, answered

| The fear | This chapter's answer |
|---|---|
| Agents kill software. | They kill the compromise: one shared interface for everyone. Tailored software is now cheap, so the average interface gets better, not worse. |
| What happens to SaaS companies? | The system of record survives. the presentation layer goes plastic. Winners expose agent interfaces: MCP, CLIs, APIs, consumption pricing. |
| Is anything defensible? | Taste, distribution, trust, the data underneath, and the infrastructure. Rauch is long anyone "moving at the speed of tokens." |
| Does engineering get easier? | The audience explodes. the deep work stays hard. Vercel cannot stop hiring engineers. |
| Who wins the agent market in 2026? | Claude Code on enterprise coding, v0 on generation-to-deploy, Cursor on distribution. |

## The honest price: retention

The chapter's price is the question the host puts
sharply: **retention**. If software is free and
disposable, do people still need it on Wednesday
morning, or was it a Saturday-morning toy? Rauch
drinks from the firehose and sees both: one-call
throwaway next to deeply embedded workflows. His bet
is reflexivity: once the efficiency is known, it is
never foregone. But he does not claim every generated
app survives. The honest version of "software is
dead" is "undifferentiated software is dead." The
next chapter prices what replaces it.

> [!QA]
> Q: What does "writing code does not make you special" mean?
> A: It means the scarce step was never authoring text. it was putting running software in front of a user. The world is full of repositories nobody can run. The learning starts when a user confronts the working version. Coding agents forced this redefinition because they deploy compulsively, without the human bias toward keeping code safe on a laptop. Value moved from the artifact (code) to the outcome (running software in front of customers).
> Follow-up: What does this imply for where a founder should build?
> A: At the deployment and distribution layer, not the generation layer. Generation is commoditizing. every model writes code. The jelly in Rauch's metaphor, the layer that takes agent-written code and puts it in front of users with domains, scaling, and security, is where the durable position sits. That is the Vercel bet restated.

> [!QA]
> Q: Walk me through the TAM math, before and after agents.
> A: Before: roughly 20 million developers in the world could create front-end projects, and Vercel sold them deployment superpowers. Cloud revenue was bounded by programmer headcount: one human, one salary, one budget of code. After: anyone who can describe what they want can create software, and agents write around the clock. The marginal creator is an agent with a token budget, not a person with a salary. The cap on how much software gets made, and how much compute it consumes, is gone.
> Follow-up: How does the TAM expansion show up in Vercel's numbers?
> A: In the deployment surge starting October 2025 with strong coding models (the guest names Opus 4.5): daily deployments doubled since January, and the company 3x'd in months on machinery it already operated. The peanut butter spread, and the jelly was already on the shelf.

> [!QA]
> Q: Is SaaS dead?
> A: Rauch's answer is precise: undifferentiated SaaS is dead, the system of record is not. SaaS was a compromise: one interface designed to make the most customers happy, because building software was expensive. With generation cheap, the presentation layer becomes plastic and tailored per business. What survives is the database, the access controls, the workflows, and the trust underneath. His two exhibits: a CEO replacing parking software with v0, and two people rebuilding Salesforce's surface inside Vercel while keeping Salesforce's data layer.
> Follow-up: Which SaaS companies survive the transition?
> A: The ones that expose themselves to agents: MCP interfaces, CLIs, APIs, consumption-based pricing, instant signup. Agents want the raw signal, not a three-month enterprise sales process. Companies built on "code is scarce," like drag-and-drop builders, or on static content aggregation, face the hardest path. Rauch is long anyone moving at the speed of tokens.

> [!QA]
> Q: What is the three-sided agentic infrastructure triangle?
> A: Side one is infrastructure for coding agents: somewhere for agent-written code to deploy. Side two is infrastructure to build your own agents: the tools to ship agents as products, like Vercel's support agent that answers 93 percent of inquiries. Side three is infrastructure automated by agents: the self-driving cloud that configures, monitors, and optimizes itself, then reports back with a PR. The triangle is Rauch's map of where the cloud is being rebuilt.
> Follow-up: Why "Amazon Agent Services"?
> A: Because the shippable entity changed. EC2 was built for human-written code, and cloud revenue was bounded by programmer headcount. Now the entity is the agent: long-running, token-consuming, deploying software. Rauch's joke is an economic claim: the cloud's unit of sale is moving from the virtual machine to the agent, and the primitives (sandbox as the new EC2, token gateway as the new CDN) are being rebuilt to match.

> [!QA]
> Q: What is the reflexivity of AI?
> A: Tobi Lutke's term, quoted by Rauch: once you know you are one prompt away from high-fidelity software, you never forego it. Efficiency, once experienced, is not given up. Engineers tell Rauch they could never code the old way again. Reflexivity is the demand-side engine of the whole chapter: free software does not kill engagement, it multiplies it, because every task becomes worth doing well.
> Follow-up: What is the retention risk?
> A: The host's challenge: Saturday-morning toy versus Wednesday-morning need. If generated software is disposable, usage may not compound. Rauch's honest answer is that both exist: one-call throwaway demos alongside deeply embedded workflows. His bet is that reflexivity wins on average, but he does not claim every generated app retains. Retention, not generation, is the metric to watch.

> [!QA]
> Q: Who wins the coding-agent market as of October 2026, and why?
> A: Claude Code leads enterprise coding at about 54 percent share, a multi-billion-dollar revenue line and the default model in Cursor. OpenAI's Codex is the challenger near 21 percent. Cursor is the distribution proof that agents are the default way to write code. Vercel's v0 closes the generation-to-deployment loop. The winner's trait is not the best model alone. It is the tightest loop: generate, deploy, observe, iterate, which is exactly Rauch's triangle as a product.
> Follow-up: What is the bear case for the leader?
> A: The September 2026 price war: OpenAI cut GPT-6 Sol to $2/$10 and Anthropic cut Opus 5.5 to $4/$20 within ninety minutes of each other. When the generation layer commoditizes, the agent's model becomes swappable and the moat moves to distribution and data. The leader's risk is that the loop matters more than the model, and someone else owns the loop.

> [!QA]
> Q: What would you ask a SaaS CEO to test the reckoning thesis?
> A: Three questions. First, what share of your interface is now generated per customer versus shared: the plastic share. Second, your agent surface: do you expose MCP, a CLI, and consumption pricing, or is an agent still stuck at your sales form. Third, your system of record: what data or workflow would a two-person team with v0 fail to reproduce. The first measures how far the reckoning has reached you. The third measures what is actually defensible.

## Recap: the whole lesson on one screen

1. **The TAM explodes.** From mainframe priesthood to
   ~20M developers to anyone who can describe what they
   want. The programmer-headcount cap on cloud demand
   is gone.
2. **The access ladder.** Mainframes, PC, web, open
   source, bootcamps, Vercel's 20M bet, agents. Each
   wave multiplied creators by an order of magnitude.
3. **Deploying is the scarce step.** Code that never
   runs teaches nothing. Agents deploy compulsively.
   Value moved from artifact to outcome.
4. **The triangle.** Infrastructure for agents, to
   build agents, automated by agents. The cloud is
   being rebuilt around the agent as the unit.
5. **SaaS was a compromise.** One interface for the
   most customers, because building was expensive.
   The expense is gone.
6. **Two exhibits.** A CEO vibe-coded the parking
   software. Two people rebuilt Salesforce's surface.
   The system of record stayed in both cases.
7. **Throwaway software.** Custom demos per sales
   call, dead by Wednesday. "Software is basically
   now free."
8. **Reflexivity.** Once you know the efficiency, you
   never forego it. Free software multiplies
   engagement instead of killing it.
9. **What stays hard.** Systems of record, trust,
   distribution, taste, and the infrastructure
   plumbing. Next: pricing the token economy.

## Go deeper

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:16px 0;">
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%;" src="https://www.youtube-nocookie.com/embed/HA7lZd7zk3M" title="Applications, Coding AI (MS&E 435, Guillermo Rauch)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

- [Applications, Coding AI (MS&E 435, first half)](https://www.youtube.com/watch?v=HA7lZd7zk3M)
- The session this lesson follows, in full.
- [MS&E 435 course site](https://mse435.stanford.edu/)
- [Enterprise LLM vendor market share, 2026](https://www.aboutchromebooks.com/enterprise-llm-vendor-market-share-statistics/)
- Mitchell Hashimoto on the "block economy": search "Mitchell Hashimoto block economy" for the current writeup.

## Official sources and further reading

**Official:**
- Applications, Coding AI (MS&E 435, Spring 2026),
  guest Guillermo Rauch, Vercel: [link](https://www.youtube.com/watch?v=HA7lZd7zk3M)
- [MS&E 435 course site](https://mse435.stanford.edu/)

**Further reading:**
- Mitchell Hashimoto on the "block economy":
  the building-blocks framing Rauch cites for agent
  ergonomics.
- Rauch's essay "it is hard to forego efficiency,"
  referenced in the session.

**Caveats from these sources.** The $9.3B valuation
is the host's intro figure. The 20M-developer TAM is
Rauch's estimate. The Opus 4.5 deployment surge is
dated "since October last year" in the session
[uncertain: October 2025]. The 93 percent support
figure is Vercel's internal metric. "Two people
rebuilt Salesforce" is Rauch's characterization of an
internal project. The October 2026 market shares are
press and vendor-reported survey estimates.

## Connections to the other courses

- **MS&E435 L04:** the specialization layer that lets
  every enterprise build its own tools: the supply
  side of this chapter's demand.
- **CS329A / CS329Z:** agents as products: harnesses,
  tool use, and evaluation of agentic systems.
- **CME295:** AI product thinking: the product
  instincts behind the agent-native rebuild.
- **MS&E435 L06:** the pricing layer: how the token
  economy replaces seat-based SaaS economics.
