
## 1. Singular Value Decomposition (SVD)

**Factorization:**

$$
A = U\,\Sigma\,V^T
$$

* **$V$** (size $n\!\times\!n$) contains right-singular vectors $v_i$: orthonormal “input” directions.
* **$\Sigma$** ($m\!\times\!n$) is diagonal with non-negative **singular values** $\sigma_1\ge\sigma_2\ge\cdots$.
* **$U$** ($m\!\times\!m$) contains left-singular vectors $u_i$: orthonormal “output” directions.

**Geometric recipe:**

1. **Rotate** your input vector $x$ by $V^T$ into principal axes.
2. **Stretch** each coordinate by $\sigma_i$.
3. **Rotate** by $U$ into the final space.

**How to compute (constructive view):**

1. Form $A^T A$ (symmetric).
2. Eigen-solve $A^T A\,v_i = \lambda_i\,v_i$. Then $\sigma_i=\sqrt{\lambda_i}$.
3. Compute $u_i = A\,v_i / \sigma_i$.
4. Repeat on the subspace orthogonal to previous $v$’s (deflation) to get all $r$ nonzero modes.

---

## 2. Matrix Rank

**Definition:**

$$
\rank(A) = \bigl|\{\,\sigma_i>0\}\bigr|
= \dim\bigl(\mathrm{span\ of\ columns\ of\ }A\bigr).
$$

Equivalently, the maximum number of linearly independent rows or columns.

**Key facts:**

* $0 \le \rank(A)\le \min(m,n)$.
* **Full-rank** if $\rank(A)=\min(m,n)$.
* **Rank-nullity**: $\rank(A)+\nullity(A)=n$.

**Compute:**

* Gaussian elimination → count nonzero rows.
* SVD → count positive $\sigma_i$.
* In NumPy: `np.linalg.matrix_rank(A)`.

---

## 3. Economy (Skinny) SVD

If $\rank(A)=r$, you only need the first $r$ singular triplets:

$$
A = U_{\!m\times r}\;\Sigma_{r\times r}\;V_{\!r\times n}^T.
$$

* **Full SVD** stores $U_{m\times m},\,\Sigma_{m\times n},\,V_{n\times n}$.
* **Economy SVD** stores only the nonzero part:

  $$
    \underbrace{m\times r}_{U} +
    \underbrace{r\times r}_{\Sigma} +
    \underbrace{r\times n}_{V^T},
  $$

  saving storage/computation whenever $r\ll\min(m,n)$.

---

## 4. Why This Matters

* **Low-rank approximation:** keep top $k$ singular values to approximate $A$ optimally.
* **Pseudoinverse:** invert nonzero $\sigma_i$, flip rotations → Moore–Penrose inverse.
* **PCA:** SVD of data matrix $X$ gives principal components (columns of $V$) directly.

---

## 5. Cartoon Example (2×2)

Let
$\displaystyle A=\begin{pmatrix}3&1\\1&3\end{pmatrix}.$

* Eigen-solve $A^TA$ → $\sigma_1=4,\;\sigma_2=2$.
* $V^T$ rotates by 45° → $\Sigma$ stretches into an ellipse → $U$ rotates back.

---

### A Little Humor

> **SVD** is just your matrix playing DJ:
>
> 1. **Gather** everyone in a circle (`V^T`),
> 2. **Pump up** the bass on each axis (`Σ`),
> 3. **Send** them out dancing (`U`).

---

You’re looking at the **Rayleigh quotient** for the symmetric matrix $B = A^T A$:

$$
R(v) \;=\;\frac{\|A\,v\|^2}{\|v\|^2}
\;=\;\frac{v^T A^T A\,v}{v^T v}
$$

---

## 1. From Rayleigh quotient to eigenproblem

To find the unit $v$ that **maximizes** $R(v)$, you solve

$$
\max_{\|v\|=1} v^T B\,v
\quad\Longleftrightarrow\quad
\delta\bigl(v^T B\,v - \lambda\,(v^T v - 1)\bigr)=0
$$

using a Lagrange multiplier $\lambda$.  Taking the gradient gives

$$
2\,B\,v - 2\lambda\,v = 0
\quad\Longrightarrow\quad
B\,v = \lambda\,v.
$$

Thus **stationary** $v$ are eigenvectors of $B=A^T A$.

---

## 2. Singular values from eigenvalues

* The **extremal values** of $R(v)$ over all $v\neq0$ are exactly the eigenvalues $\lambda_i$ of $B$.
* By ordering $\lambda_1\ge\lambda_2\ge\cdots\ge0$, the **maximum** of $R(v)$ is $\lambda_1$.
* Hence the top singular value is

  $$
    \sigma_1 = \sqrt{\lambda_1}
    = \max_{\|v\|=1} \|A\,v\|.
  $$

---

## 3. Computing subsequent singular triplets

Once $v_1$ is found (the eigenvector of $B$ for $\lambda_1$), you get

$$
u_1 = \frac{A\,v_1}{\sigma_1},
$$

and then look for the next largest eigenvalue $\lambda_2$ of $B$ **on the subspace orthogonal** to $v_1$, and so on.

---

### TL;DR

$$
\max_{v\neq0}\frac{\|A\,v\|^2}{\|v\|^2}
\;=\;\max_{\|v\|=1} v^T(A^T A)v
\;=\;\lambda_{\max}(A^T A),
\quad\sigma_{\max}(A)=\sqrt{\lambda_{\max}(A^T A)}.
$$
