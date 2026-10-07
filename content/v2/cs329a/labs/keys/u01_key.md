# Lab key U01

Keep separate from the lab. Test-mode answers live here only.

## L1.1
The diff is Monte Carlo noise with standard error about
sqrt(q(1-q)/T). It varies irregularly because each N uses an
independent RNG stream, there is no monotone pattern to expect.

## L1.2
Standard error scales as 1/sqrt(T). At N = 8, q = 0.90, SE is about
sqrt(0.09/T). For SE < 0.001 need T > 90,000. Use about 100,000 trials
with margin.

## L2.1
The noisy verifier still ranks correctly more often than chance: the
noise std 0.35 is small next to the 1.0 correctness gap, so the argmax
usually still lands on a correct sample when one exists.

## L2.2
As noise std goes to 0, the noisy rate approaches the perfect rate
(0.9044). As it goes to infinity, scores become pure noise and the
rate approaches the single-sample rate p = 0.25.

## L3.1
Higher p raises pass@N faster, so the cheap plan's coverage advantage
saturates earlier and the strong verifier's accuracy matters more at
lower budgets. The crossing moves down.

## L3.2
The true crossing is a real number between 60 and 65. Steps of 5 can
only report the first grid point past it. Finer steps pin it down but
the floor(N) jumps keep it an interval, not a point.
