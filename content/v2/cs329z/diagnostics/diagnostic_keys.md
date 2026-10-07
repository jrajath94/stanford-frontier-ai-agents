# Diagnostic keys: cs329z

Kept separate from `prerequisites.md`. Each item scores 0/1. Show the arithmetic.

- D1: exp(1)=2.718, exp(2)=7.389, exp(3)=20.086. Sum 30.193. Probabilities: 0.09, 0.24, 0.67 (sum 1.00 within rounding).
- D2: attention costs O(n^2 d) per layer for the score matrix. n^2 d = 4096^2 x 1024 = 1.7e10, so order 1e10 FLOPs per layer up to constants (QK^T plus attention-times-V each contribute n^2 d).
- D3: theta = arccos(0.8) = 36.9 degrees, roughly 37.
- D4: precision = fraction of retrieved items that are relevant. Recall = fraction of relevant items that were retrieved.
- D5: roles: MCP host, MCP client, MCP server. Transports: stdio (standard input/output), Streamable HTTP.
- D6: 0.2^3 = 0.008, under one percent.
- D7: boxes Thought, Action, Observation. Arrows: Thought to Action labeled "choose tool and arguments", Action to Observation labeled "execute and return result", Observation to Thought labeled "read result, update plan".
- D8: unbounded cost or an infinite loop. One concrete failure: the agent repeats the same failing tool call and burns the token budget with no progress.
