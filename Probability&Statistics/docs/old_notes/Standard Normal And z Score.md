* **Definition of z-scores** and why they’re useful for comparing values from different distributions.
* **Standardization process**, converting any normal distribution to the standard normal (mean = 0, σ = 1).
* **Properties of the standard normal distribution**, including the 68-95-99.7 rule and the bell-curve shape.
* **Using z-tables** to look up cumulative probabilities.
* **Worked examples**, showing how to compute z-scores and translate them into probabilities or percentiles. ([YouTube][1])

## What Is a Z-Score?

A **z-score** (or **standard score**) indicates how many standard deviations a raw score is from the population mean ([Wikipedia][2]).

* Raw scores above the mean yield **positive** z-scores; those below yield **negative** ones ([Wikipedia][2]).
* It is a **unitless** measure, letting you compare data across different scales or tests ([Wikipedia][2]).

### Formula

$$
z = \frac{x - \mu}{\sigma}
$$

* $x$ is the observed value, $\mu$ the population mean, and $\sigma$ the population standard deviation ([Wikipedia][2]).
* If only a sample is available, replace $\mu$ with $\bar{x}$ and $\sigma$ with the sample standard deviation $S$ to estimate the z-score ([Wikipedia][2]).

## Standardization Process

1. **Center**: Subtract the mean $\mu$ from each data point, shifting the distribution to zero mean.
2. **Rescale**: Divide by $\sigma$, compressing or stretching so the standard deviation is 1.
3. Result: A new variable $Z$ that follows the **standard normal distribution** $N(0,1)$ ([Wikipedia][2]).

## The Standard Normal Distribution

* It’s simply a normal (Gaussian) distribution with **mean = 0** and **σ = 1** ([Wikipedia][3]).
* Its probability density function (PDF) is

  $$
  \phi(z) = \frac{1}{\sqrt{2\pi}}e^{-z^2/2}.
  \] :contentReference[oaicite:8]{index=8}  
  $$
* **Symmetric** bell-shape centered at zero.

### Empirical Rule (68-95-99.7)

* ≈68% of values lie within **±1σ** of the mean.
* ≈95% lie within **±2σ**.
* ≈99.7% lie within **±3σ**. ([Investopedia][4])

## Using Z-Tables to Find Probabilities

* A **standard normal table** (z-table) gives cumulative probabilities $P(Z \le z)$ for $Z\sim N(0,1)$ ([Wikipedia][5]).
* To find $P(Z > z)$, compute $1 - P(Z \le z)$.
* For two-tailed probabilities (e.g., between $-z$ and $+z$), subtract the lower tail from the upper tail.

## Example Calculations

1. **Converting a test score**: If a student scores 130 on an IQ test ($\mu=100,\ \sigma=15$),

   $$
   z = \frac{130 - 100}{15} = 2.
   $$

   This means their score is **2σ above** the mean, placing them around the 97.5th percentile (since $P(Z\le2)\approx0.975$) ([Wikipedia][2], [Wikipedia][5]).

2. **Height probability**: For adult heights $X\sim N(170\,\text{cm},\,10^2)$, what’s $P(X\le180)$?

   $$
   z = \frac{180 - 170}{10} = 1,\quad P(Z\le1)\approx0.8413.
   $$

   So about **84%** of adults are shorter than 180 cm ([Wikipedia][5]).

## Practical Applications

* **Comparing across scales**: SAT vs. ACT scores, blood pressure readings, etc.
* **Outlier detection**: Data with $|z|>3$ are often flagged as outliers.
* **Process control**: Monitor deviations in manufacturing processes.
* **Hypothesis testing**: Many tests (z-tests) use standard normal critical values (e.g., 1.96 for 95% CI). ([Wikipedia][6])

---