# Notation and shapes , mse435

Every symbol used in U01-U06 lessons, with units. No symbol is used
before its row appears in a lesson.

## Market and firm economics

| Symbol | Meaning | Unit |
|--------|---------|------|
| P | price | dollars per unit |
| Q | quantity | units (tokens, GPU-hours) |
| Qd | quantity demanded | units |
| Qs | quantity supplied | units |
| P* | equilibrium price | dollars per unit |
| Q* | equilibrium quantity | units |
| MC | marginal cost | dollars per unit |
| FC | fixed cost | dollars per period |
| VC | variable cost | dollars per period |
| v | variable cost per unit | dollars per unit |
| TC | total cost = FC + v x Q | dollars per period |
| ATC | average total cost = TC / Q | dollars per unit |
| AVC | average variable cost | dollars per unit |
| R | revenue = P x Q | dollars per period |
| pi | profit = R - TC | dollars per period |
| m | unit margin = P - v | dollars per unit |
| mu | margin ratio = (P - ATC) / P | pure number |
| capex | capital expenditure | dollars (one-time) |
| opex | operating expenditure | dollars per period |
| r | discount rate | per year |
| T | horizon | years |
| NPV | net present value | dollars |
| IRR | internal rate of return | per year |
| Ep | price elasticity of demand | pure number |

## Compute and infrastructure

| Symbol | Meaning | Unit |
|--------|---------|------|
| W | power draw | watts |
| E | energy | watt-hours |
| PUE | power usage effectiveness | pure number, >= 1 |
| U | utilization | pure number, 0 to 1 |
| F | FLOPs required | operations |
| S | throughput | FLOP/s |
| B | memory bandwidth | bytes per second |
| C_gpu | GPU-hours used | hours |
| c_h | cost per GPU-hour | dollars per hour |
| MW | megawatt, 10^6 W | watts |
| GW | gigawatt, 10^9 W | watts |
| TCO | total cost of ownership | dollars |

## Token markets

| Symbol | Meaning | Unit |
|--------|---------|------|
| p_tok | token price | dollars per 1M tokens |
| D_tok | token demand | 1M-token blocks per period |
| S_tok | token supply (serving capacity) | 1M-token blocks per period |
| L | latency | seconds |
| X | throughput | tokens per second |
| B_sz | batch size | requests |
| c_task | cost per successful task | dollars |
| h | cache hit rate | pure number, 0 to 1 |
| c_c | cache-serve price | dollars per 1M tokens |
| c_m | model-call (miss) price | dollars per 1M tokens |
| p_a | API price | dollars per 1M tokens |
| p_h | hosted price | dollars per 1M tokens |
| F | fixed hosting cost | dollars per month |
| s | task success rate | pure number, 0 to 1 |
| e | escalation (human review) rate | pure number, 0 to 1 |
| r_trials | retries after the first attempt | count |
| a0, a1 | answer accuracy before/after access | pure number, 0 to 1 |
| q | questions or tasks per period | count per period |
| v_qual | value per quality point | dollars per point per period |
| w_q | value weight per accuracy point | dollars per point |
| B | build cost | dollars (one-time) |
| R | run cost | dollars per year |
| Lb | labor cost | dollars per year |
| K | risk reserve | dollars |
| Y | pilot investment threshold | pure number |
| D | pilot duration | weeks |
| L | interval lower bound | pure number |
| a_t | adoption ramp in year t | pure number, 0 to 1 |

## Conventions

- Dollars are nominal at the 2026-10-06 baseline unless labeled
  real.
- A subscript marks the unit of account: p_tok is not the same
  object as P (per-unit price of a different good).
- Toy numbers in lessons and figures are computed locally and
  labeled TOY. "Not in source" marks any value no inspected source
  provides.
