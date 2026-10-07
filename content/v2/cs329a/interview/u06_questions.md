# Interview bank U06 , Memory, caches, and long-context representations

Provenance: original practice questions. Not actual employer questions.
Keys in `u06_key.md`. Keep questions and keys separate in test mode.

## Breadth (6)

B1. Name the three MemGPT tiers and what lives in each.
B2. What is a memory action, and why is the call trace kept?
B3. Define hotness and the paging rule in one sentence each.
B4. What is a cartridge, and what does self-study change versus
naive training?
B5. When is prefix KV reuse exact, and when does it break?
B6. State the tenant-isolation rule in one sentence.

## Deep ladders (2 x 8)

Ladder 1 , MemGPT to retrieval.
D1.1 Define main context, archival storage, and recall storage.
D1.2 Toy: 20 turns, capacity 8. Compute the final split and the
eviction count.
D1.3 Derive why the model (not the scaffold) should manage
eviction.
D1.4 Implement page_in and the memory step, state the cost of
each.
D1.5 Compare MemGPT paging with truncation and with a bigger
context. When does each win?
D1.6 Debug: the agent forgot its role at turn 9. Name two causes
and the measurement that separates them.
D1.7 Critique model-managed eviction: what can go wrong that a
fixed policy would not do?
D1.8 Design the experiment that tests whether pinning beats
plain FIFO, and state the falsification.

Ladder 2 , CacheBlend to cartridges.
D2.1 Define a KV cache, a prefix hit, and HKVD tokens.
D2.2 Toy: 4 chunks of 512 tokens, r = 0.15, check cost 64.
Compute the blend ratio.
D2.3 Derive why selective recompute restores quality: the
concentration argument.
D2.4 Implement cache_blend, state the shallow-pass cost.
D2.5 Compare CacheBlend with full recompute and with
prefix-only caching. When does each win?
D2.6 Debug: quality collapses after blending. Name two causes
and the measurement that separates them.
D2.7 Critique the HKVD ranking: when does it mislead?
D2.8 Design the experiment that tests cartridge amortization
(number of queries to break even), and state the falsification.

## Analytical exercises (2)

A1. A corpus has N = 20,480 tokens. A cartridge uses p = 512
slots and costs C_train = $120 to train once. Serving a query
costs $0.002 with full context and $0.0002 with the cartridge
(toy rates). Compute the number of queries at which the
cartridge breaks even. Then recompute if the corpus updates
monthly and the cartridge must be retrained each month, with
3,000 queries per month.
A2. An agent's archive has 200 facts. Each week 5 percent go
stale. The agent answers 40 cached questions per week with no
invalidation. Compute the expected stale answers in week 4.
Then compute the stale answers with a 7-day TTL (assume
re-fetch fixes everything fetched), and state the re-fetch
cost in facts per week.

## Implementation / debug (1)

I1. Your agent's answers grow worse over a month of
continuous operation, but each single session looks fine.
Sketch the memory subsystem with the instrumentation you would
add, then name the two most likely causes and the single
measurement that separates them. State the fix for each.

## Changed-constraint scenarios (2)

S1. Constraint change: the deployment is single-tenant today
but must support 1,000 tenants tomorrow with no code change to
the agent. What survives of the cache design, and what must be
added on day one?
S2. Constraint change: the corpus behind the cartridge updates
hourly (live prices). What survives of the cartridge design,
and what replaces the trained cache?

## Research critique (1)

R1. "Bigger context windows will make all memory systems
obsolete: just stuff everything into context." Identify the
claim's strongest true part, its weakest assumption, and the
single experiment that would most change your mind.
