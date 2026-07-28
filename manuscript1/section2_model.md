## 2. Model and Exact Decomposition

### 2.1 Setup
Let $X \in \mathbb{R}^{n \times d}$ be a data matrix with i.i.d. rows 
$x_i \sim \mathcal{N}(0, \Sigma)$, where $\Sigma$ is a diagonal population 
covariance matrix. Let $y = X\theta_* + \varepsilon$ with 
$\varepsilon \sim \mathcal{N}(0, \sigma^2 I_n)$. The ridge estimator is

$$\hat{\theta}_\lambda = \left(\frac{X^\top X}{n} + \lambda I\right)^{-1} \frac{X^\top y}{n}.$$

Define the sample covariance $\hat{S} = X^\top X / n$ and the resolvent 
$M = (\hat{S} + \lambda I)^{-1}$.

### 2.2 Lemma 1: Exact Risk Decomposition
**Lemma 1.** Conditional on $X$, the population test risk decomposes exactly as

$$R_{\rm test}(\hat{\theta}_\lambda | X) = \underbrace{\lambda^2 \theta_*^\top M \Sigma M \theta_*}_{R_{\rm bias}} + \underbrace{\frac{\sigma^2}{n} \mathrm{Tr}[\Sigma M \hat{S} M]}_{\sigma^2 \chi_{\lambda,\Sigma}}.$$

**Proof.** [Your handwritten derivation, typed here.]

### 2.3 The Spectral Susceptibility
The weighted spectral susceptibility is
$$\chi_{\lambda,\Sigma} = \frac{1}{n} \mathrm{Tr}[\Sigma M \hat{S} M] = \frac{1}{n} \sum_{k=1}^n \frac{\lambda_k}{(\lambda_k + \lambda)^2} (v_k^\top \Sigma v_k),$$
where $\lambda_k$ are eigenvalues of $\hat{S}$ and $v_k$ are right singular vectors of $X$.
