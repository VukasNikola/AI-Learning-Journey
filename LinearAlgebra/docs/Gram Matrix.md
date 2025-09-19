## 1. What is the Gram matrix?

* **Definition**: If $X$ is your $n\times p$ data matrix ( $n$ samples, $p$ features), then

  $$
    G \;=\; X^T X
    \quad\text{is a \(p\times p\) matrix of all pairwise dot-products of features.}
  $$
* **Interpretation**:

  * $G_{jj} =$ “length squared” of feature $j$.
  * $G_{jk} =$ how much feature $j$ overlaps (i.e.\ correlates) with feature $k$.

---

## 2. Example 1: A simple 3×2 matrix

Suppose

$$
X = 
\begin{bmatrix}
1 & 2\\
3 & 4\\
5 & 6
\end{bmatrix}
\quad
\bigl(\text{3 samples, 2 features}\bigr).
$$

* Column 1 is $\,(1,3,5)^T$, column 2 is $\,(2,4,6)^T$.

Compute

$$
G = X^T X = 
\underbrace{\begin{bmatrix}
1 & 3 & 5\\
2 & 4 & 6
\end{bmatrix}}_{X^T}
\;\times\;
\begin{bmatrix}
1 & 2\\
3 & 4\\
5 & 6
\end{bmatrix}
=
\begin{bmatrix}
35 & 44\\
44 & 56
\end{bmatrix}.
$$

* **Diagonal entries**

  * $G_{11} = 1^2 + 3^2 + 5^2 = 35$
  * $G_{22} = 2^2 + 4^2 + 6^2 = 56$
* **Off-diagonal**

  * $G_{12} = G_{21} = 1\!\cdot\!2 + 3\!\cdot\!4 + 5\!\cdot\!6 = 44$.

So

$$
G = 
\begin{pmatrix}
\underbrace{35}_{\text{“length²” of feat 1}} &
\underbrace{44}_{\text{dot(feat 1,feat 2)}}\\
44 &
\underbrace{56}_{\text{“length²” of feat 2}}
\end{pmatrix}.
$$

---

## 3. Example 2: Perfectly orthogonal features

Let

$$
X =
\begin{bmatrix}
1 & 0\\
0 & 1\\
1 & 0
\end{bmatrix}.
$$

* Feature 1 lives in the first coordinate, feature 2 in the second; they never “see” each other.

Then

$$
G = X^T X
= \begin{bmatrix}
1^2 + 0^2 + 1^2 & 1\cdot0 + 0\cdot1 + 1\cdot0\\
\cdots & 0^2 + 1^2 + 0^2
\end{bmatrix}
=
\begin{bmatrix}
2 & 0\\
0 & 1
\end{bmatrix}.
$$

* Zero off-diagonals ⇒ no feature-feature correlation.
* Diagonals tell you each feature’s “size.”

---

## 4. Why care about $G$?

1. **Geometry**

   * It’s a snapshot of your data’s shape in feature-space.
   * Eigen-decomposition $G = Q\Lambda Q^T$ gives principal axes: large $\lambda$ = well-informed directions; small $\lambda$ = data “thin” there (ill-posed).

2. **Statistics**

   * The OLS covariance is $\sigma^2G^{-1}$.

     * Large diagonal of $G^{-1}$ → big uncertainty for that $\hat w_j$.
     * Large off-diagonal → two coefficients move together (or against each other).

3. **Inversion warnings**

   * If features are collinear (e.g.\ two identical columns), $G$ has a zero eigenvalue and can’t be inverted—OLS falls apart.

---

### TL;DR

* **$G = X^T X$** packs all pairwise feature inner products.
* **Diagonals** = feature “length²,” **off-diagonals** = feature overlap.
* **Inverse** $G^{-1}$ tells you how that geometry inflates or couples your coefficient estimates.

