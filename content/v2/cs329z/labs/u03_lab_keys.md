# U03 lab keys (execution-verified)

Seed 0 everywhere (fresh numpy default_rng(0) per RNG-consuming task). Numbers below are the actual outputs of labs/run_u03_lab.py. Re-verified 2026-10-07 (fixer run 1): empirical simulation rows now match the committed script. The builder-run values they replace differed only by RNG stream.

## Task 1

- Session: "x = [3, 1, 2]" -> ok. "x = sorted(x)" -> ok. "print(sum(x))" -> 6.
- Contamination: a second task in the same session reads x and gets [1, 2, 3]. State leaked across tasks.

## Task 2

- Validate: {a: 6, b: 7} -> True. {a: 6} -> False (missing b). {a: "six", b: 7} -> False (bad type).
- Loop trace: answer "42, not prime" in 2 tool steps.
- Always-error tool: BudgetExhausted after 10 steps.

## Task 3

- Handshake: server/discover -> versions [2026-07-28]. Negotiated 2026-07-28. Tools/list -> 3 tools. Tools/call multiply -> 42.
- Guard: bad token -> 401. Good token without permission -> 403. Good token with permission -> 200.

## Task 4

- "6*7" -> allow. "os.remove('/data')" -> deny. "import socket" -> deny.

## Task 5

- Latency simulation (10,000 calls): mean wait no timeout 0.684s (theory 0.66). With tau = 5: 0.409s (theory 0.41).
- Retry simulation (p = 0.2, r = 3): all-fail rate 0.0090 (theory 0.008). Mean tries 1.24 (theory 1.24). Mean wait 0.28s (theory 0.28).

## Task 6

- 100 charges, timeout rate 0.1, each timeout retried once: without keys total = 5500 (10 double charges at seed 0). With keys total = 5000. Keys saved $500.

## Task 7

- Gate: read -> ran. tmp_write -> ran. send_email -> paused for approval. db_delete -> refused.
- Checklist: read_file = 5. f = 1.
