# Paper 0: Novelty Assessment
**Working title:** Weighted Hard-Edge Susceptibility Controls Finite-Size Double Descent under Structured Covariance

---

## The Question

Existing work gives deterministic equivalents for the *mean* test risk of ridge regression in the $n,d \to \infty$ limit. We ask: **What controls the *fluctuations* of risk near the interpolation threshold $\gamma=1$ at finite $n$, and how does population covariance structure modify this?**

---

## Five Closest Papers

| Paper | What they did | What we do differently |
|-------|--------------|------------------------|
| **Hastie et al. (2019)** | "Surprises in High-Dimensional Ridgeless Least Squares Interpolation" — Derives deterministic asymptotic risk curve for isotropic data in $n,d \to \infty$ limit. | We study **finite-size fluctuations** at fixed $n$, not the deterministic mean. We include **structured covariance** (non-isotropic). |
| **Dobriban & Wager (2018)** | "High-Dimensional Asymptotics of Prediction" — Ridge regression deterministic equivalents for general covariance. | They give the **mean** risk equivalent. We study **variance** of risk across disorder realizations and identify the susceptibility that controls it. |
| **Mei & Montanari (2019)** | "Generalization Error of Random Features Regression" — Double descent in random-feature models, asymptotic analysis. | We work in **linear ridge regression** (simpler model), but focus on **finite-size scaling** and **structured disorder ensembles**. |
| **Atanasov et al. (2025/2026)** | Deterministic equivalents for sample covariance with structured populations (Kronecker, etc.). | They compute **deterministic** spectral densities. We study **fluctuations** and show a **weighted susceptibility** $\chi_{\lambda,\Sigma}$ captures risk variance across ensembles. |
| **Pandit (JMLR 2025)** | "Universality of kernel random matrices in the quadratic regime" — Kernel ridge asymptotics, spectral universality. | We stay in the **linear regime** but add **finite-size hard-edge physics** and explicit **covariance-weighted order parameter**. |

---

## Claim of Newness

&gt; **Finite-size fluctuations of ridge regression risk near the interpolation threshold $\gamma=1$ are controlled by the hard-edge statistics of the sample covariance matrix. For structured population covariance $\Sigma$, the test-metric-weighted spectral susceptibility**
&gt; $$\chi_{\lambda,\Sigma} = \frac{1}{n}\mathrm{Tr}\left[\Sigma (\hat{S} + \lambda I)^{-1} \hat{S} (\hat{S} + \lambda I)^{-1}\right]$$
&gt; **serves as an order parameter for this critical regime, with universal scaling across structured disorder ensembles.**

---

## Evidence for the Claim

| Observation | Strength | Location in code |
|-------------|----------|------------------|
| Pooled weighted $\chi$ explains ~45% of risk variance (R² = 0.455) across 4 covariance ensembles | Moderate | `figures_weighted/pooled_weighted_summary.txt` |
| Unweighted $\chi$ explains only ~21% (R² = 0.214) | Supporting | Same |
| Bootstrap $\Delta R^2$ = 0.241, CI = [0.206, 0.278], P($\Delta R^2 &gt; 0$) = 1.0 | Strong | `figures_weighted/pooled_weighted_summary.txt` |
| Risk identity verified: $R_{\rm test} = R_{\rm bias} + \sigma^2 \chi_{\lambda,\Sigma}$ exact | Strong | `paper0_repro/scripts/check_risk_identity.py` |
| Hard-edge scaling $\lambda_{\min} \sim n^{-2}$ confirmed numerically | Classical RMT | `figures_validation/V3_hard_edge_uniform.png` |
| Crossover from ridge-dominated ($\lambda=10^{-6}$) to hard-edge-dominated ($\lambda=10^{-10}$) observed | Physically informative | `figures_lambda_sweep/` |
| Per-ensemble improvement of weighted over unweighted $\chi$ | **Pending** | Run `V1_per_ensemble_r2.png` |

---

## Risk / Weakness (What Could Kill This Claim)

1. **R² is moderate (~0.5) and decreases with $n$ due to concentration.** We need to either:
   - Derive a theoretical prediction for the noise floor, OR
   - Frame the paper as "susceptibility-controlled fluctuations" where R² &lt; 1 is expected.

2. **No analytical derivation yet.** The link between $\chi_{\lambda,\Sigma}$ and $\mathrm{Var}(R_{\rm test})$ is empirical. For PRE/JSTAT, we need at least a cavity/replica heuristic or perturbation expansion.

3. **Limited covariance structures.** Only diagonal $\Sigma$ tested. A reviewer will ask: does this hold for non-diagonal (Kronecker, Toeplitz, general $\Sigma$)?

4. **The n=800 R² drop.** Even with 300 seeds, R² = 0.36 at n=800. We must explain this as concentration (shrinking dynamic range), not mechanism failure.

5. **Atanasov et al. may publish fluctuation results.** We must monitor their 2026 follow-up. If they cover this, our gap closes.

---

## Stop Conditions (When We Abandon or Pivot)

| Condition | Action |
|-----------|--------|
| Atanasov 2026 (or similar) publishes finite-size fluctuation theory with structured covariance | **Pivot** to extension (e.g., non-diagonal $\Sigma$, or kernelized version) |
| We cannot derive analytical link between $\chi_{\lambda,\Sigma}$ and risk variance by Dec 2026 | **Reposition** as "experimental finite-size scaling study" and submit to JSTAT (lower theory bar than PRE) |
| Per-ensemble analysis shows weighted $\chi$ only helps when pooled (mean-shift artifact) | **Kill the claim.** The mechanism is not real. |
| Referee demonstrates that unweighted $\chi$ + simple mean correction achieves same R² | **Kill the claim.** Weighting by $\Sigma$ is not doing new work. |

---

## How to Strengthen Before Submission

| Task | Deadline | Impact |
|------|----------|--------|
| Derive $\mathrm{Var}(R_{\rm test}) \propto \chi_{\lambda,\Sigma}$ via cavity/replica or perturbation | Dec 2026 | **Critical.** Moves from empirical to theoretical. |
| Add 2 non-diagonal ensembles (e.g., AR(1), Wishart-within-Wishart) | Oct 2026 | Defends universality claim. |
| Compute per-ensemble $\Delta R^2$ and show it holds within each ensemble | Aug 2026 | Defends against "pooled artifact" objection. |
| Write risk identity as exact lemma, not just numerics | Sep 2026 | Makes paper rigorous. |
| Frame $\chi_{\lambda,\Sigma}$ explicitly as order parameter in stat-mech language | Continuous | Makes paper PRE-appropriate. |

---

## Bottom Line

The gap is **real but narrow.** Existing work covers the deterministic mean; no one has framed the finite-size fluctuation near $\gamma=1$ as a critical phenomenon with an order parameter. The weighted susceptibility $\chi_{\lambda,\Sigma}$ is a defensible candidate for this order parameter, but only if we can:
1. Show it works **within** ensembles (not just pooled), and
2. Back it with **at least one analytical result** (even heuristic).

**If both fail by December 2026, we submit as experimental JSTAT paper with strong numerics.**
