1. **Why CI width grows with “distance”**

   * For a new point $x_0$, its CI uses
     $\displaystyle1 + x_0^T(X^TX)^{-1}x_0$
     because points farther from the cloud of training data have higher uncertainty.

2. **Estimating the unknown noise $\sigma^2$**

   * We fit $\hat w$ by OLS, compute residuals $r = y - X\hat w$, then

     $$
       \hat\sigma^2 = \frac{\|r\|^2}{n - p}\quad
       (n\!=\!\#\text{points},\,p\!=\!\#\text{params})
     $$
   * Dividing by $n-p$ “pays” for each parameter we estimated, giving an unbiased estimate.

3. **From “$y_0 - \hat y_0 \sim N(0,\;\sigma^2s_0^2)$” to $[\hat y_0\pm\Delta_0]$**

   * Define

     $$
       T = \frac{\hat y_0 - y_0}{\hat\sigma\,s_0}
       \sim t_{n-p},\quad
       s_0 = \sqrt{1 + x_0^T(X^TX)^{-1}x_0}.
     $$
   * Use
     $\displaystyle P(-t^*\le T\le t^*)=1-\alpha$
     then multiply through by $\hat\sigma\,s_0$ and solve for $y_0$ to get

     $$
       y_0\in[\hat y_0\pm t^*\,\hat\sigma\,s_0]
       =[\hat y_0\pm\Delta_0].
     $$

4. **Standardization trick**

   * Just like for a simple normal:
     $\;P(-z^*\le Z\le z^*)\!\implies\!P(\mu\pm z^*\sigma)$.
   * Here $Z\to T$ (a Student $t$), $\mu\to0$, $\sigma\to1$.

5. **Shifting normals**

   * If $a-b\sim N(0,\sigma^2)$ with $b$ fixed, then
     $a=(a-b)+b\sim N(b,\sigma^2)$.
   * Shifting by a constant adds to the mean, leaves variance unchanged.

6. **Variance (and SE) of the coefficients $\hat w$**

   * $\displaystyle\hat w = (X^TX)^{-1}X^T\,y$ is a linear map of $y\sim N(Xw,\sigma^2I)$, so

     $$
       \mathrm{Var}(\hat w)
       =\sigma^2\,(X^TX)^{-1},\quad
       \mathrm{Var}(\hat w_j)=\sigma^2\bigl[(X^TX)^{-1}\bigr]_{jj}.
     $$
   * **Standard error**: take the square‐root to get units of $\hat w_j$:
     $\displaystyle\mathrm{SE}(\hat w_j)   =\sigma\sqrt{[(X^TX)^{-1}]_{jj}}$,
     and in practice replace $\sigma$ with $\hat\sigma$.

7. **“Leverage” for parameters vs. predictions**

   * **Parameter SE** uses the $j$th diagonal of $(X^TX)^{-1}$.
   * **Prediction PI** uses $1 + x_0^T(X^TX)^{-1}x_0$.
   * Both come from the same matrix inverse, but slice out different entries.

---

**Bottom line:**

* You always estimate the common noise level $\sigma$ via residuals.
* For **coefficients**, your “shape factor” is $\sqrt{[(X^TX)^{-1}]_{jj}}$.
* For **new‐point predictions**, it’s $\sqrt{1 + x_0^T(X^TX)^{-1}x_0}$.
* Then standardize → apply $t$-quantile → undo standardization.
