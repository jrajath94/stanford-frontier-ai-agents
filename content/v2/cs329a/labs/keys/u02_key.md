# Lab key U02

Keep separate from the lab. Test-mode answers live here only.

## L1.1
Grounding happens at the observations: [8, 6] and 14 come from tool
runs, not from model text. The next thought reads them instead of
guessing.

## L1.2
The trace reports 15 with full confidence. Nothing in the loop checks
tool outputs, so an untrusted tool poisons the answer silently. This
is the C01 failure case.

## L2.1
The retry budget is 2. Past it, the error is no longer transient by
policy: something structural is wrong and a human or a different path
must take over.

## L2.2
Escalate is the safe default for an unrecognized shape. A content-type
check or a schema validator would reclassify it as schema drift and
route to quarantine instead.

## L3.1
The base rate of real violations among dropped drafts. If most dropped
drafts are true violations, review teaches the constitution's gaps. If
they are false alarms, review is expensive noise.

## L4.1
The gap detector cannot see it. Rotation of hidden suites (U02 C11
item 12) or a human audit of the policy's behavior is the next
instrument.
