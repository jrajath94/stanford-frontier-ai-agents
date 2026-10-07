# U03 answer keys

Kept separate from `lessons/u03_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: call 1: x = [3, 1, 2]. Call 2: x = [1, 2, 3]. Call 3: sum = 6.
- E2: both tasks share one namespace. Task B reads task A's variable x and uses it as its own. The answers mix.
- E3: reset the session between tasks, or use one session per task. State must not cross task boundaries.

## C02

- E1: {"name": "multiply", "description": "Multiply two numbers", "parameters": {"a": {"type": "number"}, "b": {"type": "number"}}, "required": ["a", "b"]}.
- E2: the descriptions carry no signal, so the model cannot distinguish the tools. Selection becomes random.
- E3: 10 x 200 = 2000 tokens of menu on every step.

## C03

- E1: think, call(multiply), observe(42), think, call(is_prime), observe(false), answer.
- E2: 10 steps x 500 tokens = 5000 tokens max.
- E3: the observation carries attacker text. The model reads it as instruction and follows it. The loop has no trust boundary on observations.

## C04

- E1: MCP host (the AI app), MCP client (one connection per server), MCP server (exposes tools, resources, prompts).
- E2: the client negotiated a version whose method set lacks the called method. The server answers "method not found".
- E3: local file tool: stdio (same machine, no network). Remote search API: Streamable HTTP (network, standard HTTP auth).

## C05

- E1: invalid-token reject rate 50/1000 = 0.05. No-permission reject rate 30/950 = 0.032, about 0.03.
- E2: 401 = the credential is bad (authentication failed). 403 = the credential is fine but the action is forbidden (authorization failed).
- E3: the MCP spec recommends OAuth for Streamable HTTP.

## C06

- E1: 30 denied, 0 escapes with default-deny. Deny-list: 27 denied, 3 escapes.
- E2: the filter scanned for file writes but the code reached the shell through subprocess. The bypass path was never in the policy.
- E3: default-deny: allow only listed operations. A forgotten entry blocks a feature instead of allowing an attack.

## C07

- E1: no timeout: 0.18 + 0.18 + 0.30 = 0.66s. Timeout 5s: 0.18 + 0.18 + 0.05 = 0.41s.
- E2: the mass above 5s is 0.01, so 1 percent of calls become timeout errors.
- E3: set the timeout from the measured p99 latency, not from a guess.

## C08

- E1: 0.2^3 = 0.008. Expected tries = 1 + 0.2 + 0.04 = 1.24.
- E2: jitter randomizes the waits so that many clients do not retry in lockstep. Without it, retries synchronize into a storm.
- E3: retry only transient failures (5xx, timeouts, rate limits). Permanent errors (400, auth) never get better on retry.

## C09

- E1: 10 timeouts retried once each = 10 extra charges x $50 = $500 extra.
- E2: one key now names many operations. The second charge returns the first charge's receipt. The money is lost and the books look clean.
- E3: one unique key per logical operation, generated once and reused across that operation's retries only.

## C10

- E1: 25 approvals x 60s / 100 actions = 15s per action.
- E2: the model shows "read file" for approval, then executes "delete file". The approved action differs from the executed one.
- E3: freeze the exact (tool, args), approve that exact pair, execute only that pair.

## C11

- E1: enum caller: 1 - 0.001 = 0.999. Abort-on-any: 1 - 0.061 = 0.939, about 0.94. Gap about 6 points.
- E2: the switch has no branch for the new code. The error falls through and the caller mishandles it (wrong retry or silent drop).
- E3: version the contract. Callers pin a version. New error codes ship in a new version.

## C12

- E1: difference 0.31. SE = sqrt(0.31 x 0.69 x 0.02) = sqrt(0.00428) = 0.065.
- E2: 50 tools x 200 tokens = 10,000 tokens of menu. The model cannot find the right tool in the noise.
- E3: one tool does one job. A three-job tool needs a three-way description and the model picks the wrong branch.
