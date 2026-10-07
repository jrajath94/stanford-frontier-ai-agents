# Interview key U06

Test-mode key. Each item: minimum answer, strong answer, red flags,
rubric, remediation.

## B1
Min: main context (instructions, recent messages, working
scratchpad), archival storage (the big pile), recall storage
(searchable summaries). Strong: adds the paging between them.
Flags: "memory is the context". Rubric: 1 per tier, 2 for
contents. Remediation: lesson C01.

## B2
Min: a typed function call the agent makes to its own memory
(insert, search, append, replace). The trace is the audit trail
of what it remembered. Strong: the hallucination-vs-memory
distinction. Flags: "the trace is just logging". Rubric:
definition 2, trace 3. Remediation: lesson C02.

## B3
Min: hotness = recency times reuse count. Paging rule: pinned
facts always, then hottest first, up to capacity. Strong: the
economic justification. Flags: "hotness is recency". Rubric: 2
per sentence, 1 for capacity. Remediation: lesson C03.

## B4
Min: a trained compact KV cache for one corpus. Self-study
trains it on synthetic conversations with a distillation
objective instead of naive next-token prediction. Strong: the
recitation-vs-answering distinction. Flags: "a bigger prompt".
Rubric: 2 per part, 1 for the contrast. Remediation: lesson
C04.

## B5
Min: exact when the new prompt's first m tokens byte-match the
cached prompt's first m tokens at the same positions. Breaks on
position shifts or tokenization drift. Strong: the causal
argument (token i depends only on 1..i). Flags: "approximate
reuse is fine". Rubric: 3 for exactness, 2 for breaks.
Remediation: lesson C05.

## B6
Min: every cache entry carries its tenant, lookups match the
tenant first, cross-tenant reuse is deny by default. Strong:
adds the scrubbed-public exception. Flags: "shared cache is
faster". Rubric: 5 for the one sentence. Remediation: lesson
C10.

## Ladder 1
D1.1 Min: main context (working window), archival (durable
store), recall (searchable summaries). Strong: the capacity of
each.
D1.2 Min: 8 in main, 12 in archival, 12 evictions. Strong:
shows the arithmetic.
D1.3 Min: only the model knows what is hot, the scaffold would
evict blindly. Strong: the information argument.
D1.4 Min: page_in O(1), memory step one call plus store I/O.
Strong: notes search cost grows with archive size.
D1.5 Min: truncation wins never for agents (silent drops),
bigger context wins for short tasks, paging wins for long
mixed tasks. Strong: the cost argument.
D1.6 Min: causes: unpinned FIFO evicted the instructions,
a bad page_in dropped them. Separating measurement: the
eviction log (were they evicted or never stored?).
D1.7 Min: the model can evict hot facts under pressure or
never evict (hoarding). Strong: the pressure-warning design.
D1.8 Min: pinned vs FIFO on long-horizon tasks, falsified by
equal success. Strong: preregisters the task set.
Flags: "bigger context fixes everything". Rubric: 2 per rung,
16 total, pass at 11. Remediation: lesson C01-C03.

## Ladder 2
D2.1 Min: KV cache (per-layer keys/values per token), prefix
hit (byte-identical first m tokens), HKVD (tokens with largest
KV deviation after reorder). Strong: the deviation definition.
D2.2 Min: recompute 307, total 371, ratio 5.52. Strong: shows
the arithmetic.
D2.3 Min: repositioning corrupts few tokens badly and most
barely, so fixing the few restores quality. Strong: the
pipelining note.
D2.4 Min: the blend code, shallow pass costs one partial
prefill. Strong: notes the check is fixed overhead.
D2.5 Min: full recompute wins when chunks are few or fixed,
prefix-only wins when order is kept, blend wins for reordered
reused chunks. Strong: the cost crossover.
D2.6 Min: causes: deviation not concentrated (r too small),
wrong chunk order fed in. Separating measurement: the
deviation histogram (concentrated vs diffuse).
D2.7 Min: the shallow pass can misrank when early layers are
the wrong lens. Strong: the layer-choice sensitivity.
D2.8 Min: vary the query count, find where total cost crosses
full-context cost, falsified by never crossing. Strong:
includes retraining on corpus change.
Flags: quoting paper speedups from memory. Rubric: 2 per rung,
16 total, pass at 11. Remediation: lesson C04-C06.

## A1
Min: per-query saving: 0.002 - 0.0002 = 0.0018. Break-even:
120 / 0.0018 = 66,667 queries. Monthly retrain: monthly cost
120, monthly saving 3,000 * 0.0018 = 5.40. Never breaks even
(120 > 5.40 every month). Strong: states the amortization
condition explicitly. Flags: forgetting the retrain cost.
Rubric: first 3, second 3, pass at 4. Remediation: lesson C04.

## A2
Min: stale share grows: week 1: 5%, week 2: about 10%, week 3:
about 15%, week 4: about 20% (200 * 0.20 = 40 stale of 200.
per week 40 questions * 0.20 = 8 stale answers). With 7-day
TTL: at most about 5% stale, so 40 * 0.05 = 2 stale answers.
Re-fetch cost: the facts older than 7 days are re-fetched
weekly, about 10 per week at steady state. Strong: shows the
weekly arithmetic. Flags: treating staleness as linear without
bounds. Rubric: no-TTL 2, TTL 2, cost 2, pass at 4.
Remediation: lesson C09.

## I1
Min: sketch: main context, archival store, recall index, with
logging of (inserts, evictions, drop log, TTL expiries) over
time. Causes: (1) compression loss compounding (repeated
summaries drop more each cycle). (2) staleness accumulating
(no invalidation). Separating measurement: the drop log vs
the staleness audit (re-fetch a sample of old facts and check
them): growing drops mean (1), growing staleness means (2).
Fixes: (1) drop logs plus lossless archive, (2) per-class
TTLs. Strong: adds the time-series plot. Flags: "restart the
agent". Rubric: sketch 2, causes 2, measurement 2, fixes 2.
Pass at 5. Remediation: lesson C08, C09.

## S1
Min: the namespace design survives (tenant id on every entry
from day one). Added: per-tenant quotas, the public-entry
scrub process, audit of the labeling. Strong: the
deny-by-default statement. Flags: "add namespaces later".
Rubric: survivor 2, additions 3. Remediation: lesson C10.

## S2
Min: the cartridge's trained snapshot dies (hourly change
never amortizes). Survivors: the distillation idea for the
stable parts. Replacement: live retrieval (RAG) for prices
plus a cartridge for the stable manual text. Strong: the
hybrid split. Flags: retraining hourly. Rubric: survivor 2,
replacement 3. Remediation: lesson C04, C07.

## R1
Min: strongest true part: for short tasks inside the window,
stuffing works and is simple. Weakest assumption: that cost,
latency, and multi-session life do not matter (quadratic
attention, per-token money, no persistence). Decisive
experiment: month-long agent tasks with mixed hot/cold facts,
matched on quality, compare cost and success of big-context
vs hierarchy. Strong: adds the persistence argument.
Flags: accepting "obsolete". Rubric: true part 2, assumption
2, experiment 3. Pass at 5. Remediation: lesson C01, C03.
