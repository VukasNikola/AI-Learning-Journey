> **Summary:**
> The video introduces the *sampling distribution*—the probability distribution of a statistic (here, the sample mean) computed from all possible samples of a given size drawn from a population. It contrasts this with the population distribution of individual observations and the empirical distribution of one sample. The core result is the **Central Limit Theorem**, which tells us that, for sufficiently large sample sizes (usually $n\ge30$), the sampling distribution of the mean is approximately Normal with
>
> $$
> \mu_{\bar X} = \mu,\quad 
> \sigma_{\bar X} = \frac{\sigma}{\sqrt{n}}
> $$
>
> regardless of the shape of the population ﹣ making inference via confidence intervals and hypothesis tests feasible.

---

## 1. Definitions and Distinctions

### 1.1 Statistic vs. Random Variable

* A **statistic** is a function of sample data only (e.g.\ the sample mean $\bar X$).
* Unlike a fixed parameter, a statistic varies from sample to sample, so it is itself a random variable whose distribution we call the **sampling distribution** ([facultyweb.kennesaw.edu][1]).

### 1.2 Population, Sample, and Sampling Distributions

* **Population distribution:** the distribution of a single observation $X$, with mean $\mu$ and standard deviation $\sigma$.
* **Sample distribution:** the empirical distribution of one realized sample of size $n$.
* **Sampling distribution:** the distribution of $\bar X$ over all possible samples of size $n$ drawn from the population ([Social Sci LibreTexts][2], [Statistics LibreTexts][3]).

---

## 2. Sampling Distribution of the Sample Mean

### 2.1 Mean and Spread

For a sample of size $n$ from a population with mean $\mu$ and standard deviation $\sigma$:

$$
\boxed{
\mu_{\bar X} = \mu
,\quad
\sigma_{\bar X} = \frac{\sigma}{\sqrt{n}}
}
$$

* $\sigma_{\bar X}$ is often called the **standard error** of the mean ([Social Sci LibreTexts][2], [facultyweb.kennesaw.edu][1]).

### 2.2 Shape

* If the population is Normal, then $\bar X$ is *exactly* Normal for any $n$.
* If the population is *not* Normal, the **Central Limit Theorem** ensures $\bar X$ is *approximately* Normal when $n$ is large (typically $n\ge30$) ([Social Sci LibreTexts][2], [Pressbooks][4]).

---

## 3. The Central Limit Theorem (CLT)

> **Statement:**
> For independent observations $X_1,\dots,X_n$ from any distribution with mean $\mu$ and finite variance $\sigma^2$, the sampling distribution of
> $\bar X = \tfrac1n\sum_{i=1}^n X_i$
> approaches $N(\mu,\sigma^2/n)$ in shape as $n\to\infty$.

* **Practical rule:** “*$n\ge30$ is usually large enough for a good Normal approximation.*” ([Social Sci LibreTexts][2], [Statistics LibreTexts][3])