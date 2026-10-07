# Lab key U06

Keep separate from the lab. Test-mode answers live here only.

## L1.1
Both numerator and denominator carry the same 2 * layers *
kv_heads * d_head * bytes-per-element factor. It cancels, leaving
N/p. The ratio is pure token counts.

## L2.1
Solve r * 2048 + 64 > 1024: r > 960/2048 = 0.4688. Above about
47 percent recompute, the blend costs more than half the full
prefill. The method needs concentration well below that.

## L2.2
The check (ranking deviations on the shallow pass) runs even on
tokens that are never recomputed. It is a fixed overhead of the
method, not part of the per-token recompute bill.

## L3.1
The 3 pinned facts (role, task, user name) plus the 5 hottest by
recency and reuse. The paging rule is pin first, hotness second,
capacity hard at 8.

## L4.1
Combined: returned 5 + 3 = 8, relevant returned 3 + 3 = 6.
Precision: 6/8 = 0.75. Recall: 6/8 = 0.75. The re-query fixed
recall without hurting precision.
