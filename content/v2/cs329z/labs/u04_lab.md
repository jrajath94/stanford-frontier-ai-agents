# U04 lab: frameworks, memory, coordination

Environment: Python 3 with NumPy. Seed 0 everywhere unless noted. Run each task as a script and keep the outputs. The keys file shows the verified numbers.

## Task 1: toy optimizer

Implement the DSPy-style toy optimizer from C01: 4 candidate prompts with fixed dev scores [0.55, 0.62, 0.70, 0.78] on 20 examples. Report the argmax, the search cost in scored calls, and the gain over the hand-written baseline 0.62.

## Task 2: pattern router

Implement the C03 router: classify 6 toy tasks (draft-then-translate, ticket triage, 5 code reviews, research brief, draft-critique-revise, open-ended bug hunt) into the five workflow patterns plus agent. Report the mapping.

## Task 3: ReAct trace and chart

(a) Build the 7-step ReAct trace for "is 42 prime?" with stub tools. Verify alternation. (b) Run it through the C05 chart runner with states {start, plan, act, observe, reflect, done}. Report valid/invalid. Then drop the observe->reflect edge and report which transition fails.

## Task 4: memory manager and file memory

(a) Implement the C06 memory manager with a 2000-token budget on a 10,000-token toy history. Report the summary size and the kept total. (b) Implement the file memory: write 3 notes, read them back in a fresh session, grep the step-3 fact. Report the grep hit.

## Task 5: handoff and bus

(a) Pack and unpack the flight envelope from C08. Report the four keys and the 40x ratio. (b) Implement the message bus with 3 agents and 10 updates each. Report sends, receives, and relevance per agent.

## Task 6: pipeline simulator and comparison rig

(a) Simulate the C10 pipeline (3 stages at 0.9, checks catch 0.8) over 10,000 runs at seed 0. Report R with and without checks. (b) Run the C11 comparison rig on single (0.74, 1x) vs multi (0.81, 5x). Report the gain per extra cost and the verdict at bar 0.03.

## Task 7: stop checker

Implement the four-rule stop checker from C12 with B = 10 and k = 3. Test: (a) answer at step 2, (b) 10 fruitless steps, (c) 3 identical observations at steps 4-6, (d) denial at step 3. Report the stopping step and rule for each.
