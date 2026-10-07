# U01 answer keys

Kept separate from `lessons/u01_lesson.md`. Each exercise shows the arithmetic.

## C01

- E1: 0.8 x 0.9 = 0.72. The conjunction: the question needs the fact retrieved AND used. Both must happen, so the rates multiply under independence.
- E2: sqrt(0.8 x 0.2 / 10) = sqrt(0.016) = 0.126, about 0.13.
- E3: model-to-retriever (query out, chunks back), model-to-tool (expression out, value back), model-to-check (answer out, pass/fail back).

## C02

- E1: 1 - 0.8 x 0.9 = 1 - 0.72 = 0.28.
- E2: the gate shares the drafter's blind spots. A model that writes a bad draft will often judge it good, so the gate passes failures and the pipeline fails silently.
- E3: any task with no cheap check, e.g. "write a moving essay". No gate can verify the seam without solving the task.

## C03

- E1: sqrt(0.8 x 0.2 / 10) = 0.126, about 0.13.
- E2: n near 0.16 x (2/0.1)^2 = 0.16 x 400 = 64.
- E3: a leaked eval measures memorization of the training items, not ability on new items. The score says nothing about deployment.

## C04

- E1: 2 x 4096^2 x 1024 = 2 x 16,777,216 x 1024 = 34,359,738,368, about 3.4e10.
- E2: softmax outputs are nonnegative and sum to 1 by construction (each term divided by the sum of terms). Output rows are convex combinations of value rows.
- E3: without the mask, training tokens read future tokens. Training loss looks good because the model cheats. Generation fails because the future is absent.

## C05

- E1: exp = [2.718, 7.389, 20.086], sum 30.193, p = [0.09, 0.24, 0.67].
- E2: p = [0.23, 0.32, 0.45]. H = -(0.23 ln 0.23 + 0.32 ln 0.32 + 0.45 ln 0.45) = 0.338 + 0.365 + 0.359 = 1.06 nats.
- E3: at T -> 0 both top tokens have equal max logit. The argmax is not unique, so the winner depends on the tie-break, not on the model's preference.

## C06

- E1: 2 x 32 x 8192 x 4096 x 2 = 4,294,967,296 bytes, about 4.3 GB.
- E2: the new token scores against n cached keys: one query against n keys is O(n d). The cache holds keys and values, so no recompute.
- E3: mid-context evidence gets less attention weight in practice. The answer ignores the gold chunk even though it is present.

## C07

- E1: 0.88 + 0.12 x 0.7 = 0.88 + 0.084 = 0.964.
- E2: {"title": string, "start": string (ISO time), "end": string (ISO time), "attendees": array of string}. Required: title, start, end.
- E3: the schema demanded an unknowable field, so the model invented a value to satisfy validation. The contract manufactured the lie.

## C08

- E1: masked logits [2.0, 1.5, 1.0]. Exp = [7.389, 4.482, 2.718]. Sum 14.589. P = [0.51, 0.31, 0.19].
- E2: P(token | allowed) = P(token, allowed) / P(allowed). For token in A, P(token, allowed) = P(token). Dividing by the allowed mass renormalizes. That is exactly masked softmax.
- E3: the grammar permits {} and the model assigns it high probability. Valid output, empty content. Downstream starves.

## C09

- E1: SFT trained the response shape (instruction -> answer format), not the fact. The fact probability barely moved. The format probability rose.
- E2: L = -sum log P(response_i | prompt_i) over the demonstration pairs.
- E3: sycophancy: annotators rewarded agreement, so the model learned to flatter instead of help.

## C10

- E1: 0.7^8 = 0.0576. 1 - 0.0576 = 0.942.
- E2: 1 - 0.4^2 = 1 - 0.16 = 0.84.
- E3: the error is systematic: all 8 samples share the same wrong reasoning. Independence fails, so pass@8 equals p.

## C11

- E1: retrieval 0.12/2 = 0.06 per unit cost. Tools 0.04/2 = 0.02 per unit cost.
- E2: a straw baseline is trivially weak, so any component looks like a breakthrough. The bar must be the best simple system, not the worst.
- E3: keep a component only if its score gain per extra cost clears the team's bar on the same eval.

## C12

- E1: RAG (0.78-0.35)/(4-1) = 0.43/3 = 0.143 per unit extra cost. Agent (0.81-0.35)/(12-1) = 0.46/11 = 0.042.
- E2: (a) single call, (b) prompt chaining, (c) RAG, (d) agent.
- E3: the verifier row was ignored. The agent is correct but its 12x cost and latency break the 10ms budget. The table must include budget rows.
