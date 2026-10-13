<!-- solve-problem:d75126da-3f93-423e-a2c3-c1e6647f373d -->
# Deterministic k-server conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/d75126da-3f93-423e-a2c3-c1e6647f373d).

## What is the problem?

The **k-server problem** is a deterministic online problem. Fix a metric space $(M, d)$ and $k$ mobile servers occupying points of $M$. An adversary issues a sequence of requests $r_1, r_2, \dots$, each a point of $M$. Upon each request, the algorithm must move some server to $r_t$ (if none is already there) before seeing future requests, paying the distance moved. Total cost = sum of all movement distances.

The conjecture (Manasse, McGeoch, Sleator, 1988/1990): **for every metric space with at least $k+1$ points, there exists a deterministic online algorithm with competitive ratio at most $k$** against the adaptive offline adversary. That is, for all request sequences $\sigma$,
$$\text{cost}_{\text{ALG}}(\sigma) \le k \cdot \text{cost}_{\text{OPT}}(\sigma) + O(1).$$

Known: $k$ is a lower bound on the competitive ratio for any metric space with $k+1$ points (so the conjectured bound is tight). The best general upper bound is $2k-1$ via the work-function algorithm (Koutsoupias–Papadimitriou 1995). Precisely, the gap to close is: construct a deterministic algorithm with ratio $k$, or prove none exists for some metric space.

Ambiguity note: the standard formulation concerns the adaptive online adversary and the additive $O(1)$ term (which can be the initial configuration offset). Randomization is a separate (also open) problem—do not conflate.

## Why does it matter?

The k-server problem is the "master problem" of online algorithms: paging/caching, metrical task systems special cases, and its study created the potential-function method central to online algorithms. Resolving it would settle the exact power of determinism in online metric service and likely yield new techniques (e.g., a polyhedral or game-dynamical machinery) transferable to paging, online matching, and robot/fleet dispatch. Its continued openness is a benchmark for the field; a refutation would restructure competitive analysis itself.

## What's already known?

- **Lower bound (MMS 1990):** No deterministic algorithm achieves ratio $< k$ on any metric with $k+1$ points; also the conjecture is tight-achievable on lines, trees, and other special metrics (ratio exactly $k$ known for lines, "WFA on trees", etc.).
- **Upper bound (Koutsoupias–Papadimitriou 1995):** The **work-function algorithm (WFA)** — serve each request by the server minimizing (movement + final work-function value) — is $(2k-1)$-competitive on every metric. This is the best known general bound, ~30 years old.
- **Special cases where ratio $k$ is achieved:** $k=2$ (all metrics), lines, trees, and metrics of size $k+2$ (verify exact frontier). Also, the "weak adversary" and refined-adversary variants give ratio $k$.
- **Failed approaches:** Direct potential functions matching WFA analysis get stuck at $2k-1$ because WFA's own competitive ratio on some metrics appears to genuinely exceed $k$; it is widely believed WFA itself is *not* $k$-competitive in general, so a new algorithm is needed. Koutsoupias's "alternation" analysis techniques and the polyhedral view (work functions as points in $\mathbb{R}^{n \choose k}$) are the main technical toolkit.
- **Related:** the randomized version (ratio polylog or $O(\log^2 k)$ for trees via BCLP-style algorithms — verify current best) is separate and *not* the target here.

## What would count as solving it?

1. **Affirmative:** A deterministic algorithm and a proof that it is $k$-competitive on every metric space with $\ge k+1$ points (additive constants allowed). Referee test: a rigorous competitive-ratio proof for all metrics and all $k$.
2. **Negative:** A metric space (for some $k$) and a proof that no deterministic algorithm has ratio $\le k - \epsilon$ improvement beyond the known $k$ lower bound — i.e., a metric where ratio exactly $k$ is unachievable (would be shocking given the lower bound is $k$).
3. **Partial credit:** ratio $k + o(k)$ or $2k - o(k)$ for WFA or any algorithm; improved bounds for new metric classes; resolution for fixed $k \ge 3$ on general metrics.

## How to start

1. Read Borodin–El-Yaniv, *Online Computation and Competitive Analysis*, chapters on the server problem — the cleanest exposition of WFA, the $2k-1$ proof, and the lower bound. Then Koutsoupias (1999) survey "The k-server problem" (Computer Science Review) for open questions.
2. Understand *why* $2k-1$ arises: the WFA analysis charges each step via work-function increase; identify where the slack factor of ~2 enters (the "surplus"/duality argument). Ask whether a modified algorithm (e.g., convex combination of WFA moves, or "lazy" corrections) can remove it.
3. Study the polyhedral formulation: work functions form a subset of Lipschitz-concave functions on configurations; a $k$-competitive algorithm corresponds to an online strategy staying near a certain potential. Try to design a potential-based algorithm directly.
4. Test candidates computationally: search small metrics (e.g., 5-point metrics, $k=3$) for adversarial sequences beating WFA at ratio $k$; use counterexample feedback to guide design. Main obstacle: no natural candidate algorithm beyond WFA, and lower-bound techniques generalize poorly.

## Key references

- Manasse, McGeoch, Sleator, "Competitive Algorithms for Server Problems," *J. Algorithms 11(2), 1990* (originally STOC 1988). Defines the k-server problem, proves the $k$ lower bound and the $k$-server conjecture's tightness targets; solves 2 servers. https://doi.org/10.1006/jagm.1990.1037 (verify)
- Koutsoupias, Papadimitriou, "On the k-Server Conjecture," *J. ACM 42(5), 1995* (STOC 1994). Proves the work-function algorithm is $(2k-1)$-competitive — the best known general bound. https://doi.org/10.1145/210118.210128 (verify)
- Borodin, El-Yaniv, *Online Computation and Competitive Analysis*, Cambridge Univ. Press, 1998. Standard textbook treatment of WFA, potential functions, and server lower bounds.
- Koutsoupias, "The k-server problem," *Computer Science Review 3(2), 2009*. Survey of the problem, techniques, and open directions. (verify)
- Chrobak, Larmore, "An optimal on-line algorithm for k servers on trees," *SIAM J. Comput. 20(1), 1991*. Achieves ratio $k$ on trees, the largest natural class fully solved. (verify)

## Warnings

- WFA is conjectured *not* to be $k$-competitive in general; do not assume optimizing its analysis suffices.
- Don't conflate with the randomized k-server conjecture (a separate, also-open problem with different bounds).
- Finite vs. infinite metric spaces, and $n = k+1$ vs. $n \ge k+2$: state which setting you address; the lower bound needs $n \ge k+1$.
- Additive constants are conventional and allowed; the ratio bound is the substance.
- Many false "proofs" circulate from mischarging adversary cost; check proofs against the simple $k+1$-point adversary (all requests to the empty point), which forces exactly ratio $k$ in the tight cases.

---
*`ALGO-000128` · unverified*

## Acceptance guidance

1. **Affirmative:** A deterministic algorithm and a proof that it is $k$-competitive on every metric space with $\ge k+1$ points (additive constants allowed). Referee test: a rigorous competitive-ratio proof for all metrics and all $k$.
2. **Negative:** A metric space (for some $k$) and a proof that no deterministic algorithm has ratio $\le k - \epsilon$ improvement beyond the known $k$ lower bound — i.e., a metric where ratio exactly $k$ is unachievable (would be shocking given the lower bound is $k$).
3. **Partial credit:** ratio $k + o(k)$ or $2k - o(k)$ for WFA or any algorithm; improved bounds for new metric classes; resolution for fixed $k \ge 3$ on general metrics.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/d75126da-3f93-423e-a2c3-c1e6647f373d?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000128.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000128)
