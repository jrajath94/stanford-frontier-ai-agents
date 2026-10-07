# Lab U02 , Feedback, tools, and constitutional learning

Run script: `runs/run_u02.py`. Deterministic, no seed needed. Status:
executed 2026-10-07. Observed outputs are recorded below.

## Exercise 1 , ReAct trace

Task: run the scripted ReAct loop on "sum the evens of [3, 8, 11, 6]".

Expected: two tool calls, observations [8, 6] then 14, answer 14.

Observed: action=filter_even obs=[8, 6], action=add obs=14, answer=14.

Verdict: PASS.

Analysis questions (answers in `keys/u02_key.md`):
L1.1: where does the grounding happen in this trace?
L1.2: what breaks if the add tool returns 15?

## Exercise 2 , error taxonomy

Task: classify six toy errors with the lesson C09 classifier.

Expected: transient/retry, transient/escalate, request_bug/repair_once,
auth/escalate, tool_bug/quarantine, unknown/escalate.

Observed: 6 of 6 match.

Verdict: PASS.

Analysis questions:
L2.1: why does the 429 with 2 retries escalate instead of retrying?
L2.2: the 200-with-HTML case returns unknown/escalate. Is that the
right call? What information would change it?

## Exercise 3 , constitutional funnel

Task: run the lesson C06 funnel counts.

Expected: 95 training pairs from 100 drafts.

Observed: drafts=100 flagged=30 revised=25 dropped=5 pairs=95.

Verdict: PASS.

Analysis questions:
L3.1: the 5 dropped drafts go to human review. What decides whether
that review is worth its cost?

## Exercise 4 , shortcut gap detector

Task: flag policies whose visible-hidden gap exceeds 0.3.

Expected: gaps 0.88 and 0.85 flagged, 0.03 not flagged.

Observed: True, True, False.

Verdict: PASS.

Analysis questions:
L4.1: a policy games both suites and shows gap 0.02. What catches it?

## Integrity note

These exercises are original equivalents built from the homework
learning objectives (intuition for tool use). They are not the course
homework and do not reproduce any assessed artifact.
