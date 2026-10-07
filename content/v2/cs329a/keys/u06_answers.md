# Answer key , U06 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
30 turns at capacity 8: 8 stay in main context, 22 are evicted
to archival storage. Eviction count: 22.

## E1.2
The context window is RAM: small, fast, and full. Archival
storage is disk: big and slow. The model pages facts between
them itself, because only it knows what is hot.

## E1.3
A plain FIFO queue with no pinning evicts the system
instructions at turn 9. The agent forgets its own role. Pin the
role and the task, always.

## E2.1
Core appends 8, archival inserts 12, archival searches 5, core
replaces 2. Total: 27 memory actions.

## E2.2
Memory work happens through typed function calls the model makes
to itself. The call trace is the audit trail: it shows exactly
what the agent chose to remember, not just what it claims.

## E2.3
An agent that inserts every turn and never searches builds
write-only memory. The archive grows, nothing is ever read, and
every insert was pure cost.

## E3.1
Desk: 3 pinned + 5 hottest = 8 facts. Cabinet: 92 facts. The
rule fills the desk by pin first, hotness second.

## E3.2
A context token costs attention over every future token, while
a stored byte costs almost nothing until retrieved. A fact
earns desk space only when its expected reuse beats the
retrieval cost.

## E3.3
Pinning 8 facts at capacity 8 freezes the desk. Hotness never
matters and new hot facts cannot enter. Pin less than capacity.

## E4.1
40,960 / 512 = 80. The ratio doubles because the corpus
doubled at fixed cartridge size.

## E4.2
The model first generates its own quiz conversations about the
corpus, then trains the small KV cache to match the output
distribution of the model with the full corpus in context. The
first step makes supervision that looks like the task, the
second distills behavior instead of recitation.

## E4.3
The corpus updates but the cartridge is a snapshot of the old
edition. Answers come from stale facts with full confidence.
Retrain on change, or version the cartridge with the corpus.

## E5.1
50 requests: without reuse 50 * 2,500 = 125,000 prefill tokens.
With reuse: 2,000 + 50 * 500 = 27,000. Saved: 98,000 tokens.

## E5.2
Token i's keys and values depend only on tokens 1..i. Two
prompts with the same first m tokens have identical first m KV
entries. Reuse skips the same computation, so it is exact.

## E5.3
The cached block was computed at positions 0..1999 but the new
prompt places the text at 500..2499. KV entries are
position-dependent, so the reuse is silently wrong. Pin the
positions with the content.

## E6.1
Recompute: 0.25 * 2,048 = 512. Total: 512 + 64 = 576. Ratio:
2,048 / 576 = 3.56. The saving shrinks as r grows.

## E6.2
Repositioning corrupts few tokens badly and most tokens barely.
Recompute only the high-deviation tokens and keep the rest.
A small surgical repair buys back full-prefill quality.

## E6.3
Every token's KV shifts a lot in the new order, so the HKVD
set is the whole input. The method becomes full recompute with
extra steps. Check concentration before trusting the ratio.

## E7.1
Precision: 4/5 = 0.80. Recall: 4/8 = 0.50. Better on both axes
than the lesson toy.

## E7.2
The agent reads what the retriever returns, so noise enters the
reasoning directly. A missed fact only costs another query.
Precision protects the trace, recall protects completeness.

## E7.3
Inserts from the memory actions never reach the search index.
The agent's own notes are unfindable and it re-derives them
every turn. Index on write, not later.

## E8.1
Loss = 2, needed = 4. Loss rate: 2/4 = 0.50. Half the needed
facts were dropped by the summary.

## E8.2
Every compression step records what it removed. When a needed
fact is later missing, the log says whether compression dropped
it or it was never stored. Without the log the two bugs look
identical.

## E8.3
Summaries are written with no drop record. A missing fact could
be compression loss or absence, and tuning the summarizer is
blind. Log the drops.

## E9.1
About 30 stale of 100, so 30 percent of cached answers are
wrong. Staleness grows with age when nothing expires.

## E9.2
A shorter TTL means fewer stale answers but more re-fetches.
A longer TTL means fewer re-fetches but more stale answers.
Set the TTL where the two costs cross for each fact class.

## E9.3
The source is down when the TTL expires the only copy. The
agent has nothing to serve. Keep a stale-while-revalidate
policy for critical facts.

## E10.1
Namespaced: 2 private blocks (one per tenant). Shared public:
1 block. The sharing saves 1 block of memory.

## E10.2
The default is no cross-tenant reuse, because KV caches can
leak prompt text. Sharing needs an explicit public label plus
a verified scrub. Deny first, share by exception.

## E10.3
The "public" system prompt contains one tenant's name in an
example. Sharing it leaks the name to every tenant. Scrub
means verify, not assume.

## E11.1
Overlap 10, 0 wrong steps: 10 fetches saved, about 10 minutes,
no loss. Net: +10 minutes. Verification cost is the only tax.

## E11.2
A fact true for task A can be false for task B: different
customer, different version, different context. Transferred
without labels, it arrives with full confidence and causes
silent errors.

## E11.3
The store drops the source task label. Cross-task hits arrive
unlabeled and interference is invisible until it bites. Label
every fact with its origin task.

## E12.1
SE = sqrt(0.72*0.28/200 + 0.58*0.42/200) = sqrt(0.002226) =
0.0472. Interval: 0.14 +/- 0.0925, which excludes 0. At n =
200 the win is proven, the toy at n = 50 was not.

## E12.2
At n = 50 the 95 percent interval covers 0, so the data do not
rule out no effect. Promising is not proven. Run more tasks
until the interval excludes 0 or the delta vanishes.

## E12.3
The memory-on arm gets easier tasks. The delta then measures
task difficulty, not memory. Lock the task set and the seeds
across arms.
