## 1. The Core Concept

1. **Model choice**
   You assume your data $x_1,\dots,x_N$ come from some family of distributions $P(x\mid\theta)$, where $\theta$ is the unknown parameter (or vector of parameters) you want to estimate.

2. **Likelihood function**
   Treat the (fixed) data as given and view the joint probability of seeing it as a function of $\theta$:

   $$
     L(\theta)
     = P(x_1,\dots,x_N\mid \theta)
     = \prod_{i=1}^N P(x_i\mid\theta).
   $$

   That product can get astronomically small—so we switch to the log:

   $$
     \ell(\theta)
     = \log L(\theta)
     = \sum_{i=1}^N \log P(x_i\mid\theta).
   $$

   **Goal**: find
   $\displaystyle \hat\theta = \arg\max_\theta \ell(\theta)$.

3. **Why “log”?**

   * Turns products into sums (easier calculus).
   * Improves numerical stability (no underflow).

---

## 2. The Recipe for Finding an MLE

1. **Write down** the pmf/pdf $P(x\mid\theta)$.
2. **Form the log-likelihood**
   $\ell(\theta)=\sum_i \log P(x_i\mid\theta).$
3. **Differentiate** $\ell(\theta)$ with respect to each component of $\theta$.
4. **Set derivatives to zero** → a system of “normal equations.”
5. **Solve** for $\hat\theta$.
6. **Check** second derivative (or Hessian) is negative definite to ensure a maximum.

If you can’t solve in closed form, you plug $\ell(\theta)$ into a numerical optimizer (e.g.\ gradient ascent, Newton–Raphson).

---

## 3. Worked Examples

### 3.1 Bernoulli (Coin-Flip)

* **Data**: $x_i\in\{0,1\}$ (0=T, 1=H), $i=1\ldots N$.
* **Model**: $P(x_i\mid p)=p^{x_i}(1-p)^{1-x_i}$.
* **Log-likelihood**:

  $$
    \ell(p)
    = \sum_{i=1}^N [\,x_i\log p + (1-x_i)\log(1-p)\,]
    = \bigl(\sum x_i\bigr)\log p \;+\;\bigl(N-\sum x_i\bigr)\log(1-p).
  $$
* **Derivative**:

  $$
    \frac{d\ell}{dp}
    = \frac{\sum x_i}{p} \;-\;\frac{N-\sum x_i}{1-p}
    \;\overset{!}{=}\; 0
    \quad\Longrightarrow\quad
    \frac{\sum x_i}{p} = \frac{N-\sum x_i}{1-p}.
  $$
* **Solve**:

  $$
    p\,N = \sum x_i 
    \;\;\Longrightarrow\;\; 
    \boxed{\hat p = \frac{1}{N}\sum_{i=1}^N x_i.}
  $$

  *Interpretation:* fraction of heads in your sample.

---

### 3.2 Gaussian (Normal) with Known Variance

* **Data**: real $x_i$.
* **Model**:

  $$
    p(x_i\mid\mu)
    = \frac1{\sqrt{2\pi\sigma^2}}
      \exp\!\Big(-\frac{(x_i-\mu)^2}{2\sigma^2}\Big),
  $$

  assume $\sigma^2$ known for now.
* **Log-likelihood** (dropping constant terms):

  $$
    \ell(\mu)
    = -\frac1{2\sigma^2}\sum_{i=1}^N (x_i-\mu)^2 + \text{const}.
  $$
* **Derivative**:

  $$
    \frac{d\ell}{d\mu}
    = -\frac1{\sigma^2}\sum (x_i-\mu)
    \;\overset{!}{=}\;0
    \;\Longrightarrow\;
    \sum x_i - N\mu = 0.
  $$
* **Solve**:

  $$
    \boxed{\hat\mu = \frac1N\sum_{i=1}^N x_i.}
  $$

  *Interpretation:* the sample mean is the MLE for the true mean.

---

### 3.3 Gaussian with Unknown Variance

If you also treat $\sigma^2$ as unknown:

* **Log-likelihood**
  $\ell(\mu,\sigma^2)= -\tfrac N2\log\sigma^2 - \frac1{2\sigma^2}\sum(x_i-\mu)^2 +\text{const}.$
* **Set**
  $\partial\ell/\partial\mu=0$ ➔ $\hat\mu=\bar x$.
  $\partial\ell/\partial\sigma^2=0$ ➔
  $\displaystyle\hat\sigma^2=\frac1N\sum(x_i-\bar x)^2.$

---

### 3.4 Poisson (Event Counts)

* **Model**: $P(k\mid\lambda)=e^{-\lambda}\,\lambda^k/k!$.
* **Log-likelihood**:
  $\ell(\lambda)=\sum [\, -\lambda + k_i\log\lambda - \log(k_i!)\, ].$
* **Derivative**:
  $\frac{d\ell}{d\lambda}=-N + \frac1\lambda\sum k_i=0$.
* **Solve**:
  $\hat\lambda=\frac1N\sum_{i=1}^N k_i$.
  *Interpretation:* sample mean of counts.

---

### 3.5 Categorical / Multinomial

* **Data**: each $x_i$ takes one of $K$ categories.
* **Model**: $\theta_1,\dots,\theta_K$, $\sum \theta_j=1$,
  $\,P(x_i=j)=\theta_j.$
* **Log-likelihood**:
  $\ell(\boldsymbol\theta)=\sum_{j=1}^K n_j\log\theta_j$,
  where $n_j$ = count of category $j$.
* **Use Lagrange multiplier** for the constraint $\sum\theta_j=1$, or notice symmetry:
  $\hat\theta_j = n_j/N.$

---

## 4. When Closed-Form Isn’t an Option

* Some models (e.g.\ mixture models, logistic regression) give log-likelihoods **without** a simple derivative=zero solve.
* You then use numerical methods:

  * **Gradient ascent** on $\ell(\theta)$.
  * **Newton–Raphson** (uses second derivatives).
  * Off-the-shelf routines (e.g.\ `scipy.optimize`).

---

## 5. Practical Tips

* **Always** work with the log-likelihood for stability.
* Check your second derivative (or use convexity) to ensure a **max**, not a **min** or saddle.
* In code, make sure to guard against $\log(0)$ by adding tiny epsilons or using specialized libraries.
* **Regularization** (e.g.\ adding a prior) turns MLE into MAP estimation—helpful if you have zero counts or want to control overfitting.