# U03 lab: tools and runtime safety

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: REPL simulator

Implement the namespace REPL from C01. Run the three-call session (define x, sort x, print sum). Report the outputs. Then run a second task in the same session that reads x and report the contamination.

## Task 2: registry and loop

(a) Implement the schema registry with validate and dispatch. Test the three validation cases from C02. (b) Implement the tool/result loop with budget B = 10 and two stub tools (multiply, is_prime). Run the C03 trace and report the answer and the step count. Then set the is_prime tool to always error and report the outcome.

## Task 3: MCP handshake and guard

(a) Simulate the JSON-RPC handshake: server/discover, version negotiation (client 2026-07-28, server supports 2026-07-28), tools/list, tools/call. Report the four messages. (b) Add the auth guard. Test bad token, good token with no permission, good token with permission. Report the three status codes.

## Task 4: sandbox checker

Implement the toy policy checker with allow = {arithmetic, tmp_write} and default deny. Test "6*7", "os.remove('/data')", and "import socket". Report allow/deny for each.

## Task 5: timeout and retry simulator

(a) Simulate 10,000 calls from the C07 latency distribution at seed 0. Report the mean wait without timeout and with tau = 5. (b) Simulate the C08 retry loop with p = 0.2, r = 3, waits [1, 2]. Report the all-fail rate, mean tries, and mean wait.

## Task 6: idempotency dedupe

Implement the key store. Simulate 100 charges with timeout rate 0.1 at seed 0, each timed-out charge retried once. Report total charged with and without keys.

## Task 7: approval gate and design checklist

(a) Implement the tiered gate with tiers {read: auto, tmp_write: auto, send_email: approve, db_delete: deny}. Process the four actions and report the outcomes. (b) Score the read_file and f schemas with the C12 checklist. Report both scores.
