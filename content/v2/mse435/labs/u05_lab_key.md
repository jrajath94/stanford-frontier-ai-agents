# Lab key , U05

Verified outputs from `u05_lab_run.py`, executed 2026-10-07.

## Task 1

| f $ | vibe $ | verified $ |
|-----|--------|-----------|
| 25 | 10,000 | 4,000 |
| 100 | 40,000 | 7,000 |

Tie review cost at f = 100: 36,000 dollars. Expensive
defects make verification nearly always right.

## Task 2

| c $ | D $ | total $ |
|-----|-----|---------|
| 0.50 | 50,000 | 250,000 |
| 5.00 | 500,000 | 700,000 |

Expert labels make the dataset the dominant asset.

## Task 3

- Base blended margin: 7.60 dollars per user per month.
- Viral shift (power share 0.15 at usage 50): 1.40.
- The power cohort wipes out most of the margin.

## Task 4

| churn | service margin $ | winner |
|-------|-----------------|--------|
| 0 | 612.00 | service |
| 0.03 | 377.38 | license |
| 0.10 | 166.17 | license |

Churn flips the boundary decision.

## Task 5

| extra cycles | speedup | time ratio |
|--------------|---------|-----------|
| 0 | 1.400 | 0.714 |
| 0.30 | 1.400 | 0.929 |
| 0.60 | 1.400 | 1.143 |

At 60 percent extra cycles the AI path is slower than
baseline. Design quality gates the speedup.

## Task 6

- Base: 111,001,000 dollars
- AI doubles assay survivors: 112,001,000 (costs an extra
  1M)
- Triage (100 assays): 110,501,000 (saves 500k)

## Task 7

| p | E $/yr | decision |
|---|--------|----------|
| 0.001 | 50,000 | accept risk |
| 0.004 | 200,000 | accept risk (boundary) |
| 0.01 | 500,000 | protect |
| 0.02 | 1,000,000 | protect |

The decision flips at p = 0.004. Boundary ties go to
accept risk only with a margin of safety.

## Task 8

| c $ | feasible n/mo | bill for 200 $ |
|-----|---------------|----------------|
| 5,000 | 80 | 1,000,000 |
| 1,000 | 400 | 200,000 |

Cheaper assays move the bottleneck back to design.

## Task 9

| h | bill $ | max releases/mo |
|---|--------|-----------------|
| 500 | 150,000 | 0.64 |
| 150 | 45,000 | 2.13 |
| 80 | 24,000 | 4.00 |

Triage is the highest-ROI move in the program.

## Task 10

| curve | PV $ |
|-------|------|
| base | 906,085.65 |
| trained (net of 200k) | 1,074,981.22 |
| stall | 248,685.20 |

The stall case kills the business case. Training pays
168,895.57 over base.

## Task 11

| e | per task $ | yearly $ |
|---|-----------|----------|
| 0.05 | 9.50 | 475,000 |
| 0.02 | 5.00 | 250,000 |

Upgrade payback: 500,000 / 225,000 = 2.22 years.

## Task 12

| o | true accuracy | expected net $ |
|---|---------------|----------------|
| 0.0 | 0.950 | 42,500 |
| 0.3 | 0.830 | 36,500 |
| 0.7 | 0.670 | 28,500 |
| 1.0 | 0.550 | 22,500 |

Novelty floor (a_ood = 0.20 at o = 0.70): accuracy
0.425, net 16,250 dollars. Still positive, but thin.
