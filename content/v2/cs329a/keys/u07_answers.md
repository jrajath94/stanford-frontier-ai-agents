# Answer key , U07 exercises

Keep separate from the lesson. Test-mode answers live here only.

## E1.1
15: Nov 10, Denny Zhou, LLM Reasoning. 16: Nov 14, Thang Luong,
AlphaProof, AlphaGeometry, IMO Gold. 18: Nov 21, Misha Laskin,
Building Agentic Systems for Autonomy. 19: Dec 1, Danny Driess,
Multimodal AI Agents in Robotics.

## E1.2
A schedule line names the speaker and the topic, nothing more.
Any claim about what was said needs a stronger source, so the
honest teaching level is the line itself.

## E1.3
Explaining what a guest "said" from the schedule line alone.
That is fabrication with a famous name attached. State the
line, state the gap, stop.

## E2.1
Success rate: 2/6 = 1/3. Nodes visited: 6. The kernel judged all
6 for free.

## E2.2
The kernel accepts or rejects each tactic deterministically, so
every search node is labeled right or wrong at no cost. The two
hard problems of search (scoring nodes, knowing when to stop)
are solved by construction.

## E2.3
The theorem is formalized wrong. The system proves the wrong
statement perfectly, and the kernel's yes certifies the wrong
thing. Check the statement before the search.

## E3.1
Close rate: 2/5 = 0.40. The proposer is right 40 percent of the
time, the engine does the rest.

## E3.2
The neural net generates ideas (constructions) and the symbolic
engine finishes (deduction to closure). Ideas are cheap and
often wrong, deduction is certain, so the loop tries ideas
until the engine closes the proof.

## E3.3
The needed deduction rule is absent from the engine. No
construction closes the proof, and the proposer takes the blame
for an engine gap. Check rule completeness first.

## E4.1
Ratio: 13/4 = 3.25 checks per proof step. The report must say
"4-step proof found after 13 checks".

## E4.2
Search is the process of trying guesses, proof is the accepted
artifact. Reporting the 9 dead ends as part of the proof lies
about what the system knows. Keep the two numbers separate.

## E4.3
The proof path depends on randomness and does not replay. It is
a lucky trace, not a proof. Replay every claimed proof from
the statement.

## E5.1
Random play: (1/12)^4 = 1/20736, about 0.00005. Guided play:
(1/3)^4 = 1/81, about 0.012. The policy buys about a 250x
improvement.

## E5.2
The environment labels every step: a tactic that closes a
subgoal is visible progress before the full proof. The agent
learns from a perfect teacher instead of a noisy reward model.

## E5.3
The needed tactic is absent from the action set. The agent
plays perfectly and never wins. The action space is part of
the environment design, check it first.

## E6.1
(0.95, low): safe, wasted. (0.95, high): safe, useful.
(0.60, high): dangerous, rejected. (0.60, low): safe, limited.
The envelope admits 3 of 4.

## E6.2
Capability is what the agent does well, measured. Authority is
what it may do alone, granted. Authority must not exceed
verified capability, with margin for drift.

## E6.3
Capability was measured on easy tasks. The agent earns high
authority and meets hard tasks. Measure on representative
tasks or the envelope is fiction.

## E7.1
Attempt success: 1/3. Task success: 1/1 (the task allows 3
tries). The loop converges because perception error fell below
the action tolerance.

## E7.2
The world decides whether the grasp worked, not the plan. Each
observation is a fact from outside the model, and each action
is re-planned from the corrected state. Physics does not
negotiate.

## E7.3
The camera is miscalibrated by 5 cm and nobody recalibrated.
Every plan is 5 cm wrong and retries never converge. Calibrate
on a schedule, and check calibration when retries stall.

## E8.1
Fused miss: 0.20 * 0.10 * 0.30 = 0.006. Three imperfect
channels beat any one of them.

## E8.2
The product rule needs independent failures. Two sensors with
the same blind spot do not fuse, they echo. Independence is
the load-bearing assumption of the whole calculation.

## E8.3
Vision and the depth camera share one lens. Both miss the
transparent cup together, and fusion adds nothing. Audit the
failure modes, not just the channel count.

## E9.1
Before: gap = 0.95 - 0.70 = 0.25. After: gap = 0.88 - 0.76 =
0.12. The sim number fell and the real number rose.

## E9.2
Randomization widens the training distribution to cover
reality, so sim performance falls and real performance rises.
The trade works when the gap narrows even as the sim
number drops.

## E9.3
Reality's friction lies outside the randomized interval. The
policy meets a world it never dreamed and the gap stays wide.
Cover the real range or state the scope.

## E10.1
Block rate: 1/10 = 0.10. Safety tax: 30 seconds for the
re-planned action. The 9 good actions are unaffected.

## E10.2
The safety layer does not share the planner's model, so a
planner bug does not become a safety bug. It checks each
action against hard rules and vetoes. Dumb and independent
beats clever and shared.

## E10.3
The safety layer reads the planner's own state estimate. A
perception bug blinds both, and the veto is theater. Feed the
safety layer from independent sensors.

## E11.1
Faithfulness rate: 7/10 = 0.70. Three traces were stories.

## E11.2
Change the fact the trace cites and hold everything else. If
the behavior changes, the trace named a real cause. If not,
the trace is post-hoc rationalization.

## E11.3
The intervention changes X and accidentally changes Y too. The
behavior moves, and a story passes as faithful. Design
interventions that move one fact.

## E12.1
4 sessions, 3 questions each: 12 gaps. Pointers: 12. Coverage:
12/12 = 1.00, fully actionable.

## E12.2
The inventory lists what was not learned, one open question
per row, each with a pointer to the answer. It makes
ignorance explicit and actionable instead of hiding it.

## E12.3
The pointers lead to paywalled or dead sources. The gaps are
listed but not closable. Check every pointer before
publishing the inventory.
