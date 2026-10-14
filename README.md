<!-- solve-problem:53836f03-26e9-4eea-b62b-1940d813c48f -->
# Disclosure schedules under strategic signaling

A [Tangle Solve problem](https://solve.tangle.tools/problems/53836f03-26e9-4eea-b62b-1940d813c48f).

## What is the problem?

A stablecoin issuer holds reserves backing a token redeemable at par (say 1). Reserve quality θ (fraction of backing assets that is real/liquid, or asset value net of markdowns) is the issuer's private information or partially observable. Holders decide sequentially or simultaneously whether to redeem ("run") or hold; runs are individually rational when expected recovery from redeeming early exceeds the (fragile) continuation value — a Diamond–Dybvig–style coordination structure with limited reserves, so a run occurs if enough holders believe enough others will run.

On top of this, the issuer (or a regulator/policy-maker) chooses a **disclosure schedule**: a signal structure σ mapping true reserve state θ to a distribution over public announcements, possibly with timing (when announcements are released, e.g., before/after liquidity shocks) and precision (noise of the signal). The open problem: characterize the disclosure schedule (timing × precision × persuasion mapping) that minimizes run probability / maximizes token stability or issuer welfare, given that holders are strategic Bayesians who invert the issuer's motive.

The natural formalization: a dynamic Bayesian coordination game where the designer commits (or does not commit) to σ; solve for the optimal σ in the Bayesian-persuasion sense (Kamenica–Gentzkow) adapted to a run game with strategic complementarities. Key ambiguities to resolve: (i) commitment assumption — is the schedule chosen ex ante and verifiable, or is it cheap talk?; (ii) whose objective — issuer profit vs. social stability; (iii) whether timing is modeled as continuous or as a small number of disclosure dates.

## Why does it matter?

This is the design question behind real policy fights: Tether's reserve attestations, post-UST collapse disclosure mandates, and BIS/FSB proposals to require periodic reserve reporting. A characterization would tell regulators whether mandated frequency and granularity of disclosure reduces or *increases* run risk — the 2024 analysis showing transparency can cut both ways makes this urgent. It would also connect stablecoin design to the bank stress-test disclosure literature (Goldstein–Sapra, Morris–Shin), yielding testable predictions for empirical work.

## What's already known?

- Ahmed, Aldasoro and Duley (2024): an empirical/theoretical study of stablecoin runs showing public information announcements (e.g., attestation releases, reserve disclosures) can trigger runs, but conversely can prevent them by resolving adverse selection — the sign depends on precision and timing. They document that transparency effects are heterogeneous; they do not solve for an optimal schedule. (Details of their model: verify against WP 1164.)
- Classic results imported by analogy: Morris–Shin (2002) — public information is a coordination device and can be a double-edged sword (over-reliance on common signals can increase fragility when fundamentals are sound but signals noisy). Goldstein–Leitner (2018) on optimal stress tests: full transparency destroys risk-sharing; optimal disclosure is a delicate rosy-vs-doomsday signaling.
- Kamenica–Gentzkow (2011) Bayesian persuasion: concavification gives optimal signals when the receiver's action is a monotone function of the posterior — but run games have non-monotone, coordination-dependent best responses (threshold strategies in others' actions), so standard concavification does not directly apply.
- No published work solves the issuer-optimal or welfare-optimal disclosure *schedule* (timing + precision jointly) for stablecoin runs. That is the gap.

## What would count as solving it?

Any of the following would be a publishable solution:
1. **A characterization**: in a stated model (specify commitment, timing structure, objective), derive the run-equilibrium as a function of the signal structure, and prove which σ minimizes run probability — e.g., "threshold-triggered disclosure: reveal only if θ exceeds θ*, with precision decreasing in distance from θ*, dominates all schedules in the commitment class."
2. **A sign result**: prove the boundary conditions under which more precision/timeliness increases vs. decreases run risk (formalizing the "transparency cuts both ways" finding).
3. **A lower bound / impossibility**: show no disclosure schedule (even with commitment) attains zero run probability above some θ, or that no-commitment (cheap-talk) schedules necessarily pool.
4. **Comparative statics**: monotone comparative statics of optimal precision in reserve composition, redemption queue priority, or holder dispersion.

## How to start

1. Read Ahmed–Aldasoro–Duley (BIS WP 1164) first to pin down their run model and the empirical transparency channels; then Goldstein–Leitner (2018) for the stress-test disclosure template — the closest solved analogue.
2. Build the minimal model: two-date coordination game, θ ∈ {high, low}, issuer commits to a binary signal; solve for run equilibria via global-games-style uniqueness (add small private noise à la Morris–Shin to kill multiplicity). Compute issuer-optimal σ by brute force numerically to conjecture structure.
3. Extend timing: allow disclosure before/after a liquidity shock hits; check whether delay is ever optimal (information becomes decision-irrelevant but coordination-relevant).
4. Main obstacle: run best responses depend on posterior beliefs *about others' beliefs* (higher-order uncertainty), so the designer's objective is not a concavifiable function of the first-order posterior — expect to work with posterior distributions over the run threshold rather than posteriors over θ directly.

## Key references

- Ahmed, R., Aldasoro, I., Duley, M. (2024), "Public information and stablecoin runs," BIS Working Paper 1164. — Documents how public announcements affect stablecoin run dynamics and shows transparency can raise or lower run risk; the motivating analysis. https://www.bis.org/publ/work1164.htm
- Morris, S., Shin, H.S. (2002), "Social Value of Public Information," *AER* 92(5). — Shows public signals serve as coordination devices whose welfare effect can be negative when agents over-coordinate on noisy public information.
- Goldstein, I., Leitner, Y. (2018), "Stress Tests and Information Disclosure," *Journal of Economic Theory* 177. — Derives optimal bank stress-test disclosure: full transparency is generally not optimal; the closest solved disclosure-design problem.
- Kamenica, E., Gentzkow, M. (2011), "Bayesian Persuasion," *AER* 101(6). — Provides the concavification toolkit for optimal information design, the baseline technique this problem must extend beyond.
- Diamond, D., Dybvig, P. (1983), "Bank Runs, Deposit Insurance and Liquidity," *JPE* 91(3). — Canonical run/coordination model underlying the stablecoin fragility structure.

## Warnings

- The census record is a research *target*, not a stated theorem — you must fix the model yourself; state your commitment and timing assumptions explicitly, as results differ sharply between them.
- Naïve application of Kamenica–Gentzkow concavification fails here because the run outcome depends on the posterior over *others' actions*, not just the receiver's posterior over θ.
- Do not assume transparency is monotone: the entire point of the 2024 finding is the non-monotone effect; a model where more information always helps has already assumed away the question.
- Equilibrium multiplicity in coordination games will plague comparative statics; use global-games perturbations early.
- (Verify) the precise modeling choices and results in BIS WP 1164 before citing its implications in detail.

---
*`BCGT-000332` · flagged for review*

## Acceptance guidance

Any of the following would be a publishable solution:
1. **A characterization**: in a stated model (specify commitment, timing structure, objective), derive the run-equilibrium as a function of the signal structure, and prove which σ minimizes run probability — e.g., "threshold-triggered disclosure: reveal only if θ exceeds θ*, with precision decreasing in distance from θ*, dominates all schedules in the commitment class."
2. **A sign result**: prove the boundary conditions under which more precision/timeliness increases vs. decreases run risk (formalizing the "transparency cuts both ways" finding).
3. **A lower bound / impossibility**: show no disclosure schedule (even with commitment) attains zero run probability above some θ, or that no-commitment (cheap-talk) schedules necessarily pool.
4. **Comparative statics**: monotone comparative statics of optimal precision in reserve composition, redemption queue priority, or holder dispersion.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/53836f03-26e9-4eea-b62b-1940d813c48f?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000332.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000332)
